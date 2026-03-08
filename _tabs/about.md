---
# the default layout is 'page'
title: Start Here
icon: fas fa-compass
order: 3
---

<section class="kh-hero kh-hero--cyan">
  <p class="kh-eyebrow">Knowledge Desk</p>
  <h1>A practical AI resource site for solo builders.</h1>
  <p>
    This site is a live reference point for what matters now: tools, market signals, working systems,
    and curated knowledge loops.
  </p>
</section>

<section class="kh-section">
  <h2>How to use this site</h2>
  <div class="kh-grid">
    <article class="kh-card">
      <h3>1. Scan current signals</h3>
      <p>Start with the home feed and read the newest radar posts first.</p>
    </article>
    <article class="kh-card">
      <h3>2. Explore channels</h3>
      <p>Use <a href="{{ '/categories/' | relative_url }}">Knowledge Channels</a> to focus by domain.</p>
    </article>
    <article class="kh-card">
      <h3>3. Pull resources</h3>
      <p>Use <a href="{{ '/tags/' | relative_url }}">Resource Index</a> for tools and references.</p>
    </article>
    <article class="kh-card">
      <h3>4. Track your own work</h3>
      <p>Use <a href="{{ '/idea-map/' | relative_url }}">Idea Map</a> and <a href="{{ '/books/' | relative_url }}">Books</a> for long-term learning.</p>
    </article>
  </div>
</section>

<section class="kh-section kh-panel">
  <h2>Editorial intent</h2>
  <p>Every post should answer one of these questions:</p>
  <ul class="kh-list">
    <li>What changed recently that founders should know?</li>
    <li>Which resources are worth attention right now?</li>
    <li>What signals should change product decisions this month?</li>
  </ul>
</section>

{% include knowledge_ui_styles.html %}
