# Yantra AI Labs — Proposal Page System

A reusable static HTML proposal page builder.
Built for Vision AI Physical Security. Expandable to any AI product domain.

---

## What's in this folder

```
project-root/
│
├── README.md                 ← You are here
├── CLAUDE.md                 ← Claude Code instructions (commands, brand rules, section map)
├── CONTEXT.md                ← Project context, domain config, asset rules
├── SKILL.md                  ← Full build spec: all 11 sections + CSS patterns
├── COMMANDS.md               ← All slash command prompts (copy-paste ready)
├── HOOKS.md                  ← Session start/end/guard behaviour
│
├── security_proposal.html    ← BUILT OUTPUT — Physical Security domain
├── contact.html              ← BUILT OUTPUT — Demo request form
│
└── assets/
    ├── Logo/                 ← Company logo (SVG preferred)
    ├── video/                ← Hero video (MP4)
    ├── IAAS/                 ← Intelligence layer visual (HTML or GIF)
    ├── use-case/             ← 4 use case visuals (GIF or PNG)
    ├── Scale/                ← Deployment steps content (TXT/MD)
    └── Team/                 ← Team card design image + team photo
```

---

## Page Structure — 11 Sections

| # | Section | Key Design Pattern |
|---|---------|-------------------|
| 1 | Hero | Large heading, `.reactive` red strikethrough word, pill CTA |
| 2 | Video | Full-width autoplay, no controls |
| 3 | Platform Overview | 8 capability cards, 4×2 grid, hover border |
| 4 | Intelligence Layer | Full-screen IAAS visual |
| 5 | Deployment & Scale | **Horizontal 3-step row** with vertical dividers |
| 6 | Partner Logos | **5×2 seamless grid**, real logos, grayscale→colour on hover |
| 7 | Core Benefits | 3 stat blocks in a horizontal row |
| 8 | Use Cases | 4 black full-width sections, alternating layout |
| 9 | Core Team | Padded container, team card image |
| 10 | Team Photo | Full-width edge-to-edge photo |
| 11 | Footer | Logo + nav links + contact details |

---

## Setup

1. Drop your assets into the correct folders (see Asset Requirements below)
2. Open Claude Code in this folder
3. Run `/init` — Claude checks readiness and lists all assets
4. Run `/build` — Claude generates both HTML files

---

## All Commands

| Command | What it does |
|---------|-------------|
| `/init` | Check folders, list assets, print readiness |
| `/build` | Build full page for the first time |
| `/rebuild` | Rebuild entire page from scratch |
| `/section [N]` | Rebuild only section N |
| `/contact` | Rebuild contact.html only |
| `/assets` | List all assets and their section mapping |
| `/preview` | Summarise what's currently built |
| `/fix [problem]` | Fix a specific issue |
| `/style [change]` | Apply a styling change |
| `/scale-content` | Re-read Scale/ folder and update Section 5 |
| `/add-usecase [N] "[title]" "[desc]"` | Update a use case in Section 8 |
| `/partner-logos [companies]` | Find and apply real logo images for Section 6 |
| `/core-team [image]` | Update Section 9 team image and copy |
| `/new-domain [name] "[Company]"` | Clone the design system for a new domain |

Full prompts for every command are in `COMMANDS.md`.

---

## Building for a New Domain

Run:
```
/new-domain healthcare "MediSense AI"
/new-domain manufacturing "Yantra AI Labs"
/new-domain retail "RetailMind AI"
```

Claude will:
1. Reuse the entire design system (fonts, colors, layout patterns, CSS)
2. Replace only domain-specific content (headline, capabilities, logos, stats, use cases)
3. Output `[domain]_proposal.html` + updated `contact.html`

The Domain Variable Config schema is in `CONTEXT.md`.

---

## Asset Requirements

| Folder | What to put here | Format |
|--------|-----------------|--------|
| `Logo/` | Company logo | SVG preferred, PNG ok |
| `video/` | Hero/demo video | MP4 preferred |
| `IAAS/` | Intelligence layer animation or interactive visual | HTML or GIF |
| `use-case/` | 4 use case visuals, named by keyword | GIF or PNG |
| `Scale/` | Deployment phases text | TXT or MD |
| `Team/` | Team card design image (Section 9) + full team photo (Section 10) | PNG or JPG |

---

## Brand Rules (Quick Reference)

- **Fonts**: Syne (headings) + Inter (body) — always from Google Fonts
- **Palette**: White bg + Black text (main) · Black bg + White text (Use Cases section)
- **Accent**: Red `#e63030` — only on the `.reactive` word in the hero heading
- **No gradients. No purple. No rounded hero cards.**
- Both CTA button and footer link to `contact.html`

---

## Current Domain: Physical Security

**Company**: Yantra AI Labs
**Contact**: Rohit · +91 91231 02267 · rohit@yantrailabs.com
**Partners**: Hikvision, Allegion, Software House, Avigilon, Honeywell, Brivo, Samsung, Hanwha Vision, Genetec, Bosch
