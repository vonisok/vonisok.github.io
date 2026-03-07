---
# the default layout is 'page'
title: Books
icon: fas fa-book-open
order: 5
---

{% assign books = site.data.books | default: empty %}
{% assign grouped_books = books | sort: "title" | group_by_exp: "book", "book.category" %}

> A curated library for solo founders and builders. Add PDFs and first-page preview images to keep your reading system visual and searchable.

## Quick setup for adding books

1. Add a PDF file to: `assets/books/pdfs/`
2. Add a preview image (first page screenshot) to: `assets/books/covers/`
3. Add a new entry in: `_data/books.yml`

```yaml
- title: "Book Title"
  author: "Author Name"
  category: "Category Name"
  cover_image: "/assets/books/covers/book-title.jpg"
  pdf_url: "/assets/books/pdfs/book-title.pdf"
  description: "One-line summary"
```

---

{% if books.size > 0 %}
  {% for group in grouped_books %}
  <section class="book-category-block">
    <h2>{{ group.name }}</h2>
    <div class="book-grid">
      {% for book in group.items %}
      <article class="book-card">
        {% if book.cover_image %}
          <img src="{{ book.cover_image | relative_url }}" alt="{{ book.title }} preview image" loading="lazy" />
        {% else %}
          <div class="book-image-placeholder">No Preview Image</div>
        {% endif %}

        <div class="book-card-body">
          <h3>{{ book.title }}</h3>
          {% if book.author %}<p class="book-meta">By {{ book.author }}</p>{% endif %}
          {% if book.year %}<p class="book-meta">Published {{ book.year }}</p>{% endif %}
          {% if book.description %}<p>{{ book.description }}</p>{% endif %}

          {% if book.tags %}
          <p class="book-tags">
            {% for tag in book.tags %}
            <span>{{ tag }}</span>
            {% endfor %}
          </p>
          {% endif %}

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
  </section>
  {% endfor %}
{% else %}
  <p>No books added yet. Start by editing <code>_data/books.yml</code>.</p>
{% endif %}

<style>
.book-category-block {
  margin-top: 1.6rem;
}

.book-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}

.book-card {
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.25));
  border-radius: 12px;
  overflow: hidden;
  background: var(--card-bg, rgba(127, 127, 127, 0.06));
}

.book-card img,
.book-image-placeholder {
  width: 100%;
  height: 260px;
  object-fit: cover;
  display: block;
  background: rgba(127, 127, 127, 0.1);
}

.book-image-placeholder {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9rem;
  opacity: 0.75;
}

.book-card-body {
  padding: 0.9rem;
}

.book-card-body h3 {
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.book-meta {
  margin: 0;
  opacity: 0.85;
  font-size: 0.92rem;
}

.book-tags {
  display: flex;
  gap: 0.35rem;
  flex-wrap: wrap;
  margin-top: 0.7rem;
}

.book-tags span {
  font-size: 0.75rem;
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.35));
  border-radius: 999px;
  padding: 0.15rem 0.5rem;
}

.book-actions {
  margin-top: 0.9rem;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.book-actions a {
  display: inline-block;
  padding: 0.35rem 0.6rem;
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.35));
  border-radius: 8px;
  text-decoration: none;
}
</style>
