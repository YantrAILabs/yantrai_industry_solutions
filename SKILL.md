---
name: proposal-page-builder
description: Builds AI product proposal webpages for any domain. Use this skill for ANY command related to building, editing, or regenerating a proposal page or contact page. Triggers on /build, /rebuild, /section, /preview, /contact, /new-domain, /partner-logos, /core-team commands.
---

# Proposal Page Builder — Full Skill Spec

## Overview

You are building a single-file HTML proposal page for an AI product company.
The page is a B2B sales/proposal page targeting enterprise decision-makers.
Read `CONTEXT.md` for the current domain's variable config before executing any command.

**Deliverables:**
- `[domain]_proposal.html` — main proposal page (e.g. `security_proposal.html`)
- `contact.html` — contact form + sales details page

Both files go in the project root alongside the `assets/` folder.

---

## Design System (Shared Across All Domains)

### Fonts
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@400;500&display=swap" rel="stylesheet">
```

### CSS Variables
```css
:root {
  --bg: #ffffff;
  --bg-alt: #f5f5f5;
  --dark: #0a0a0a;
  --gray: #555;
  --gray-dim: #999;
  --border: #e5e5e5;
  --red: #e63030;
}
```

### Shared Section Label / Heading / Subtext
```css
.section-label {
  font-family: 'Inter', sans-serif;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--gray-dim);
  margin-bottom: 20px;
}
.section-heading {
  font-family: 'Syne', sans-serif;
  font-size: clamp(2.4rem, 4.5vw, 4.5rem);
  font-weight: 800;
  line-height: 1.08;
  letter-spacing: -0.02em;
  color: var(--dark);
  margin-bottom: 18px;
}
.section-subtext {
  font-family: 'Inter', sans-serif;
  font-size: 1.05rem;
  line-height: 1.75;
  color: var(--gray);
}
```

---

## Section Specs

### SECTION 1 — Hero

- **BG**: White | **Text**: Black | **Layout**: Centered, `padding: 140px 60px 120px`
- **Heading**: Domain-specific headline with `.reactive` strikethrough word
  ```css
  .reactive { color: #e63030; text-decoration: line-through; text-decoration-thickness: 4px; }
  ```
- **CTA Button** — Camera-frame style (corner brackets via pseudo-elements):
  ```css
  .pill-btn {
    display: inline-block;
    padding: 16px 40px;
    border: 1.5px solid var(--dark);
    font-family: 'Inter', sans-serif;
    font-size: 14px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    background: var(--dark);
    color: white;
    text-decoration: none;
    border-radius: 50px;
    transition: opacity 0.2s;
  }
  .pill-btn:hover { opacity: 0.85; }
  ```
- CTA links to `contact.html`

---

### SECTION 2 — Hero Video

- Full-width video, no controls, autoplay, muted, loop
- `<video autoplay muted loop playsinline style="width:100%;display:block;max-height:90vh;object-fit:cover;">`
- Source: first `.mp4` or `.webm` in `./assets/video/`
- No heading, no caption

---

### SECTION 3 — Platform Overview (Capabilities)

- **BG**: White | Centered heading + subtext + 8-card grid (4×2 desktop, 2×4 mobile)
- Card CSS:
  ```css
  .platform-card {
    border: 1px solid var(--border);
    padding: 28px 24px;
    transition: border-color 0.2s, box-shadow 0.2s;
  }
  .platform-card:hover {
    border-color: var(--dark);
    box-shadow: 0 4px 20px rgba(0,0,0,0.06);
  }
  ```
- Domain-specific: icon (Unicode emoji) + label per card

---

### SECTION 4 — Intelligence Layer (Full-screen Visual)

- Full-screen section, zero padding, `line-height: 0`
- Source: first `.html` or `.gif` in `./assets/IAAS/`
- If `.html`: `<iframe src="..." style="width:100%;min-height:100vh;border:none;display:block;">`
- If `.gif` or image: `<img src="..." style="width:100%;display:block;min-height:60vh;object-fit:cover;">`

---

### SECTION 5 — Deployment & Scale (HORIZONTAL TIMELINE)

- **BG**: `var(--bg-alt)` (`#f5f5f5`) | Left-aligned heading
- Steps rendered as a **single horizontal row** (NOT vertical):
  ```css
  .timeline {
    display: flex;
    flex-direction: row;
    align-items: stretch;
    margin-top: 64px;
  }
  .timeline-item {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 48px 40px;
    border-right: 1px solid var(--border);
  }
  .timeline-item:first-child { padding-left: 0; }
  .timeline-item:last-child { border-right: none; }
  .timeline-num {
    font-family: 'Syne', sans-serif;
    font-size: 88px;
    font-weight: 800;
    color: rgba(0,0,0,0.06);
    line-height: 1;
    margin-bottom: 24px;
  }
  .timeline-content h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 14px;
  }
  .timeline-content p {
    font-family: 'Inter', sans-serif;
    font-size: 0.95rem;
    line-height: 1.8;
    color: var(--gray);
  }
  /* Mobile: revert to column */
  @media (max-width: 768px) {
    .timeline { flex-direction: column; }
    .timeline-item { padding: 40px 0; border-right: none; border-bottom: 1px solid var(--border); }
    .timeline-item:last-child { border-bottom: none; }
  }
  ```
- Read step content from `./assets/Scale/` — use whatever file type is present
- Default 3 steps (if no file): Connect Infrastructure → Unified Intelligence Layer → Deploy & Scale Fast

---

### SECTION 6 — Partner Logos (5×2 LOGO GRID)

- **BG**: `#f5f5f5` | Centered label + subtext
- **10 logos** arranged in a **5 column × 2 row seamless grid** (not badges):
  ```css
  .logo-grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 0;
    margin-top: 56px;
    border: 1px solid #e0e0e0;
  }
  .logo-card {
    background: #fff;
    border-right: 1px solid #e0e0e0;
    border-bottom: 1px solid #e0e0e0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 40px 28px;
    gap: 16px;
    transition: background 0.25s, box-shadow 0.25s;
    min-height: 140px;
  }
  .logo-card:nth-child(5n) { border-right: none; }
  .logo-card:nth-child(n+6) { border-bottom: none; }
  .logo-card:hover { background: #fafafa; box-shadow: inset 0 0 0 1.5px #111; }
  .logo-card img {
    max-width: 120px;
    max-height: 42px;
    object-fit: contain;
    filter: grayscale(100%);
    opacity: 0.5;
    transition: filter 0.3s, opacity 0.3s;
  }
  .logo-card:hover img { filter: grayscale(0%); opacity: 1; }
  .logo-card .brand-name {
    font-family: 'Inter', sans-serif;
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #ccc;
    transition: color 0.25s;
  }
  .logo-card:hover .brand-name { color: #888; }
  /* Mobile */
  @media (max-width: 768px) {
    .logo-grid { grid-template-columns: repeat(2, 1fr); }
    .logo-card:nth-child(5n) { border-right: 1px solid #e0e0e0; }
    .logo-card:nth-child(2n) { border-right: none; }
  }
  ```
- **Logo source strategy** (in priority order):
  1. Wikimedia Commons SVG: `https://upload.wikimedia.org/wikipedia/commons/[path]/[Company]_logo.svg`
  2. Company's own CDN (found via their press/media page)
  3. Branded wordmark `<div>` using Syne font + company brand colour (fallback only)
- Each card: `<img src="[url]" alt="[Company]">` + `<span class="brand-name">[Category]</span>`
- **Security domain logos**: Hikvision, Allegion, Software House, Avigilon, Honeywell, Brivo, Samsung, Hanwha Vision, Genetec, Bosch

---

### SECTION 7 — Core Benefits

- **BG**: White | Centered
- Large statement heading + 3 stat blocks in a horizontal row
  ```css
  .stats-row { display: flex; border: 1px solid var(--border); margin-top: 64px; }
  .stat-block { flex: 1; padding: 56px 40px; border-right: 1px solid var(--border); text-align: center; }
  .stat-block:last-child { border-right: none; }
  .stat-num { font-family: 'Syne', sans-serif; font-size: clamp(3.5rem,6vw,5.5rem); font-weight: 800; }
  .stat-label { font-family: 'Inter', sans-serif; font-size: 0.9rem; color: var(--gray); margin-top: 8px; }
  ```
- Domain-specific: 3 stats (value + label)

---

### SECTION 8 — Use Cases (4 full-width black sections)

- **BG**: `#0a0a0a` | **Text**: White
- 4 sections, alternating layout (image left/text right, text left/image right):
  ```css
  .use-case-section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    min-height: 70vh;
    background: #0a0a0a;
    border-bottom: 1px solid rgba(255,255,255,0.06);
  }
  .use-case-section.reverse { direction: rtl; }
  .use-case-section.reverse > * { direction: ltr; }
  .use-case-media { overflow: hidden; }
  .use-case-media img, .use-case-media video { width:100%; height:100%; object-fit:cover; }
  .use-case-text { padding: 80px 60px; display:flex; flex-direction:column; justify-content:center; }
  .use-case-text h2 { font-family:'Syne',sans-serif; font-size:clamp(2rem,3.5vw,3.2rem); font-weight:800; color:white; margin-bottom:24px; }
  .use-case-text p { font-family:'Inter',sans-serif; font-size:1.05rem; line-height:1.8; color:rgba(255,255,255,0.7); max-width:480px; }
  .uc-num { font-size:11px; letter-spacing:0.2em; text-transform:uppercase; color:rgba(255,255,255,0.3); margin-bottom:20px; }
  ```
- Media: match filename in `./assets/use-case/` by keyword; use dark placeholder div if missing

---

### SECTION 9 — Core Team

- **BG**: White | Left-aligned heading with right-padded container
- Shows team member cards via a single composite image from `assets/Team/`
  ```css
  .core-team-wrap { background: var(--bg); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
  .core-team { max-width: 1200px; margin: 0 auto; padding: 100px 72px; }
  .core-team .section-label, .core-team .section-heading, .core-team .section-subtext { text-align: left; }
  .core-team .section-subtext { margin: 0 0 60px; max-width: 560px; }
  .team-img-wrap img { width: 100%; height: auto; display: block; border-radius: 4px; }
  ```
- Source: `./assets/Team/[team-card-design-image]` — the team card design PNG/JPG
- Subheading: domain-appropriate description of the founding team

---

### SECTION 10 — Full-width Team Photo (Secondary)

- No heading, edge-to-edge image
- Source: first image found in `./assets/Team/` (if multiple, use the full-width/landscape one)
  ```css
  .team-section { line-height: 0; }
  .team-section img { width: 100%; display: block; }
  ```

---

### SECTION 11 — Footer

- **BG**: `#0a0a0a` | **Text**: White
- 3-column layout: logo left | nav links centre | contact right
- Logo: white/light version from `./assets/Logo/`
- Nav links: `contact.html`, `#platform`, `#benefits`
- Contact: name, mobile, email from domain config
- Bottom bar: `© [year] [Company]. All rights reserved.`

---

## contact.html Spec

Standalone page, same visual language as main page.

- **Nav**: Logo + "← Back to [Domain] Solutions" link
- **Left column** (40%): Sales contact block — name, mobile, email, 2-hour response promise
- **Right column** (60%): Form — Full Name*, Company*, Email*, Phone, Message, "Request a Demo" button
- **On submit**: JS success message: `"Thank you! [Name] will reach out within 2 hours."`
- No backend. Pure HTML/JS.

---

## Quality Checklist

Before saving any file, verify ALL of these:
- [ ] `Syne` + `Inter` loaded via Google Fonts `<link>` in `<head>`
- [ ] `.reactive` span has `color: #e63030` + `text-decoration: line-through`
- [ ] Section 5 (timeline) is **horizontal row** on desktop, column on mobile
- [ ] Section 6 (logo grid) is **5 columns** desktop, 2 columns mobile, seamless borders
- [ ] Section 8 background is `#0a0a0a`, text is white / `rgba(255,255,255,x)`
- [ ] Section 9 (Core Team) uses image from `./assets/Team/` with side padding
- [ ] Hero CTA button → `contact.html`
- [ ] Footer "Contact Team" → `contact.html`
- [ ] No purple anywhere. No gradients.
- [ ] All `src=` paths verified against actual `ls` output
- [ ] Mobile breakpoint `@media (max-width: 768px)` present
