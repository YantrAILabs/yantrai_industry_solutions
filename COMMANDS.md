# Proposal Page Builder — Slash Commands

Read `SKILL.md` and `CONTEXT.md` before executing any command.

---

## /build

**Purpose**: Build the complete proposal page from scratch (first-time setup)

```
/build

Read SKILL.md and CONTEXT.md first.

Then:
1. Run ls on every folder inside ./assets/ and note all exact filenames
2. Read any text files in ./assets/Scale/ for deployment step content
3. Build [domain]_proposal.html — all 11 sections complete, per SKILL.md spec
4. Build contact.html — standalone contact/demo form page
5. Save both files in the project root

Output the file paths when done.
```

---

## /rebuild

**Purpose**: Rebuild the entire page from scratch, overwriting existing files

```
/rebuild

Read SKILL.md and CONTEXT.md first.

Discard existing [domain]_proposal.html and contact.html.
Re-run the full build: all 11 sections + contact page.
Re-scan all asset folders before writing any src= path.

Save both files in the project root.
```

---

## /section [number] [optional: instructions]

**Purpose**: Rebuild or fix a single section without touching the rest of the page

```
/section [NUMBER] [optional instructions]

Read SKILL.md.
Open [domain]_proposal.html.
Locate Section [NUMBER] and replace only that section's HTML and CSS.
Do not modify any other section.
Save the file.

Examples:
  /section 1
  /section 5 rebuild the deployment steps from assets/Scale/
  /section 6 update partner logos to match the new list
  /section 8 make the use case headings larger
  /section 9 update team image
```

---

## /contact

**Purpose**: Rebuild only the contact page

```
/contact

Read SKILL.md and CONTEXT.md.
Rebuild contact.html from scratch.
Include: logo, back link, sales contact details from CONTEXT.md, and demo request form.
Save as contact.html in project root.
```

---

## /assets

**Purpose**: Scan and report all available assets

```
/assets

List all files in:
- ./assets/Logo/
- ./assets/video/
- ./assets/IAAS/
- ./assets/use-case/
- ./assets/Scale/
- ./assets/Team/

Report: filename, file type, and which section it maps to.
Flag any empty folders that will need placeholder divs.
```

---

## /preview

**Purpose**: Summarise what the current page looks like without modifying files

```
/preview

Open [domain]_proposal.html.
Give a section-by-section summary:
- What is in each section
- Which asset files are referenced
- Any placeholders or missing content
- Any brand rule violations

Do not modify the file.
```

---

## /fix [description]

**Purpose**: Fix a specific issue in the page

```
/fix [DESCRIBE THE PROBLEM]

Read SKILL.md.
Open [domain]_proposal.html (and contact.html if relevant).
Identify and fix the described issue.
Save the file.

Examples:
  /fix the reactive word is not showing in red
  /fix section 8 background is white instead of black
  /fix the timeline is showing vertically instead of horizontally
  /fix logo grid is not showing 5 columns
  /fix mobile layout breaks on use case sections
  /fix partner logos are not loading
```

---

## /style [description]

**Purpose**: Apply a style or design change while maintaining brand rules

```
/style [DESCRIBE THE CHANGE]

Read SKILL.md.
Open [domain]_proposal.html.
Apply the style change. Maintain brand rules: Syne + Inter fonts, black/white palette, no purple, no gradients.
Save the file.

Examples:
  /style increase section heading sizes
  /style add scroll-triggered fade-in animations on section headings
  /style make the hero section taller
  /style add a top progress bar indicator
```

---

## /scale-content

**Purpose**: Re-read the Scale folder and update Section 5 with latest deployment steps

```
/scale-content

Read the file(s) inside ./assets/Scale/.
Extract deployment step names and descriptions.
Update Section 5 (Deployment & Scale) in [domain]_proposal.html.
Keep the horizontal timeline layout. Replace only the step content (numbers, headings, paragraphs).
Save the file.
```

---

## /add-usecase [number] "[title]" "[description]"

**Purpose**: Add or update a specific use case in Section 8

```
/add-usecase [NUMBER] "[TITLE]" "[DESCRIPTION]"

Open [domain]_proposal.html.
Locate use case [NUMBER] in Section 8.
Update the heading and paragraph text.
Keep the alternating layout and black background.
Save the file.
```

---

## /partner-logos [optional: list of companies]

**Purpose**: Update Section 6 partner logos (find real logo URLs, replace wordmarks if needed)

```
/partner-logos [optional comma-separated company names]

For each partner company in Section 6 (or as specified):
1. Search for a reliable direct image URL (SVG preferred):
   - Wikimedia Commons: https://upload.wikimedia.org/wikipedia/commons/...
   - Company's official press/media CDN
2. Update each .logo-card with the actual <img src="[url]"> tag
3. Set appropriate alt text and .brand-name category label
4. Verify all images load (naturalWidth > 0)
5. Save the file.

Fallback if no logo found: branded wordmark <div> in Syne font with company brand colour.
```

---

## /core-team [optional: image path or team description]

**Purpose**: Update the Core Team section (Section 9)

```
/core-team [optional image path]

Open [domain]_proposal.html.
Locate the Core Team section.
Update the team image src to use the specified image path, or re-scan ./assets/Team/ for the latest file.
Update heading and subtext if new team description provided.
Keep the padded container layout (max-width: 1200px, padding: 100px 72px).
Save the file.
```

---

## /new-domain [domain-name] "[Company Name]"

**Purpose**: Clone the design system and configure it for a new domain

```
/new-domain [DOMAIN] "[COMPANY NAME]"

1. Read SKILL.md and CONTEXT.md to understand the full page structure
2. Create [domain]_proposal.html with:
   - Same 11-section architecture
   - Same CSS design system (fonts, colors, patterns)
   - Domain-appropriate content in all variable sections:
     * Section 1: New hero headline with domain-specific reactive word
     * Section 3: 8 capability cards relevant to the new domain
     * Section 5: 3 deployment steps relevant to the new domain
     * Section 6: 10 partner/integration logos for the new domain
     * Section 7: 3 stats relevant to the new domain
     * Section 8: 4 use cases relevant to the new domain
     * Section 9: Placeholder team section
     * Section 11: Updated contact details if provided
3. Create or update contact.html with domain-appropriate copy
4. Save [domain]_proposal.html in project root

Example:
  /new-domain healthcare "MediSense AI"
  /new-domain manufacturing "Yantra AI Labs"
  /new-domain retail "RetailMind AI"
```

---

## /init

**Purpose**: First-time setup — confirm all folders exist and print pre-build checklist

```
/init

Read CONTEXT.md.

1. Confirm these folders exist: assets/Logo, assets/video, assets/IAAS, assets/use-case, assets/Scale, assets/Team
2. List all files found in each folder
3. Print a readiness checklist (✅ ready / ⚠️ empty / ❌ missing)
4. Confirm which proposal HTML file(s) currently exist
5. Recommend the next command to run
```
