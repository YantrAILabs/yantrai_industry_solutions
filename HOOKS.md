# Session Hooks — Proposal Page Builder

---

## PRE-SESSION HOOK

At the start of every session, before any command:

1. **Read project files**
   ```
   Read: CONTEXT.md
   Read: SKILL.md
   ```

2. **Scan asset folders**
   ```bash
   ls ./assets/Logo/ ./assets/video/ ./assets/IAAS/ ./assets/use-case/ ./assets/Scale/ ./assets/Team/
   ```

3. **Report status** (one line each):
   - Which asset folders are populated vs empty
   - Whether `[domain]_proposal.html` exists
   - Whether `contact.html` exists
   - Recommended next command

4. **Await explicit command** — do not auto-build.

---

## POST-BUILD HOOK

After every `/build`, `/rebuild`, or `/new-domain`:

1. **Verify all `src=` paths** — confirm every referenced file exists in `./assets/`
2. **Verify section count** — confirm all 11 sections are present
3. **Verify layout patterns**:
   - Section 5 `.timeline` has `flex-direction: row` (horizontal)
   - Section 6 `.logo-grid` has `grid-template-columns: repeat(5, 1fr)` (5 columns)
   - Section 9 `.core-team` has `padding: 100px 72px` (padded container)
4. **Flag placeholders** — list any `<!-- ADD: ... -->` placeholder divs
5. **Print summary**:
   ```
   ✅ [domain]_proposal.html — 11 sections built
   ✅ contact.html — form + contact details
   ⚠️  Missing assets: [list or "none"]
   📁 Files saved to: [path]
   ```

---

## POST-SECTION HOOK

After every `/section [N]` command:

1. Confirm which section was modified
2. Confirm no other sections were changed
3. Verify section-specific brand rules (see Style Guard below)
4. Print: `✅ Section [N] updated — no other sections modified`

---

## VERIFICATION HOOK

After any file edit while a preview server is running:

1. Reload the preview
2. Scroll to the modified section
3. Take a screenshot to confirm visual output
4. Check browser console for errors
5. Confirm layout with a DOM inspection (dimensions, computed styles)

---

## STYLE GUARD HOOK

Before saving any file, validate ALL of these — fix automatically if any fail:

| Rule | Check |
|------|-------|
| Fonts | `font-family` references `Syne` and `Inter` — never Arial, Roboto, system-ui alone |
| Reactive word | Hero heading has `.reactive` span with `color:#e63030` and `text-decoration:line-through` |
| Section 5 layout | `.timeline` uses `flex-direction: row` on desktop |
| Section 6 layout | `.logo-grid` uses `grid-template-columns: repeat(5, 1fr)` on desktop |
| Section 8 background | Uses `#0a0a0a` or `black` |
| Section 8 text | White or `rgba(255,255,255,x)` |
| Section 9 padding | `.core-team` has horizontal padding (never full-bleed) |
| CTA links | Hero button and footer both link to `contact.html` |
| Google Fonts | `<link>` for Syne + Inter present in `<head>` |
| No purple | No `purple`, `violet`, `#8b5cf6`, or similar anywhere |
| No gradients | No `linear-gradient` or `radial-gradient` in brand-facing elements |
| Mobile breakpoint | `@media (max-width: 768px)` block present |

---

## ASSET PATH HOOK

Before writing any `src=` attribute:

```bash
ls ./assets/[folder-name]/
```

Use exact filenames from output. Never guess or hardcode.

**Multi-file priority:**
- `Logo/`: `.svg` > `.png` > `.jpg`
- `video/`: `.mp4` > `.webm`
- `IAAS/`: first `.html`, fallback to first `.gif`
- `use-case/`: match by keyword (monitor, efficiency, threat, data) → fallback to alphabetical
- `Team/`: for Section 9 use the team-card design image; for Section 10 use the landscape/full-width photo

---

## ERROR HOOK

| Error | Action |
|-------|--------|
| Missing asset folder | Create folder, add `.gitkeep`, print: `⚠️ Created empty: assets/[name]/ — add your file here` |
| Scale/ content unreadable | Fall back to 3 default steps from SKILL.md, note it in output |
| Video not found | Dark placeholder div: `<div style="background:#111;min-height:60vh;display:flex;align-items:center;justify-content:center;"><p style="color:#555;font-family:Inter,sans-serif;font-size:14px;">ADD VIDEO TO assets/video/</p></div>` |
| Use-case media not found | Same dark placeholder pattern with `<!-- ADD: use-case-[N].gif -->` comment |
| Partner logo URL fails (naturalWidth=0) | Replace `<img>` with branded wordmark `<div>` in Syne font + company brand colour |
| Team image not found | Placeholder div: `<div style="background:#f5f5f5;min-height:400px;display:flex;align-items:center;justify-content:center;"><p style="font-family:Inter,sans-serif;color:#999;">ADD TEAM IMAGE TO assets/Team/</p></div>` |

---

## DOMAIN EXPANSION HOOK

When `/new-domain` is run:

1. Read the existing `[security]_proposal.html` as a structural template
2. Copy all CSS patterns verbatim — do not redesign
3. Replace only domain-variable content (headlines, card labels, stats, use cases, partner logos)
4. Keep all section IDs, class names, and layout patterns identical
5. Verify the new page passes the full Style Guard before saving
