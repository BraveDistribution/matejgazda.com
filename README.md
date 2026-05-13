# matejgazda.com

Personal site and AI research blog. Built with [Quarto](https://quarto.org/),
deployed via GitHub Actions to GitHub Pages, served from the apex
`matejgazda.com`.

## Why Quarto

Quarto is the right tool for an AI / scientific blog: native math, code
highlighting, citations with hover preview, executable `.qmd` and `.ipynb`
documents, beautiful default theme, single binary install.

## Local development

Install Quarto ≥ 1.5 from <https://quarto.org/docs/get-started/>. Then:

```bash
git clone git@github.com:BraveDistribution/matejgazda.com.git
cd matejgazda.com
quarto preview     # live-reload at http://localhost:4xxx
```

To produce a one-shot build:

```bash
quarto render
```

Output goes to `_site/` (git-ignored).

## Adding content

### New blog post

Drop a Markdown or Quarto file into `posts/`:

```bash
$EDITOR posts/my-post-slug.qmd
```

Minimal front matter:

```yaml
---
title: "Post title"
date: 2026-05-13
description: "One-line summary."
categories: [machine-learning, medical-imaging]
---
```

For math, just write LaTeX inline: `$E = mc^2$` or block `$$ ... $$` — Quarto
renders via KaTeX automatically. For executable code, switch the chunk to
`{python}` or `{r}`:

````markdown
```{python}
import numpy as np
np.random.randn(3)
```
````

### Publications

Edit `publications.qmd`. For BibTeX-driven listings, see Quarto's [bibliography
support](https://quarto.org/docs/authoring/footnotes-and-citations.html).

### Projects

Edit `projects.qmd`.

## Project layout

```
_quarto.yml           Site config (navbar, theme, listings)
index.qmd             Home (profile + recent posts)
about.qmd
publications.qmd
projects.qmd
posts/
  index.qmd           Auto-listing of all posts
  _metadata.yml       Defaults for every post
  *.qmd               Individual posts
wp-assets/            Mirror of the old WordPress images/equations
assets/               SCSS theme + global CSS
CNAME                 Custom domain for GitHub Pages
.github/workflows/
  quarto.yml          CI: render + deploy to Pages
```

## WordPress migration

The original WordPress posts (2017–2019) were pulled via the WP REST API,
converted to Markdown, and live in `posts/` tagged `legacy`. All referenced
images and Jetpack-LaTeX `.gif` equations were mirrored into `wp-assets/`
(served at `/wp-assets/...`). Each ported post sets an `aliases:` entry so the
old URLs (`/tsp-algorithms-2-opt-3-opt-in-python/` etc.) keep working.

## Deployment

- Push to `main` → `.github/workflows/quarto.yml` renders and publishes.
- DNS: point `matejgazda.com` A records at GitHub Pages IPs
  (`185.199.108.153` etc.), enable HTTPS in repo Settings → Pages.
