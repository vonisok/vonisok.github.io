---
layout: post
title: "How to Connect AI Agents to Any API"
description: "Hands-on, script-first tutorial: authenticate, call APIs, parse JSON, feed results into GPT-4 (or an agent framework), and implement retries/rate limits—ending with a working Semantic Scholar + GPT-4 research agent."
date: 2025-08-10
categories: [ai, agents, apis, tutorials]
tags: [python, requests, langchain, crewai, openai, semantic-scholar, retries, rate-limiting]
permalink: /guides/connect-ai-agents-to-any-api/
image: /assets/images/connect-ai-agents-to-any-api/cover.png
excerpt_separator: "<!--more-->"
---

This guide shows you how to wire any API into an AI agent using a **script-first** approach (Python). You’ll learn how to get an API key, authenticate, make test calls, parse JSON, and pass results to an LLM (GPT-4) or a framework tool (LangChain/CrewAI). We’ll finish with a **working research agent** that queries the **Semantic Scholar** API and produces a **citation-backed summary**.
<!--more-->

- Table of Contents
{:toc}

## What you’ll build (and what you need)

You’ll build a small script that:
- calls a web API,
- extracts the fields you need,
- formats them for an LLM,
- asks the LLM to synthesize a result with citations,
- handles errors and rate limits.

**Prerequisites**
- Python 3.10+  
- `pip install requests openai`  
- Environment variables set: `OPENAI_API_KEY`, and (optionally) the target API key (e.g., `S2_API_KEY` for Semantic Scholar).

> **Note:** This guide avoids no-code tools. We focus on CLI + scripts so you fully control formatting, costs, and reliability.

## Step 1 — Obtain an API key and make a clean test call

1) **Create a key** on the provider’s developer portal.  
2) **Store it safely** (environment variables, not hard-coded).  
3) **Read the docs** for base URL, auth header, query params, response fields.  
4) **Smoke test** with `requests`:

```python
# test_call.py
import os, requests

API_KEY = os.getenv("S2_API_KEY")  # Semantic Scholar example; replace as needed
BASE = "https://api.semanticscholar.org/graph/v1"
endpoint = f"{BASE}/paper/search"
params = {"query": "large language models", "limit": 1, "fields": "title,year"}
headers = {"x-api-key": API_KEY} if API_KEY else {}

r = requests.get(endpoint, params=params, headers=headers, timeout=15)
print("Status:", r.status_code)
print(r.json() if r.headers.get("content-type","").startswith("application/json") else r.text)
```

> **Tip:** Always request only the fields you need (smaller payloads, faster, cheaper).

## Step 2 — Isolate API logic (make it a reusable function)

```python
# api_client.py
import os, time, requests
from typing import Dict, Any, List

S2_API_KEY = os.getenv("S2_API_KEY")
BASE = "https://api.semanticscholar.org/graph/v1"
HEADERS = {"x-api-key": S2_API_KEY} if S2_API_KEY else {}

def search_papers(query: str, limit: int = 3) -> List[Dict[str, Any]]:
    """
    Search Semantic Scholar for papers and return a list of dicts with key fields.
    Retries on transient failures and respects basic rate limits.
    """
    endpoint = f"{BASE}/paper/search"
    params = {
        "query": query,
        "limit": limit,
        "fields": "title,year,abstract,citationCount,externalIds,authors"
    }

    backoff = 1.5
    for attempt in range(5):
        try:
            r = requests.get(endpoint, params=params, headers=HEADERS, timeout=20)
            # Rate limit handling
            if r.status_code == 429:
                retry_after = int(r.headers.get("Retry-After", 2))
                time.sleep(max(retry_after, 2))
                continue
            if 200 <= r.status_code < 300:
                data = r.json()
                return data.get("data", [])
            # 5xx: transient server errors → retry
            if 500 <= r.status_code < 600:
                time.sleep(backoff)
                backoff *= 1.6
                continue
            # Other errors: surface details for debugging
            raise RuntimeError(f"API error {r.status_code}: {r.text[:500]}")
        except requests.RequestException as e:
            # Network/timeout → retry with backoff
            time.sleep(backoff)
            backoff *= 1.6
    # If we got here, all retries failed
    raise RuntimeError("Failed to fetch papers after multiple attempts.")
```

> **Warning:** Never log full API keys. Redact or use environment variables.

## Step 3 — Parse JSON and shape it for an LLM

LLMs work best with **concise, structured context**. Extract only what matters and compress long abstracts.

```python
# formatting.py
from typing import List, Dict, Any

def format_papers_for_prompt(papers: List[Dict[str, Any]], max_abs_sentences: int = 2) -> str:
    """
    Convert paper dicts into a numbered list the LLM can cite like [1], [2], …
    """
    lines = []
    for i, p in enumerate(papers, start=1):
        title = p.get("title", "Untitled")
        year = p.get("year", "n.d.")
        authors = ", ".join(a.get("name","") for a in p.get("authors", [])[:3]) or "Unknown"
        abstract = (p.get("abstract") or "").strip()
        if abstract:
            sentences = abstract.split(". ")
            abstract = ". ".join(sentences[:max_abs_sentences]).strip()
            if not abstract.endswith("."):
                abstract += "."
        lines.append(f"{i}. {title} ({year}) — {authors}. {abstract}".strip())
    return "\n".join(lines)
```

> **Tip:** If responses are huge, summarize or truncate **before** sending to the model to save tokens and reduce noise.

## Step 4 — Call the LLM (raw OpenAI API or via a framework)

**Raw OpenAI (Chat Completions)**

```python
# llm.py
import os, openai

openai.api_key = os.getenv("OPENAI_API_KEY")

def summarize_with_citations(topic: str, paper_block: str) -> str:
    """
    Ask the model to write a concise summary using only the provided papers.
    It must cite with [1], [2], … matching the numbered list.
    """
    prompt = f"""You are a precise research assistant.

Topic: "{topic}"

You are given numbered paper notes:

{paper_block}

Instructions:
- Write a concise synthesis of key findings about the topic.
- When using a claim from a paper, cite it with its number in square brackets (e.g., [2]).
- End with a "References" section listing the numbers and titles.

Now produce the summary:
"""
    resp = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}],
        temperature=0.4,
        max_tokens=700
    )
    return resp["choices"][0]["message"]["content"].strip()
```

**As a LangChain tool (optional)**

```python
# tool_semantic_scholar.py
from langchain.tools import BaseTool
from api_client import search_papers
from formatting import format_papers_for_prompt

class SemanticScholarTool(BaseTool):
    name = "semantic_scholar_search"
    description = "Searches Semantic Scholar and returns a numbered list of brief paper notes."

    def _run(self, query: str) -> str:
        papers = search_papers(query, limit=5)
        return format_papers_for_prompt(papers)
```

You can then register this tool in a LangChain/CrewAI agent so the model decides when to call it.

## Step 5 — Put it together: a CLI research agent

```python
# research_agent.py
import sys
from api_client import search_papers
from formatting import format_papers_for_prompt
from llm import summarize_with_citations

def main():
    if len(sys.argv) < 2:
        print("Usage: python research_agent.py \"your topic here\"")
        sys.exit(1)

    topic = sys.argv[1]
    papers = search_papers(topic, limit=5)
    if not papers:
        print("No papers found.")
        sys.exit(2)

    paper_block = format_papers_for_prompt(papers, max_abs_sentences=2)
    out = summarize_with_citations(topic, paper_block)
    print("\n=== Summary ===\n")
    print(out)

    print("\n=== Sources ===\n")
    for i, p in enumerate(papers, start=1):
        title = p.get("title","Untitled")
        year  = p.get("year","n.d.")
        doi   = (p.get("externalIds") or {}).get("DOI")
        print(f"[{i}] {title} ({year})" + (f" — DOI: {doi}" if doi else ""))

if __name__ == "__main__":
    main()
```

Run:

```bash
export OPENAI_API_KEY=sk-...
export S2_API_KEY=your_s2_key   # optional; recommended
python research_agent.py "generative AI for music"
```

## Production-grade error handling & rate limiting

- **HTTP checks:** handle `401/403` (auth), `404` (bad path/resource), `429` (rate limit), `5xx` (server).  
- **Retries:** exponential backoff (jitter helps); cap attempts and surface clear errors to the user/logs.  
- **Timeouts:** always set `timeout=…` on HTTP calls.  
- **Circuit breakers:** if an API keeps failing, pause or fall back to cached results.  
- **Batching:** prefer batch endpoints to reduce request count when available.  
- **Token budgets:** trim/aggregate API results before sending to the LLM.

## Troubleshooting

> **Model hallucinates citations**  
> Make the prompt stricter: “Only use the numbered papers. If information is missing, say so.” Reduce temperature.

> **429 Too Many Requests**  
> Add backoff, observe `Retry-After`. Lower concurrency; switch to batch endpoints.

> **Large abstracts blow context**  
> Pre-summarize abstracts to 1–2 sentences; include titles/authors/years for grounding.

> **Intermittent timeouts**  
> Increase timeout modestly (15–30s). Retry a few times; then fail fast with a clear message.

## File layout (suggested)

```
/connect-ai-agents-to-any-api/
├─ api_client.py
├─ formatting.py
├─ llm.py
├─ research_agent.py
└─ README.md
```

## Next steps

- Swap Semantic Scholar for other APIs (arXiv, Crossref, PubMed) with the same adapter pattern.  
- Register your API function as a **LangChain/CrewAI tool** so the agent can decide when to call it.  
- Persist results (e.g., Notion, Google Sheets) and schedule runs (cron/systemd).  
- Add a vector store for retrieved paper chunks and build RAG over PDFs.

## Resources

- OpenAI Python SDK (Chat Completions)  
- Semantic Scholar API (Graph endpoints)  
- LangChain agents & tools (function/tool calling patterns)  
- CrewAI (multi-agent orchestration)

> **Definition of done:** front matter is valid, no `<h1>` in body, intro ends with `<!--more-->`, TOC block present, fenced code blocks with languages, no raw HTML required.
