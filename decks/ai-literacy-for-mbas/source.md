# Deck: AI Literacy for MBAs

**Subtitle**: avidLearning · Workshop
**Date**: Friday 22nd May 2026

> 3-hour workshop. Sister deck to [SQL for MBAs](../sql-for-mbas/index.html).
> Audience: MBAs who are casual ChatGPT/Claude users — week-1 personal use,
> never been taught how to prompt or where AI fits in a professional workflow.
> Goal: lift them to professional-grade use across the AI landscape, prompting,
> data work, and the failure modes (hallucination, sycophancy, over-reliance).

## Slides

### 1. Title — "AI Literacy for MBAs" (title slide, navy bg)
- Kicker: avidLearning · Workshop
- Title: AI Literacy / for MBAs (teal accent on "for MBAs")
- Date: Friday 22nd May 2026
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2×3 card grid with dashed break card)
- 01 Intro & expectations
- 02 The AI landscape
- 03 How to prompt
- (dashed) 10 minute break
- 04 AI + data
- 05 Where it goes wrong

### 3. Workshop Expectations (full-slide, 3 cards with teal top borders)
- Cameras on — "If at all possible"
- Double-screen works best — "Keep these slides on one screen and Claude on the other"
- Ask questions — "Just come off mute and shout out"

### 4. Who am I? (full-slide, 3 horizontal rows with teal numerals + divider + company logos)
- 01 Ex-data scientist — >2 years at Deliveroo
- 02 Ex-consultant — >4 years at Strategy& — data and analytics specialty
- 03 Experienced instructor — >5 years teaching analytics & AI

### 5. Today's aim (full-slide, two stacked quote-style blocks with coloured left borders)
- THE GOAL (teal border): become a **sophisticated** and **better-informed** user of AI tools at work
- NOT (grey border): to become a machine-learning engineer or build models from scratch

### 6. Speak fluent AI (full-slide, single-statement layout)
- Single statement, 44px: "Most people use AI like a **search engine**. The ones who get value from it use it like a **junior analyst**." (with the two phrases inline-coloured)
- Small-caps caption below: "That's the gap we're closing today"

### 7. Section divider — "The AI landscape" (section divider, teal accent, Section 02)

### 8. What is an LLM? (full-slide, two-column: light card + dark card)
- Left (light card): Stands for **Large Language Model**. A statistical engine that predicts the next chunk of text given everything before it — trained on roughly the public internet.
- Right (dark card): It's not a search engine, not a database, not a calculator. **It's a writer that has read a lot.** Treat it accordingly.

### 9. Why do you care? (full-slide, intro line + 4 cards in 2×2 grid, alternating teal/pink left borders)
- Intro: "AI fluency is no longer a 'nice to have'. A working command makes you:"
- 10× faster on first drafts — Memos, decks, models, summaries
- Less reliant on junior staff — Self-serve the things you'd have delegated
- More dangerous in meetings — Synthesise documents in seconds, not hours
- Day-one credible — Employers expect this on arrival, not after training

### 10. The frontier labs (full-slide, operator-style table `.ot`)
- Columns: Lab, Flagship product, Known for, Best for
- Anthropic — Claude — Writing & reasoning — Long-form analysis, careful answers
- OpenAI — ChatGPT — Broad ecosystem — General-purpose, image generation, voice
- Google — Gemini — Google integration — Docs, Sheets, Gmail workflows
- Meta — Llama (open) — Open weights — Running locally, fine-tuning
- xAI — Grok — Real-time X data — Live search, social context

### 11. The tool layers (full-slide, 2×2 card grid, alternating teal/pink left borders)
- Intro line: "AI doesn't live in one box. It shows up in four shapes:"
- Chatbot UIs — claude.ai, chatgpt.com, gemini.google.com — the front door
- IDE & doc assistants — Cursor, Copilot, Notion AI — AI inside the tool you already use
- Agentic tools — Claude Code, Devin, Manus — AI that can take actions, not just answer
- APIs — Anthropic / OpenAI / Google APIs — what powers everything your engineering team builds

### 12. Which tool when (full-slide, operator-style table `.ot`)
- Columns: Task, Pick this, Why
- Long-form writing & reasoning — Claude — Best instruction-following, longest careful answers
- General questions & images — ChatGPT — Largest feature surface, image generation built in
- Inside Google Docs / Sheets / Gmail — Gemini — Native, sees your files
- Code in your editor — Cursor / Copilot — Sees your repo, edits in place
- Live search & citations — Perplexity — Built around web search with sources
- Synthesise many documents — NotebookLM — Upload a pile, query the pile

### 13. The AI building blocks (full-slide, `.bb` list, 5 items)
- MODEL — Which AI you pick (Claude, GPT-4, Gemini…)
- CONTEXT — What you give it (files, links, conversation history)
- PROMPT — What you ask it to do
- TOOLS — What it can use (search, code execution, files)
- OUTPUT — The shape you want back (prose, table, JSON…)

### 14. Let's get connected (full-slide, terminal-window card with URL / account / fallback)
- URL: https://claude.ai/new
- Account: Use your LBS Google or a personal account
- Fallback: chatgpt.com works too — examples will use Claude

### 15. Section divider — "How to prompt" (section divider, teal accent, Section 03)

### 16. Anatomy of a prompt (full-slide, `.bb` list, 5 items)
- ROLE — Who the AI should act as
- CONTEXT — What it needs to know first
- TASK — What you want it to do
- FORMAT — How the answer should look
- EXAMPLES — What "good" looks like (optional but powerful)

### 17. The bad prompt (split code, prompt as `.cb` left, mediocre output right)
- Table label: prompt → output
- Question (qlbl): "Why is the output so generic?"
- Code (left): "write me something about pricing strategy" (with weak words highlighted via `.hi`)
- Right: mediocre output card — 4 bullets of vague McKinsey-ese. Annotations: no role, no context, no task shape, no audience.

### 18. The good prompt (split code, same prompt rewritten)
- Question: "Same topic. Different output. What changed?"
- Code (left): structured prompt with explicit ROLE / CONTEXT / TASK / FORMAT labels (in `.kw`)
- Right: sharper output (3 numbered recommendations, each with a tradeoff). Annotations: role anchors tone; context narrows scope; task spells out the deliverable; format dictates the shape.

### 19. Exercise 1: Rewrite the vague prompt (split code, EXERCISE badge)
- Question: "Take this lazy prompt and rewrite it using the 5 building blocks"
- Code (left, placeholder): `ROLE: [pl] / CONTEXT: [pl] / TASK: [pl] / FORMAT: [pl] / EXAMPLES: [pl]`
- Right hints:
  - Original lazy prompt (in a pill): "help me with a hiring decision"
  - Scenario: you're a PM at a fintech, hiring a senior data analyst, comparing two final candidates
  - Run your rewrite in Claude — compare to your unprompted answer

### 20. Answer 1 (split code, no badge)
- Code (left): worked rewrite, with each block labelled in `.kw`
  - ROLE: experienced hiring manager at an early-stage fintech
  - CONTEXT: pasting two anonymised CV summaries, hiring for senior data analyst, team of 4
  - TASK: produce a structured comparison and a recommended hire with risks
  - FORMAT: markdown table of strengths/weaknesses + a paragraph
  - EXAMPLES: (skipped — covered next)
- Annotations: role gives it a voice; context bounds the answer; task names the deliverable; format prevents prose-soup.

### 21. Few-shot prompting (split code)
- Question: "How do you teach Claude a pattern? Show it the pattern."
- Code (left): prompt with 2 worked examples of "complaint → root cause category" then asks for the third
- Right annotations: examples are stronger than instructions; 2-5 examples is the sweet spot; pick edge cases that show the rule.

### 22. Exercise 2: Classify customer complaints (split code, EXERCISE badge)
- Question: "Use few-shot prompting to classify 5 new complaints"
- Code (left, placeholder): "I'll show you 3 examples, then 5 to classify…" with `[pl]` for examples
- Right hints: categories — Pricing / Product quality / Delivery / Support / Other; paste the prompt into Claude; check that the labels match what you'd say.

### 23. Answer 2 (split code, no badge)
- Code (left): completed prompt with 3 example mappings (e.g. "Item arrived broken" → Product quality)
- Right: typical output (5 lines: complaint → category), annotations on why few-shot beats describing the categories.

### 24. Chain of thought (split code)
- Question: "Hard problems get better when you ask AI to think first."
- Code (left): prompt ending with `Think step by step before giving your final answer.` (last line in `.hi`)
- Right annotations: forces the model to "show its work" in tokens; catches arithmetic & logic errors; harmless on easy questions, transformative on hard ones.

### 25. Exercise 3: Reason through a deal memo (split code, EXERCISE badge)
- Question: "Use chain-of-thought to evaluate a small acquisition"
- Code (left): scenario block + prompt asking for: (1) the three biggest risks (2) the multiple paid (3) a go/no-go — with `Think step by step` at the end
- Right hints: paste the financials given; ask for the work shown; the goal is the **reasoning**, not the answer.

### 26. Answer 3 (split code, no badge)
- Code (left): full prompt as a student should have built it
- Right: notes on what to look for — does it surface the right risks first; does it ground the multiple in the financials; can you defend the answer in a meeting?

### 27. Asking for format (split code, three small `.cb` blocks left, why-it-matters right)
- Question: "The shape of the answer matters as much as the content."
- Left: three labelled mini-prompts — "as a markdown table", "as JSON with keys X, Y, Z", "as a 5-bullet exec summary, max 25 words each"
- Right: annotations — table beats prose for comparisons; JSON makes it pasteable into other tools; word limits force prioritisation.

### 28. Iterating, not restarting (full-slide, summary bullets `.si`)
- Intro line: "Don't start over. Edit the conversation."
- Bullets:
  - "Now do it again but **shorter**." — keeps the structure, trims the volume
  - "**Challenge that** — what would change your mind?" — surfaces hidden assumptions
  - "Now in **a table** with these columns: X, Y, Z." — restructures, doesn't recompute
  - "Imagine the **opposite view** is correct. Now what?" — second-mind, free
  - "Cite the **source** for each claim." — forces it to admit what it doesn't know

### 29. Prompt patterns recap (full-slide, 4 cards in 2×2 grid with mono-pill headers)
- ROLE & CONTEXT — Anchor the tone, bound the scope
- EXAMPLES — Show, don't describe
- FORMAT — Name the shape (table, JSON, bullets, word count)
- ITERATE — Edit the answer, don't restart

### 30. Comprehension check (full-slide, MCQ in 2×2 grid — mirrors intermediate-sql MCQ pattern)
- Quick-check badge
- Question (qlbl): "Which of these is the strongest move when an answer feels generic?"
- A — Start a new chat with a different model
- B — Ask the model to "be more specific"
- C — Add role, context, and an example of what good looks like (correct)
- D — Switch from a chatbot to an API

### 31. Break (inline dark navy bg, coffee icon, "10 minute break" + "Back soon" subtitle)

### 32. Section divider — "AI + data" (section divider, teal accent, Section 04)

### 33. The data + AI workflow (full-slide, 4 cards in 2×2 grid, alternating teal/pink left borders)
- Ingest — Get the data into the model (paste, upload, connect)
- Analyse — Ask the model to interrogate it (counts, outliers, trends)
- Synthesise — Combine multiple sources into one answer
- Communicate — Convert the answer into the artefact you need (memo, slide, email)

### 34. Three ways AI handles data (full-slide, `.bb` list, 3 items)
- PASTE-IN — Drop a table into the chat — fastest, fine for small data
- FILE UPLOAD — Attach a CSV / PDF / image — Claude & ChatGPT both support this
- CONNECTORS — MCP, Gemini-on-Drive, Copilot-on-Office — the model reads live from your tools

### 35. Pasting structured text (split code, prompt with embedded table)
- Question: "For small tables, paste is the fastest move."
- Code (left): a prompt containing a small markdown table of 8 product SKUs (price, units sold) and the ask: "find the 3 biggest revenue contributors and the one whose price/unit is out of line"
- Right annotations: markdown tables paste cleanly; works up to ~few hundred rows; for thousands of rows, upload instead.

### 36. Uploading a CSV (split code, prompt walkthrough)
- Question: "For bigger data, attach and ask."
- Code (left, mono): step-by-step — `1. Click the paperclip → 2. Attach the CSV → 3. Prompt:` then the prompt text "You are a data analyst. The attached CSV is a year of regional sales. Find the 3 biggest outliers and explain what could cause each. Show your working."
- Right annotations: model writes & runs code to inspect the file; checks file shape first; tell it the columns matter so it doesn't guess.

### 37. Exercise 4: Analyse a sample CSV (split code, EXERCISE badge — hands-on)
- Question: "Upload the FT MBA Rankings CSV and ask three questions"
- Code (left, mono): the three questions to ask, as pill rows
  - "How many schools are in the dataset, and what columns do you have?"
  - "Which 5 schools have the largest **gap** between rank and salary?"
  - "Are there any countries where the **average** salary is misleading because of one school?"
- Right: link / location of the CSV (`shared/assets/business_schools.csv` — download instructions); reminder to verify each answer against the file.

### 38. Answer 4 (split code, no badge)
- Code (left): example of how Claude responds — shows it inspecting the file first
- Right gotchas:
  - It will often confuse `weighted_salary_usd` with `current_salary_usd` — name the column you mean
  - "Outlier" is undefined — ask for a definition (z-score? top decile?)
  - **Verify**: if a chart is in the output, sanity-check 2-3 numbers against the CSV by eye

### 39. AI writes SQL (split code, NL → SQL — callback to SQL for MBAs)
- Question: "Most analyst questions become SQL. AI shortens that distance."
- Code (left): NL prompt on top — "From the `business.business_schools` table, show the top 5 schools in the UK by weighted_salary_usd"; generated SQL below (highlighted with `.kw` `.fn` `.str` `.num`).
- Right annotations: works best when you tell the model the schema; ask it to explain the query; **always run it yourself before trusting the answer**. Callback: this is exactly the workflow from the SQL for MBAs course.

### 40. Schema sharing (split code, callback to Intermediate SQL)
- Question: "AI doesn't know your database. You tell it."
- Code (left, mono): example of pasting a `CREATE TABLE` block first, then asking the question
- Right annotations: paste the schema once at the start of the chat; refresh the schema if your data model changes; without it, AI invents column names that don't exist.

### 41. Exercise 5: NL → SQL (split code, EXERCISE badge)
- Question: "Get Claude to write a query you can run"
- Code (left): scenario — schema for a `pizza_orders` table (columns: order_id, city, total_gbp, ordered_at, customer_id) + business question "What's the average order value by city for the last 30 days, ranked highest to lowest?"
- Right hints: paste the schema first; then the question; ask Claude to explain the query line by line; **then** ask Claude to spot what could go wrong with it.

### 42. Answer 5 (split code, no badge)
- Code (left): worked SQL using GROUP BY + DATE filter + ORDER BY (highlighted spans)
- Right verify-it list:
  - Does the date filter handle timezones? (probably no — flag it)
  - Should "average" be mean or median? (Claude defaulted to mean)
  - Is `total_gbp` the right column? (Could be a `total_after_discount_gbp` next to it)

### 43. Many docs → one answer (full-slide, two-column: how it works + when to use it)
- Lead-in: "When you have a pile of documents — a deal room, a literature review, six earnings reports — uploading to a chat is the wrong shape."
- Left card: **How it works** — Tools like **NotebookLM**, **Claude Projects**, **ChatGPT Custom GPTs**. Upload once, query repeatedly, the model only answers from your sources.
- Right (navy) card: **When to use it** — Deal due diligence, board prep, literature review, deposition prep. Anything where you need answers grounded in **specific documents** rather than the open web.

### 44. What AI can and can't see (full-slide, summary bullets `.si`)
- Intro line: "Three things to internalise about how AI 'sees' the world:"
- Bullets:
  - **Context windows are finite** — even long ones (~200k tokens / ~500 pages) — past that, it forgets the start
  - **It has no memory across chats by default** — every new conversation starts cold (unless you've turned memory on)
  - **It can't see the internet** unless you turn on web search — out of the box, knowledge cuts off at training time

### 45. Section divider — "Where it goes wrong" (section divider, **pink accent**, Section 05)

### 46. The four big pitfalls (full-slide, 4 cards in 2×2 grid, all with pink top borders)
- Hallucination — Confidently wrong; invented facts, citations, quotes
- Sycophancy — Agrees with you because you asked, not because you're right
- Over-reliance — Stops you doing the thinking the answer was meant to inform
- Confidentiality — Anything you paste may train future models or leak

### 47. Hallucination (split code)
- Question: "Confident, fluent, wrong."
- Code (left, mono): a real example prompt — "Summarise the key findings of the 2024 Harvard Business Review article on 'Mid-Market PE Pricing'" — followed by Claude's *fabricated* response citing a non-existent article and authors (key claims in `.hi` to flag them)
- Right annotations: ask for **sources you can verify**; if it sounds too clean, it's invented; web-search models hallucinate less but still cite wrongly.

### 48. Sycophancy (split code)
- Question: "AI tells you what you want to hear."
- Code (left): a user prompt — "I think we should fire our top sales rep because she pushes back too much. Don't you agree?" — followed by a sycophantic response that lists supportive reasons.
- Right annotations: AI is trained on human feedback and humans reward agreement; the failure is **silent** — you won't notice unless you check; the fix on the next slide.

### 49. How to push back (full-slide, summary bullets `.si`)
- Intro line: "Five moves to break the sycophancy loop:"
- Bullets:
  - "**What's the strongest argument against this?**" — explicit counter-prompt
  - "**Imagine you disagreed with me. What would you say?**" — role-flip
  - "Rate this on a **1-10 scale**, then justify the score." — forces non-binary judgement
  - "**What did I miss?**" — open-ended catch-all
  - **Switch model** for a second opinion — Claude → ChatGPT, or vice versa

### 50. Confidentiality red lines (full-slide, `.bb` list, 4 items)
- CLIENT DATA — Names, contracts, financials of a third party — never paste
- PII — Customer names, emails, payment info — strip or never paste
- TRADE SECRETS — Internal strategy decks, source code, pre-announcement plans — only into enterprise-tier tools with no-training settings
- FREE TIERS TRAIN ON YOU — Default ChatGPT, Gemini, Claude Free retain & may train on input; the paid Team/Enterprise tiers don't

### 51. Wrap-up (title-slide style, dark navy, 2×3 keyword pill grid)
- Section 05 kicker
- Title: Wrap-up
- 2×3 keyword pill grid:
  - ROLE · CONTEXT — Anchor every prompt
  - EXAMPLES — Show, don't describe
  - FORMAT — Name the shape
  - ITERATE — Edit, don't restart
  - VERIFY — Sources, not vibes
  - CONFIDENTIALITY — Mind what you paste

### 52. You can all now… (full-slide, two-column: 4 checklist rows on left + image on right)
- Left column: 4 rows with teal check-circle icons
  - Pick the right AI tool for the job at hand
  - Write a prompt that gets a usable answer first time
  - Use AI to interrogate data you couldn't analyse manually
  - Spot when AI is hallucinating, agreeing, or making you lazy
- Right column: `../../shared/assets/logo.png` (or a placeholder image card)

### 53. What's next? (full-slide, intro line + 2 course cards with teal / pink top borders)
- Intro: "Build on this with the rest of the curriculum"
- Card 1 (teal top border) — Course 01: **SQL for MBAs** / tagline "Talk to data, not analysts." / You'll learn: SELECT/FROM/WHERE; comparison & filtering; aggregates & GROUP BY; CASE WHEN
- Card 2 (pink top border) — Course 02: **Intermediate SQL** / tagline "From comfortable to confident." / You'll learn: JOINs; Subqueries & CTEs; Window functions; Query optimisation with AI

### 54. Questions & Feedback (final slide, dark navy, two-column: heading + two QR cards)
- Left: "Questions & Feedback" heading (teal accent on "Feedback") + pink underline + "Thanks for joining!" subtitle
- Right: two white rounded cards side-by-side
  - Feedback QR: pink small-caps label "Feedback" — placeholder until real QR generated
  - LinkedIn QR: teal small-caps label "Let's connect" + `shared/assets/LinkedIn.png`
- Logo at bottom
