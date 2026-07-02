# Component Library

Copy-paste HTML for every reusable component in the Levels design system. The CSS for all of these ships inside `assets/deck-template.html` (deck components) and `assets/doc-template.html` (doc components). Match the class names exactly — the templates already carry the styling.

Split by surface: **Deck components** render on full-bleed slides; **Report components** render in the paginated `report-template.html` (styled by `levels-report.css`); **Doc components** render inside a scrolling `.content` column of `doc-template.html`. Many (eyebrow, chip, metric, card, matrix table, glossary) share class names across surfaces.

---

## Deck components

### Eyebrow label

Mono, uppercase, wide-tracked, with a leading rule. Green on light, lime on dark.

```html
<div class="eyebrow">The situation</div>
```

### Slide title + lead

```html
<h2>Self-funded means SpaceX can act<br>where insured employers can't</h2>
<p class="lead">Partnership options grounded in drug effectiveness and benefits-law compliance.</p>
```

### Card grid

`.grid` + `.g2`/`.g3`/`.g4` for column count. Each card: mono kicker (`.num`), serif `h3`, sans body.

```html
<div class="grid g3">
  <div class="card">
    <div class="num">THE PAYER</div>
    <h3>Self-insured, ~15k</h3>
    <p>Pays claims itself; broad plan-design latitude — ERISA preempts state mandates.</p>
  </div>
  <div class="card accent">
    <div class="num">WHY THIS SHAPE</div>
    <h3>Clean by design</h3>
    <p>A fixed fee set in advance sidesteps anti-kickback exposure.</p>
    <span class="chip green">Set in advance</span>
  </div>
</div>
```

`.card.accent` adds a green border + ring for the one card to emphasize.

### Metric hero

Oversized serif number in green with a mono unit beside/below. The data-hero move.

```html
<div class="metric">
  <span class="big">~15–35%</span>
  <span class="unit">GLP-1 spend reduction</span>
</div>
```

### Evidence exhibit

A framed data callout — mono label, serif title, a metric, and a mono caveat.

```html
<div class="exhibit">
  <div class="exhibit-label">Evidence · SELECT trial</div>
  <div class="exhibit-title">Cardiovascular benefit persists off-drug</div>
  <div class="exhibit-body">
    <div class="metric"><span class="big">20%</span><span class="unit">MACE reduction</span></div>
    <p>Sustained over the trial window in the treated arm.</p>
  </div>
  <div class="exhibit-caveat">Large-employer benchmark — SpaceX figure unknown.</div>
</div>
```

### Two-column split

Asymmetric split (`.85fr / 1.15fr`), used to pair a list with an accent card.

```html
<div class="split">
  <div class="rows"> … rows … </div>
  <div class="card accent"> … </div>
</div>
```

### Definition rows

Mono label on the left, body on the right, hairline divider between.

```html
<div class="rows">
  <div class="row"><span class="lab">Levels</span><span class="body"><b>Operating costs + fixed fee</b> per member transitioned — <span class="muted">set in advance.</span></span></div>
  <div class="row" style="border:none"><span class="lab">Twin</span><span class="body"><span class="muted">Savings-share — deliberately not this.</span></span></div>
</div>
```

### Chips

Mono, uppercase, pill-shaped status markers.

```html
<span class="chip green">Set in advance</span>
<span class="chip lime">In range</span>
<span class="chip banned">⛔ Off the table</span>
```

### Banned bar

A full-width caution row — for the "off the table" / ruled-out callout.

```html
<div class="banned-bar">
  <span class="chip banned">⛔ Off the table</span>
  <span><b>Savings-share comp.</b> That model belongs to Twin, not this arrangement.</span>
</div>
```

### Engagement / substitution ladder

Ascending indented rungs (`.r1`–`.r5` add right-margin to climb), circular mono numbers, right-aligned mono unlock labels, dashed `.future` rungs. Insert a `.gate` divider between tiers.

```html
<div class="ladder">
  <div class="rung r1"><span class="rn">1</span><div class="mid"><h3>Baseline</h3><p>Current-state spend.</p></div><span class="unlock">Data ask</span></div>
  <div class="gate"><span class="line"></span><span class="txt">Gate · data confirmed</span></div>
  <div class="rung r2"><span class="rn">2</span><div class="mid"><h3>First substitution</h3><p>Switch to first-line.</p></div><span class="unlock">~10% saved</span></div>
  <div class="rung r3 future"><span class="rn">3</span><div class="mid"><h3>Full program</h3><p>Future state.</p></div><span class="unlock">TBD</span></div>
</div>
```

### Matrix table (appendix / options grid)

Mono column headers with a green underline, hairline row dividers, bold first column.

```html
<table class="matrix">
  <thead><tr><th>Option</th><th>Mechanism</th><th>Comp model</th></tr></thead>
  <tbody>
    <tr><td>A</td><td>Displace Twin</td><td>Per-transition fee</td></tr>
    <tr><td>B</td><td>Run parallel</td><td>FMV clinical</td></tr>
  </tbody>
</table>
```

### Glossary (two-column term list)

```html
<div class="gloss">
  <div><b>Self-insured</b> — employer pays claims itself → broad plan-design latitude.</div>
  <div><b>UM</b> — utilization management: PA, step therapy, medical-necessity criteria.</div>
</div>
```

### Notes and footnotes

```html
<p class="note">This deck surfaces partnership <b>options</b>, not a single fixed deal.</p>
```

---

## Report / print components

These render in `report-template.html`, which links `levels-report.css`. The report shares `metric`, `card`, `row`/`rows`, `rung` ladder, `matrix` tables, `gloss`, `chip`, and `eyebrow` with the deck — plus these paginated-document pieces.

### Full-bleed cover

A dark cover page with a lime rule and a mono meta grid. In print it fills a zero-margin page.

```html
<section class="cover">
  <div class="eyebrow">Levels · Report Kicker · Internal</div>
  <h1>Report Title</h1>
  <div class="rule"></div>
  <p class="lead">One-sentence framing.</p>
  <div class="meta">
    <span><b>Prepared by</b><br>Levels / PLC</span>
    <span><b>Status</b><br>Draft</span>
    <span><b>Date</b><br>Month 2026</span>
  </div>
</section>
```

### Report body + sections

Wrap all post-cover content in `.report`. Each `<section class="section">` starts a new printed page; add `.no-break-before` to the first section so it follows the cover without a blank page.

```html
<div class="report">
  <section class="section no-break-before">
    <div class="eyebrow">Executive summary</div>
    <h2>Headline thesis</h2>
    <div class="prose"><p>Body copy at a comfortable measure.</p></div>
    <div class="docfoot"><span>Report Title · Levels</span><span>Draft · Internal · Month 2026</span></div>
  </section>
</div>
```

### Prose

Continuous body text under `h2`/`h3`/`h4`. Wrap paragraphs and lists in `.prose` for the report's editorial measure and list-marker styling.

### Callout

A sage-fill aside for a thesis, scope note, or key decision.

```html
<div class="callout">
  <div class="label">Thesis</div>
  <p>The single sentence a reader should remember.</p>
</div>
```

### Hero stats

Grouped headline metrics with a mono group label. Add `.ours` to a label to mark owned/first-party data (vs. external benchmark).

```html
<div class="herostats">
  <div class="herogroup">
    <div class="herogroup-label">External benchmark</div>
    <div class="herorow">
      <div class="metric"><span class="big">15–35%</span><span class="unit">Headline range</span></div>
    </div>
  </div>
  <div class="herogroup">
    <div class="herogroup-label ours">Our data · IRB cohort</div>
    <div class="herorow">
      <div class="metric"><span class="big">51%</span><span class="unit">Owned metric · n=1,865</span></div>
    </div>
  </div>
</div>
```

### Off-table / caution markers

`.offtable` (danger red) for a ruled-out option; `.caution` (amber) for a softer warning.

```html
<div class="offtable"><span class="tag">⛔ Off the table</span><span>The excluded option and why.</span></div>
```

### Running footer

`.docfoot` sits at the end of each section as an on-screen footer band (hidden in print, where page numbers come from the print dialog).

---

## Doc / spec-site components

### Sticky top bar

```html
<header class="topbar">
  <span class="tb-title">GLP-1 Program</span>
  <span class="tb-sub">Levels × PLC · Product Structure</span>
  <span class="tb-spacer"></span>
  <span class="tb-stat"><span class="dec">6 decided</span><span class="dot">·</span><span class="opn">2 open</span></span>
  <button class="hamburger" aria-label="Menu"><span></span><span></span><span></span></button>
</header>
```

### Sidebar TOC

Collapsible nav groups with mono index numbers; active link gets a lime left-border. Scrollspy JS ships in the template.

```html
<nav class="sidebar">
  <div class="nav-group">
    <button class="nav-top"><span class="idx">01</span>Member journey<span class="caret">▾</span></button>
    <ul class="nav-subs">
      <li class="nav-sub"><a href="#journey-a">Enrollment</a></li>
      <li class="nav-sub"><a href="#journey-b">Titration</a></li>
    </ul>
  </div>
</nav>
```

### Prose section

```html
<section id="clinical-model">
  <div class="eyebrow">Section 02</div>
  <h2>Clinical model</h2>
  <p class="measure">Body copy capped at ~720px for readability …</p>
  <hr class="sec-rule">
</section>
```

### Deal note / callout

An inline mono callout on a sage fill — for a decision, assumption, or aside.

```html
<div class="deal-note">Deal shape: fixed per-transition fee, set in advance. Not savings-share.</div>
```

### Pills and chips (doc)

```html
<span class="pill">Decided</span>
<span class="chip on">Included</span>
<span class="chip off">Out of scope</span>
```

### Data table (prose)

```html
<div class="table-scroll">
  <table>
    <thead><tr><th>Tier</th><th>Who</th><th>Cadence</th></tr></thead>
    <tbody>
      <tr><td>Core</td><td>All members</td><td>Monthly</td></tr>
    </tbody>
  </table>
</div>
```

### Care-stack bands (tapering layers)

Stacked bands of decreasing width (`.cs-band-1/2/3`) with a mono arrow between — visualizes a stack or a funnel. Lime highlight on the active/output band via `.disposes`.

```html
<div class="cs-diagram">
  <div class="cs-band cs-band-1"><span class="cs-name">Medication</span><span class="cs-owner">PLC clinician</span></div>
  <div class="cs-arrow"><span class="glyph">↓</span> tapers into</div>
  <div class="cs-band cs-band-2"><span class="cs-name">Coaching</span><span class="cs-owner">Levels coach</span></div>
</div>
```

> Interactive click-to-expand widgets (a horizontal journey **stepper**, a **tier comparator** with tabs, a **staged timeline** with fork diamonds) are intentionally omitted from `doc-template.html` to keep it lean. Build them only when the doc genuinely needs interactive drill-down; static tables and prose sections cover most cases. To add one, follow the same pattern as the care-stack bands: a row of `<button>` nodes with a top-border accent (`border-top:2px solid var(--green)` on `.active`), a hidden detail panel toggled by a click handler, and lime (`--lime`) to mark the active/gate node. Mono micro-labels for badges, serif for panel titles, `--bg-mint` for panel fills.
