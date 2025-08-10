---
layout: post
title: "Guide to APIs for AI Agents"
description: "Curated, up-to-date APIs for AI agents—search, document parsing/OCR, data, translation, academic, productivity, dev, ML, and cybersecurity—with pricing tiers and use cases."
date: 2025-08-10
categories: [ai, ai agents, API]
tags: [ai, research, ai-agents, tutorial, beginners]
permalink: /guides/guide-to-apis/
image:
  path: /assets/img/posts/javascript-intro.jpg  # Change this to your own image path
---

## Guide to APIs for AI Agents

APIs (Application Programming Interfaces) enable AI agents and applications to access web services and data for various tasks. Below is a comprehensive guide to important APIs (categorized by purpose) along with their cost models (Free, Freemium, Paid) and typical use cases.
## Web Search APIs

Free APIs:

- Brave Search API – Provides privacy-focused web search results via a simple API. Free plan allows 1 query/second and up to 2,000 queries per month
  brave.com
  . Useful for AI agents needing independent search index data (an alternative to Google/Bing) with recent web results
  brave.com
  .

- DuckDuckGo Instant Answer API – Offers free access to DuckDuckGo’s instant answers (e.g. topic summaries, definitions, “!Bang” redirects) in JSON format
  postman.com
  . Note: It does not return full search result listings due to licensing limits
  postman.com
  . Good for quick factual answers without scraping search pages.

- Wikipedia API (MediaWiki) – A free public API to search and retrieve content from Wikipedia. Developers can query articles, fetch summaries, and more via RESTful endpoints
  developer.wikimedia.org
  . Ideal for knowledge retrieval (e.g. definitions, background info) in research agents.

Freemium APIs:

- Google Custom Search JSON API – Official Google Search results API. Allows 100 free queries per day
  empowerlearning1.zohodesk.com
  ; beyond that, it costs ~$5 per 1000 queries
  empowerlearning1.zohodesk.com
  . Returns Google’s web results in JSON, suitable for integrating web search into AI workflows. (Beginner-friendly, but requires a Google API key).

- Bing Web Search API – Microsoft’s search API (part of Azure Cognitive Services). Offers a free tier of 1,000 queries/month (up to 3 queries/second)
  zenserp.com
  . Provides web, image, news, and video search results in JSON. Note: Changes in 2025 will transition Bing Search API into new Azure offerings
  ppc.land
  . Useful for multi-modal search needs in agents.

- SerpAPI (Google/Bing SERP scraper) – A third-party service that parses search engine results. It has a free plan (e.g. 100 searches/month)
  capturekit.dev
  and higher paid tiers for volume. Simplifies getting Google/Bing results (bypassing captchas, etc.) in JSON. Good for intermediate users who need reliable SERP data.

- Zenserp, SerpStack, ScrapingBee, etc. – Similar SERP APIs offering some free credits (e.g. 50 searches/month free on Zenserp
  zenserp.com
  ) and paid plans. They let agents perform web searches at scale by scraping results behind the scenes
  zenserp.com
  .

Paid APIs (enterprise or advanced):

- Google Programmable Search (Site Restricted) – High-cap query packages (beyond 10k/day) require a paid subscription
  empowerlearning1.zohodesk.com
  . Useful if an agent needs Google search across specific sites with no daily limits.

- Bing Search (Enterprise) – Higher tiers on Azure with SLA, e.g. 10+ queries/second and large monthly caps (paid)
  stackoverflow.com
  . Intended for production systems requiring guaranteed throughput.

- You.com Search API – Emerging search API from You.com (if available), likely paid and oriented toward AI integration with their multimodal search results (advanced use cases).

## Document Parsing & OCR APIs

Free APIs:

- OCR.space OCR API – A free OCR service for images/PDFs. Provides a simple endpoint to extract text from images or multi-page PDFs, returning JSON results
  ocr.space
  . The free tier allows ~500 calls/day per IP
  ocr.space
  . Great for AI researchers to quickly convert scanned documents or screenshots to text.

- Google Drive/Docs API – Allows programmatic access to Google Docs and Drive files (free with a Google account). Agents can retrieve document text, comments, etc., to parse and analyze content. (Beginner-friendly with client libraries).

- Tesseract OCR (open-source) – Not a web API but a library; worth noting for local agent use. It’s free and can be wrapped in a local service to parse images for text (requires more setup, intermediate level).

Freemium APIs:

- Google Cloud Vision API – Powerful image analysis API which includes text detection (OCR). First 1000 images per month are free
  cloud.google.com
  , then usage is billed per 1000 images. Can extract text, detect document structure, and more. Useful for parsing images of documents in research (e.g. graphs or tables in PDFs)
  cloud.google.com
  .

- Google Document AI (Document OCR & Form Parser) – Cloud service for structured document parsing (forms, invoices, etc.). Free tier available (uses Google’s Vision quota) and paid for high volume. Good for advanced use (extracting key fields from forms).

- AWS Textract – AWS’s OCR and form extraction service. Offers a free trial (for new users, e.g. 1,000 pages per month for 3 months
  aws.amazon.com
  ) and then pay-per-page. Capable of detecting text, tables, form fields from scanned PDFs. Suitable for intermediate users familiar with AWS.

- Azure Form Recognizer (Document Intelligence) – Microsoft’s document parsing API. Free tier: 500 pages/month free
  lanternstudios.com
  , then paid per page. Can extract text, tables, and key-value pairs from forms. Integrates with Azure AI stack, great for enterprise agents handling forms.

- Adobe PDF Extract API – Part of Adobe Document Services, it uses AI to extract structured content (text, tables, figures) from PDFs. Free tier: 500 documents/month
  developer.adobe.com
  , then enterprise plans. Useful for researchers needing high-quality PDF content extraction (e.g. parsing academic papers for sections).

- Parseur / Docparser – SaaS APIs for document data extraction (popular for invoices, reports). They offer free tiers (e.g. 20 pages/month on Parseur
  parseur.com
  ) and paid plans beyond. These are no-code friendly: ideal for beginners who want to pull specific data fields from recurring document formats.

- OCR.Space PRO / On-Premise – The same OCR.space offers paid plans with higher rate limits and even self-hosted options
  ocr.space
  . Useful if you need guaranteed uptime or to process very large PDFs beyond the free limits.

Paid APIs (advanced/specialized):

Mistral AI OCR API – A cutting-edge OCR by Mistral AI that converts PDFs into markdown for AI-readiness. It’s a paid service (~$1 per 1k pages), with some free credits for trial. Useful for advanced workflows where preserving formatting (like images in base64, table structure) is important
reddit.com
.

ABBYY Cloud OCR/Finereader API – Enterprise-grade OCR with superior accuracy and layout retention. Fully paid, typically used in corporate settings (invoices, passports, etc.) – suitable for advanced agents needing high accuracy.

Diffbot Article API – A paid API that extracts clean text, metadata, and article structure from URL links (great for parsing blog posts, news). Not free, but powerful for agents doing web research (summarizing or analyzing online articles).

## Data Retrieval & Open Data APIs

Free APIs:

- OpenWeatherMap API – Provides weather data (current forecasts, historical). Requires a free API key; 1,000 calls/day free
  openweathermap.org
  (then pay-as-you-go for more). Useful for agents that need weather info for planning or analysis tasks.

- CoinGecko API – A cryptocurrency data API that is free and doesn’t require an API key. Offers real-time and historical data on thousands of coins
  crawlbase.com
  . Great for AI agents analyzing market trends or building portfolio trackers.

- Alpha Vantage – Free stock market data API (JSON) for equity and forex. Provides up to 5 API calls per minute and 500 calls per day free
  alphavantage.co
  (additional requests require premium keys). Useful for research agents pulling financial time series or indicators
  alphavantage.co
  .

- Public Government Data APIs – Many governments provide open APIs (e.g., NASA Open APIs for space data, US Census API for demographic data, World Bank API for economic indicators). These are typically free and useful for academic or data science agents (though require understanding specific data formats).

- Wikipedia/DBpedia – Beyond the Wikipedia search API, DBpedia and Wikimedia APIs let agents retrieve structured data (entities, categories) from Wikipedia for free, enabling knowledge graph building or entity recognition in text.

- Stack Exchange API – Allows free querying of the Stack Overflow network for questions, answers, tags, etc. It’s completely free with usage limits (no API key required for basic use)
  stackapps.com
  . Great for a coding assistant agent to search programming Q&A or for gathering community knowledge (e.g., common errors and solutions).

Freemium APIs:

NewsAPI.org – Aggregates news articles from 100k+ sources
newsapi.org
. Offers a free developer plan (e.g. 500 or 1,000 API calls/day) for non-commercial use, and paid plans for higher volume
newsapi.org
. Useful for agents doing real-time news monitoring or summarization.

Twitter API (v2) – Note: Twitter (now X) dramatically restricted its free tier. The free tier allows posting up to 1,500 tweets/month and no free read access
techcrunch.com
. Meaningful data retrieval now requires a paid Basic plan (~$100/month)
techcrunch.com
. Advanced agents can use the paid API for sentiment analysis, trend detection, etc., but for most users the free option is extremely limited post-2023.

Reddit API – Reddit’s API is free for personal use (with an API key) but has tightened rules on third-party apps (as of 2023). Agents can still retrieve posts and comments for research, within modest rate limits. Heavy usage or commercial use might require special approval or premium services. (Beginner agents can easily use this for small-scale data collection; advanced text-mining on Reddit may need additional arrangements.)

RapidAPI Hub – Not an API itself, but a marketplace that offers many community APIs (for sports scores, recipes, etc.) often with freemium models. Useful for quickly finding an API for a niche task (e.g., dictionary API, movie database API), usually offering a small free quota and paid options.

Paid APIs:

Bloomberg/Refinitiv APIs – Enterprise finance data APIs (historical stock prices, news, etc.) requiring expensive subscriptions. Used only in advanced, domain-specific agents (e.g., trading bots or economic research).

LexisNexis API – Paid access to legal and news archives. Suitable for specialized research agents in law or journalism (advanced users only).

Diffbot Knowledge Graph – A paid AI-curated knowledge graph of the web (entities, relationships extracted from billions of pages). This can feed an AI agent rich structured knowledge, but it’s a commercial service (with a free trial) – mostly for advanced users needing web-scale data aggregation.

## Language Translation APIs

Free APIs:

    LibreTranslate – An open-source translation API (with some free public endpoints). Allows translation between many languages without relying on big tech services. Good for personal projects or when data privacy is a concern (beginner-friendly if you find a hosted instance).

    IBM Watson Language Translator – IBM offers a Lite tier: 1,000,000 characters/month free
    ibm.com
    on their cloud. Supports dozens of languages. Useful for research agents that need basic translation, with easy upgrade to paid for more volume.

    Google Translate (Web) – While the Google Cloud Translation API is paid, the Google Translate web unofficial endpoints are sometimes used for free (not officially supported, and against TOS if automated extensively). For a beginner, using official APIs is recommended to avoid IP blocking.

Freemium APIs:

    Google Cloud Translation API – High-quality neural translation for 100+ languages. No always-free tier (beyond an initial free credit), so effectively a paid service. However, Google often provides $300 credits for new accounts. It charges per character translated (e.g., $20 per million chars). Best for intermediate users requiring consistent, automated translation in an agent.

    Microsoft Translator (Azure Cognitive Services) – Enterprise-grade translator. Free tier allows 2 million characters per month
    blogs.nottingham.ac.uk
    , then it’s pay-as-you-go. Integrates with Azure ecosystem. Great for agents that need multi-language support with a generous initial quota
    blogs.nottingham.ac.uk
    .

    DeepL API – A highly regarded translation API (especially for European languages). Offers DeepL API Free plan up to ~500k characters/month
    byteplus.com
    developers.deepl.com
    , then requires a subscription (DeepL Pro) for higher usage and better speed. Produces very fluent translations – ideal for agents summarizing or conversing across languages (beginner to intermediate friendly).

    Amazon Translate – AWS’s neural translation service. Has a free tier of 2M chars/month for 12 months for new users
    smartling.com
    . After that, it’s paid per million chars. Supports a wide range of languages. Integrates with other AWS AI (like Amazon Comprehend for language detection, etc.), suitable for intermediate users on AWS stack.

Paid APIs:

    Anthropic Claude API – (Also an AI model, but mentionable for translation tasks) It’s a large language model that can perform translation as part of its capabilities. Requires a paid API access – advanced usage where an agent might leverage a general AI model to translate and summarize simultaneously.

    Professional Localization APIs – e.g., Lilt or Smartling APIs, which provide translation memory and human-in-the-loop capabilities. These are enterprise services for advanced applications (e.g., an agent orchestrating human translators for high quality output).

    Yandex Translate API – A cloud translation API by Yandex (Russia’s equivalent to Google). It used to have a free tier, but currently likely requires a paid key for significant usage. Could be considered if an agent needs an alternate engine for redundancy or specific language pairs.

## Academic Research APIs

Free APIs:

    arXiv API – Allows programmatic search and retrieval of scholarly papers from arXiv (e-print repository heavily used in physics, math, CS). It’s completely open – developers can query by title, author, category, etc., and get paper metadata and abstracts
    info.arxiv.org
    info.arxiv.org
    . Perfect for research agents compiling literature reviews or finding relevant papers.

    CrossRef REST API – Provides metadata for millions of scholarly articles (DOIs, titles, authors, citations). It’s an open API accessible to all (no auth required for basic use)
    crossref.org
    . Agents can use it to look up DOI information or to find references/citations. CrossRef’s data powers reference managers – very useful for academic agents.

    OpenAlex API – An open index of the global research graph (papers, authors, institutions, concepts). Indexes over 250 million works with rich metadata
    ethz.ch
    . Free to use (CC0 data). Agents can leverage OpenAlex to find related works, citation counts, or build domain-specific knowledge graphs
    ethz.ch
    . This is a modern replacement for the former Microsoft Academic Graph.

    Semantic Scholar API – AI-driven scholarly data from Semantic Scholar (AI2). Provides paper details, citations, influential citations, authors, etc. Most endpoints are free to use without an API key (with generous rate limits, e.g. 1000 requests per second globally)
    semanticscholar.org
    ; an API key can provide higher dedicated limits. Excellent for literature discovery – e.g., an agent can find papers similar to a given paper, or get a paper’s summary and references
    semanticscholar.org
    .

    Unpaywall API – Offers free access to a database of Open Access papers. Given a DOI, it returns a link to a free PDF if available (from repositories or journals). Free and no request charges
    unpaywall.org
    (just rate limiting). Great for an academic agent trying to retrieve full-text PDFs for a list of references, legally
    unpaywall.org
    .

    PubMed E-Utilities – Free API for biomedical literature (Medline/PubMed). Allows searching by keywords, fetching article metadata, etc. Useful for healthcare or bio-oriented research agents to find relevant studies.

    DOI Content Negotiation – Not exactly an API, but using HTTP requests on a DOI can fetch metadata in JSON or BibTeX. This is free and provided by DOI registrars – an agent can quickly get citation info for a DOI by adding headers (advanced but handy trick).

Freemium/Academic APIs:

    Elsevier Scopus API – Provides article metadata, abstracts, and citation counts from Scopus (a large academic database). Free access is typically given to researchers or subscribers (with API keys), often through an institution. Limited to a certain number of queries per day for non-commercial use. Useful for advanced academic agents that need comprehensive search beyond arXiv/PubMed.

    Clarivate Web of Science API – Similar to Scopus, with subscription access. Provides rich metadata and citation data. Only for advanced use (requires WoS subscription).

    Dimensions API – An open academic search API by Digital Science. Free for research use (with API key request), offering access to publications, grants, patents data. It has higher limits than free public APIs but requires approval. A capable agent could use this for large-scale bibliometric analysis (intermediate to advanced users).

    CORE API – Aggregates open access research papers from many repositories. Free to use with an API key. Useful to get full-text or analyze research trends. For example, an agent could query CORE for all papers on a topic and then use an NLP model to summarize them.

    Lens.org API – Provides scholarly and patent data. Free tier available for academic use with registration. Could be harnessed by an agent doing innovation research, prior art searches, etc.

Paid APIs:

    Academic Knowledge APIs (paid) – Some providers offer premium data feeds (e.g., Semantic Scholar’s S2 Data via partners, or Clarivate’s custom data solutions). These are for heavy-duty use where an advanced agent needs big data dumps or live updates.

    Patent APIs – If an AI agent needs patent data: the USPTO and EPO have some open APIs, but commercial services like LexisNexis or Derwent have paid APIs for more curated patent analytics. Only relevant to specialized agents in legal/tech research.

## Productivity & Office Tool APIs

Free APIs:

    Google Calendar API – Enables reading and writing of calendar events. Free of charge with a Google account (it has usage quotas but no billing)
    elfsight.com
    . An AI assistant can use it to schedule meetings, list upcoming events, or find free time slots. (Beginner-friendly, well-documented by Google
    reddit.com
    ).

    Google Sheets & Drive API – Also free to use within Google’s usage limits (great for agents logging data or reading from spreadsheets). For example, an agent could output research results into a Google Sheet or read a task list from one.

    Notion API – Allows integration with Notion’s workspace (notes, databases). Free to use for any Notion user with an integration token. Lets an agent create or update pages, query databases, etc., making it powerful for note-taking or knowledge base management in workflows
    developers.notion.com
    . (Beginner to intermediate; excellent for building a personal research assistant that stores findings in Notion).

    Slack API (Web API & RTM) – Slack provides a free API for bots/apps in workspaces. It uses a tiered limit (free workspaces have rate limits but no direct cost). The Slack Web API is RPC-style and lets your app retrieve information or post messages to channels programmatically
    community.n8n.io
    . Great for AI agents that need to send alerts, summaries, or interact with users via chat. (Many AI research teams use Slack bots for notifications).

    Trello API – Lets you programmatically manage Trello boards, lists, and cards. Free with a Trello account (no extra cost). Useful for productivity agents – e.g., an agent that creates task cards for new research ideas or moves cards when tasks complete. The API can search across cards, update items, etc.
    developer.atlassian.com
    .

    Todoist API – A task management API (free for personal use with an API token). An agent can add tasks, check them off, or organize projects. For example, an AI agent could add “read this paper” as a Todoist task with a due date. (Beginner-friendly JSON API).

    Microsoft Graph API – Microsoft’s unified API for Office 365 (Outlook mail/calendar, OneDrive, Teams, etc.). Free to use with a free Microsoft account or organizational account, though some data (like corporate email) requires appropriate licensing. Allows an agent to do things like schedule meetings on Outlook, read OneNote notebooks, or send Teams messages. This is powerful but more complex (intermediate to advanced).

    Zapier Webhooks – Zapier offers a free tier where you can trigger zaps via webhook. While not a direct data API, an AI agent can use this to interface with hundreds of apps (Gmail, Asana, etc.) by triggering a Zapier workflow. Good for non-coders or quick integrations (though limited tasks in free plan).

Freemium/Subscription APIs:

    Notion AI (API integration) – Notion’s own AI features can be accessed within Notion, but no public API for them yet. However, as an example of “productivity AI,” one could imagine using the Notion API to feed content and then calling an OpenAI API to generate summaries, integrating back – a multi-API workflow.

    Zapier/IFTTT – Both offer APIs or webhooks that an agent can call to trigger automation. Free tier allows some usage (e.g., IFTTT’s webhooks are free for small applets, Zapier free tier has a limited number of tasks). For more extensive use, paid plans are needed. Useful to have an AI agent orchestrate other apps (e.g., if a new paper is found, the agent uses Zapier to email it and upload to Dropbox).

    Monday.com / Asana API – Project management tools with APIs. Typically require a team plan (paid) to get full API access. If an AI agent is managing project tasks or reporting status, these APIs could be used in advanced scenarios (e.g., updating a project board based on some analysis).

Paid APIs:

    Evernote API – Evernote’s older API allowed note creation and retrieval; Evernote now has a new platform and it might require a paid account. If someone still uses it, an agent could store notes or pull research snippets from Evernote.

    Confluence/Jira APIs – In a company setting, an AI agent might create pages or tickets. These require the user (or bot user) to have the appropriate license in Atlassian products. It’s not “paid API” per se (no additional fee beyond product subscription), but relevant in advanced organizational use.

    Enterprise Workflow APIs – E.g., SAP or SalesForce APIs – not relevant to research per se, but an AI agent in a corporate environment might interface with these (all are paid enterprise systems).

    Microsoft Power Automate API – Microsoft’s automation platform can be called via API but generally part of paid Office 365 plans. An AI agent could invoke flows that connect to legacy systems (advanced usage).

## Programming & Developer APIs

Free APIs:

    GitHub REST & GraphQL API – Provides programmatic access to virtually all GitHub data: repos, issues, commits, pull requests, etc. It’s free with authentication (rate limited, e.g., 5k requests/hour with a token). With this API, an AI coding assistant could create issues, comment on PRs, or fetch code for analysis
    geeksforgeeks.org
    . For example, an agent might use GitHub API to retrieve repository README files or to open an issue after detecting a security vulnerability.

    Stack Exchange API (Stack Overflow) – (Mentioned above in Data Retrieval but also relevant to programming.) Free and allows searching questions and answers. An AI developer assistant can use it to find solutions to error messages or coding problems on behalf of the user, then formulate an answer.

    Stack Overflow RSS/Stack API – In addition to the official API, simpler integrations like RSS feeds for new questions tags can be used by basic bots (free).

    GitLab API – Similar to GitHub’s, for GitLab users. Free to use on GitLab.com or self-hosted instances. Lets an agent manage repos or issues in GitLab projects.

    Package Registry APIs – e.g., NPM Registry or PyPI have free APIs to query packages (metadata, versions). Useful for an agent that needs to check for library updates or vulnerabilities.

    Judge0 Code Execution API – An open-source code runner API. There’s a free public instance (with limitations) that allows running code in multiple languages and returning the output. Great for an AI agent that needs to execute code snippets (e.g., evaluating user-written code in a lesson) without setting up its own sandbox (beginner-friendly via REST).

    JDoodle API – Another online compiler API offering free usage up to a certain limit (it supports 70+ languages). You get some free credits and then can pay for more
    jdoodle.com
    . This can turn an AI agent into a “cloud IDE,” running code on demand.

    Hacker News API – A free JSON API for the HN community, often used by dev-oriented agents to fetch trending discussion or tech news (no key needed). Could be useful for an agent that keeps a user updated on programming trends or major library releases.

Freemium APIs:

    OpenAI Codex API – (Part of OpenAI’s offerings, though not separate now as Codex, it’s integrated into GPT-4/GPT-3.5 for code). This is a paid API, but OpenAI did provide initial free credits. An AI coding agent might use it to generate or refactor code. Freemium in the sense of free trial credits and then pay-as-you-go.

    CircleCI API / GitHub Actions API – DevOps pipeline APIs, typically accessible with tokens (no extra cost, but the services themselves have free tiers). An advanced agent could trigger CI builds or check build statuses via these APIs if managing software projects.

    Snyk API or GitHub Security API – These can provide security scan results for dependencies. Free for open-source projects, paid for private – an agent could call them to warn about vulnerabilities in a project’s code (intermediate scenario for a cybersecurity coding assistant).

    StackExchange Triage/AI Assist API – Stack Overflow for Teams might have APIs to assist in knowledge base creation (hypothetical). Or using the Stack Exchange API for writing (with an API key for higher rate limits) – free for moderate use, but heavy use might hit limits and require partnership.

Paid/Advanced APIs:

    Compiler-as-a-Service – e.g., Sphere Engine API (allows running code in many languages, with a robust queue system). This is a paid alternative to free compilers, used in programming judges or education platforms. An AI agent tutoring programming might leverage it for scale beyond free limits.

    Static Analysis APIs – Some companies (like SonarQube) provide APIs to analyze code quality. These are usually self-hosted or enterprise tools, not open public APIs, but an advanced coding agent in a dev team could use such an API to give feedback on code.

    Developer Knowledge Bases – E.g., Microsoft Docs API or MDN Web Docs API (experimental) for documentation. If available, these tend to be free, but not widely used. A highly advanced programming agent might integrate directly with official docs via API instead of scraping HTML.

## AI & Machine Learning APIs

Free/Open APIs:

    Hugging Face Inference API – Allows running thousands of open-source ML models (for text generation, sentiment analysis, image recognition, etc.) via a unified API. Hugging Face offers a free access tier for small-scale use (limited number of calls)
    postman.com
    and a generous free trial for new users
    huggingface.co
    . Great for experimenting with different ML models (e.g., an agent can use a HuggingFace QA model for academic questions, or a image captioning model – all with one API). Beginner-friendly, since no deep ML setup is needed – just HTTP calls.

    IBM Watson Assistant/API – IBM offers some free tier for Watson AI services (NLU, speech, etc.) on IBM Cloud Lite. For example, Watson Assistant (chatbot) or Watson Natural Language Understanding have free monthly quotas. An AI agent could use these to analyze sentiment or entities in text, for instance, without immediate cost.

    OpenAI Gym/Universe – (If an agent interacts with learning environments, OpenAI Gym doesn’t have a remote API, it’s a local library; just noting it as AI-related – likely out of scope for “APIs” here.)

Freemium APIs:

    OpenAI API (GPT-3.5/GPT-4) – The most popular AI model API. OpenAI provides a pay-as-you-go service, but new users get a small free credit. It enables powerful language understanding and generation – an AI research agent can use GPT-4 to summarize articles, answer questions, or even generate code. Costs are usage-based (e.g., ~$0.003 per 1K tokens for GPT-3.5). No free tier beyond trial, so effectively freemium. (Intermediate – requires handling prompt design and cost management).

    Azure OpenAI Service – Microsoft’s hosted version of OpenAI models (GPT-4, GPT-3.5, etc.) on Azure. Pricing is similar to OpenAI’s, sometimes with Azure free credits available. Good for enterprise agents needing integration with Azure data (advanced scenario).

    Cohere AI API – Provides large language models for text generation and classification. They have a free trial and then a paid plan. Useful for agents that might need custom fine-tuned language models (e.g., for specific domains like legal or scientific text).

    AI21 Studio API – Offers Jurassic-2 family LLMs. Free tier includes some number of tokens, then paid. Could be used by an AI agent as an alternative to OpenAI for text generation or to ensemble multiple models.

    Anthropic Claude API – Claude is an AI assistant model, accessible via API (currently invite-only or limited release). It’s paid (pricing comparable to OpenAI’s), though some promotions may allow limited free use. Claude excels at dialogue and longer context – an agent might use it for conversational tasks or summarizing very long documents.

    Stability.ai (Stable Diffusion API) – For image generation tasks. Stability offers a cloud API (the DreamStudio API) to generate images from text. Freemium model: small free credits, then pay-per-image. An AI agent in a creative or research context might use this to generate illustrative images or data visualizations. (For example, an agent writing a report could generate an image of a concept).

    Google Cloud Vision AI – (Beyond OCR) includes Vision features like label detection, face detection, etc. 1,000 units/month free for features like label detection
    cloud.google.com
    , then paid. An agent can use this to analyze images in research (e.g., auto-tagging figures in papers or extracting text from charts).

    Google Cloud Natural Language API – NLP API for entity extraction, sentiment analysis, syntax. Has a free quota (usually a few thousand text records/month free) and then paid. An agent could use this to analyze sentiment of articles or extract key entities from documents automatically.

    AssemblyAI / OpenAI Whisper API – Speech-to-text APIs. AssemblyAI has a free trial, then paid, and OpenAI’s Whisper (via API) is paid per minute of audio. These allow an agent to transcribe audio (lectures, interviews) for analysis. For instance, an AI research assistant could transcribe a podcast about AI and summarize it.

Paid APIs:

    OpenAI GPT-4 (beyond free credits) – Usage is fully paid. Advanced agents might fine-tune models (OpenAI offers fine-tuning for some models for a fee) to specialize in certain research domains.

    DeepMind API – Not publicly offered, but in future if Google opens up models like PaLM or others via API (they have, under Google Cloud Vertex AI), those would be paid. E.g., PaLM 2 is accessible in Vertex AI with a pricing similar to OpenAI’s.

    SaaS AutoML APIs – E.g., Google AutoML, Amazon Sagemaker endpoints – these allow custom model training via API. They are paid services for advanced users (like training a custom image classifier for lab images and having your agent call it). Only for agents operated by users with ML expertise.

    Vision APIs (Advanced) – e.g., Google Video Intelligence API (paid for video content analysis), or Clarifai API (customizable vision models with a free tier but largely a paid service for significant use). These would let an agent analyze visual data deeply (e.g., detect objects in research experiment videos).

    OpenAI DALL-E 3 API – (if/when available) – would be paid per image generation. Could be used by an agent that needs to create visual content for reports or presentations, under user guidance.

    Enterprise AI platforms – IBM Watson has premium plans for higher throughput or data privacy, as do Azure and AWS for their AI services (e.g., training custom models). Those fall under paid tiers that advanced enterprise agents would use when operating at scale.

## Cybersecurity & Networking APIs

Free APIs:

    Shodan API – Allows search of internet-connected devices and vulnerabilities. Basic usage requires a free API key (obtained with a free account). The free tier (Shodan Membership) provides a limited number of query credits (e.g., 100 query credits/month) for searching the Shodan database
    help.shodan.io
    . This is enough for small research tasks, like an agent checking if a specific IP is open or querying how many devices run a certain software. More intensive use needs a paid plan.

    Have I Been Pwned (HIBP) API – An API to check if an email or password appears in known data breaches. The anonymized password check API is free (k-Anonymity model), but the full email search API now requires a modest subscription due to high demand. An agent could use the free password endpoint to help users assess password safety, for example.

    VirusTotal Public API – Provides crowd-sourced antivirus scan results for files and URLs. The public API is free but rate-limited to 4 requests/minute and 500 requests/day
    docs.virustotal.com
    . An AI security agent can use this to check if a downloaded file hash is malicious or if a URL is known for malware
    docs.virustotal.com
    . For low-volume personal use, this suffices (e.g., checking a few links or files a day).

    ipinfo.io or IP-API – Free IP geolocation and ISP lookup APIs (with daily limits). Useful for an agent that monitors network logs or needs to enrich data with location (e.g., “the login came from X country”).

    OTX (AlienVault Open Threat Exchange) API – Community threat intelligence feed. Free API to query threat indicators (IPs, domains) for known malicious activity. An agent could use this to warn if an IoC (indicator of compromise) appears in data.

    InternetDB (Shodan) – Shodan has introduced InternetDB, a no-key required API with basic info on open ports per IP, updated weekly
    news.ycombinator.com
    . Free for non-commercial use. An agent can quickly get an overview of an IP’s exposure using this without consuming Shodan credits.

Freemium APIs:

    Shodan (paid tiers) – For more queries or on-demand scanning, Shodan offers one-time payment options (e.g., $49 for Shodan membership) and API plans ranging from 10,000 queries to unlimited
    help.shodan.io
    . Advanced cybersecurity agents might leverage this to continuously monitor IP ranges or perform complex queries (e.g., all devices with a certain vulnerability in a region).

    VirusTotal Premium API – Provides higher rates and additional features (like downloading samples). Paid plans remove the 500/day limit and allow bulk scanning. An advanced malware analysis agent in a corporate SOC might use this for large-scale threat monitoring (where cost is justified).

    GreyNoise API – A service that labels IPs that are “noise” on the internet (like benign scanners). They have a free community API (limited daily queries) and paid tiers. Useful for filtering out false positives in threat data – an agent can ask GreyNoise if an IP hitting a honeypot is just a known scanner (freemium model).

    Have I Been Pwned (Enterprise) – HIBP offers a commercial API for querying breach data at scale (often used by domain administrators to check all company emails). An enterprise security agent could use this, but requires a subscription.

Paid APIs:

    Security Information APIs – e.g., CrowdStrike Falcon, FireEye APIs – these are vendor-specific and require their product subscription. An advanced agent integrated in an enterprise might use them to pull alerts or send data to those platforms.

    Vulnerability DB APIs – e.g., NVD (National Vulnerability Database) is free (bulk data feeds), but services like VulnDB or Kenna have APIs for enriched vulnerability data (paid). If an agent is doing automated vulnerability assessment, it might cross-reference CVEs via such APIs.

    Threat Intelligence Feeds – Many threat intel providers (Recorded Future, ThreatConnect) have APIs for subscribers. Only relevant to a very advanced AI agent in cybersecurity operations, and those are fully paid services.

    Penetration Testing APIs – Some tools like Qualys or Nessus have APIs to start scans or retrieve results (with a license). An automated security agent might use those to scan systems and then interpret the results.

Sources: The information and usage limits above are referenced from official documentation and reputable sources – for example, Google’s developer docs for API quotas
empowerlearning1.zohodesk.com
cloud.google.com
, Microsoft and IBM resource pages
blogs.nottingham.ac.uk
ibm.com
, as well as third-party analyses and community discussions for newer changes (e.g., Twitter’s API policy updates
techcrunch.com
, Brave Search API launch details
brave.com
, etc.). Each API’s linked documentation provides further details on up-to-date pricing and usage terms. This guide focuses on the current (2025) offerings and will be a useful starting point for selecting the right APIs for your AI agent’s needs.