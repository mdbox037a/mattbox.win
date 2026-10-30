# Site Administrator Guide

Welcome to the **mattbox.win** Administrator Guide. This document provides everything you need to know about managing site content, understanding the Astro SSG architecture, and configuring Cloudflare Pages for automatic deployments.

---

## 🏗️ Architecture & Framework Overview

**mattbox.win** is built as a static site using [Astro](https://astro.build/).

* **Static Site Generation (SSG)**: Astro compiles your source code, templates, and content files into raw, pre-rendered HTML, CSS, and SVG during the build phase (`npm run build`).
* **Zero Client-Side JavaScript**: The generated output in `dist/` contains zero client-side JavaScript overhead, ensuring lightning-fast page load times and top performance metrics.
* **Separation of Concerns**: Content is decoupled from page layouts and styling.

### Directory Structure

```
.
├── astro.config.mjs     # Astro configuration file
├── package.json         # Dependencies & npm scripts
├── docs/                # Administrator documentation & style guide
├── dist/                # Output directory generated during build (git-ignored)
└── src/
    ├── content/         # Structured content files (JSON/Markdown)
    │   └── site.json    # Homepage text, titles, and social profile links
    ├── layouts/         # Page shell & global styles
    │   └── Layout.astro # Base layout containing <head>, styles, and viewport config
    └── pages/           # Astro page routes
        └── index.astro  # Homepage entrypoint (renders Layout + site.json)
```

---

## 📝 Modifying Site Content

All site text content is managed in structured JSON files under `src/content/`.

### Updating the Homepage (`src/content/site.json`)

To modify the text or social links on the main page, open `src/content/site.json`:

```json
{
  "title": "mattbox.win",
  "paragraphs": [
    "Thanks for stopping by! This is just my site for experimenting with Cloudflare :)",
    "Please don't judge me - I don't know anything about web development..."
  ],
  "socials": [
    { "name": "GitHub", "url": "https://github.com/mdbox037a" },
    { "name": "LinkedIn", "url": "https://www.linkedin.com/in/matthewdbox/" }
  ]
}
```

* **`title`**: Displayed as the main heading (`<h1>`) and the `<title>` tag in the browser tab.
* **`paragraphs`**: Array of string sentences rendered in the main text body.
* **`socials`**: Array of social profile link objects (`name` and `url`). Adding a new item to this array automatically renders a new link separated by a bullet (`•`) in the footer.

### Adding New Pages in the Future

Astro uses file-based routing based on files in `src/pages/`:
1. Create a new `.astro` or `.md` file in `src/pages/` (e.g., `src/pages/about.astro` or `src/pages/projects.md`).
2. Astro will automatically generate the route at `mattbox.win/about` or `mattbox.win/projects`.

---

## 🛠️ Local Development & Build Commands

Run all commands from the root project directory:

| Command | Purpose |
| :--- | :--- |
| `npm run dev` | Starts a local development server at `http://localhost:4321` with hot-module reloading. |
| `npm run build` | Compiles the production site into static assets inside the `dist/` folder. |
| `npm run preview` | Previews the compiled `dist/` production build locally before pushing. |

---

## ☁️ Cloudflare Pages Configuration

The site automatically deploys on Cloudflare Pages whenever changes are merged into the `main` branch.

### Recommended Cloudflare Build Settings

When connecting or reviewing the Cloudflare Pages project configuration:

* **Framework Preset**: `Astro`
* **Build Command**: `npm run build`
* **Build Output Directory**: `dist`
* **Root Directory**: `/` (default)
* **Node.js Version**: `20.x` or `>=22.0.0` (Environment variable: `NODE_VERSION = 22`)

### How Deployment Works
1. A git commit or PR merge to `main` triggers a Cloudflare Pages deployment runner.
2. Cloudflare runs `npm install` and `npm run build`.
3. Cloudflare serves the generated static files in `dist/` directly from its global edge CDN.
