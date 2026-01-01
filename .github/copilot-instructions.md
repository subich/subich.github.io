# Copilot Instructions for subich.github.io

## Overview

Personal portfolio website for Stefan Subich hosted on GitHub Pages.
Built with Jekyll (static site generator) using the `github-pages` gem for compatibility with GitHub Pages deployment.

**Type:** Static website / Jekyll site  
**Languages:** HTML, SCSS/CSS, JavaScript, Liquid templating, YAML, Markdown  
**Runtime:** Ruby 3.4.4, Jekyll 3.10.0 (via github-pages gem)  
**Size:** Small (~50 files)

## Build Commands

**Always use `mise` to manage the local Ruby environment.**
The `.tool-versions` file specifies Ruby 3.4.4.

### Setup (run once or after cleaning vendor/)

```bash
mise install
mise exec -- bundle install
```

### Build

```bash
mise exec -- bundle exec jekyll build
```

Output goes to `_site/` directory.
Build takes ~0.2 seconds.

### Local Development Server

```bash
mise exec -- bundle exec jekyll serve
```

Serves at <http://127.0.0.1:4000/> with auto-regeneration enabled.

### Clean Build

```bash
rm -rf _site .jekyll-cache .sass-cache
mise exec -- bundle exec jekyll build
```

## Validation

1. **Build must succeed** - Run `mise exec -- bundle exec jekyll build` and verify exit code 0
2. **Check for Liquid errors** - Build output shows errors if templates have syntax issues
3. **Verify _site/ output** - Key pages should exist: `_site/index.html`, `_site/about/index.html`, `_site/blog/index.html`

**Note:** The warning "To use retry middleware with Faraday v2.0+,
install `faraday-retry` gem" is expected and harmless.

## Project Layout

```
├── _config.yml          # Jekyll configuration (site title, author, plugins, nav)
├── _data/               # YAML data files
│   ├── programming-skills.yml
│   ├── other-skills.yml
│   ├── timeline.yml     # Work history for About page
│   └── social-media.yml # Social links config
├── _includes/           # Reusable HTML partials
│   ├── about/           # About page components (skills.html, timeline.html)
│   ├── blog/            # Blog components (index.html, search.html, tags.html)
│   ├── head.html        # <head> with CDN links (Bootstrap, Font Awesome, Animate.css)
│   ├── navbar.html      # Navigation bar
│   ├── footer.html      # Footer with social links
│   ├── landing.html     # Homepage content
│   └── scripts.html     # JS includes (Bootstrap, wow.js)
├── _layouts/            # Page templates
│   ├── default.html     # Base layout
│   ├── page.html        # Standard page
│   └── post.html        # Blog post with metadata
├── _sass/               # SCSS partials (imported via main.scss)
│   └── main.scss        # Imports all partials
├── assets/
│   ├── css/style.scss   # Entry point (imports _sass/main.scss)
│   └── js/theme.js      # Dark/light theme toggle
├── pages/               # Site pages
│   ├── index.html       # Homepage (permalink: /)
│   ├── about.md         # About page (permalink: /about/)
│   ├── blog.html        # Blog listing
│   └── 404.html
├── Gemfile              # Ruby dependencies (github-pages gem)
├── .tool-versions       # mise/asdf Ruby version (3.4.4)
└── CNAME                # Custom domain (subich.dev)
```

## Key Configuration (_config.yml)

- **Plugins:** `jemoji` (emoji support)
- **nav_exclude:** Pages excluded from navbar (tags, 404, index)
- **Author info:** Name, image, email, social handles (github, linkedin, mastodon)
- **Defaults:** Projects collection uses `page` layout

## Adding Content

### New Page

Create in `pages/` with front matter:

```yaml
---
layout: page
title: Page Title
permalink: /url-path/
weight: 4  # navbar order
---
```

### New Data Entry

Edit YAML files in `_data/`.
Skills use `name`, `percentage`, `color` fields.
Timeline uses `title`, `from`, `to`, `description`.

### Styling

**Prefer Markdown > HTML > CSS for stylistic changes:**
1. Use Markdown for formatting when possible (headings, emphasis, lists, etc.)
2. Use HTML when Markdown is insufficient (specific structure, classes, attributes)
3. Only edit CSS in `_sass/` when the desired effect cannot be accomplished in pure Markdown or HTML

Variables in `_variables.scss`.
Theme colors in `_theme.scss` and `_theme-dark.scss`.

## CI/CD

No GitHub Actions workflows.
Site deploys automatically via GitHub Pages when pushed to the default branch.
GitHub Pages builds Jekyll sites using the `github-pages` gem version specified in Gemfile.lock.

## Dependencies

- External CDNs: Bootstrap 5.3.7, Font Awesome 6.7.2, Animate.css 4.1.1, wow.js 1.1.2
- Google Fonts: Poppins, Chicago (via cdnfonts)

## Trust These Instructions

These instructions are accurate and verified.
Only search the codebase if information here is incomplete or found to be incorrect during execution.

If these instructions are found to be inaccurate,
update them to reflect the correct information.
