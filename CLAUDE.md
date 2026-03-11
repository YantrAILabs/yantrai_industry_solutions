# CLAUDE.md

This file provides guidance to Claude Code when working with code in this repository.

## What This Project Is

A reusable static HTML proposal page system for **Yantra AI Labs**.
Currently built for the **Vision AI Physical Security** domain.
Designed to be cloned and reconfigured for any AI product domain.

Output is always two files:
- `[domain]_proposal.html` — 11-section proposal page
- `contact.html` — demo request form

No build tools, frameworks, or backend — pure HTML + CSS + JS.

---

## Slash Commands

Read `SKILL.md` and `CONTEXT.md` before executing any command.

| Command | Action |
|---------|--------|
| `/build` | Generate both HTML files from scratch |
| `/rebuild` | Overwrite and regenerate both files |
| `/section [N]` | Replace only section N in the proposal HTML |
| `/contact` | Regenerate `contact.html` only |
| `/assets` | Scan all asset folders and report status |
| `/preview` | Summarise current build without modifying files |
| `/fix [problem]` | Fix a specific issue |
| `/style [change]` | Apply a style change while maintaining brand rules |
| `/scale-content` | Re-read `assets/Scale/` and update Section 5 |
| `/add-usecase [N] "[title]" "[desc]"` | Update a specific use case in Section 8 |
| `/partner-logos [companies]` | Update Section 6 with real logo images from the web |
| `/core-team [image path]` | Update Section 9 team section |
| `/new-domain [name] "[Company]"` | Clone design system for a new domain |
| `/init` | Check folders, list assets, print readiness checklist |

---

## Pre-Session Checklist

At the start of every session, before executing any command:
1. Read `CONTEXT.md` and `SKILL.md`
2. Run `ls` on each asset subfolder to discover actual filenames — never hardcode filenames
3. Report which asset folders are populated and whether the output HTML files exist
4. Await an explicit command — do not auto-build

---

## Asset Path Rules

Always run `ls ./assets/[folder]/` before writing any `src=` attribute.
If a folder is empty, use a dark placeholder `<div>` with a comment like `<!-- ADD: use-case-1.gif -->`.

Asset priority when multiple files exist:
- **Logo/**: prefer `.svg` > `.png` > `.jpg`
- **video/**: prefer `.mp4` > `.webm`
- **IAAS/**: use first `.html` or `.gif`
- **use-case/**: match by filename keyword (monitor, efficiency, threat, data); fallback to alphabetical
- **Team/**: Section 9 → team card design image; Section 10 → landscape/full-width photo
- **Scale/**: read whichever file type is present (`.txt`, `.md`, `.rtf`, `.docx`)

---

## Brand Rules (Non-Negotiable)

Before saving any file, verify ALL of these:
- **Fonts**: `Syne` (headings, 700/800 weight) + `Inter` (body, 400/500 weight) via Google Fonts `<link>` in `<head>`
- **Colors**: White background + black text (main); black background + white text (Section 8)
- **Red `#e63030`** used **only** for the `.reactive` span in the hero heading (with `text-decoration: line-through`)
- **No gradients, no purple, no rounded hero cards**
- Section 8 must have `background: #0a0a0a` (or `black`) and white/rgba text
- Hero CTA button and footer must both link to `contact.html`
- Logo appears in header (dark version) and footer (light/white version if available)

If any brand rule fails during an edit → fix automatically before saving.

---

## Page Sections (11 sections, in order)

| # | Section | Layout Pattern |
|---|---------|---------------|
| 1 | Hero | Centred heading + `.reactive` strikethrough + pill CTA → `contact.html` |
| 2 | Video | Full-width autoplay from `assets/video/` |
| 3 | Platform Overview | 8 capability cards in 4×2 grid |
| 4 | Intelligence Layer | Full-screen visual from `assets/IAAS/` |
| 5 | Deployment & Scale | **Horizontal 3-step row** — `flex-direction: row`, vertical dividers |
| 6 | Partner Logos | **5×2 seamless logo grid** — real logos, grayscale→colour hover |
| 7 | Core Benefits | 3 stat blocks in a horizontal row |
| 8 | Use Cases | 4 full-width black sections, alternating image/text |
| 9 | Core Team | Padded container (`max-width: 1200px`, `padding: 100px 72px`) + team image |
| 10 | Full-width Team Photo | Edge-to-edge photo from `assets/Team/` |
| 11 | Footer | Logo + contact: Rohit, +91 91231 02267, rohit@yantrailabs.com |

---

## Key CSS Patterns (Do Not Break)

### Section 5 — Horizontal Timeline
```css
.timeline { display: flex; flex-direction: row; align-items: stretch; }
.timeline-item { flex: 1; display: flex; flex-direction: column; padding: 48px 40px; border-right: 1px solid var(--border); }
.timeline-item:last-child { border-right: none; }
/* Mobile: revert to column */
@media (max-width: 768px) { .timeline { flex-direction: column; } }
```

### Section 6 — 5×2 Logo Grid
```css
.logo-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 0; border: 1px solid #e0e0e0; }
.logo-card { border-right: 1px solid #e0e0e0; border-bottom: 1px solid #e0e0e0; }
.logo-card:nth-child(5n) { border-right: none; }
.logo-card:nth-child(n+6) { border-bottom: none; }
.logo-card img { filter: grayscale(100%); opacity: 0.5; transition: filter 0.3s, opacity 0.3s; }
.logo-card:hover img { filter: grayscale(0%); opacity: 1; }
```

### Section 9 — Core Team (Padded)
```css
.core-team { max-width: 1200px; margin: 0 auto; padding: 100px 72px; }
```

---

## Domain Expansion

To build for a new domain, run `/new-domain [domain] "[Company Name]"`.

The command reuses the entire CSS design system and replaces only the content variables:
hero headline, capability cards, deployment steps, partner logos, stats, use cases, and contact details.

See `CONTEXT.md` for the full Domain Variable Config schema.
See `COMMANDS.md` for the full `/new-domain` command spec.

---

## Post-Build Verification

After any `/build`, `/rebuild`, `/new-domain`, or `/section` command:
1. Verify every `src=` path has a corresponding file in assets
2. Verify Section 5 is horizontal, Section 6 is 5-column, Section 9 is padded
3. List any placeholder divs used (missing assets)
4. Confirm no unintended sections were modified (for `/section` commands)
5. Print a summary of what was built and what's missing
