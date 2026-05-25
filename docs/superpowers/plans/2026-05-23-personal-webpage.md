# Personal Webpage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build two separate static personal websites (academic and industry) in pure HTML/CSS/JS, each self-contained in its own subfolder and deployable independently to Netlify.

**Architecture:** Each site is a single-page scrolling site with a sticky nav and anchor-linked sections. Both use identical CSS design tokens (navy/blue palette, Inter font) for visual consistency but differ in content tone. Each site is fully self-contained — its own `assets/` subfolder holds the photo and PDF so each folder can be drag-dropped to Netlify independently.

**Tech Stack:** HTML5, CSS3 (custom properties, Grid, Flexbox), vanilla JS (ES6), Google Fonts (Inter), Netlify for deployment.

---

## File Structure

```
Personal Webpage/
├── academic/
│   ├── index.html         — full single-page academic site
│   ├── styles.css         — design tokens + all academic styles
│   ├── script.js          — sticky nav shadow + hamburger menu
│   └── assets/
│       ├── photo.jpg      — profile photo (user provides)
│       └── resume.pdf     — academic CV (user provides)
├── industry/
│   ├── index.html         — full single-page industry site
│   ├── styles.css         — design tokens + all industry styles
│   ├── script.js          — same nav behaviour as academic
│   └── assets/
│       ├── photo.jpg      — same photo (copy from academic/assets/)
│       └── resume.pdf     — industry resume (may differ from academic CV)
└── docs/
    └── superpowers/
        ├── specs/2026-05-23-personal-webpage-design.md
        └── plans/2026-05-23-personal-webpage.md
```

> **Why self-contained subfolders:** Netlify deploys a folder as the site root. If `assets/` were at the project root, `../assets/photo.jpg` would resolve locally but break on Netlify since there is nothing above the deployed root. Keeping `assets/` inside each subfolder means paths are simply `assets/photo.jpg` and work identically locally and on Netlify.

---

## Task 1: Project scaffold

**Files:**
- Create: `academic/index.html`, `academic/styles.css`, `academic/script.js`
- Create: `industry/index.html`, `industry/styles.css`, `industry/script.js`
- Create: `academic/assets/`, `industry/assets/`
- Create: `.gitignore`

- [ ] **Step 1: Create directory structure**

Run in PowerShell from `C:\Users\Mostafa\Desktop\Personal Webpage`:
```powershell
New-Item -ItemType Directory -Force academic/assets, industry/assets
New-Item -ItemType File -Force academic/index.html, academic/styles.css, academic/script.js
New-Item -ItemType File -Force industry/index.html, industry/styles.css, industry/script.js
```

- [ ] **Step 2: Create .gitignore**

Create `.gitignore`:
```
.superpowers/
Thumbs.db
*.DS_Store
```

- [ ] **Step 3: Initialize git and commit**

```powershell
git init
git add .gitignore academic/ industry/ docs/
git commit -m "chore: project scaffold"
```

---

## Task 2: Academic site — HTML

**Files:**
- Modify: `academic/index.html`

Write the complete HTML for the academic site. All content comes from `resume.tex`.

- [ ] **Step 1: Write the full HTML**

Write `academic/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mostafa Habibi — Academic</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <nav id="navbar">
    <div class="nav-inner">
      <a href="#top" class="nav-logo">Mostafa Habibi</a>
      <button class="nav-toggle" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav-links">
        <li><a href="#about">About</a></li>
        <li><a href="#research">Research</a></li>
        <li><a href="#publications">Publications</a></li>
        <li><a href="#teaching">Teaching</a></li>
        <li><a href="#certifications">Certifications</a></li>
        <li><a href="#cv" class="nav-cta">CV</a></li>
      </ul>
    </div>
  </nav>

  <section id="top" class="hero">
    <div class="container">
      <h1>Mostafa Habibi Dehsheikhi</h1>
      <p class="hero-title">Ph.D. Candidate in Computer Engineering</p>
      <p class="hero-institution">University of Texas at Dallas</p>
      <p class="hero-tagline">AI-powered video monitoring, computer vision, and agentic AI for healthcare</p>
      <div class="hero-links">
        <a href="mailto:mxh220053@utdallas.edu" class="icon-link">Email</a>
        <a href="https://www.linkedin.com/in/mostafa-habibi-78b841284/" class="icon-link" target="_blank" rel="noopener">LinkedIn</a>
        <a href="https://scholar.google.com/citations?user=dHXIkhMAAAAJ&hl=en" class="icon-link" target="_blank" rel="noopener">Google Scholar</a>
        <a href="https://www.credly.com/users/mostafa-habibi-dehsheikhi/badges#credly" class="icon-link" target="_blank" rel="noopener">Credly</a>
      </div>
    </div>
  </section>

  <section id="about" class="section bg-surface">
    <div class="container about-grid">
      <div class="about-photo">
        <img src="assets/photo.jpg" alt="Mostafa Habibi" width="180" height="180">
      </div>
      <div class="about-text">
        <h2>About Me</h2>
        <p>I am a Ph.D. candidate in Computer Engineering at the University of Texas at Dallas, advised by Prof. Mehrdad Nourani. My research focuses on AI-driven healthcare monitoring systems that combine computer vision, deep learning, and large language models to analyze patient behavior, assess ambulation, and convert unstructured clinical data into structured, actionable information.</p>
        <p>I have published at IEEE EMBC, IEEE ICHI, IEEE SMARTCOMP, and IEEE SSIAI, and am a recipient of the IEEE Best Paper Award at ICHI 2025 and the ECE Doctoral Excellence Award (Spring 2026) at UTD.</p>
      </div>
    </div>
  </section>

  <section id="research" class="section">
    <div class="container">
      <h2>Research</h2>
      <div class="cards-grid">
        <div class="card">
          <div class="card-icon">🏥</div>
          <h3>Healthcare AI &amp; Vision</h3>
          <p>AI-driven systems for patient ambulation assessment, posture recognition, behavioral analysis, and human–object interaction using multi-camera platforms and vision-language models.</p>
        </div>
        <div class="card">
          <div class="card-icon">🤖</div>
          <h3>Agentic AI &amp; LLMs</h3>
          <p>Multi-agent orchestration pipelines for converting unstructured clinical notes into FHIR-compliant structured data, using LangChain, LangGraph, and locally deployed open-weight LLMs.</p>
        </div>
        <div class="card">
          <div class="card-icon">🏃</div>
          <h3>Sports Analytics</h3>
          <p>AI-based performance analysis for track and field athletes, including posture classification, kinematic analysis, and performance ranking using MediaPipe and machine learning.</p>
        </div>
        <div class="card">
          <div class="card-icon">🔬</div>
          <h3>Low-light &amp; Medical Imaging</h3>
          <p>Deep learning research in illumination-aware object detection, MRI-based radiogenomic classification, and contrast-free feature reconstruction for glioblastoma analysis.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="publications" class="section bg-surface">
    <div class="container">
      <h2>Selected Publications</h2>
      <ol class="publications-list">
        <li><strong>M. Habibi</strong> and M. Nourani, "Agentic AI to Augment Unstructured Data for Information Exchange and LLM," <em>IEEE Journal of Biomedical and Health Informatics (JBHI)</em>, 2026. <span class="badge badge-review">Under Review</span></li>
        <li>F. Parsaee, M. C. Stefan, and <strong>M. Habibi</strong>, "Reconstruction of T1-Weighted Contrast-Enhanced MRI for Glioblastoma Radiogenomic Classification," <em>IEEE EMBC</em>, 2026. <span class="badge badge-review">Submitted</span></li>
        <li><strong>M. Habibi</strong> and M. Nourani, "An Integrated Deep Learning Architecture for Illumination-Aware Object Detection," <em>IEEE SSIAI</em>, Santa Fe, NM, March 2026.</li>
        <li><strong>M. Habibi</strong>, M. Nourani, and M. M. Nourani, "AI-Based Performance Analysis for Track and Field Athletes," <em>IEEE EMBC</em>, Copenhagen, Denmark, July 2025.</li>
        <li><strong>M. Habibi</strong> and M. Nourani, "Utilizing Generative AI for Patient Behavioral Assessment," <em>IEEE DCAS</em>, 2025.</li>
        <li><strong>M. Habibi</strong>, Z. Delaram, M. Nourani, and D. H. Sullivan, "Video-Based Human-Object Interaction Analysis for Patient Behavioral Monitoring," <em>IEEE ICHI</em>, Rende, Italy, 2025. <span class="badge badge-award">Best Paper Award</span></li>
        <li><strong>M. Habibi</strong>, M. Nourani, and D. H. Sullivan, "A Scalable Dual-Camera Platform for Behavioral Assessment in Healthcare," <em>Journal of Healthcare Informatics Research (JHIR)</em>, 2025. <span class="badge badge-review">Submitted</span></li>
        <li><strong>M. Habibi</strong>, M. Nourani, and D. H. Sullivan, "An AI-Driven Camera-Based Platform for Patient Ambulation Assessment," <em>IEEE EMBC</em>, 2024.</li>
        <li><strong>M. Habibi</strong>, M. Nourani, and M. M. Nourani, "AI-Based Kinematic Analysis for Track Athletes," <em>IEEE SMARTCOMP</em>, Osaka, Japan, 2024.</li>
        <li><strong>M. Habibi</strong>, Z. Delaram, and M. Kouchaki, "HOPNET Enhanced Routing Protocol Using Bee Colony (Bee-HOPNET)," <em>18th International Conference on Recent Research in Science and Technology</em>, Dec. 2019.</li>
      </ol>
    </div>
  </section>

  <section id="teaching" class="section">
    <div class="container">
      <h2>Teaching</h2>
      <div class="teaching-list">
        <div class="teaching-item">
          <h3>Introduction to Electrical and Computer Engineering</h3>
          <p class="teaching-meta">Teaching Assistant · University of Texas at Dallas · Multiple Semesters</p>
          <p>Lab support, grading, office hours, and technical guidance on core engineering and programming concepts.</p>
        </div>
        <div class="teaching-item">
          <h3>Introduction to Digital Systems</h3>
          <p class="teaching-meta">Teaching Assistant · University of Texas at Dallas · Multiple Semesters</p>
          <p>Helped students understand digital logic and complete coursework through office hours and assignment guidance.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="certifications" class="section bg-surface">
    <div class="container">
      <h2>Certifications</h2>
      <div class="certs-grid">
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-aws">AWS</div>
          <span>AWS Certified AI Practitioner</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>Introduction to Generative AI Learning Path</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>IBM Data Science Professional Certificate</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>Introduction to Data Science</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>Multi-Agent Systems with LangGraph</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Understanding Prompt Engineering</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Introduction to AI Agents</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Building Scalable Agentic Systems</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Building AI Agents with Google ADK</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Introduction to Generative AI (DataCamp)</span>
        </a>
      </div>
      <p class="certs-note">Replace each <code>href="#"</code> with the individual credential URL (Credly, Coursera, or DataCamp) once available.</p>
    </div>
  </section>

  <section id="cv" class="section download-section">
    <div class="container text-center">
      <h2>Curriculum Vitae</h2>
      <p>Download my full academic CV as a PDF.</p>
      <a href="assets/resume.pdf" class="btn-download" download>Download Academic CV (PDF)</a>
    </div>
  </section>

  <footer>
    <div class="container">
      <p>&copy; 2026 Mostafa Habibi Dehsheikhi &middot; <a href="mailto:mxh220053@utdallas.edu">mxh220053@utdallas.edu</a></p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify structure**

Open `academic/index.html` directly in Chrome/Edge (no server needed). Unstyled is fine at this stage. Verify:
- All 6 section headings visible: About, Research, Publications, Teaching, Certifications, CV
- Publications list numbered 1–10
- Certifications section shows 10 links

- [ ] **Step 3: Commit**

```powershell
git add academic/index.html
git commit -m "feat: academic site HTML"
```

---

## Task 3: Academic site — CSS

**Files:**
- Modify: `academic/styles.css`

- [ ] **Step 1: Write the complete CSS**

Write `academic/styles.css`:

```css
/* ===== TOKENS ===== */
:root {
  --color-primary: #1a2744;
  --color-accent:  #2d7dd2;
  --color-bg:      #ffffff;
  --color-surface: #f8f9fb;
  --color-text:    #1e1e2e;
  --color-muted:   #6b7280;
  --color-border:  #e5e7eb;
  --font:          'Inter', sans-serif;
  --radius:        8px;
  --shadow:        0 1px 3px rgba(0,0,0,.08);
  --shadow-md:     0 4px 6px rgba(0,0,0,.07);
  --max-w:         900px;
  --nav-h:         64px;
}

/* ===== RESET ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body { font-family: var(--font); color: var(--color-text); background: var(--color-bg); line-height: 1.6; font-size: 16px; }
a { color: var(--color-accent); text-decoration: none; }
a:hover { text-decoration: underline; }
img { max-width: 100%; display: block; }
ul, ol { list-style: none; }
h2 { font-size: 1.75rem; font-weight: 700; color: var(--color-primary); margin-bottom: 1.5rem; }
h3 { font-size: 1.05rem; font-weight: 600; color: var(--color-primary); margin-bottom: .5rem; }

/* ===== LAYOUT ===== */
.container { max-width: var(--max-w); margin: 0 auto; padding: 0 1.5rem; }
.section    { padding: 5rem 0; }
.bg-surface { background: var(--color-surface); }
.text-center { text-align: center; }

/* ===== NAV ===== */
#navbar {
  position: sticky; top: 0; z-index: 100;
  background: var(--color-bg);
  border-bottom: 1px solid var(--color-border);
  height: var(--nav-h);
  transition: box-shadow .2s;
}
#navbar.scrolled { box-shadow: var(--shadow-md); }
.nav-inner {
  max-width: var(--max-w); margin: 0 auto; padding: 0 1.5rem;
  height: 100%; display: flex; align-items: center; justify-content: space-between;
}
.nav-logo { font-weight: 700; font-size: 1rem; color: var(--color-primary); }
.nav-logo:hover { text-decoration: none; }
.nav-links { display: flex; gap: 1.75rem; align-items: center; }
.nav-links a { font-size: .875rem; font-weight: 500; color: var(--color-text); }
.nav-links a:hover { color: var(--color-accent); text-decoration: none; }
.nav-cta {
  background: var(--color-accent); color: #fff !important;
  padding: .35rem .85rem; border-radius: var(--radius);
}
.nav-cta:hover { background: var(--color-primary); }
.nav-toggle {
  display: none; flex-direction: column; gap: 5px;
  background: none; border: none; cursor: pointer; padding: .25rem;
}
.nav-toggle span {
  display: block; width: 22px; height: 2px;
  background: var(--color-primary); border-radius: 2px;
}

/* ===== HERO ===== */
.hero { padding: 6rem 0 5rem; text-align: center; }
.hero h1 { font-size: 2.5rem; font-weight: 700; color: var(--color-primary); margin-bottom: .75rem; }
.hero-title { font-size: 1.15rem; font-weight: 600; color: var(--color-accent); margin-bottom: .25rem; }
.hero-institution { font-size: .95rem; color: var(--color-muted); margin-bottom: .75rem; }
.hero-tagline { font-size: .95rem; color: var(--color-muted); font-style: italic; max-width: 520px; margin: 0 auto 2rem; }
.hero-links { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; }
.icon-link {
  display: inline-block; padding: .4rem 1rem;
  border: 1.5px solid var(--color-border); border-radius: var(--radius);
  font-size: .875rem; font-weight: 500; color: var(--color-text);
  transition: border-color .2s, color .2s;
}
.icon-link:hover { border-color: var(--color-accent); color: var(--color-accent); text-decoration: none; }

/* ===== ABOUT ===== */
.about-grid { display: grid; grid-template-columns: auto 1fr; gap: 3rem; align-items: start; }
.about-photo img { width: 180px; height: 180px; border-radius: 50%; object-fit: cover; border: 3px solid var(--color-border); }
.about-text p { margin-bottom: 1rem; }
.about-text p:last-child { margin-bottom: 0; }

/* ===== RESEARCH CARDS ===== */
.cards-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.5rem; }
.card {
  background: var(--color-surface); border: 1px solid var(--color-border);
  border-radius: var(--radius); padding: 1.75rem; box-shadow: var(--shadow);
}
.card-icon { font-size: 1.75rem; margin-bottom: .75rem; }
.card p { color: var(--color-muted); font-size: .9rem; line-height: 1.6; }

/* ===== PUBLICATIONS ===== */
.publications-list { list-style: decimal; padding-left: 1.5rem; }
.publications-list li {
  margin-bottom: 1.25rem; padding-bottom: 1.25rem;
  border-bottom: 1px solid var(--color-border);
  font-size: .9rem; line-height: 1.7;
}
.publications-list li:last-child { border-bottom: none; margin-bottom: 0; }
.badge { display: inline-block; padding: .15rem .55rem; border-radius: 4px; font-size: .72rem; font-weight: 600; margin-left: .4rem; vertical-align: middle; }
.badge-award { background: #fef3c7; color: #92400e; }
.badge-review { background: #e0f2fe; color: #0369a1; }

/* ===== TEACHING ===== */
.teaching-list { display: flex; flex-direction: column; gap: 1.5rem; }
.teaching-item { border-left: 3px solid var(--color-accent); padding-left: 1.25rem; }
.teaching-meta { font-size: .82rem; color: var(--color-muted); margin-bottom: .4rem; }
.teaching-item p:last-child { font-size: .9rem; color: var(--color-muted); }

/* ===== CERTIFICATIONS ===== */
.certs-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 1rem; margin-bottom: 1rem; }
.cert-badge {
  display: flex; flex-direction: column; align-items: center; text-align: center;
  gap: .6rem; padding: 1rem .75rem;
  border: 1px solid var(--color-border); border-radius: var(--radius);
  background: var(--color-bg); color: var(--color-text);
  font-size: .78rem; font-weight: 500;
  transition: box-shadow .2s, border-color .2s;
}
.cert-badge:hover { box-shadow: var(--shadow-md); border-color: var(--color-accent); text-decoration: none; color: var(--color-primary); }
.cert-logo {
  width: 40px; height: 40px; border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: .72rem; color: #fff; flex-shrink: 0;
}
.cert-logo-aws      { background: #232f3e; }
.cert-logo-coursera { background: #0056d3; }
.cert-logo-datacamp { background: #03ef62; color: #000; }
.certs-note { font-size: .78rem; color: var(--color-muted); margin-top: .5rem; }

/* ===== DOWNLOAD ===== */
.download-section { background: var(--color-primary); }
.download-section h2 { color: #fff; }
.download-section p  { color: rgba(255,255,255,.72); margin-bottom: 1.5rem; }
.btn-download {
  display: inline-block; padding: .875rem 2.5rem;
  background: var(--color-accent); color: #fff;
  border-radius: var(--radius); font-weight: 600; font-size: 1rem;
  transition: background .2s, transform .1s;
}
.btn-download:hover { background: #1a5fa8; text-decoration: none; transform: translateY(-1px); }

/* ===== FOOTER ===== */
footer {
  background: var(--color-surface); border-top: 1px solid var(--color-border);
  padding: 1.5rem 0; text-align: center;
  font-size: .875rem; color: var(--color-muted);
}

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
  .hero h1 { font-size: 1.75rem; }
  h2 { font-size: 1.4rem; }
  .section { padding: 3rem 0; }

  .nav-links {
    display: none; flex-direction: column; gap: .5rem;
    position: absolute; top: var(--nav-h); left: 0; right: 0;
    background: var(--color-bg); border-bottom: 1px solid var(--color-border);
    padding: 1rem 1.5rem;
  }
  .nav-links.open { display: flex; }
  .nav-toggle { display: flex; }

  .about-grid { grid-template-columns: 1fr; text-align: center; }
  .about-photo { display: flex; justify-content: center; }
  .cards-grid { grid-template-columns: 1fr; }
  .certs-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .certs-grid { grid-template-columns: repeat(3, 1fr); }
}
```

- [ ] **Step 2: Open in browser and verify styling**

Open `academic/index.html`. Verify:
- Navy hero with name, blue subtitle, italic tagline, bordered icon links
- About section has grey circular avatar placeholder (or photo if provided)
- Research shows 2×2 card grid on white background
- Publications on light surface background, numbered list, yellow award badge on item 6
- Teaching items have left blue border
- Certifications show 5-column badge grid
- CV section has dark navy background, blue download button
- Nav sticks to top

- [ ] **Step 3: Commit**

```powershell
git add academic/styles.css
git commit -m "feat: academic site CSS"
```

---

## Task 4: Academic site — JavaScript

**Files:**
- Modify: `academic/script.js`

- [ ] **Step 1: Write the script**

Write `academic/script.js`:

```js
(function () {
  const navbar   = document.getElementById('navbar');
  const toggle   = document.querySelector('.nav-toggle');
  const navLinks = document.querySelector('.nav-links');

  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 10);
  }, { passive: true });

  toggle.addEventListener('click', () => {
    const open = navLinks.classList.toggle('open');
    toggle.setAttribute('aria-expanded', String(open));
  });

  navLinks.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      navLinks.classList.remove('open');
      toggle.setAttribute('aria-expanded', 'false');
    });
  });
})();
```

- [ ] **Step 2: Verify in browser**

Open `academic/index.html`. In Chrome DevTools, set device to iPhone 12 Pro (390px wide):
- Hamburger icon (three bars) appears in top-right
- Click it — nav links drop down as a vertical list
- Click any nav link — dropdown closes, page scrolls to section

On desktop (full width):
- Scroll past the hero — nav bar gains a subtle shadow

- [ ] **Step 3: Commit**

```powershell
git add academic/script.js
git commit -m "feat: academic site JS"
```

---

## Task 5: Industry site — HTML

**Files:**
- Modify: `industry/index.html`

- [ ] **Step 1: Write the full HTML**

Write `industry/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mostafa Habibi — AI/ML Engineer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <nav id="navbar">
    <div class="nav-inner">
      <a href="#top" class="nav-logo">Mostafa Habibi</a>
      <button class="nav-toggle" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav-links">
        <li><a href="#about">About</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#experience">Experience</a></li>
        <li><a href="#certifications">Certifications</a></li>
        <li><a href="#resume" class="nav-cta">Resume</a></li>
      </ul>
    </div>
  </nav>

  <section id="top" class="hero">
    <div class="container">
      <h1>Mostafa Habibi Dehsheikhi</h1>
      <p class="hero-title">AI/ML Engineer &amp; Researcher</p>
      <p class="hero-tagline">Building intelligent systems at the intersection of computer vision, LLMs, and healthcare AI</p>
      <div class="hero-links">
        <a href="mailto:mostafa.habibi6010@gmail.com" class="icon-link">Email</a>
        <a href="https://www.linkedin.com/in/mostafa-habibi-78b841284/" class="icon-link" target="_blank" rel="noopener">LinkedIn</a>
        <a href="https://github.com/habibi6010" class="icon-link" target="_blank" rel="noopener">GitHub</a>
        <a href="https://www.credly.com/users/mostafa-habibi-dehsheikhi/badges#credly" class="icon-link" target="_blank" rel="noopener">Credly</a>
        <a href="assets/resume.pdf" class="btn-hero" download>Download Resume</a>
      </div>
    </div>
  </section>

  <section id="about" class="section bg-surface">
    <div class="container about-grid">
      <div class="about-photo">
        <img src="assets/photo.jpg" alt="Mostafa Habibi" width="180" height="180">
      </div>
      <div class="about-text">
        <h2>About Me</h2>
        <p>I am an AI/ML engineer and researcher with 3+ years of hands-on experience building production-grade computer vision systems, LLM-powered pipelines, and cloud-connected AI applications. I specialize in designing and delivering end-to-end intelligent systems — from multi-camera tracking and object detection to agentic AI workflows and FHIR-compliant data pipelines.</p>
        <p>Currently completing my Ph.D. at the University of Texas at Dallas, I have shipped AI systems used in real healthcare settings, published at top IEEE venues, and hold the AWS Certified AI Practitioner credential. I bring strong Python, PyTorch, and AWS skills alongside a practical engineering mindset focused on results.</p>
      </div>
    </div>
  </section>

  <section id="skills" class="section">
    <div class="container">
      <h2>Skills</h2>
      <div class="skills-groups">
        <div class="skill-group">
          <h3>AI, ML &amp; Computer Vision</h3>
          <div class="skill-tags">
            <span>Computer Vision</span><span>Deep Learning</span><span>Object Detection</span>
            <span>YOLO</span><span>MediaPipe</span><span>OpenCV</span><span>PyTorch</span>
            <span>3D Localization</span><span>Multi-Camera Tracking</span><span>Image Enhancement</span>
          </div>
        </div>
        <div class="skill-group">
          <h3>LLMs &amp; Agentic Systems</h3>
          <div class="skill-tags">
            <span>LLMs</span><span>RAG</span><span>Agentic AI</span><span>Multi-Agent Systems</span>
            <span>LangChain</span><span>LangGraph</span><span>Prompt Engineering</span>
            <span>n8n</span><span>Workflow Automation</span><span>Tool Calling</span>
          </div>
        </div>
        <div class="skill-group">
          <h3>Programming &amp; Frameworks</h3>
          <div class="skill-tags">
            <span>Python</span><span>Java</span><span>C/C++</span><span>JavaScript</span>
            <span>SQL</span><span>Flask</span><span>scikit-learn</span><span>pandas</span>
            <span>NumPy</span><span>MATLAB</span><span>Bash</span>
          </div>
        </div>
        <div class="skill-group">
          <h3>Cloud &amp; Data</h3>
          <div class="skill-tags">
            <span>AWS EC2</span><span>AWS S3</span><span>AWS Lambda</span><span>API Gateway</span>
            <span>Cloud Deployment</span><span>Data Pipelines</span><span>SQL Server</span>
            <span>Schema Design</span><span>EER Modeling</span>
          </div>
        </div>
        <div class="skill-group">
          <h3>Networking &amp; Hardware</h3>
          <div class="skill-tags">
            <span>CCNA</span><span>TCP/IP</span><span>Windows Server</span><span>CompTIA A+</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="projects" class="section bg-surface">
    <div class="container">
      <h2>Projects</h2>
      <div class="projects-grid">
        <div class="project-card">
          <h3>Dual-Camera Behavioral Assessment Platform</h3>
          <div class="tech-tags"><span>YOLO</span><span>DeepFace</span><span>SIFT</span><span>Epipolar Geometry</span><span>Python</span></div>
          <p>Designed a dual-camera system integrating YOLO, DeepFace, SIFT-based matching, and triangulation for robust patient tracking and human–object interaction analysis in clinical environments.</p>
        </div>
        <div class="project-card">
          <h3>Agentic FHIR Clinical Data Pipeline</h3>
          <div class="tech-tags"><span>LangGraph</span><span>LangChain</span><span>LLMs</span><span>FHIR</span><span>Python</span></div>
          <p>Built a multi-agent AI platform that converts unstructured clinical notes into standardized, queryable FHIR-compliant structured data using adaptive auditing and locally deployed open-weight LLMs.</p>
        </div>
        <div class="project-card">
          <h3>AI Sports Analytics System</h3>
          <div class="tech-tags"><span>MediaPipe</span><span>Random Forest</span><span>PCA</span><span>FFT</span><span>PyTorch</span></div>
          <p>Developed AI-based performance analysis for track and field athletes — posture classification, kinematic analysis, and performance ranking using landmark extraction and ART2 clustering.</p>
        </div>
        <div class="project-card">
          <h3>Vision-Language Patient Monitoring System</h3>
          <div class="tech-tags"><span>YOLO</span><span>LLMs</span><span>Flask</span><span>AWS</span><span>Python</span></div>
          <p>Built scalable vision-language systems combining computer vision outputs with LLM summarization to generate clinically relevant patient behavior reports for caregivers, deployed on AWS.</p>
        </div>
        <div class="project-card">
          <h3>Illumination-Aware Object Detection</h3>
          <div class="tech-tags"><span>PyTorch</span><span>Deep Learning</span><span>OpenCV</span><span>YOLO</span></div>
          <p>Designed and evaluated an integrated deep learning architecture for robust object detection under challenging low-light conditions, published at IEEE SSIAI 2026.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="experience" class="section">
    <div class="container">
      <h2>Experience</h2>
      <div class="timeline">
        <div class="timeline-item">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <div class="timeline-header">
              <div>
                <h3>Graduate Research Assistant</h3>
                <p class="timeline-org">University of Texas at Dallas, Richardson, TX</p>
              </div>
              <span class="timeline-date">Spring 2023 – Present</span>
            </div>
            <ul>
              <li>Led healthcare AI projects using YOLO, MediaPipe, monocular depth estimation, and multi-camera 3D localization.</li>
              <li>Built an agentic AI platform for converting clinical notes to FHIR-compliant structured data using LangChain and LangGraph.</li>
              <li>Developed cloud-connected AI workflows on AWS EC2, S3, Lambda, and API Gateway.</li>
            </ul>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <div class="timeline-header">
              <div>
                <h3>Teaching Assistant</h3>
                <p class="timeline-org">University of Texas at Dallas, Richardson, TX</p>
              </div>
              <span class="timeline-date">5 Semesters</span>
            </div>
            <ul>
              <li>Assisted with Introduction to ECE and Introduction to Digital Systems.</li>
              <li>Provided lab support, grading, and office hours for undergraduate students.</li>
            </ul>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <div class="timeline-header">
              <div>
                <h3>Research Assistant</h3>
                <p class="timeline-org">Shahid Bahonar University, Kerman, Iran</p>
              </div>
              <span class="timeline-date">Aug 2013 – Aug 2015</span>
            </div>
            <ul>
              <li>Conducted research in mobile ad hoc networks (MANETs) and routing algorithms.</li>
              <li>Fully funded by the Ministry of Science, Research, and Technology.</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="certifications" class="section bg-surface">
    <div class="container">
      <h2>Certifications</h2>
      <div class="certs-grid">
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-aws">AWS</div>
          <span>AWS Certified AI Practitioner</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>Introduction to Generative AI Learning Path</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>IBM Data Science Professional Certificate</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>Introduction to Data Science</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-coursera">C</div>
          <span>Multi-Agent Systems with LangGraph</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Understanding Prompt Engineering</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Introduction to AI Agents</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Building Scalable Agentic Systems</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Building AI Agents with Google ADK</span>
        </a>
        <a href="#" class="cert-badge" target="_blank" rel="noopener">
          <div class="cert-logo cert-logo-datacamp">DC</div>
          <span>Introduction to Generative AI (DataCamp)</span>
        </a>
      </div>
      <p class="certs-note">Replace each <code>href="#"</code> with the individual credential URL once available.</p>
    </div>
  </section>

  <section id="resume" class="section download-section">
    <div class="container text-center">
      <h2>Resume</h2>
      <p>Download my one-page resume as a PDF.</p>
      <a href="assets/resume.pdf" class="btn-download" download>Download Resume (PDF)</a>
    </div>
  </section>

  <footer>
    <div class="container">
      <p>&copy; 2026 Mostafa Habibi Dehsheikhi &middot; <a href="mailto:mostafa.habibi6010@gmail.com">mostafa.habibi6010@gmail.com</a></p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify structure**

Open `industry/index.html` (unstyled is fine). Verify:
- 6 section headings: About, Skills, Projects, Experience, Certifications, Resume
- Skills section has 5 groups
- Projects section has 5 cards
- Experience section has 3 entries

- [ ] **Step 3: Commit**

```powershell
git add industry/index.html
git commit -m "feat: industry site HTML"
```

---

## Task 6: Industry site — CSS

**Files:**
- Modify: `industry/styles.css`

- [ ] **Step 1: Write the complete CSS**

Write `industry/styles.css` — identical design tokens and base styles as academic, plus industry-specific components (skills, projects, timeline):

```css
/* ===== TOKENS ===== */
:root {
  --color-primary: #1a2744;
  --color-accent:  #2d7dd2;
  --color-bg:      #ffffff;
  --color-surface: #f8f9fb;
  --color-text:    #1e1e2e;
  --color-muted:   #6b7280;
  --color-border:  #e5e7eb;
  --font:          'Inter', sans-serif;
  --radius:        8px;
  --shadow:        0 1px 3px rgba(0,0,0,.08);
  --shadow-md:     0 4px 6px rgba(0,0,0,.07);
  --max-w:         960px;
  --nav-h:         64px;
}

/* ===== RESET ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body { font-family: var(--font); color: var(--color-text); background: var(--color-bg); line-height: 1.6; font-size: 16px; }
a { color: var(--color-accent); text-decoration: none; }
a:hover { text-decoration: underline; }
img { max-width: 100%; display: block; }
ul { list-style: none; }
h2 { font-size: 1.75rem; font-weight: 700; color: var(--color-primary); margin-bottom: 1.5rem; }
h3 { font-size: 1.05rem; font-weight: 600; color: var(--color-primary); margin-bottom: .5rem; }

/* ===== LAYOUT ===== */
.container { max-width: var(--max-w); margin: 0 auto; padding: 0 1.5rem; }
.section    { padding: 5rem 0; }
.bg-surface { background: var(--color-surface); }
.text-center { text-align: center; }

/* ===== NAV ===== */
#navbar {
  position: sticky; top: 0; z-index: 100;
  background: var(--color-bg); border-bottom: 1px solid var(--color-border);
  height: var(--nav-h); transition: box-shadow .2s;
}
#navbar.scrolled { box-shadow: var(--shadow-md); }
.nav-inner {
  max-width: var(--max-w); margin: 0 auto; padding: 0 1.5rem;
  height: 100%; display: flex; align-items: center; justify-content: space-between;
}
.nav-logo { font-weight: 700; font-size: 1rem; color: var(--color-primary); }
.nav-logo:hover { text-decoration: none; }
.nav-links { display: flex; gap: 1.75rem; align-items: center; }
.nav-links a { font-size: .875rem; font-weight: 500; color: var(--color-text); }
.nav-links a:hover { color: var(--color-accent); text-decoration: none; }
.nav-cta { background: var(--color-accent); color: #fff !important; padding: .35rem .85rem; border-radius: var(--radius); }
.nav-cta:hover { background: var(--color-primary); }
.nav-toggle { display: none; flex-direction: column; gap: 5px; background: none; border: none; cursor: pointer; padding: .25rem; }
.nav-toggle span { display: block; width: 22px; height: 2px; background: var(--color-primary); border-radius: 2px; }

/* ===== HERO ===== */
.hero { padding: 6rem 0 5rem; text-align: center; }
.hero h1 { font-size: 2.5rem; font-weight: 700; color: var(--color-primary); margin-bottom: .75rem; }
.hero-title { font-size: 1.15rem; font-weight: 600; color: var(--color-accent); margin-bottom: .75rem; }
.hero-tagline { font-size: .95rem; color: var(--color-muted); font-style: italic; max-width: 560px; margin: 0 auto 2rem; }
.hero-links { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; align-items: center; }
.icon-link {
  display: inline-block; padding: .4rem 1rem;
  border: 1.5px solid var(--color-border); border-radius: var(--radius);
  font-size: .875rem; font-weight: 500; color: var(--color-text);
  transition: border-color .2s, color .2s;
}
.icon-link:hover { border-color: var(--color-accent); color: var(--color-accent); text-decoration: none; }
.btn-hero {
  display: inline-block; padding: .45rem 1.25rem;
  background: var(--color-accent); color: #fff;
  border-radius: var(--radius); font-weight: 600; font-size: .875rem;
  transition: background .2s;
}
.btn-hero:hover { background: var(--color-primary); text-decoration: none; }

/* ===== ABOUT ===== */
.about-grid { display: grid; grid-template-columns: auto 1fr; gap: 3rem; align-items: start; }
.about-photo img { width: 180px; height: 180px; border-radius: 50%; object-fit: cover; border: 3px solid var(--color-border); }
.about-text p { margin-bottom: 1rem; }
.about-text p:last-child { margin-bottom: 0; }

/* ===== SKILLS ===== */
.skills-groups { display: flex; flex-direction: column; gap: 2rem; }
.skill-group h3 { font-size: 1rem; margin-bottom: .75rem; }
.skill-tags { display: flex; flex-wrap: wrap; gap: .5rem; }
.skill-tags span {
  display: inline-block; padding: .3rem .8rem;
  background: var(--color-surface); border: 1px solid var(--color-border);
  border-radius: 20px; font-size: .82rem; font-weight: 500; color: var(--color-text);
}

/* ===== PROJECTS ===== */
.projects-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.5rem; }
.project-card {
  background: var(--color-bg); border: 1px solid var(--color-border);
  border-radius: var(--radius); padding: 1.75rem; box-shadow: var(--shadow);
  transition: box-shadow .2s, transform .2s;
}
.project-card:hover { box-shadow: var(--shadow-md); transform: translateY(-2px); }
.tech-tags { display: flex; flex-wrap: wrap; gap: .4rem; margin-bottom: 1rem; }
.tech-tags span { padding: .18rem .55rem; background: #e0f2fe; color: #0369a1; border-radius: 4px; font-size: .72rem; font-weight: 600; }
.project-card p { font-size: .88rem; color: var(--color-muted); line-height: 1.6; }

/* ===== TIMELINE ===== */
.timeline { position: relative; padding-left: 1.5rem; }
.timeline::before {
  content: ''; position: absolute; left: 7px; top: 8px; bottom: 8px;
  width: 2px; background: var(--color-border);
}
.timeline-item { position: relative; margin-bottom: 2.5rem; }
.timeline-item:last-child { margin-bottom: 0; }
.timeline-marker {
  position: absolute; left: -1.5rem; top: 6px;
  width: 16px; height: 16px; border-radius: 50%;
  background: var(--color-accent); border: 3px solid var(--color-bg);
  box-shadow: 0 0 0 2px var(--color-accent);
}
.timeline-content {
  background: var(--color-surface); border: 1px solid var(--color-border);
  border-radius: var(--radius); padding: 1.5rem;
}
.timeline-header { display: flex; justify-content: space-between; align-items: flex-start; gap: 1rem; margin-bottom: 1rem; }
.timeline-org  { font-size: .85rem; color: var(--color-muted); margin-top: .2rem; }
.timeline-date { font-size: .82rem; font-weight: 500; color: var(--color-accent); white-space: nowrap; flex-shrink: 0; }
.timeline-content ul { padding-left: 1.25rem; list-style: disc; }
.timeline-content li { font-size: .88rem; color: var(--color-muted); margin-bottom: .5rem; line-height: 1.6; }
.timeline-content li:last-child { margin-bottom: 0; }

/* ===== CERTIFICATIONS ===== */
.certs-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 1rem; margin-bottom: 1rem; }
.cert-badge {
  display: flex; flex-direction: column; align-items: center; text-align: center;
  gap: .6rem; padding: 1rem .75rem;
  border: 1px solid var(--color-border); border-radius: var(--radius);
  background: var(--color-bg); color: var(--color-text);
  font-size: .78rem; font-weight: 500;
  transition: box-shadow .2s, border-color .2s;
}
.cert-badge:hover { box-shadow: var(--shadow-md); border-color: var(--color-accent); text-decoration: none; color: var(--color-primary); }
.cert-logo {
  width: 40px; height: 40px; border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: .72rem; color: #fff;
}
.cert-logo-aws      { background: #232f3e; }
.cert-logo-coursera { background: #0056d3; }
.cert-logo-datacamp { background: #03ef62; color: #000; }
.certs-note { font-size: .78rem; color: var(--color-muted); margin-top: .5rem; }

/* ===== DOWNLOAD ===== */
.download-section { background: var(--color-primary); }
.download-section h2 { color: #fff; }
.download-section p  { color: rgba(255,255,255,.72); margin-bottom: 1.5rem; }
.btn-download {
  display: inline-block; padding: .875rem 2.5rem;
  background: var(--color-accent); color: #fff;
  border-radius: var(--radius); font-weight: 600; font-size: 1rem;
  transition: background .2s, transform .1s;
}
.btn-download:hover { background: #1a5fa8; text-decoration: none; transform: translateY(-1px); }

/* ===== FOOTER ===== */
footer {
  background: var(--color-surface); border-top: 1px solid var(--color-border);
  padding: 1.5rem 0; text-align: center;
  font-size: .875rem; color: var(--color-muted);
}

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
  .hero h1 { font-size: 1.75rem; }
  h2 { font-size: 1.4rem; }
  .section { padding: 3rem 0; }

  .nav-links {
    display: none; flex-direction: column; gap: .5rem;
    position: absolute; top: var(--nav-h); left: 0; right: 0;
    background: var(--color-bg); border-bottom: 1px solid var(--color-border);
    padding: 1rem 1.5rem;
  }
  .nav-links.open { display: flex; }
  .nav-toggle { display: flex; }

  .about-grid { grid-template-columns: 1fr; text-align: center; }
  .about-photo { display: flex; justify-content: center; }
  .projects-grid { grid-template-columns: 1fr; }
  .timeline-header { flex-direction: column; gap: .2rem; }
  .certs-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .projects-grid { grid-template-columns: 1fr; }
  .certs-grid { grid-template-columns: repeat(3, 1fr); }
}
```

- [ ] **Step 2: Open in browser and verify styling**

Open `industry/index.html`. Verify:
- Hero shows "AI/ML Engineer & Researcher" with a solid blue "Download Resume" button alongside the icon links
- Skills section shows pill-shaped tags in 5 labelled groups
- Projects cards have blue tech stack tags and lift on hover
- Experience has a vertical timeline with blue circle markers
- Certifications 5-column badge grid
- Navy download section at the bottom

- [ ] **Step 3: Commit**

```powershell
git add industry/styles.css
git commit -m "feat: industry site CSS"
```

---

## Task 7: Industry site — JavaScript

**Files:**
- Modify: `industry/script.js`

- [ ] **Step 1: Write the script**

Write `industry/script.js` — identical logic to `academic/script.js`:

```js
(function () {
  const navbar   = document.getElementById('navbar');
  const toggle   = document.querySelector('.nav-toggle');
  const navLinks = document.querySelector('.nav-links');

  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 10);
  }, { passive: true });

  toggle.addEventListener('click', () => {
    const open = navLinks.classList.toggle('open');
    toggle.setAttribute('aria-expanded', String(open));
  });

  navLinks.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      navLinks.classList.remove('open');
      toggle.setAttribute('aria-expanded', 'false');
    });
  });
})();
```

- [ ] **Step 2: Verify in browser**

Open `industry/index.html`. At mobile width (390px):
- Hamburger appears, nav links hidden
- Click hamburger — vertical dropdown appears
- Click "Skills" link — dropdown closes, page scrolls to Skills section

- [ ] **Step 3: Commit**

```powershell
git add industry/script.js
git commit -m "feat: industry site JS"
```

---

## Task 8: Profile photo placeholder

**Files:**
- Create: `academic/assets/photo-placeholder.svg`
- Create: `industry/assets/photo-placeholder.svg`
- Modify: `academic/index.html`
- Modify: `industry/index.html`

The `assets/photo.jpg` files don't exist yet. Without a placeholder the About section shows a broken image icon and the circular frame collapses. Create an SVG placeholder so the layout renders correctly during development.

- [ ] **Step 1: Create the SVG placeholder (academic)**

Create `academic/assets/photo-placeholder.svg`:

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="180" height="180" viewBox="0 0 180 180">
  <rect width="180" height="180" rx="90" fill="#e5e7eb"/>
  <circle cx="90" cy="72" r="28" fill="#9ca3af"/>
  <ellipse cx="90" cy="130" rx="42" ry="28" fill="#9ca3af"/>
</svg>
```

- [ ] **Step 2: Copy placeholder to industry assets**

```powershell
Copy-Item academic/assets/photo-placeholder.svg industry/assets/photo-placeholder.svg
```

- [ ] **Step 3: Update both HTML files to reference the placeholder**

In `academic/index.html`, change:
```html
<img src="assets/photo.jpg" alt="Mostafa Habibi" width="180" height="180">
```
to:
```html
<img src="assets/photo.jpg" alt="Mostafa Habibi" width="180" height="180" onerror="this.src='assets/photo-placeholder.svg';this.onerror=null;">
```

Apply the identical change to the `<img>` tag in `industry/index.html`.

> The `onerror` attribute silently falls back to the placeholder when `photo.jpg` is missing. When the user drops in `photo.jpg`, the placeholder disappears automatically — no HTML change needed.

- [ ] **Step 4: Verify both sites show the placeholder**

Open `academic/index.html` and `industry/index.html`. The About section should show a grey circular silhouette instead of a broken image.

- [ ] **Step 5: Commit**

```powershell
git add academic/assets/photo-placeholder.svg industry/assets/photo-placeholder.svg academic/index.html industry/index.html
git commit -m "feat: profile photo placeholder with onerror fallback"
```

---

## Task 9: Cross-browser and responsive verification

**Files:** No code changes — verification only. Make fixes as needed and commit at the end.

- [ ] **Step 1: Desktop check — both sites (1280px+)**

Open each site in Chrome. For each:
- [ ] Sticky nav — all links visible, no text wrapping
- [ ] Hero readable, tagline fits in one block
- [ ] About Me: photo left, text right
- [ ] Research/Projects: 2-column grid
- [ ] Publications: numbered, badges visible
- [ ] Certifications: 5-column grid, badges aligned
- [ ] Timeline (industry): vertical line and blue dots visible
- [ ] Download section: dark navy background, blue button

- [ ] **Step 2: Tablet check (resize to 900px)**

- [ ] Nav links still visible (hamburger not yet shown)
- [ ] Projects grid collapses to 1 column (industry)
- [ ] Certs grid is 3 columns

- [ ] **Step 3: Mobile check (resize to 375px)**

- [ ] Hamburger icon visible, nav links hidden until tapped
- [ ] About Me: photo centered above bio text
- [ ] Cards/projects: single column
- [ ] Certifications: 2 columns
- [ ] Hero text at 1.75rem or smaller — no overflow

- [ ] **Step 4: Commit any fixes**

```powershell
git add .
git commit -m "fix: responsive layout adjustments"
```

---

## Task 10: Add assets (user-action required)

**Files:**
- Create: `academic/assets/photo.jpg`
- Create: `industry/assets/photo.jpg`
- Create: `academic/assets/resume.pdf`
- Create: `industry/assets/resume.pdf`

These files must be provided by the user. This task documents the steps.

- [ ] **Step 1: Add profile photo**

Copy your profile photo into both asset folders and name it `photo.jpg`:
```
academic/assets/photo.jpg
industry/assets/photo.jpg
```
Both can be the same file. Once placed, the `onerror` fallback in the HTML will stop firing and the real photo will appear automatically.

- [ ] **Step 2: Add resume PDFs**

Place your CV PDF at `academic/assets/resume.pdf`.
Place your industry resume at `industry/assets/resume.pdf` (can be the same file or a different version).

To compile from `resume.tex` if you have LaTeX installed:
```powershell
pdflatex resume.tex
```
Or compile it in Overleaf and download the PDF.

- [ ] **Step 3: Verify downloads work**

Open each site and click the download button. The PDF should download (not show a 404).

- [ ] **Step 4: Commit**

```powershell
git add academic/assets/photo.jpg industry/assets/photo.jpg academic/assets/resume.pdf industry/assets/resume.pdf
git commit -m "feat: add profile photo and resume PDFs"
```

---

## Task 11: Add certification URLs (user-action required)

**Files:**
- Modify: `academic/index.html`
- Modify: `industry/index.html`

- [ ] **Step 1: Collect all 10 credential URLs**

Gather the direct verification URL for each of the 10 certifications. The badges appear in this order in both HTML files:
1. AWS Certified AI Practitioner
2. Introduction to Generative AI Learning Path (Coursera)
3. IBM Data Science Professional Certificate (Coursera)
4. Introduction to Data Science (Coursera)
5. Multi-Agent Systems with LangGraph (Coursera)
6. Understanding Prompt Engineering (DataCamp)
7. Introduction to AI Agents (DataCamp)
8. Building Scalable Agentic Systems (DataCamp)
9. Building AI Agents with Google ADK (DataCamp)
10. Introduction to Generative AI (DataCamp)

- [ ] **Step 2: Replace `href="#"` in academic/index.html**

In `academic/index.html`, find the 10 `<a href="#" class="cert-badge"` elements in the Certifications section (in order) and replace each `href="#"` with the corresponding credential URL from Step 1.

- [ ] **Step 3: Repeat for industry/index.html**

Apply the identical URL replacements in `industry/index.html`. The badge order is the same.

- [ ] **Step 4: Verify links open correct pages**

Click each badge in the browser — each should open the correct credential page in a new tab.

- [ ] **Step 5: Commit**

```powershell
git add academic/index.html industry/index.html
git commit -m "feat: add certification credential URLs"
```

---

## Task 12: Netlify deployment

**Files:** No code changes.

Each site deploys as a separate Netlify site from its own subfolder.

- [ ] **Step 1: Deploy the academic site**

1. Go to [netlify.com](https://netlify.com), sign in, click **Add new site → Deploy manually**.
2. Drag and drop the entire `academic/` folder onto the upload area.
3. Wait for Netlify to process (~10 seconds). A URL appears (e.g., `https://random-words.netlify.app`).
4. In **Site configuration → General**, rename the site to something memorable (e.g., `mostafa-academic`).

- [ ] **Step 2: Smoke-test the academic site**

Open the deployed URL and verify:
- [ ] All 6 nav links scroll to correct sections
- [ ] Profile photo or placeholder renders in About section
- [ ] Best Paper Award badge appears on publication #6
- [ ] CV download button downloads `resume.pdf` (if added) or shows graceful failure
- [ ] All external links (LinkedIn, Scholar, Credly) open in new tab
- [ ] Site is readable on mobile (test with Chrome DevTools → iPhone 12 Pro)

- [ ] **Step 3: Deploy the industry site**

Repeat Step 1 using the `industry/` folder. This creates a second, separate Netlify site.

- [ ] **Step 4: Smoke-test the industry site**

Open the second deployed URL and verify:
- [ ] All 6 nav links scroll to correct sections
- [ ] Hero "Download Resume" button downloads the PDF
- [ ] Skills pills and project cards render correctly
- [ ] Timeline vertical line and blue dots visible
- [ ] Certifications 5-column grid loads correctly
- [ ] Site is readable on mobile
