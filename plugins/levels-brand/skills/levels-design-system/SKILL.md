---
name: levels-design-system
description: This skill should be used when building HTML slide decks, print/PDF reports, one-pagers, or long-form doc-sites in the Levels visual style — e.g. "build a Levels deck", "make a Levels PDF report", "make this look like Levels", "design a Levels × PLC report", "export this as a branded PDF", "style this in the Levels aesthetic", "Levels-branded HTML page", or any executive/clinical artifact for Levels or Precision Longevity that should carry the Levels look (warm off-white, editorial serif, electric-lime accent). Provides the color tokens, typography, component library, runnable HTML templates for deck/report/web, and a print-to-PDF workflow.
version: 0.1.0
---

# Levels Design System

Reverse-engineered from levels.com production CSS (June 2026) and adapted for dense, executive B2B artifacts. The look is **editorial-clinical, warm, and calm** — a high-contrast serif for display, a geometric-humanist sans for everything else, a monospace for micro-labels, warm off-white backgrounds (never pure white), and one electric-lime accent used with discipline. It reads as a health company that treats data as the hero, not a techy-neon startup.

Use this skill to produce three formats that share one token set:

- **Slide deck** — full-bleed HTML slides, keyboard-navigable, presented on screen. Start from `assets/deck-template.html`.
- **Print report (PDF)** — a paginated US-Letter document with a full-bleed cover, per-section page breaks, and a running footer. This is the format to hand off as a PDF. Start from `assets/report-template.html` (styled by `assets/levels-report.css`).
- **Web doc / spec-site** — sticky top bar, sidebar TOC, editorial prose, data widgets, read in a browser. Start from `assets/doc-template.html`.

All are single self-contained HTML files with Google-hosted fonts and zero build step. Deck and doc-site inline their CSS; the report links `levels-report.css` (keep the two files together).

Choosing between them: **deck** for a walked-through pitch, **report** for a document a reader keeps and prints, **doc-site** for reference material a reader scans and jumps around. The deck and report cover the same material at different densities — a deck is one claim per slide; a report is continuous prose with the same components.

Do not apply this system to non-Levels brands. It carries specific brand provenance; for a generic health aesthetic, adapt the tokens rather than presenting them as Levels.

## Workflow

1. **Pick the format.** Deck for a walked-through narrative; doc-site for reference material the reader scans and jumps around. When unsure, ask.
2. **Copy the matching template** from `assets/` and rename it. Never author the CSS from scratch — the templates carry the full token set, type scale, component CSS, and (for the deck) the navigation controller.
3. **Fill in content** using the component patterns in `references/components.md`. Keep the token variables and type primitives; replace only the content.
4. **Apply the discipline rules** below — they are what separate an on-brand result from a generic one.
5. **Verify** by opening the file in a browser. For the deck, arrow keys navigate and `F` toggles fullscreen. For the report, check that sections break cleanly (see PDF below).

## Producing a PDF

Both the report and the deck export to PDF; the report is the format designed for it.

- **Report → PDF (the primary path).** Open `report-template.html` and print: Destination "Save as PDF", Paper **Letter**, Margins **Default**, and **Background graphics ON** (without it the dark cover and sage fills drop out). The stylesheet's `@page` rules produce Letter portrait, a zero-margin full-bleed cover page, one page per `<section>` (except `.no-break-before`), `break-inside:avoid` so cards and tables stay intact, and repeating table headers.
- **Deck → PDF.** The deck's `@media print` block renders one slide per page. Print with **Background graphics ON** and orientation **Landscape** to match slide proportions.
- **Headless / scripted.** `chrome --headless --print-to-pdf=out.pdf --no-pdf-header-footer report-template.html` (Chrome, Edge, or Chromium). Headless print-to-PDF renders background graphics by default, so no extra flag is needed. Use this for repeatable exports or CI.
- **Discipline.** Keep `print-color-adjust:exact` in the CSS (already set) — it is what preserves the brand colors on paper. Page numbers come from the browser's print dialog or the `--print-to-pdf` header/footer, not from the document.

## The tokens (memorize the anchors)

The full palette lives in `references/style-guide.md`; the CSS `:root` block in every template is the source of truth. The anchors that define the look:

| Token | Value | Role |
|---|---|---|
| `--green` | `#1d7d6c` | **The Levels green.** Anchor — key numbers, buttons, eyebrows, row labels. |
| `--ink` | `#131413` | Near-black. Body text, headlines on light. |
| `--bg` | `#fcfcf8` | Warm off-white page. **Never pure `#fff`.** |
| `--bg-sage` / `--bg-mint` | `#e6eeeb` / `#edf5f2` | Alt section + card fills. |
| `--bg-dark` | `#131413` | Full-bleed dark slides (chapter breaks / big-idea slides only). |
| `--lime` | `#cdff00` | **The signature accent.** One idea per slide, max. Signal, not decoration. |
| `--amber` | `#be8d35` | Rare "elevated" / caution marker (e.g. open-items count). The ⛔ "off the table" callout uses the red `.banned` styles, not amber. |
| `--hair` | `#c9d0ce` | Hairline rules and table dividers. Separate with lines, not nested boxes. |

Fonts (Google-hosted, ~90% match to the licensed Levels faces):

- **Fraunces** (display serif) → slide titles, headlines, big metric numbers. This is what makes it read as Levels. Real face: GT Sectra Fine.
- **Hanken Grotesk** (sans) → all UI, body, subheads. Real face: TT Hoves; Inter is the shared fallback.
- **Geist Mono** (mono) → uppercase eyebrow labels, units, data values, footnotes, source flags. Wide tracking (~0.1–0.18em).

## Type roles

- **Titles** → serif, large, tight leading (`line-height:~1.04`, `letter-spacing:-.014em`), near-black. One idea per title.
- **Body / bullets** → sans, weight 400–500, generous line-height, never below ~18px equivalent.
- **Eyebrow labels** (section name, "LEVER 1", slide kicker) → mono, uppercase, wide tracking, green (or lime on dark), small.
- **Big numbers / metrics** (`~15–35%`, `~4% wt loss`) → serif or heavy sans, oversized, green, unit in mono beside it. This is the Levels data-hero move — lead with the number.

## Discipline rules (do not skip)

These are the difference between on-brand and generic:

- **Lime is signal, not decoration.** One lime element per slide, ideally — it marks the single thing the eye should land on. Overusing lime kills the effect.
- **Warm off-white, never pure white.** Backgrounds are `--bg` (`#fcfcf8`) or a sage/mint tint. Pure `#fff` reads wrong.
- **Dark = chapter break.** Reserve dark slides for the cover, section dividers, and one or two big-idea slides. Do not alternate light/dark randomly.
- **Separate with hairlines, not boxes.** Prefer `--hair` rules and generous whitespace over boxes-within-boxes. Cards are flat: rounded 16–20px, subtle sage fill or hairline border, no heavy drop shadows.
- **Mono micro-labels everywhere small.** Units, footnotes, source flags ("large-employer benchmark"), the ⛔ "off the table" callouts — all mono, uppercase, wide-tracked.
- **Data is the hero.** Lean into clean tabular slides — mono column headers, generous row padding, hairline dividers, green for the row label or key cell — rather than hiding the rigor.
- **One claim per slide.** The deck is dense, so use a strict grid and let each slide carry one claim with supporting structure, not a wall of text.

## Signature motifs

- **In-range band** — Levels' core visual is a value sitting inside or outside a target zone. Reuse it for "savings range" bars, substitution ladders, and any before/after.
- **Engagement / substitution ladder** — indented rungs that ascend, dashed "future" rungs, mono unlock labels on the right. See `.ladder` in `references/components.md`.
- **Metric hero** — oversized serif number in green with a mono unit label beside it.
- **Editorial-clinical tone** — warm, calm, confident. The lime is the only loud thing.

## Resources

### Reference files

- **`references/style-guide.md`** — full palette table with provenance, the levels.com source tokens, font-licensing notes, and the complete design rationale. Read when choosing colors or explaining/adapting the system.
- **`references/components.md`** — copy-paste HTML for every component: eyebrow, card, metric, exhibit, split, rows, chips, banned-bar, matrix table, ladder, plus the doc-site widgets (topbar, sidebar TOC, stepper, tier comparator, care-stack, timeline). Consult while assembling slides or sections.

### Assets (templates — copy, don't read into context unless editing the CSS)

- **`assets/deck-template.html`** — runnable slide deck: full token set, component CSS, keyboard/click navigation, progress bar, print-to-PDF support, and sample slides (dark cover, card grid, sage split, metric hero, appendix table).
- **`assets/report-template.html`** + **`assets/levels-report.css`** — runnable paginated print/PDF report: full-bleed cover, executive summary with hero stats, prose sections, callouts, off-table markers, tables, glossary, and the `@page` print rules. The two files travel together.
- **`assets/doc-template.html`** — runnable long-form doc-site: sticky top bar, collapsible sidebar TOC with scrollspy, editorial prose styles, data tables, callouts, and chips.
