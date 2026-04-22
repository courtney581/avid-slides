# avid-slides

avidLearning's slide decks. Each deck is a self-contained HTML file that renders a 1920×1080 presentation in the browser, with keyboard nav, auto-scaling, and one-slide-per-page PDF export built in.

## Decks

- **[SQL for MBAs](decks/sql-for-mbas/)** — Friday 24th April 2026

(Also viewable as a list at the root [index.html](index.html).)

## Preview a deck locally

1. Install the **Live Server** extension in VS Code ([ritwickdey.LiveServer](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)).
2. Open any `index.html` (root or inside a deck).
3. Right-click → **Open with Live Server**. Edits auto-reload.

Keyboard: `← →` navigate, `R` reset to slide 1, `1–9` jump to slide, `Cmd+P` print to PDF.

## Edit an existing deck

Open the deck's `index.html` in VS Code. Each slide is a `<section>`. Change text, save, Live Server reloads. The inline `<style>` block at the top of each deck's file defines its look; don't rip pieces out unless you know what you're doing — most of it is shared across slide types.

## Create a new deck (AI-assisted workflow)

1. Create the folder: `mkdir -p decks/my-new-deck/assets`
2. Write a bullet outline at `decks/my-new-deck/source.md`. See [decks/sql-for-mbas/source.md](decks/sql-for-mbas/source.md) for the format — one `###` per slide, bullets for content, parenthetical hint about layout (e.g. "(3 cards)", "(split code)").
3. Open Claude Code in this repo and ask: **"Build the deck at `decks/my-new-deck/` from `source.md`, matching the sql-for-mbas style."** Claude will read [CLAUDE.md](CLAUDE.md) + the SQL deck as reference and produce `index.html`.
4. Preview with Live Server, iterate with Claude ("shrink the title", "swap slide 5 for a split-code pattern", etc.).
5. Add a line to the root [index.html](index.html) linking to the new deck.
6. Commit and push.

You can also edit the generated HTML by hand — Claude's output is just regular HTML in the same patterns as the SQL deck.

## Export a deck to PDF

Open the deck in a browser (Live Server or GitHub Pages) → **Cmd+P** → Save as PDF. The deck's print CSS paginates one slide per page at 1920×1080 with no margins.

## Publish (GitHub Pages)

After pushing the repo to GitHub:
1. Repo Settings → **Pages**
2. Source: **Deploy from a branch**, Branch: **main**, Folder: **/ (root)**
3. Save. Decks will be live at `https://<your-username>.github.io/avid-slides/decks/<deck-name>/`.

The `.nojekyll` file in the root disables Jekyll processing so files/folders starting with `_` (if any) aren't stripped.

## Repo layout

- [shared/deck-stage.js](shared/deck-stage.js) — the web component powering every deck. Shared so bug fixes apply everywhere.
- [shared/assets/](shared/assets/) — shared imagery (the avidLearning logo).
- [decks/](decks/) — one folder per deck, containing `index.html`, `source.md`, and any deck-specific `assets/`.
- [CLAUDE.md](CLAUDE.md) — style bible + instructions for Claude when scaffolding new decks.
