# Deck: Intermediate SQL

**Subtitle**: avidLearning · Workshop
**Date**: [TODO: add date]

> Follow-on workshop to [SQL for MBAs](../sql-for-mbas/source.md). Covers JOINs,
> subqueries, window functions, and using GenAI to move faster.
> Layout-hint conventions follow [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "Intermediate SQL" (title slide)
- Kicker: avidLearning · Workshop
- Date: [TODO]
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2-column numbered card grid + dashed break card)
- 01 Intro & expectations
- 02 JOINs
- (dashed) 10 minute break
- 03 Subqueries
- 04 Using GenAI to move faster (window functions are introduced as a fresh concept inside this section)

### 3. Workshop Expectations (full-slide, 3 cards with colored top borders)
- Cameras on — interactive environment
- Double-screen works best — slides on one screen, SQL tool on other
- Ask questions — just come off mute

### 4. Learning Objectives (full-slide, bulleted list `.si`/`.st`)
- Understand what a JOIN is; distinguish INNER / LEFT / RIGHT / FULL OUTER
- Combine multiple tables using table aliases and a shared key
- Write subqueries in the WHERE and FROM clauses
- Apply window functions like RANK() OVER for row-level analytics
- Use AI assistants to accelerate SQL learning

### 5. Section divider — "JOINs" (section divider, Section 01)
- Subtitle: "A JOIN combines columns from multiple tables using a common unique identifier or 'key.'"

### 6. A note on relational databases (full-slide, bullets `.si`/`.st`)
- SQL's superpower: store enormous amounts of data efficiently
- Efficiency comes from storing each entity separately in its own table
- To get a full picture we need to JOIN tables back together

### 7. JOIN Syntax — building blocks (full-slide, `.bb` list, FROM highlighted + alias callout)
- SELECT / FROM / WHERE / GROUP BY / ORDER BY / LIMIT
- Callout: JOINs live inside FROM. Use `AS` (or whitespace) to alias long table names

### 8. Types of JOINs (full-slide, inline 4-panel Venn SVG)
- LEFT JOIN / INNER JOIN / RIGHT JOIN / FULL OUTER JOIN

### 9. New data — `business.tuition_fees` (full-slide, `.dt` data table)
- Two columns: `school_id`, `tuition_fees_usd` · 95 rows

### 10. How much will I have to pay? (split code, INNER JOIN marker top-right)
- Code: INNER JOIN on `bs.school_rank = tf.school_id`
- Callout: only 95 rows returned — INNER JOIN drops unmatched

### 11. LEFT JOINs (split code, LEFT JOIN marker top-right)
- Code: LEFT JOIN variant
- Callout: 100 rows — every school retained, unmatched become NULL

### 12. Essential JOIN-ing tips (full-slide, 3 numbered rows)
- Know your keys
- Sense-check the size
- Alias sensibly

### 13. Let's test your understanding on some new data (exercise, full-slide, EXERCISE badge)
- Setup: dvdrental database in PGAdmin; identify primary keys
- 5 questions: film+language, rentals per customer, actors in PG films, customer+city, films per category

### 14. Solutions — skeleton queries (full-slide, 5 pink-title cards)

### 15. Solutions — full queries (full-slide, 5 teal-title cards)

### 16. Break (navy bg, coffee icon, "10 minute break")

### 17. Section divider — "Subqueries" (section divider, Section 02)
- Subtitle: "A query inside another query."

### 18. Subqueries (full-slide, concentric-circles SVG + bullets)
- Subquery runs first; parent uses the result in WHERE / SELECT / FROM

### 19. Subquery worked example (split code)
- Find schools with `weighted_salary_usd` above the overall average
- Subquery in the WHERE clause

### 20. Exercise: your turn (split code, EXERCISE badge, skeleton starter)
- Question: find schools with tuition fee data — without a JOIN
- Starter code with `[?]` placeholders for the operator and the subquery's SELECT column
- Hints: subquery returns a list; which operator checks "is in" a list?

### 21. Solution: subquery in WHERE (split code, SOLUTION badge)
- Reveal of the answer: `WHERE school_id IN (SELECT school_id FROM tuition_fees)`
- Annotations explaining the subquery + IN pattern

### 22. Exercise: subquery in FROM (split code, EXERCISE badge)
- Question: countries where avg weighted salary > $180,000
- Starter code: derived table `country_avg` aggregated by `primary_location`

### 23. Solution: subquery in FROM (split code, SOLUTION badge)
- Reveal of the answer with the derived table `country_avg` named via `AS`
- Annotations explaining the mini table → name it → parent filters it

### 24. Section divider — "Using GenAI to move faster" (section divider, Section 03)
- Subtitle: "You have the fundamentals — now let AI help you go further, faster."

### 25. Two ways AI can help (full-slide, 2-card grid)
- Card 1 (teal): Give Claude your schema — same question, completely different answer
- Card 2 (pink): Use Claude to learn new concepts — window functions today

### 26. Without your schema, Claude is guessing (full-slide, mocked Claude chat + "Won't run" panel)
- Question: for each customer, show their name and rental count, ordered by most rentals first (dvdrental)
- Claude response uses generic guesses: `customers`, `c.name`, `r.id`
- Right column flags what's wrong vs the real dvdrental schema

### 27. Giving Claude the schema (split code)
- Code: `SELECT table_name, column_name, data_type FROM information_schema.columns WHERE table_schema = 'public'`
- Numbered steps: run in pgAdmin → copy result → paste into Claude with "Here is my schema:"

### 28. Now Claude knows your tables (full-slide, mocked Claude chat + takeaway)
- Same question as slide 26, but user pasted the schema first
- Claude returns a correct query using `customer`, `rental`, `customer_id`, `rental_id`, with `GROUP BY customer_id`
- Takeaway: real table names, real column names, smarter grouping

### 29. Ask better questions (full-slide, 3-card grid + maxim)
- Intro: when Claude gives you a query, don't stop there — the follow-up is where you actually learn
- Card 1 (teal): Explain each line — ask Claude to comment every line so you can see what each piece does
- Card 2 (pink): Why is this correct? — ask Claude why this is the right query and what would break if you changed it
- Card 3 (teal): Is there a better way? — ask if there's a more elegant or efficient solution
- Closing maxim (centred, italic, muted): "The best answers come from asking the best questions."

### 30. Your turn — learn window functions with Claude (full-slide, EXERCISE badge, 15 min)
- Step 1 (teal card): paste schema, ask Claude what a window function is and for an example
- Step 2 (pink card): ask Claude to write a query for "rank films from longest to shortest within each category"
- Run the query in pgAdmin and verify the output

### 31. Knowledge check — what's a window function? (full-slide, MCQ, 4 lettered cards)
- A: collapses rows like GROUP BY (wrong)
- B: calculation across a set of rows related to the current row, without collapsing (correct)
- C: a subquery in WHERE (wrong)
- D: a way to JOIN tables (wrong)

### 32. RANK worked example (split code, fallback if students struggled)
- Same RANK example on `business.business_schools` — instructor pulls this up only if the room didn't get there themselves
- Uses `RANK() OVER (PARTITION BY primary_location ORDER BY weighted_salary_usd DESC)`

---

## TODO list (for later iteration)

- [ ] Fill in title date
- [ ] Consider a CTEs section as a follow-on to subqueries
- [ ] Add a wrap-up / Q&A closing slide
