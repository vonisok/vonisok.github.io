---
# the default layout is 'page'
title: Books
icon: fas fa-book-open
order: 5
---

{% assign books = site.data.books | default: empty %}
{% assign categories = books | map: 'category' | uniq | sort %}
{% assign subcategories = books | map: 'subcategory' | uniq | sort %}
{% assign category_defs = site.data.book_categories | default: empty %}

> A visual library with category + subcategory filters. Add first-page screenshots and PDFs, then browse everything in one compact grid.

## Quick setup

1. Add PDFs in `assets/books/pdfs/`
2. Add cover/first-page images in `assets/books/covers/`
3. Add entries in `_data/books.yml`

{% if category_defs.size > 0 %}
<section class="category-thumbnail-section">
  <h2>Browse by Category</h2>
  <div class="category-thumbnail-grid">
    {% for item in category_defs %}
    <button type="button" class="category-thumb-card" data-category-select="{{ item.name | downcase }}">
      {% if item.thumbnail %}
      <img src="{{ item.thumbnail | relative_url }}" alt="{{ item.name }} category thumbnail" loading="lazy" draggable="false" class="category-thumb-img" />
      {% else %}
      <div class="category-thumb-placeholder">{{ item.name }}</div>
      {% endif %}
      <span>{{ item.name }}</span>
    </button>
    {% endfor %}
  </div>
</section>
{% endif %}

<div class="book-filter-bar">
  <label>
    Category
    <select id="category-filter">
      <option value="all">All categories</option>
      {% for category in categories %}
      <option value="{{ category | downcase }}">{{ category }}</option>
      {% endfor %}
    </select>
  </label>

  <label>
    Subcategory
    <select id="subcategory-filter">
      <option value="all">All subcategories</option>
      {% for subcategory in subcategories %}
      {% if subcategory %}
      <option value="{{ subcategory | downcase }}">{{ subcategory }}</option>
      {% endif %}
      {% endfor %}
    </select>
  </label>

  <button id="reset-book-filters" type="button">Reset</button>
</div>

<p id="book-count" class="book-count"></p>

{% if books.size > 0 %}
<div class="book-grid" id="book-grid">
  {% for book in books %}
  <article class="book-card" data-category="{{ book.category | downcase }}" data-subcategory="{{ book.subcategory | downcase }}">
    {% if book.cover_image %}
      <img src="{{ book.cover_image | relative_url }}" alt="{{ book.title }} preview image" loading="lazy" />
    {% else %}
      <div class="book-image-placeholder">No Preview Image</div>
    {% endif %}

    <div class="book-card-body">
      <h3>{{ book.title }}</h3>
      {% if book.author %}<p class="book-meta">By {{ book.author }}</p>{% endif %}
      <p class="book-taxonomy">
        <span>{{ book.category }}</span>
        {% if book.subcategory %}<span>{{ book.subcategory }}</span>{% endif %}
      </p>

      <div class="book-actions">
        {% if book.pdf_url %}
        <a href="{{ book.pdf_url | relative_url }}" target="_blank" rel="noopener">Open PDF</a>
        {% endif %}
        {% if book.source_url %}
        <a href="{{ book.source_url }}" target="_blank" rel="noopener">External Link</a>
        {% endif %}
      </div>
    </div>
  </article>
  {% endfor %}
</div>
{% else %}
  <p>No books added yet. Start by editing <code>_data/books.yml</code>.</p>
{% endif %}

<style>
.category-thumbnail-section { margin-top: 1.2rem; }
.category-thumbnail-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(170px,1fr)); gap:0.7rem; margin-top:0.6rem; }
.category-thumb-card { border:1px solid var(--card-border-color, rgba(128,128,128,.35)); border-radius:10px; padding:0; overflow:hidden; background:transparent; color:inherit; cursor:pointer; }
.category-thumb-card img, .category-thumb-placeholder { width:100%; height:120px; object-fit:cover; display:block; background:transparent; }
.category-thumb-card .category-thumb-img { pointer-events:none; user-select:none; }
.category-thumb-placeholder { display:flex; align-items:center; justify-content:center; font-weight:600; }
.category-thumb-card span { display:block; padding:.45rem .55rem; font-size:.85rem; }

.book-filter-bar { margin:1.2rem 0 .8rem; display:flex; gap:.75rem; align-items:end; flex-wrap:wrap; }
.book-filter-bar label { display:grid; gap:.35rem; font-weight:600; }
.book-filter-bar select, .book-filter-bar button { font:inherit; border:1px solid var(--card-border-color, rgba(128,128,128,.35)); border-radius:8px; background:var(--card-bg, rgba(127,127,127,.08)); color:inherit; padding:.4rem .6rem; }
.book-count { opacity:.8; margin-bottom:.8rem; }

.book-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(190px,1fr)); gap:.9rem; }
.book-card { border:1px solid var(--card-border-color, rgba(128,128,128,.25)); border-radius:12px; overflow:hidden; background:var(--card-bg, rgba(127,127,127,.06)); }
.book-card img, .book-image-placeholder { width:100%; height:220px; object-fit:cover; display:block; background:rgba(127,127,127,.1); }
.book-image-placeholder { display:flex; align-items:center; justify-content:center; font-size:.9rem; opacity:.75; }
.book-card-body { padding:.75rem; }
.book-card-body h3 { margin:0 0 .3rem; font-size:1rem; }
.book-meta { margin:0; opacity:.85; font-size:.88rem; }
.book-taxonomy { margin:.55rem 0 0; display:flex; gap:.35rem; flex-wrap:wrap; }
.book-taxonomy span { font-size:.72rem; border:1px solid var(--card-border-color, rgba(128,128,128,.35)); border-radius:999px; padding:.12rem .45rem; }
.book-actions { margin-top:.7rem; display:flex; gap:.45rem; flex-wrap:wrap; }
.book-actions a { display:inline-block; font-size:.82rem; padding:.28rem .52rem; border:1px solid var(--card-border-color, rgba(128,128,128,.35)); border-radius:8px; text-decoration:none; }
</style>

<script>
(() => {
  const categoryFilter = document.getElementById('category-filter');
  const subcategoryFilter = document.getElementById('subcategory-filter');
  const resetBtn = document.getElementById('reset-book-filters');
  const cards = Array.from(document.querySelectorAll('.book-card'));
  const countEl = document.getElementById('book-count');
  const categoryButtons = Array.from(document.querySelectorAll('[data-category-select]'));

  if (!categoryFilter || !subcategoryFilter || cards.length === 0) return;

  function updateSubcategoryOptions() {
    const selectedCategory = categoryFilter.value;
    const allOptions = Array.from(subcategoryFilter.querySelectorAll('option'));

    allOptions.forEach((option) => {
      if (option.value === 'all') return (option.hidden = false);
      if (selectedCategory === 'all') return (option.hidden = false);
      option.hidden = !cards.some((card) => card.dataset.category === selectedCategory && card.dataset.subcategory === option.value);
    });

    if (subcategoryFilter.selectedOptions[0]?.hidden) subcategoryFilter.value = 'all';
  }

  function applyFilters() {
    const selectedCategory = categoryFilter.value;
    const selectedSubcategory = subcategoryFilter.value;
    let visibleCount = 0;

    cards.forEach((card) => {
      const categoryMatches = selectedCategory === 'all' || card.dataset.category === selectedCategory;
      const subcategoryMatches = selectedSubcategory === 'all' || card.dataset.subcategory === selectedSubcategory;
      const show = categoryMatches && subcategoryMatches;
      card.hidden = !show;
      if (show) visibleCount += 1;
    });

    countEl.textContent = `${visibleCount} book${visibleCount === 1 ? '' : 's'} shown`;
  }

  categoryFilter.addEventListener('change', () => { updateSubcategoryOptions(); applyFilters(); });
  subcategoryFilter.addEventListener('change', applyFilters);

  categoryButtons.forEach((button) => {
    button.addEventListener('click', () => {
      categoryFilter.value = button.dataset.categorySelect;
      subcategoryFilter.value = 'all';
      updateSubcategoryOptions();
      applyFilters();
      window.scrollTo({ top: categoryFilter.getBoundingClientRect().top + window.scrollY - 120, behavior: 'smooth' });
    });
  });

  resetBtn?.addEventListener('click', () => {
    categoryFilter.value = 'all';
    subcategoryFilter.value = 'all';
    updateSubcategoryOptions();
    applyFilters();
  });

  updateSubcategoryOptions();
  applyFilters();
})();
</script>
