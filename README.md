# Personal Blog

A modern, responsive personal blog built with Jekyll and the beautiful Chirpy theme.

## 🌟 Features

- **Clean, Modern Design**: Professional and minimalist aesthetic
- **Dark/Light Mode**: Automatic theme switching with manual toggle
- **Responsive Layout**: Looks great on all devices
- **Search Functionality**: Fast and efficient content search
- **SEO Optimized**: Built-in SEO features for better visibility
- **Social Integration**: Easy social media sharing and contact options
- **Code Highlighting**: Beautiful syntax highlighting for code blocks
- **Categories & Tags**: Organized content discovery
- **Archives**: Timeline view of all posts

## 🚀 Quick Start

### Prerequisites

- Ruby (version 3.0 or higher)
- Bundler gem

### Local Development

1. **Clone the repository**:
   ```bash
   git clone https://github.com/vonisok/vonisok.github.io.git
   cd vonisok.github.io
   ```

2. **Install dependencies**:
   ```bash
   bundle install
   ```

3. **Run the site locally**:
   ```bash
   bundle exec jekyll serve
   ```

4. **View your site**: Open your browser to `http://localhost:4000`

## 📝 Writing Posts

Create new posts in the `_posts` directory using the naming convention: `YYYY-MM-DD-title.md`

### Front Matter Example

```yaml
---
title: Your Post Title
date: 2025-01-17 16:00:00 -0500
categories: [Category1, Category2]
tags: [tag1, tag2, tag3]
image:
  path: /path/to/image.jpg
  alt: Alt text for the image
---

Your post content here...
```

## ⚙️ Customization

### Personal Information

Edit `_config.yml` to update:
- Site title and description
- Your name and contact information
- Social media links
- Google Analytics ID (optional)
- Timezone

### Navigation

Customize the sidebar navigation by editing files in the `_tabs` directory:
- `categories.md` - Categories page
- `tags.md` - Tags page  
- `archives.md` - Archives page
- `about.md` - About page

### Contact Options

Edit `_data/contact.yml` to configure social media links in the sidebar.

### Sharing Options

Edit `_data/share.yml` to configure social sharing buttons on posts.

## 🎨 Theme Features

This site uses the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) theme, which includes:

- Progressive Web App (PWA) support
- Table of Contents for posts
- Code block copy buttons
- Math expression support (LaTeX)
- Mermaid diagram support
- Disqus comments integration
- Google Analytics integration

## 📚 Learn More

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Chirpy Theme Documentation](https://chirpy.cotes.page/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Suggestions and improvements are welcome! Feel free to open an issue or submit a pull request.

---

Built with ❤️ using [Jekyll](https://jekyllrb.com/) and [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) 