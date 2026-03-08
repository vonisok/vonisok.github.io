---
# the default layout is 'page'
title: Categories
icon: fas fa-layer-group
order: 1
---

{% assign live_categories = site.categories | sort %}

<section class="category-hub-hero">
  <p class="eyebrow">Category Hub</p>
  <h1>Browse the playbooks, not just the posts.</h1>
  <p>
    This page groups ideas by execution style so you can move from reading to building faster.
    Start with a track, scan recent posts, and pick one concrete move for this week.
  </p>
</section>

<section class="category-hub-section">
  <h2>Suggested Tracks</h2>
  <div class="suggested-track-grid">
    <article class="track-card">
      <p class="track-chip">Founder Track</p>
      <h3>Problem Validation</h3>
      <p>Interview-first workflows, fast demand checks, and risk reduction before code.</p>
      <ul>
        <li>10 customer conversations in 7 days</li>
        <li>One landing page with one clear promise</li>
        <li>Evidence log in Idea Map</li>
      </ul>
    </article>

    <article class="track-card">
      <p class="track-chip">MVP Build</p>
      <h3>Ship Thin, Learn Fast</h3>
      <p>Scope control, API-first architecture, and practical release loops for solo teams.</p>
      <ul>
        <li>Cut to one painful job-to-be-done</li>
        <li>Use paid APIs before custom infra</li>
        <li>Launch in 14 days max</li>
      </ul>
    </article>

    <article class="track-card">
      <p class="track-chip">Automation</p>
      <h3>Agent Workflows</h3>
      <p>Reusable automations for research, summaries, and API-driven production tasks.</p>
      <ul>
        <li>Design prompt + tool contracts</li>
        <li>Add retries, guardrails, monitoring</li>
        <li>Turn ops into templates</li>
      </ul>
    </article>

    <article class="track-card">
      <p class="track-chip">Research Systems</p>
      <h3>Decision Velocity</h3>
      <p>Run better market and technical research with source quality and citation hygiene.</p>
      <ul>
        <li>Define question scopes upfront</li>
        <li>Summarize with source links</li>
        <li>Convert findings into next actions</li>
      </ul>
    </article>
  </div>
</section>

<section class="category-hub-section">
  <div class="section-head">
    <h2>Live Categories</h2>
    <label class="category-search">
      <span>Filter</span>
      <input id="category-search-input" type="search" placeholder="Search categories..." autocomplete="off" />
    </label>
  </div>

  {% if live_categories.size > 0 %}
    <div class="live-category-grid" id="live-category-grid">
      {% for category in live_categories %}
      {% assign category_name = category[0] %}
      {% assign category_posts = category[1] %}
      {% assign category_url = '/categories/' | append: category_name | slugify | append: '/' %}
      <article class="live-category-card" data-category-name="{{ category_name | downcase }}">
        <div class="live-category-top">
          <a href="{{ category_url | relative_url }}">{{ category_name }}</a>
          <span>{{ category_posts.size }} post{% if category_posts.size != 1 %}s{% endif %}</span>
        </div>
        <p class="live-category-subtext">Recent in this category:</p>
        <ul>
          {% for post in category_posts limit: 3 %}
          <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
          {% endfor %}
        </ul>
      </article>
      {% endfor %}
    </div>
    <p id="category-search-empty" class="category-search-empty" hidden>No matching categories yet.</p>
  {% else %}
    <div class="empty-live-categories">
      <h3>No categories found yet</h3>
      <p>Add `categories: [your-category]` in post front matter and this section will auto-populate.</p>
    </div>
  {% endif %}
</section>

<section class="category-hub-section resource-strip">
  <h2>Starter Queue</h2>
  <div class="resource-grid">
    <article>
      <h3>Week 1 Sprint</h3>
      <p>Pick one category, publish one learning post, and capture one reusable template.</p>
    </article>
    <article>
      <h3>Ops Baseline</h3>
      <p>Track activation, retention, and conversion in one scorecard before scaling effort.</p>
    </article>
    <article>
      <h3>Knowledge Loop</h3>
      <p>Feed books, notes, and project outcomes back into your category system each Friday.</p>
    </article>
  </div>
</section>

<style>
.category-hub-hero {
  margin-top: .8rem;
  padding: 1.2rem 1.1rem;
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, .35));
  border-radius: 14px;
  background:
    radial-gradient(120% 130% at 95% 0%, rgba(59, 130, 246, .18), transparent 50%),
    radial-gradient(110% 130% at 0% 100%, rgba(16, 185, 129, .12), transparent 45%),
    var(--card-bg, rgba(127, 127, 127, .08));
}

.category-hub-hero .eyebrow {
  margin: 0;
  font-size: .75rem;
  letter-spacing: .11em;
  text-transform: uppercase;
  opacity: .75;
}

.category-hub-hero h1 {
  margin: .35rem 0 .55rem;
  font-size: clamp(1.45rem, 2.2vw, 2rem);
  line-height: 1.15;
}

.category-hub-hero p {
  margin: 0;
  max-width: 70ch;
  opacity: .9;
}

.category-hub-section {
  margin-top: 1.2rem;
}

.section-head {
  display: flex;
  gap: .7rem;
  align-items: end;
  justify-content: space-between;
  flex-wrap: wrap;
}

.category-search {
  display: grid;
  gap: .3rem;
}

.category-search span {
  font-size: .78rem;
  opacity: .8;
}

.category-search input {
  width: min(320px, 100%);
  font: inherit;
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, .35));
  border-radius: 9px;
  background: var(--card-bg, rgba(127, 127, 127, .08));
  color: inherit;
  padding: .46rem .6rem;
}

.suggested-track-grid,
.live-category-grid,
.resource-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
  gap: .72rem;
}

.track-card,
.live-category-card,
.resource-grid article,
.empty-live-categories {
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, .3));
  border-radius: 12px;
  background: var(--card-bg, rgba(127, 127, 127, .06));
}

.track-card,
.live-category-card,
.resource-grid article,
.empty-live-categories {
  padding: .78rem .82rem;
}

.track-chip {
  margin: 0 0 .35rem;
  display: inline-block;
  font-size: .68rem;
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, .35));
  border-radius: 999px;
  padding: .11rem .45rem;
  opacity: .9;
}

.track-card h3,
.resource-grid h3,
.empty-live-categories h3 {
  margin: 0 0 .3rem;
  font-size: 1.02rem;
}

.track-card p,
.resource-grid p,
.empty-live-categories p {
  margin: 0;
  opacity: .9;
}

.track-card ul {
  margin: .62rem 0 0;
  padding-left: 1rem;
  opacity: .95;
}

.track-card li {
  margin: .12rem 0;
}

.live-category-top {
  display: flex;
  justify-content: space-between;
  gap: .45rem;
  align-items: baseline;
}

.live-category-top a {
  font-weight: 700;
}

.live-category-top span {
  font-size: .75rem;
  opacity: .78;
}

.live-category-subtext {
  margin: .44rem 0 .3rem;
  font-size: .78rem;
  opacity: .75;
}

.live-category-card ul {
  margin: 0;
  padding-left: 1rem;
}

.live-category-card li {
  margin: .17rem 0;
}

.category-search-empty {
  margin-top: .55rem;
  opacity: .85;
}

.resource-strip {
  border-top: 1px dashed var(--card-border-color, rgba(128, 128, 128, .35));
  padding-top: 1rem;
}

@media (max-width: 700px) {
  .category-hub-hero {
    padding: 1rem .88rem;
  }
}
</style>

<script>
(() => {
  const input = document.getElementById('category-search-input');
  const cards = Array.from(document.querySelectorAll('.live-category-card'));
  const empty = document.getElementById('category-search-empty');

  if (!input || cards.length === 0) return;

  function applyCategorySearch() {
    const term = input.value.trim().toLowerCase();
    let visible = 0;

    cards.forEach((card) => {
      const show = term === '' || card.dataset.categoryName.includes(term);
      card.hidden = !show;
      if (show) visible += 1;
    });

    if (empty) empty.hidden = visible !== 0;
  }

  input.addEventListener('input', applyCategorySearch);
})();
</script>
