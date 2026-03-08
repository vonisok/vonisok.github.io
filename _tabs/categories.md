---
# the default layout is 'page'
title: Knowledge Channels
icon: fas fa-layer-group
order: 1
---

{% assign live_categories = site.categories | sort %}

<section class="kh-hero kh-hero--gold">
  <p class="kh-eyebrow">Current Knowledge</p>
  <h1>Browse by active knowledge channel.</h1>
  <p>Use channels to follow shifts in tools, markets, workflows, and operator strategy.</p>
</section>

<section class="kh-section">
  <h2>Core channels</h2>
  <div class="kh-grid">
    <article class="kh-card">
      <h3>Market Signals</h3>
      <p>What changed this month and why it matters.</p>
    </article>
    <article class="kh-card">
      <h3>Tooling Radar</h3>
      <p>Promising tools, stack updates, and practical tradeoffs.</p>
    </article>
    <article class="kh-card">
      <h3>Resource Stack</h3>
      <p>Libraries, datasets, communities, and references worth using.</p>
    </article>
    <article class="kh-card">
      <h3>Operator Systems</h3>
      <p>Routines and workflows that help solo teams execute consistently.</p>
    </article>
  </div>
</section>

<section class="kh-section">
  <div class="kh-toolbar">
    <h2>Live channels from posts</h2>
    <label class="kh-search">
      <span>Filter</span>
      <input id="channel-search" type="search" placeholder="Search channels..." autocomplete="off" />
    </label>
  </div>

  {% if live_categories.size > 0 %}
  <div class="kh-grid">
    {% for category in live_categories %}
    {% assign category_name = category[0] %}
    {% assign category_posts = category[1] %}
    {% assign category_url = '/categories/' | append: category_name | slugify | append: '/' %}
    <article class="kh-card js-live-card" data-category-name="{{ category_name | downcase }}">
      <div class="kh-live-head">
        <a href="{{ category_url | relative_url }}">{{ category_name }}</a>
        <span>{{ category_posts.size }} post{% if category_posts.size != 1 %}s{% endif %}</span>
      </div>
      <ul class="kh-list">
        {% for post in category_posts limit: 3 %}
        <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
        {% endfor %}
      </ul>
    </article>
    {% endfor %}
  </div>
  <p id="channel-empty" class="kh-empty" hidden>No matching channels.</p>
  {% else %}
  <p>No categories yet. Add categories to posts and this section auto-populates.</p>
  {% endif %}
</section>

{% include knowledge_ui_styles.html %}

<script>
(() => {
  const input = document.getElementById('channel-search');
  const cards = Array.from(document.querySelectorAll('.js-live-card'));
  const empty = document.getElementById('channel-empty');

  if (!input || cards.length === 0) return;

  function applyFilter() {
    const term = input.value.trim().toLowerCase();
    let visible = 0;

    cards.forEach((card) => {
      const show = term === '' || card.dataset.categoryName.includes(term);
      card.hidden = !show;
      if (show) visible += 1;
    });

    if (empty) empty.hidden = visible !== 0;
  }

  input.addEventListener('input', applyFilter);
})();
</script>
