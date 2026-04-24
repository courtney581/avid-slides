# CLAUDE.md — brief for Claude sessions in avid-slides

This repo stores avidLearning's HTML slide decks. Each deck is a single `index.html` using the `<deck-stage>` web component (see [shared/deck-stage.js](shared/deck-stage.js)). No build step, no framework — open an HTML file in a browser and it works.

**The canonical deck is [decks/sql-for-mbas/index.html](decks/sql-for-mbas/index.html).** When building anything new, match its style. When in doubt, read it.

## Repo layout

```
avid-slides/
├── CLAUDE.md                      # this file
├── README.md                      # human-facing guide
├── index.html                     # landing page listing all decks (GH Pages root)
├── .gitignore / .nojekyll
├── shared/
│   ├── deck-stage.js              # web component — do not modify without reason
│   └── assets/logo.png            # avidLearning logo, used by every deck
└── decks/
    └── <deck-name>/
        ├── index.html             # the deck
        ├── source.md              # bullet outline the deck was built from
        └── assets/                # deck-specific imagery
```

Every deck's HTML references shared files via **`../../shared/...`** relative paths. Do not use absolute paths.

## When asked to build a new deck

The user will write an outline at `decks/<name>/source.md` (format below) and ask you to turn it into an `index.html`. Do this:

1. **Read [decks/sql-for-mbas/index.html](decks/sql-for-mbas/index.html) in full first.** It is the style bible. Also re-read this file.
2. **Read `decks/<name>/source.md`** — the content.
3. Write `decks/<name>/index.html`:
   - Copy the `<head>` + inline `<style>` block from sql-for-mbas **verbatim**. Do not invent new CSS classes. Do not restyle. If a slide needs a pattern that doesn't exist yet, ask the user before adding CSS.
   - Inside `<deck-stage width="1920" height="1080">`, emit one `<section>` per slide in source.md, using the patterns below.
   - Script references: `<script src="../../shared/deck-stage.js"></script>`
   - Logo references: `<img src="../../shared/assets/logo.png" class="logo">`
   - Keep the inline `<script>` block at the bottom (it injects the footer bar and handles the tweaks panel). Copy it verbatim too.
4. **Add a line to the root [index.html](index.html)** linking to the new deck.
5. Tell the user to open the deck with VS Code Live Server to preview.

## Style bible (from sql-for-mbas)

**Palette**:
- Teal `#2899A4` — primary accent, section numbers, highlights
- Pink `#E05FA0` — secondary accent, exercise badges, dividers
- Navy `#0d1b2a` — dark backgrounds (title, section dividers, code panels)
- Off-white `#fafafa` — default slide background
- Code panel `#0f1e2d` — background for `.code-l`
- Text `#111827` / `#374151` / `#6b7280` — headings / body / muted

**Fonts**: `DM Sans` (body), `DM Mono` (code + small-caps labels). Both are loaded from Google Fonts in the `<head>`.

**Canvas**: fixed 1920×1080. Always set `<deck-stage width="1920" height="1080">`.

## Slide patterns (all present in sql-for-mbas)

| Pattern | Class | Use for |
|---|---|---|
| **Title slide** | inline styles, navy bg | Deck opener (name, subtitle, date) |
| **Section divider** | `.sec-div` | "Section 02 · What is SQL?" chapter breaks |
| **Full slide with header** | `.full-slide` | Most content slides — gradient stripe + title bar + logo + body |
| **Split code/annotation** | `.split` with `.code-l` + `.code-r` | SQL snippet on left, explanation/question on right |
| **Card grid** | `.grid2` / `.grid3` with `.card` | Workshop expectations, "why you care", summaries |
| **Data table** | `.dt` | Raw sample data display |
| **Operator/reference table** | `.ot` with `.op` | Comparison operators, aggregate functions |
| **Building blocks list** | `.bb` / `.bb-kw` / `.bb-desc` | "SELECT / FROM / WHERE / ORDER BY" stack |
| **Summary bullets** | `.si` / `.sd` / `.st` | Bulleted lists with teal dots |
| **Exercise badge** | `.ex-badge` | Pink pill that says "EXERCISE" above a split-code slide |
| **Break / wrap-up** | inline styles, navy bg | Coffee-break slide, wrap-up, Q&A |

**Code highlighting in `<pre class="cb">`**: wrap tokens in spans:
- `.kw` (keywords, blue) — SELECT, FROM, WHERE
- `.fn` (functions, green) — COUNT, AVG, MAX
- `.str` (strings, pink) — `'US'`
- `.num` (numbers, orange) — `120000`
- `.hi` (highlighted, yellow bold) — current focus of the slide
- `.cm` (comments, grey italic) — `-- comment`
- `.pl` (placeholder, grey italic) — `[columns]` for exercises

**Every slide needs `data-label="Human-readable label"`** on the `<section>`. Used by the comment flow. Keep it short (<30 chars).

## `source.md` format

```markdown
# Deck: <Title>

**Subtitle**: <e.g. avidLearning · Workshop>
**Date**: <e.g. Friday 24th April 2026>

## Slides

### 1. Title — "<Deck Title>"
- Subtitle line
- Date

### 2. Agenda (6 items + break)
- Intro & expectations
- ...

### 3. Workshop expectations (3 cards)
- Cameras on — creates interactive environment
- ...

### 4. Section divider — "What is X?"

### 5. X definition (two-column: definition + "why it matters")
- Stands for: ...
- Why it matters: ubiquitous in ...

### 6. SELECT example (split code)
- Code: `SELECT * FROM foo LIMIT 10`
- Question: "Show me the first 10 rows"
- Annotations:
  - SELECT * — all columns
  - FROM foo — from this table
  - LIMIT 10 — first 10 rows
```

Keep slide numbering continuous and include a **parenthetical hint about layout** so Claude picks the right pattern (e.g. "(3 cards)", "(split code)", "(section divider)", "(table)"). See [decks/sql-for-mbas/source.md](decks/sql-for-mbas/source.md) for the full worked example.

## Rules

- **Never modify `shared/deck-stage.js`** unless the user explicitly asks — it's production code shared across every deck.
- **Do not invent CSS.** If source.md calls for a pattern that doesn't exist in sql-for-mbas, ask the user how to style it rather than guessing.
- **Do not add dependencies** (no npm, no frameworks). Everything is plain HTML/CSS/JS.
- **Keep the footer-injection `<script>` at the bottom of every deck.** It's what makes the "Private and Confidential" footer bar appear.
- **Preview with Live Server**, not `file://`. The `<script src="../../shared/deck-stage.js">` relative path works over HTTP but can get finicky with `file://` on some browsers.

## Adding a deck to the landing page

Append one `<a class="deck-link">` entry inside the `<main>` of the root [index.html](index.html). Follow the existing pattern exactly.

## Proposals & one-pagers

Single-page printable docs (sales proposals, briefs) live under `proposals/<name>/index.html`. They share the deck palette and fonts but use A4 print CSS instead of the `<deck-stage>` web component — sized in `mm`/`pt` rather than the deck's `px`-on-1920 canvas. Canonical reference: [proposals/lbs-sql-programme/index.html](proposals/lbs-sql-programme/index.html). Export the same way as a deck: open in Chrome → Cmd+P → Save as PDF (Paper: A4, Margins: None, Background graphics: on). Don't list proposals on the root [index.html](index.html) — that page is the public GitHub Pages landing for decks.
