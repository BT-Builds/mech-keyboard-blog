# Site Architecture for Mechanical Keyboards Affiliate Site

## Overview
This document outlines the architecture, file structure, content taxonomy, and SEO considerations for a static site built with Astro and deployed to GitHub Pages, targeting the mechanical keyboards affiliate niche.

## Static Site Generator Selection
**Chosen: Astro**
- Astro offers excellent performance with minimal JavaScript by default.
- Supports Markdown content collections, ideal for blog-style articles.
- Easy deployment to GitHub Pages via static site generation.
- Flexible templating with support for various UI frameworks (we'll use no framework for minimal JS).
- Hugo was considered but Astro's developer experience and built-in content optimizations make it more suitable for this content-focused site.

## File Layout
```
mechanical-keyboards-site/
├── public/
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── Disclosure.astro
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   └── Card.astro
│   ├── layouts/
│   │   ├── Layout.astro
│   │   └── ArticleLayout.astro
│   ├── pages/
│   │   ├── index.astro          # Home page
│   │   ├── categories/
│   │   │   └── [category].astro # Dynamic category pages
│   │   ├── about.astro
│   │   └── [...slug].astro      # Dynamic article pages (catch-all)
│   └── content/
│       ├── articles/
│       │   ├── *.md             # Article markdown files
│       │   └── config.ts        # Content collection config
│       └── config.ts            # Content collections configuration
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── README.md
```

### Key Directories
- `public/`: Static assets served at root.
- `src/components/`: Reusable UI components.
- `src/layouts/`: Layout wrappers for pages.
- `src/pages/`: Routing-based pages (Astro's file-based routing).
- `src/content/`: Markdown content collections for articles.

## Content Taxonomy
Articles are organized by:
1. **Categories** (e.g., "Typing", "Gaming", "Budget", "Customization", "Ergonomic", "Wireless", "Maintenance")
2. **Tags** (optional, for cross-cutting topics like "Keycaps", "Switches", "RGB")
3. **Date** (for chronological listings)

Each article in `src/content/articles/` includes frontmatter:
```markdown
---
title: "Article Title"
description: "Meta description for SEO"
pubDate: 2024-01-15
category: "Typing"
tags: ["Keycaps", "Switches"]
featured: false
---
```

## SEO Considerations
1. **Metadata**:
   - Each page defines `<title>` and `<meta description>` via Astro's `<Head>` component.
   - Open Graph tags for social sharing (og:title, og:description, og:image).
   - Twitter Card tags.

2. **Structure**:
   - Semantic HTML5 elements (header, nav, main, article, footer).
   - Proper heading hierarchy (H1 once per page, H2 for sections, etc.).
   - Breadcrumb navigation on article and category pages.

3. **Performance**:
   - Astro's automatic image optimization (when using `<Image>` component).
   - Minimal CSS: utility-first approach or scoped component CSS.
   - No JavaScript by default; interactive components load only when needed.

4. **Sitemap & Robots**:
   - Automatically generated sitemap.xml via Astro integration.
   - Robots.txt to allow crawling of all content.

5. **Affiliate Disclosure**:
   - A reusable `<Disclosure>` component placed at the beginning of every article.
   - Site-wide disclosure in the footer.

6. **Canonical URLs**:
   - Set canonical tag to avoid duplicate content issues.

## Disclosure Component
The `Disclosure.astro` component contains:
```astro
<p class="disclosure">
  As an Amazon Associate and affiliate with other programs, I earn from qualifying purchases.
  This helps support the site at no extra cost to you.
</p>
```
This component is imported and used in `ArticleLayout.astro` above the article content.

## CSS & Styling
- Use Astro's built-in `<style is:global>` or scoped component styles.
- Consider a minimal CSS framework like Pico.css or custom CSS for consistency.
- Dark mode support via CSS media query.

## Deployment to GitHub Pages
The site is built as static HTML and deployed to the `gh-pages` branch using GitHub Actions (see `.github/workflows/deploy.yml`).

## Development Commands
- `npm install` - Install dependencies
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview built site locally
