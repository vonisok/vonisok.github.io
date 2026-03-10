---
layout: post
title: "Post Title Goes Here"
description: "Write a clear search-friendly summary that explains what the post covers and why it matters."
date: 2026-03-10
categories: [primary-category, secondary-category]
tags: [topic-one, topic-two, topic-three]
permalink: /category/slug-goes-here/
author: Von
toc: true
excerpt_separator: "<!--more-->"
image:
  path: /assets/img/posts/your-post/hero.jpg
  alt: "Describe the featured image clearly for accessibility and SEO"
---

{% include editorial_post_styles.html %}

Start with a sharp opening sentence that tells the reader what happened, what this post explains, or why this subject matters now.

Add a second paragraph that expands the context and sets the stakes. Keep the opening readable, specific, and direct.  
<!--more-->

Use the third paragraph to define the article's promise. Tell the reader what they will learn, what evidence you are using, or what makes this post worth their time.

<div class="ep-intro-grid">
  <div>
    <p class="ep-lead">Write one strong lead paragraph here. This should read like the core thesis of the post and help the page feel premium immediately.</p>
  </div>
  {% include editorial_fact_card.html
    title="At a Glance"
    items="Key fact one||Key fact two||Key fact three||Key fact four||Key fact five"
  %}
</div>

{% include editorial_figure.html
  src="/assets/img/posts/your-post/hero.jpg"
  alt="Describe the visual clearly"
  caption="Use captions to add context, interpretation, or source significance."
%}

## Why This Matters

Open with the significance section early. This is where you explain the broader relevance of the subject and anchor the reader before going deeper.

## Main Section Heading

Write the main body in clean sections. Favor short paragraphs, useful subheads, and evidence-backed claims.

- Use bullets when the content is naturally list-shaped
- Keep each bullet high signal
- Avoid filler and vague transitions

{% include editorial_figure.html
  src="/assets/img/posts/your-post/supporting-image.jpg"
  alt="Supporting image alt text"
  caption="A second figure can break up long sections and support the argument visually."
%}

## Timeline or Sequence

Use this block when the post has a chronology or step-by-step progression.

<div class="ep-timeline">
  {% include editorial_timeline_card.html
    label="Date or Phase"
    body="Brief explanation of what happened in this phase and why it matters."
  %}
  {% include editorial_timeline_card.html
    label="Date or Phase"
    body="Add the second milestone, turning point, or sequence marker here."
  %}
  {% include editorial_timeline_card.html
    label="Date or Phase"
    body="Use the third card for outcome, public exposure, or downstream impact."
  %}
</div>

## Key Detail or Case Study

This is a good place for a concrete example, a specific person, a small narrative, or a focused subtopic.

{% include editorial_note.html
  title="Research Note"
  body="Use this for nuance, caution, controversy, source limitations, or an interpretive note that should stand out."
%}

## Image Gallery Section

Use a gallery when multiple visuals belong together conceptually.

{% capture example_gallery %}
/assets/img/posts/your-post/gallery-1.jpg|Describe image one|Write a concise caption for image one.||
/assets/img/posts/your-post/gallery-2.jpg|Describe image two|Write a concise caption for image two.||
/assets/img/posts/your-post/gallery-3.jpg|Describe image three|Write a concise caption for image three.
{% endcapture %}
{% include editorial_gallery.html items=example_gallery %}

## Primary Sources or References

Use source cards for document packs, official references, archives, or research links.

<div class="ep-source-grid">
  {% include editorial_source_card.html
    title="Primary Source Title"
    description="Explain what this source is and why it matters."
    url="https://example.com/source-one"
  %}
  {% include editorial_source_card.html
    title="Secondary Source Title"
    description="Use short descriptions that help readers understand what they will find."
    url="https://example.com/source-two"
  %}
  {% include editorial_source_card.html
    title="Archive or Database"
    description="This works especially well for archives, official repositories, and PDFs."
    url="https://example.com/source-three"
  %}
</div>

## Further Reading

- *Book or report title* - Author Name
- *Second title* - Author Name
- *Third title* - Author Name

## Closing Notes

End with a short section that helps the reader interpret the topic well.

1. State what is clearly documented.
2. Note what remains uncertain or debated.
3. Give the reader a sensible next step for deeper reading or follow-up.
