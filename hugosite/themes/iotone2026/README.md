# iotone2026 — Hugo theme

Custom theme for [iotone.co](https://iotone.co) — 2026 refresh. Replaces the prior `hugrid` fork.

## What it ships

- **Spatial / XR studio aesthetic** — light + airy background (`#F7F6F2`), iridescent gradient accents (`#6E8CFF → #C062FF → #FF6FB8`), Inter typography.
- **Project showcase** sourced from `content/projects/*.md`, with status pills, language, GitHub link, optional hero visual (gradient or image).
- **News section** with magazine-style index and article view, year-grouped, RSS feed.
- **Per-page SEO** — `<title>`, meta description, canonical, Open Graph (og:type/title/description/url/image), Twitter card, JSON-LD `Organization` (home) + `Article` (news posts).
- **Mobile-first** — single-column layouts at &lt;880px.
- **Brand mark** — uses `static/images/thumbs/iotone_logo_v1d250x250.png` (project static, not theme static).

## Layouts

```
layouts/
  index.html              # home (hero, project showcase, news strip, about)
  _default/
    single.html           # generic single page (e.g. /contact/)
    list.html             # fallback list
  projects/
    list.html             # /projects/ index
    single.html           # /projects/<slug>/
  news/
    list.html             # /news/ magazine index
    single.html           # /news/<slug>/ article
  partials/
    head.html             # <head> with full SEO + OG + canonical
    seo.html              # SEO meta + Twitter card
    jsonld-organization.html
    jsonld-article.html
    header.html           # top nav + brand
    footer.html           # site footer with brand block, link cols, dynamic copyright
    nav-links.html        # shared nav link list
    project-card.html     # showcase panel
    news-strip.html       # 3-up recent news on home
```

## Frontmatter conventions

### `content/projects/<slug>.md`

```yaml
---
title: "Spectacles-polynode"
date: 2026-03-01
status: "active"             # active | shipped | eol | experiment
language: "TypeScript"
github_url: "https://github.com/IoTone/Spectacles-polynode"
weight: 10                   # lower = earlier on home showcase
featured: true               # appears on home showcase
hero_visual: "gradient"      # gradient | alt-1 | alt-2 | alt-3 | (image path)
pill: "Lensfest 2nd Place 2026"
summary: "The 'missing' web utility/core libraries for Snap Spectacles."
tags: ["spectacles", "ar", "polyfill"]
---
```

### `content/news/<date>-<slug>.md`

```yaml
---
title: "Polynode wins 2nd Place at Lensfest March 2026"
date: 2026-03-30
tags: ["award", "spectacles"]
summary: "..."               # optional dek shown on index + article
source_url: "https://..."    # optional external source attribution
og_image: "/images/full/iotone_logo_v1d.png"  # optional override
---
```

## Development

```sh
cd hugosite
hugo server -D       # http://localhost:1313
```

## Production build

```sh
cd hugosite
hugo -d ../public -b https://iotone.co/
```
