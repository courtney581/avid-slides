# avidLearning brand reference

A self-contained spec for matching avidLearning's printed/PDF look in single-page A4 documents (invoices, briefs, one-pagers). Drop the CSS into a `<style>` block, copy `logo.png` next to the HTML, and you're done — no build step, no framework, no external CSS file required.

This file is the source of truth for *consumers outside the `avid-slides` repo*. If you're working **inside** `avid-slides`, prefer reading [`../proposals/lbs-sql-programme/index.html`](../proposals/lbs-sql-programme/index.html) directly — that's the canonical proposal and the master from which this reference is extracted.

---

## 1. Assets you need

Two things must exist alongside the HTML file (or somewhere it can reach by relative path):

| Asset | Source | Notes |
|---|---|---|
| `logo.png` | Copy from `avid-slides/shared/assets/logo.png` | Rendered at **44px** in the page header and **22px** in the footer. PNG with transparent background. |
| DM Sans + DM Mono | Google Fonts (loaded via `<link>`) | No local font files needed — the `<link>` tag in section 4 below loads them. |

No JS. No build tooling. The page is a single `.html` file.

---

## 2. Palette

| Token | Hex | Used for |
|---|---|---|
| Teal | `#2899A4` | Primary accent — kickers, `h1 .accent`, link colour, bullet dots, table `part-lbl`, top stripe (start), footer link |
| Pink | `#E05FA0` | Secondary accent — `.accent-bar`, `.divider`, top stripe (end), badges |
| Navy | `#0d1b2a` | Headings, strong text, table header background |
| Off-white | `#fafafa` | Page background (the A4 sheet itself) |
| Page-gutter grey | `#d9d9d9` | Body background outside the sheet (screen only — turns white in print) |
| Text strong | `#111827` | Default body colour, used inside `<strong>` |
| Text body | `#374151` | Paragraph copy, table cells |
| Text muted | `#6b7280` | Footer copy, `.meta`, table labels |
| Border | `#e5e7eb` | Cards, tables, footer rule |
| Zebra light | `#f3f4f6` | `row-lbl` / `part-lbl` table cell backgrounds |
| Zebra dark | `#1a2a3d` | `th.row-lbl` (a slightly lighter navy than the header) |

The teal→pink gradient (top stripe and bottom stripe) is the single most recognisable brand element. Always include both stripes on a page — top is 6px, bottom is 4px.

---

## 3. Fonts

Paste this into `<head>`:

```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
```

- **DM Sans** — body text. Weights 400 / 500 / 600 / 700. Default `font-family`.
- **DM Mono** — small-caps labels (kickers, `.section-kicker`, table `part-lbl`, footer meta). Weights 400 / 500. Always uppercase, with letter-spacing.

Body font declaration:

```css
font-family: 'DM Sans', -apple-system, sans-serif;
```

Mono usage (kickers, labels) is always paired with `text-transform: uppercase` and `letter-spacing: .08em` to `.15em`.

---

## 4. Base stylesheet

Paste this verbatim into a `<style>` block (or save as `branding.css` and `<link>` it). This is all the shared primitives — page wrapper, stripes, header, footer, divider, kicker, paragraph, bullet list, generic table.

```css
@page { size: A4; margin: 0; }

* { box-sizing: border-box; margin: 0; padding: 0; }
html, body {
  background: #d9d9d9;
  font-family: 'DM Sans', -apple-system, sans-serif;
  color: #111827;
  -webkit-print-color-adjust: exact;
  print-color-adjust: exact;
}
body { display: flex; justify-content: center; padding: 20px 0; }

.page {
  width: 210mm;
  height: 297mm;
  background: #fafafa;
  position: relative;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-shadow: 0 8px 40px rgba(0,0,0,.18);
}
@media print {
  html, body { background: #fff; padding: 0; }
  body { display: block; }
  .page { box-shadow: none; margin: 0; }
}

.stripe {
  height: 6px;
  background: linear-gradient(90deg, #2899A4 0%, #E05FA0 100%);
  flex-shrink: 0;
}

.content {
  flex: 1;
  min-height: 0;
  padding: 9mm 14mm 4mm;
  display: flex;
  flex-direction: column;
  gap: 4mm;
}

/* ---------- Header ---------- */
.hdr { display: flex; justify-content: space-between; align-items: flex-start; }
.hdr .kicker {
  font-family: 'DM Mono', monospace;
  font-size: 8pt;
  color: #2899A4;
  letter-spacing: .15em;
  text-transform: uppercase;
  margin-bottom: 4mm;
}
.hdr h1 {
  font-size: 26pt;
  font-weight: 700;
  color: #0d1b2a;
  line-height: 1;
  letter-spacing: -.02em;
  margin-bottom: 2mm;
}
.hdr h1 .accent { color: #2899A4; }
.hdr .subtitle {
  font-size: 12pt;
  color: #374151;
  font-weight: 500;
  margin-bottom: 2mm;
}
.hdr .meta {
  font-size: 9pt;
  color: #6b7280;
}
.hdr .strapline {
  font-size: 9pt;
  color: #2899A4;
  font-style: italic;
  margin-top: 1.5mm;
}
.hdr .accent-bar {
  width: 50px; height: 3px;
  background: #E05FA0;
  margin-top: 3mm;
}
.hdr .logo { height: 44px; flex-shrink: 0; }

/* ---------- Divider (pink rule) ---------- */
.divider {
  width: 50px;
  height: 3px;
  background: #E05FA0;
  margin: 1mm 0;
}

/* ---------- Section kicker (small-caps label above a block) ---------- */
.section-kicker {
  font-family: 'DM Mono', monospace;
  font-size: 8pt;
  color: #2899A4;
  text-transform: uppercase;
  letter-spacing: .12em;
  font-weight: 500;
  margin-bottom: 2mm;
}

/* ---------- Body copy ---------- */
p { font-size: 9.5pt; line-height: 1.45; color: #374151; }
p + p { margin-top: 2mm; }
p strong { color: #0d1b2a; font-weight: 600; }
p .hl { color: #2899A4; font-weight: 600; }

/* ---------- Bulleted list (teal dot) ---------- */
ul.bullets { list-style: none; }
ul.bullets li {
  display: flex;
  align-items: flex-start;
  gap: 3mm;
  margin-bottom: 1.8mm;
  font-size: 9.5pt;
  color: #374151;
  line-height: 1.4;
}
ul.bullets li::before {
  content: '';
  width: 5px; height: 5px;
  border-radius: 50%;
  background: #2899A4;
  flex-shrink: 0;
  margin-top: 6px;
}
ul.bullets li strong { color: #0d1b2a; font-weight: 600; }

/* ---------- Data / reference table ---------- */
table.dt {
  width: 100%;
  border-collapse: collapse;
  font-size: 8.5pt;
  background: #fff;
  border-radius: 8px;
  overflow: hidden;
  border: 1px solid #e5e7eb;
}
table.dt th {
  background: #0d1b2a;
  color: #fff;
  padding: 3mm 3mm;
  text-align: left;
  font-weight: 500;
  font-size: 8.5pt;
}
table.dt th.row-lbl { background: #1a2a3d; }
table.dt td {
  padding: 1.8mm 3mm;
  border-top: 1px solid #e5e7eb;
  color: #374151;
  vertical-align: top;
  line-height: 1.35;
}
table.dt td.row-lbl {
  font-weight: 600;
  color: #0d1b2a;
  background: #f3f4f6;
  width: 30%;
}
table.dt td.part-lbl {
  font-family: 'DM Mono', monospace;
  font-size: 7.5pt;
  color: #2899A4;
  text-transform: uppercase;
  letter-spacing: .06em;
  background: #f3f4f6;
  font-weight: 500;
  width: 30%;
}

/* ---------- Footer ---------- */
.footer {
  border-top: 1px solid #e5e7eb;
  padding: 4mm 14mm 3mm;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 8pt;
  color: #6b7280;
  flex-shrink: 0;
}
.footer a { color: #2899A4; text-decoration: none; }
.footer .logo { height: 22px; }
.footer-stripe {
  height: 4px;
  background: linear-gradient(90deg, #2899A4 0%, #E05FA0 100%);
  flex-shrink: 0;
}
```

---

## 5. Page skeleton

Every single-page A4 document follows this shape — top stripe, content, footer, bottom stripe, all inside one `.page` block:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Invoice 0001 — avidLearning</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  /* paste the full stylesheet from section 4 here */
</style>
</head>
<body>

<div class="page">

  <div class="stripe"></div>

  <div class="content">

    <!-- ===== Header ===== -->
    <div class="hdr">
      <div>
        <div class="kicker">avidLearning &middot; Invoice</div>
        <h1>Invoice <span class="accent">0001</span></h1>
        <div class="subtitle">One-line description of the engagement</div>
        <div class="meta">Issued: 16 May 2026 &middot; Due: 30 May 2026</div>
        <div class="accent-bar"></div>
      </div>
      <img src="logo.png" alt="avidLearning" class="logo">
    </div>

    <!-- invoice body goes here -->

  </div>

  <div class="footer">
    <div><a href="mailto:courtney@avidlearning.tech">courtney@avidlearning.tech</a></div>
    <div><a href="https://avidlearning.tech/">avidlearning.tech</a></div>
  </div>

  <div class="footer-stripe"></div>

</div>

</body>
</html>
```

Key invariants:

- `<deck-stage>` is **not** used here (that's the slide-deck format). Single A4 documents just use `.page`.
- The `.stripe` and `.footer-stripe` sit **outside** `.content` — they span the full width of the sheet.
- `.content` has `flex: 1` so it expands to push the footer to the bottom of the page.
- `padding: 9mm 14mm 4mm` inside `.content` sets the standard side gutters. The footer has its own `4mm 14mm 3mm` so it lines up.

---

## 6. Pattern reference

Each pattern is a small HTML snippet that drops into `.content`. Mix and match.

### Header

The page-opening block. Kicker (small caps label) → big title with optional `.accent` colour swap → subtitle → meta line → pink accent bar. Logo floats to the right.

```html
<div class="hdr">
  <div>
    <div class="kicker">avidLearning &middot; Invoice</div>
    <h1>Invoice <span class="accent">0001</span></h1>
    <div class="subtitle">SQL for Business Leaders — Cohort 1</div>
    <div class="meta">Issued: 16 May 2026 &middot; Due: 30 May 2026</div>
    <div class="accent-bar"></div>
  </div>
  <img src="logo.png" alt="avidLearning" class="logo">
</div>
```

### Section kicker

A small-caps mono label above any block of content. Use to introduce a section without a heavy heading.

```html
<div class="section-kicker">Bill to</div>
<p>London Business School<br>Regent's Park, London NW1 4SA</p>
```

### Divider

50px pink rule. Use between major sections instead of a heavy `<hr>`.

```html
<div class="divider"></div>
```

### Body paragraph

Default `<p>` is already styled. Use `<strong>` for emphasis (darkens to navy `#111827`), and `<span class="hl">` for teal highlight.

```html
<p>Thank you for your business. Payment is due <strong>within 14 days</strong> of issue, via <span class="hl">bank transfer</span> to the account below.</p>
```

### Bulleted list

Teal-dot bullets. Use `<strong>` inside `<li>` for emphasis.

```html
<ul class="bullets">
  <li><span><strong>Bank:</strong> Wise — sort 23-08-01 / acc 12345678</span></li>
  <li><span><strong>Reference:</strong> please use invoice number 0001</span></li>
  <li><span><strong>VAT:</strong> not VAT registered — no VAT charged</span></li>
</ul>
```

(The `<span>` wrapper is required — `ul.bullets li` is `display: flex` and the `::before` dot is the first flex child, so the text needs to be in its own element to wrap correctly.)

### Table

Generic reference table with navy header. Two label-cell variants:

- `td.row-lbl` — navy bold label in a light-grey cell (use for key/value pairs)
- `td.part-lbl` — small-caps teal mono label (use for grouped/numbered rows)

```html
<table class="dt">
  <thead>
    <tr>
      <th>Description</th>
      <th>Qty</th>
      <th>Rate</th>
      <th>Amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>SQL for Business Leaders — Part 1 delivery</td>
      <td>1</td>
      <td>&pound;5,000</td>
      <td>&pound;5,000</td>
    </tr>
    <tr>
      <td>SQL for Business Leaders — Part 2 delivery</td>
      <td>1</td>
      <td>&pound;5,000</td>
      <td>&pound;5,000</td>
    </tr>
  </tbody>
</table>
```

Or the key/value form:

```html
<table class="dt">
  <tbody>
    <tr><td class="row-lbl">Invoice number</td><td>0001</td></tr>
    <tr><td class="row-lbl">Issue date</td><td>16 May 2026</td></tr>
    <tr><td class="row-lbl">Due date</td><td>30 May 2026</td></tr>
  </tbody>
</table>
```

### Footer

Two-column: email on the left, website on the right. Lives outside `.content`, before `.footer-stripe`.

```html
<div class="footer">
  <div><a href="mailto:courtney@avidlearning.tech">courtney@avidlearning.tech</a></div>
  <div><a href="https://avidlearning.tech/">avidlearning.tech</a></div>
</div>
<div class="footer-stripe"></div>
```

---

## 7. Exporting to PDF

The whole point of this format is to print to PDF identically across machines. Always export via Chrome:

1. Open the `.html` file in **Chrome** (other browsers handle `@page` and `print-color-adjust` inconsistently).
2. `Cmd+P` (or `Ctrl+P`).
3. **Destination:** Save as PDF
4. **Paper size:** A4
5. **Margins:** None
6. **Background graphics:** ON ← critical, otherwise the stripes and colours disappear
7. Save.

The `@media print` block in the stylesheet handles the difference between screen view (grey gutter, drop shadow on the sheet) and print view (white background, no shadow).

---

## 8. Versioning

Canonical source: [`proposals/lbs-sql-programme/index.html`](https://github.com/) inside the `avid-slides` repo (Courtney's private repo). If this `BRANDING.md` falls out of sync with the proposals, re-extract from there — the proposal `<style>` block is always the authoritative version.

If you need a pattern that isn't in section 6 (stat cards, timelines, testimonial quote blocks, investment cards, callouts), check the canonical proposal CSS — those patterns exist there but were deliberately omitted from this reference because they're proposal-specific. Either pull the CSS for the specific block you need, or ask before inventing new styles.
