# Levels Design System — Style Guide

Full aesthetic reference. Reverse-engineered from levels.com production CSS (June 2026), then adapted for dense, executive B2B artifacts (decks, reports, program specs). Read this when choosing colors, explaining the system, or adapting it to a new artifact.

## Source of truth — what Levels actually uses

Pulled from their live stylesheets:

| Token | Value | Role |
|---|---|---|
| Primary green | `#1d7d6c` | The Levels green. Brand anchor — logo, primary buttons, key numbers. |
| Deep green | `#176456` / `#127868` | Darker pressed/hover states, dark section backgrounds. |
| Near-black | `#131413` | Body text, headlines on light. |
| Graphite | `#2d3130`, `#585a59`, `#6a6f6d` | Secondary text, captions, hairlines. |
| Sage tints | `#9fc5bc`, `#b9d7d0`, `#c9d0ce` | Muted accents, borders, chart fills. |
| Mint washes | `#e6eeeb`, `#edf5f2`, `#f3f5f4` | Section backgrounds, card fills. |
| Off-white | `#fcfcf8` / `#f7f7f5` | Page background — warm, never pure `#fff`. |
| Electric lime | `#cdff00` / `#bde92d` | The signature accent. Data highlights, "in-range" glucose. Used *sparingly*. |
| Amber | `#be8d35` | Rare secondary accent (warnings / "elevated"). |

Typography:
- **GT Sectra Fine** — high-contrast editorial serif. Display headlines only. This is what makes Levels look like Levels and not a generic health startup.
- **TT Hoves** — geometric-humanist sans. All UI, body, subheads. Falls back to Inter.
- **Mono** (their `--font-mono`) — uppercase eyebrow labels, data values, metric units. Wide tracking (~1.7px).
- Weights in play: 400 body, 500/600 emphasis, 700–900 display.

Both branded fonts (GT Sectra Fine, TT Hoves) are commercial licenses — not free to redistribute in an HTML file. See the font decision below.

## Deck / doc token set

The adapted CSS custom properties used in every template. This is the working palette — richer than the raw Levels tokens because it adds the intermediate tints an artifact needs. The `:root` block inside `assets/deck-template.html` and `assets/doc-template.html` is canonical; if this listing ever drifts from the templates, the templates win.

```css
:root{
  --bg:#fcfcf8;        /* warm off-white page */
  --bg-sage:#e6eeeb;   /* alt section / card fill */
  --bg-mint:#edf5f2;   /* lighter card fill, code/inline backgrounds */
  --bg-dark:#131413;   /* full-bleed dark slides */
  --green:#1d7d6c;     /* primary — anchor, key numbers, buttons */
  --green-deep:#176456;/* on dark, hover, pressed */
  --ink:#131413;       /* primary text */
  --ink-2:#585a59;     /* secondary text */
  --ink-3:#8a908d;     /* tertiary text, captions, disabled */
  --hair:#c9d0ce;      /* rules, borders, table lines */
  --hair-soft:#e1e5e2; /* softer dividers, card borders */
  --lime:#cdff00;      /* accent — one idea per slide, max */
  --amber:#be8d35;     /* rare "elevated" / caution marker (e.g. open-items count) */
  --serif:"Fraunces",Georgia,serif;
  --sans:"Hanken Grotesk","Inter",system-ui,sans-serif;
  --mono:"Geist Mono",ui-monospace,"IBM Plex Mono",monospace;
}
```

## Two surface modes

- **Light** (default) — warm off-white bg, green accents. The workhorse.
- **Sage** — `--bg-sage` fill for an alternate section, to break rhythm without going dark.
- **Dark** — near-black bg, sage/lime text. Reserve for the cover, section dividers, and one or two big-idea slides. On dark, eyebrows and the accent shift to `--lime`; secondary text goes to `#c9d0ce`. Do not alternate light/dark randomly — dark means "chapter break."

## Type roles

- **Slide titles / page H2** → serif display, large, tight leading (`line-height:~1.04`, `letter-spacing:-.014em`), near-black. One idea per title.
- **Body / bullets** → sans, weight 400–500, generous line-height (~1.45–1.6). Never below ~18px equivalent in a deck; 17px base in a doc.
- **Eyebrow labels** (section name, slide number, "LEVER 1") → mono, uppercase, wide tracking (0.1–0.18em), green or graphite, small. Often prefixed with a short rule (`::before` 1.6em bar in `currentColor`).
- **Big numbers / metrics** (the "~15–35%", "~4% wt loss") → serif or heavy sans, oversized, green, `line-height` under 1, negative letter-spacing. Unit in mono beside it. This is the Levels data-hero move.
- **Kicker / caption** → mono, small, `--ink-3`.

## Layout

- **Generous margins.** Levels never crowds. Decks use `padding:clamp(2.2rem,5.2vw,5.5rem)` on each slide.
- **Strict grid.** The artifact is dense, so use a 12-col mentality and let each slide carry *one* claim with supporting structure, not a wall.
- **Cards.** Rounded 16–20px, subtle sage fill or hairline border, no heavy drop shadows — flat with soft elevation at most. Accent cards get a green border + `box-shadow:0 0 0 1px var(--green)`.
- **Hairline rules** (`--hair`, `--hair-soft`) separate content — not boxes within boxes.
- **Tables** (levers grid, options A–D, regulations): mono column headers, generous row padding, hairline dividers, green for the row label or key cell. Data is the hero — lean into clean tabular slides rather than hiding the rigor. First column often bold sans in `--ink` while the rest is `--ink-2`.
- **Doc measure:** cap prose at ~720px; let tables/widgets run wider (~840px).

## Signature motifs

- **In-range band** — Levels' core visual is a value sitting inside or outside a target zone. Reuse for "savings range" bars and the substitution ladder.
- **Lime as signal, not decoration** — it marks the one thing the eye should land on. One lime element per slide, ideally.
- **Mono micro-labels everywhere small text appears** — units, footnotes, source flags ("large-employer benchmark"), the ⛔ "off the table" callouts.
- **Engagement / substitution ladder** — indented rungs ascending, dashed "future" rungs at reduced opacity, mono unlock labels on the right, dashed gate rows between tiers.
- **Warm, calm, confident.** Editorial-clinical, not techy-neon. The lime is the only loud thing.

## Fonts — decided

Both real Levels faces are commercial licenses and cannot ship in a redistributable HTML file. Free Google-hosted near-matches (zero licensing risk, ~90% Levels):

- **Display serif → Fraunces** (variable, high-contrast, optical sizing — closest free GT Sectra Fine).
- **Sans → Hanken Grotesk** (geometric-humanist, closest free TT Hoves; Inter is the same fallback Levels uses).
- **Mono → Geist Mono** (eyebrow labels, units, data values).

Google Fonts import used in the templates:

```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=Hanken+Grotesk:wght@400;500;600;700&family=Geist+Mono:wght@400;500&display=swap" rel="stylesheet">
```

Swap to the real licensed faces (TT Hoves, GT Sectra Fine) if an artifact goes external and licensing is cleared — the token names stay the same, only the `@font-face` sources change.
