# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Two separate static personal websites — one academic, one industry — for Mostafa Habibi Dehsheikhi. Each site is fully self-contained and deploys independently to Netlify.

## Structure

```
academic/          ← Academic site (targets professors, collaborators, committees)
  index.html       ← Single-page site: Hero → About → Research → Publications → Teaching → Certifications → CV Download
  styles.css       ← All styles; --max-w: 900px
  script.js        ← Nav scroll shadow + hamburger toggle
  assets/
    photo.jpg      ← Profile photo
    resume.pdf     ← Academic CV
    photo-placeholder.svg  ← Fallback shown via onerror if photo.jpg missing

industry/          ← Industry site (targets hiring managers, recruiters)
  index.html       ← Single-page site: Hero → About → Skills → Projects → Experience → Certifications → Resume Download
  styles.css       ← All styles; --max-w: 960px (wider than academic)
  script.js        ← Identical nav logic to academic
  assets/          ← Same structure as academic/assets/

assets/            ← Source files only (NOT deployed); used to copy into each site's assets/
  profile-img.jpg  ← Source photo
  Resume.pdf       ← Source resume

resume.tex         ← LaTeX source for the CV (not deployed, untracked by git)
docs/superpowers/  ← Design spec and implementation plan (reference only)
```

## Previewing Locally

No build step. Open either HTML file directly in a browser:
- `academic/index.html`
- `industry/index.html`

Or serve with Python if you need proper MIME types:
```
python -m http.server 8000 --directory academic
python -m http.server 8001 --directory industry
```

## Deployment

Each site is deployed separately on Netlify by dragging its subfolder:
- Drag `academic/` → academic Netlify site
- Drag `industry/` → industry Netlify site

**Why self-contained subfolders:** Netlify sets the dragged folder as the site root, so `../assets/` would break. All assets must live inside `academic/assets/` or `industry/assets/`.

## Design System

Both sites share identical CSS custom properties (defined at top of each `styles.css`):

| Token | Value |
|---|---|
| `--color-primary` | `#1a2744` (navy) |
| `--color-accent` | `#2d7dd2` (steel blue) |
| `--color-surface` | `#f8f9fb` (off-white) |
| Font | Inter (Google Fonts) |

**Responsive breakpoints:**
- `≤ 768px` — hamburger nav, single-column layout
- `769px–1024px` — tablet adjustments (industry only: projects → 1 col, certs → 3 col)

## Key Patterns

**Nav behaviour** (`script.js` in both sites): Adds `.scrolled` to `#navbar` on scroll (triggers CSS shadow). Toggles `.open` on `.nav-links` for hamburger menu. Closes menu on nav link click.

**Photo fallback**: Both `<img src="assets/photo.jpg">` tags have `onerror="this.src='assets/photo-placeholder.svg';this.onerror=null;"` — the SVG renders automatically if the photo is missing.

**Certification links**: All 10 cert badges currently have `href="#"`. Replace with real Credly/Coursera/DataCamp URLs in both `academic/index.html` and `industry/index.html` (same order in both files).

## Content Source

All content originates from `resume.tex`. The two sites differ in tone:
- **Academic**: scholarly tone, shows publications list with badges, research area cards, teaching entries
- **Industry**: results-oriented tone, shows skill pill tags, project cards with tech stack badges, vertical timeline for experience
