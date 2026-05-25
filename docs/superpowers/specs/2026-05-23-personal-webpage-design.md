# Personal Webpage Design Spec
**Date:** 2026-05-23  
**Author:** Mostafa Habibi Dehsheikhi  

---

## Overview

Two separate static websites — one academic, one industry — built with pure HTML/CSS/JS and deployed independently to Netlify. Both share a consistent visual brand but differ in tone and content emphasis. Content is sourced from `resume.tex`.

---

## Project Structure

```
Personal Webpage/
├── academic/
│   ├── index.html
│   ├── styles.css
│   └── script.js
├── industry/
│   ├── index.html
│   ├── styles.css
│   └── script.js
├── assets/
│   ├── resume.pdf          (shared downloadable CV/resume)
│   └── photo.jpg           (profile photo, to be provided by user)
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-05-23-personal-webpage-design.md
```

Each subfolder (`academic/` and `industry/`) is deployed as a separate Netlify site.

---

## Shared Brand Identity

Both sites use the same CSS custom properties for visual consistency. Tone differences come from content and copy, not from visual divergence.

| Token | Value | Usage |
|---|---|---|
| `--color-primary` | `#1a2744` | Nav, headings, footer |
| `--color-accent` | `#2d7dd2` | Links, buttons, badges |
| `--color-bg` | `#ffffff` | Page background |
| `--color-surface` | `#f8f9fb` | Cards, section backgrounds |
| `--color-text` | `#1e1e2e` | Body text |
| Font | Inter (Google Fonts) | All text |

**Navigation (both sites):**
- Sticky top bar
- Left: name as home link
- Right: anchor links to each section
- Hamburger menu on mobile (vanilla JS toggle)

**Overall style:** Clean and minimalist — generous whitespace, subtle card borders, no heavy gradients or decorative elements.

---

## Academic Site

**Target audience:** Professors, research collaborators, PhD committees, conference reviewers.  
**Tone:** Formal, scholarly, research-first.  
**Deploy target:** Separate Netlify site from `academic/` folder.

### Sections (scroll order)

**1. Hero**
- Name (large display type)
- Title: "Ph.D. Candidate in Computer Engineering"
- Institution: University of Texas at Dallas
- Research tagline: *"AI-powered video monitoring, computer vision, and agentic AI for healthcare"*
- Icon link row: Email · LinkedIn · Google Scholar · Credly · Personal site
- No photo in hero (academic convention)

**2. About Me**
- Profile photo (left, circular crop) + bio paragraph (right)
- Bio focuses on research identity, academic trajectory, and current dissertation focus
- Photo sourced from `../assets/photo.jpg` (user to provide)

**3. Research**
- 4 research area cards in a 2×2 responsive grid
- Areas derived from resume: Healthcare AI & Vision · Agentic AI & LLMs · Sports Analytics · Low-light & Medical Imaging
- Each card: icon + bold title + 2-sentence description

**4. Publications**
- Numbered list, newest first (10 entries from resume)
- Format per entry: authors · **title** · *venue* · year · award badge if applicable
- "Best Paper Award" badge on ICHI 2025 entry
- "(Under review)" / "(Submitted)" labels where applicable
- No cards — clean spaced list for readability

**5. Teaching**
- Two entries: Introduction to Electrical and Computer Engineering · Introduction to Digital Systems
- Format: course name, semesters (5 total), 1-line description

**6. Certifications**
- Responsive badge grid (5 columns desktop, 3 tablet, 2 mobile)
- 10 badges grouped by issuer: AWS (1) · Coursera (4) · DataCamp (5)
- Each badge: issuer logo + certification name + "Verify" link (URLs to be provided by user)

**7. CV Download**
- Full-width section with centered "Download Academic CV (PDF)" button
- Links to `../assets/resume.pdf`

---

## Industry Site

**Target audience:** Hiring managers, recruiters, engineering teams.  
**Tone:** Modern, results-oriented, skill-forward.  
**Deploy target:** Separate Netlify site from `industry/` folder.

### Sections (scroll order)

**1. Hero**
- Name (large display type)
- Title: "AI/ML Engineer & Researcher"
- Tagline: *"Building intelligent systems at the intersection of computer vision, LLMs, and healthcare AI"*
- Icon link row: Email · LinkedIn · GitHub · Credly
- "Download Resume" CTA button inline with hero content

**2. About Me**
- Same profile photo as academic site
- Bio reframed for industry: emphasizes what is *built* and *delivered*, not just research titles
- Highlights: 2+ years AWS, 3+ years computer vision systems, LLM/agentic pipelines

**3. Skills**
- 5 category groups, each with pill/badge-style skill tags
- Categories: AI, ML & Computer Vision · LLMs & Agentic Systems · Programming & Frameworks · Cloud & Data · Networking & Hardware
- Skills sourced directly from resume Skills section

**4. Projects**
- 5 project cards in a responsive grid
- Projects derived from resume research entries, reframed as deliverables:
  - Dual-Camera Behavioral Assessment Platform
  - Agentic FHIR Clinical Data Pipeline
  - AI Sports Analytics System
  - Vision-Language Patient Monitoring System
  - AI-Based Illumination-Aware Object Detection
- Each card: title · tech stack tags (e.g., YOLO, LangGraph, PyTorch) · 2-sentence impact description · optional link

**5. Experience**
- Timeline layout (vertical line with nodes)
- Entries: Graduate Research Assistant (UTD, Spring 2023–Present) · Teaching Assistant (UTD, 5 semesters) · Research Assistant (Shahid Bahonar, 2013–2015)
- Each entry: role · org · dates · 2–3 bullet points

**6. Certifications**
- Same badge grid layout as academic site (same 10 certs, same Verify links)

**7. Resume Download**
- Full-width section with centered "Download Resume (PDF)" button
- Links to `../assets/resume.pdf`

---

## Technical Notes

- **No build tools.** Plain `.html`, `.css`, `.js` files. Open in browser directly or serve with any static host.
- **Google Fonts.** Inter loaded via `<link>` in `<head>`. No self-hosting needed.
- **Responsive.** All layouts use CSS Grid and Flexbox with media queries. Mobile breakpoint at 768px, tablet at 1024px.
- **JS scope.** Only vanilla JS, used for: sticky nav shadow on scroll, hamburger menu toggle, smooth scroll to anchors.
- **Photo.** User will provide a photo file. Named `photo.jpg` and placed in `assets/`. Both sites reference `../assets/photo.jpg`.
- **Certifications.** User will provide individual credential URLs for each of the 10 certifications. Placeholder `href="#"` used until provided.
- **PDF.** User will provide or generate `resume.pdf`. Placed in `assets/`. Both sites reference `../assets/resume.pdf`.
- **Netlify deployment.** Each site deployed separately: point Netlify to the `academic/` subfolder for the academic site, and `industry/` for the industry site.

---

## Out of Scope

- Blog or news feed
- Contact form (email link is sufficient)
- CMS or dynamic content
- Dark mode toggle
- Analytics integration
- Custom domain configuration (handled post-build by user)
