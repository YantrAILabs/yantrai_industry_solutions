# Proposal Page System — Project Context

## What This System Is

A reusable static HTML proposal page builder for **Yantra AI Labs** and future AI-product domains.
Output is always two files: `[domain]_proposal.html` + `contact.html`.
No build tools, frameworks, or backend — pure HTML + CSS + JS.

The design system was built and refined during the **Security domain** (Vision AI physical security platform).
All future domains reuse the same visual language, layout patterns, and component library.

---

## Current Domain: Physical Security

**Company**: Yantra AI Labs (also: Yantrai Labs)
**Builder**: Rohit, Co-founder
**Audience**: CISOs, Security Heads, Facility Managers at manufacturing plants, corporate campuses, institutions
**Output file**: `security_proposal.html`

### Contact Details (used in form and footer)
- **Name**: Rohit
- **Company**: Yantra AI Labs
- **Mobile**: +91 91231 02267
- **Email**: rohit@yantrailabs.com
- **CTA destination**: `contact.html`

---

## Tech Stack

- Pure HTML + CSS + JS (no frameworks, no build tools)
- Two output files: `[domain]_proposal.html` + `contact.html`
- Assets served from relative `./assets/` folder
- Hosted as static page (GitHub Pages / direct browser open)

---

## Asset Folder Structure

```
project-root/
├── [domain]_proposal.html      ← main page (e.g. security_proposal.html)
├── contact.html                ← contact/demo form page
├── assets/
│   ├── Logo/                   ← Company logo files (SVG preferred)
│   ├── video/                  ← Hero video file (MP4 preferred)
│   ├── IAAS/                   ← Intelligence layer visual (HTML or GIF)
│   ├── use-case/               ← 4 use case visuals (GIF or PNG)
│   ├── Scale/                  ← Deployment phases text content (TXT/MD/RTF)
│   └── Team/                   ← Team photo or team card design image (PNG)
├── CLAUDE.md
├── CONTEXT.md
├── SKILL.md
├── COMMANDS.md
├── HOOKS.md
└── README.md
```

**Asset priority rules (always apply):**
- `Logo/`: prefer `.svg` > `.png` > `.jpg`
- `video/`: prefer `.mp4` > `.webm`
- `IAAS/`: use first `.html` or `.gif`
- `use-case/`: match by filename keyword; fallback to alphabetical
- `Team/`: use first image file

---

## Brand Rules (non-negotiable across all domains)

1. **Fonts**: `Syne` (headings, weight 700/800) + `Inter` (body, 400/500) — loaded via Google Fonts
2. **Palette**: White `#ffffff` bg + Black `#0a0a0a` text (main); Black bg + White text (Use Cases section)
3. **Accent**: Red `#e63030` — used **only** on the `.reactive` strikethrough word in the hero heading
4. **No gradients. No purple. No rounded hero cards.**
5. Logo appears in header (dark version) and footer (light/white version if available)
6. Hero CTA button and footer both link to `contact.html`

---

## Page Architecture — 11 Sections

| # | Section | Background | Key Pattern |
|---|---------|-----------|-------------|
| 1 | Hero | White | Large heading + `.reactive` strikethrough + camera-frame CTA |
| 2 | Video | White | Full-width autoplay, no controls |
| 3 | Platform Overview | White | 8-card grid (4×2 desktop), hover border black |
| 4 | Intelligence Layer | Black | Full-screen visual from `assets/IAAS/` |
| 5 | Deployment & Scale | Light gray `#f5f5f5` | **Horizontal 3-step row**, vertical dividers between steps |
| 6 | Partner Logos | Light gray `#f5f5f5` | **5×2 logo grid**, seamless borders, grayscale→color on hover |
| 7 | Core Benefits | White | 3 stat blocks in a row (95%, 10×, 24/7) |
| 8 | Use Cases | Black `#0a0a0a` | 4 full-width sections, alternating image/text layout |
| 9 | Core Team | White | Section heading + team card image from `assets/Team/`, padded container |
| 10 | Full-width Team Photo | — | Edge-to-edge image from `assets/Team/` (secondary visual) |
| 11 | Footer | Black `#0a0a0a` | Logo + links + contact details |

---

## Domain Expansion — Variable Config

When building for a new domain, only these variables change.
Everything else (layout, fonts, colors, CSS patterns) is reused as-is.

```yaml
domain:
  name: "physical-security"           # used in filename: [name]_proposal.html
  company: "Yantra AI Labs"
  tagline_verb: "reactive"            # the strikethrough word in hero heading
  hero_headline: "Make your security preventive, not [reactive]"
  hero_subtext: "Vision AI turns traditional surveillance into an intelligent security layer..."
  section3_heading: "One Platform. All Security Solutions."
  section3_cards: [8 capability cards with icon + label]
  section5_steps: [3 deployment steps]
  section6_partners: [10 partner companies with logo URLs]
  section7_stats: [{value, label}, {value, label}, {value, label}]
  section8_usecases: [4 use cases with title, body, media keyword]
  contact:
    name: "Rohit"
    mobile: "+91 91231 02267"
    email: "rohit@yantrailabs.com"
```

**Known future domains:**
- `healthcare` — AI diagnostics / hospital operations
- `manufacturing` — AI quality control / factory safety
- `retail` — AI customer analytics / inventory intelligence
- `logistics` — AI fleet / warehouse monitoring

---

## Session Continuity Rules

- Always run `ls ./assets/[folder]/` before writing any `src=` attribute
- Never hardcode filenames — use actual output from `ls`
- If a folder is empty: use a dark placeholder `<div>` with `<!-- ADD: filename -->` comment
- Read `Scale/` content file (whatever type is present) before building Section 5
- The `SKILL.md` file contains all CSS patterns and section specs — read it before any build
