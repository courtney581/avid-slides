# Deck: Intermediate SQL

**Subtitle**: avidLearning · Workshop
**Date**: [TODO: add date]

> Follow-on workshop to [SQL for MBAs](../sql-for-mbas/source.md). Scaffolded from
> the initial 10-slide outline; more slides will be added as the course develops.
> Layout-hint conventions follow [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "Intermediate SQL" (title slide)
- Kicker: avidLearning · Workshop
- Date: [TODO]
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2-column numbered card grid + dashed break card)
- 01 Intro & expectations
- 02 Learning objectives
- 03 JOINs
- (dashed) 10 minute break
- 04 Subqueries
- 05 Wrap-up & questions

### 3. Workshop Expectations (full-slide, 3 cards with colored top borders)
- Cameras on — interactive environment
- Double-screen works best — slides on one screen, SQL tool on other
- Ask questions — no silly questions, come off mute

### 4. Learning Objectives (full-slide, bulleted list `.si`/`.st`)
- Understand what a JOIN is and when to use one
- Combine data from multiple tables using a shared key
- Distinguish between INNER, LEFT, RIGHT, and FULL OUTER JOINs
- Write multi-table queries with table aliases

### 5. Section divider — "JOINs" (section divider, Section 01, teal accent)
- Subtitle: "A JOIN combines columns from multiple tables using a common unique identifier or 'key.'"

### 6. A note on relational databases (full-slide, bullets `.si`/`.st`)
- SQL's superpower: store enormous amounts of data efficiently
- Efficiency comes from storing each entity separately in its own table
- To get a full picture we need to JOIN tables back together

### 7. JOIN Syntax — building blocks (full-slide, `.bb` list, FROM highlighted + alias callout)
- SELECT / FROM / WHERE / GROUP BY / ORDER BY / LIMIT
- FROM row highlighted (teal border, yellow keyword)
- Callout: JOINs live inside FROM. Use `AS` (or whitespace) to alias long table names

### 8. Types of JOINs (full-slide, inline 4-panel Venn SVG)
- LEFT JOIN / INNER JOIN / RIGHT JOIN / FULL OUTER JOIN

### 9. New data — `business.tuition_fees` (full-slide, `.dt` data table)
- Two columns: `school_id`, `tuition_fees_usd`
- Caption: Table: business.tuition_fees · 100 rows

### 10. How much will I have to pay? (split code, INNER JOIN marker top-right)
- Question: How do tuition fees compare between top MBA schools?
- Code: `SELECT bs.*, tf.* FROM business.business_schools AS bs JOIN business.tuition_fees AS tf ON bs.school_rank = tf.school_id`
- Annotations: `bs`/`tf` aliases; JOIN combines matching rows; ON defines the matching key
- Callout: only 95 rows returned — INNER JOIN drops the 5 unmatched schools

### 11. LEFT JOINs (split code, LEFT JOIN marker top-right)
- Question: What if we want to keep every school, even those without tuition data?
- Code: same as slide 10 but with `LEFT JOIN`
- Annotations: LEFT JOIN keeps all rows from left table; result ≥ left table; unmatched rows become NULL
- Callout: 100 rows — every school retained, 5 show NULL

### 12. Essential JOIN-ing tips (full-slide, 3 numbered rows)
- 01 Know your keys — understand primary keys; that's what you JOIN ON
- 02 Sense-check the size — INNER JOIN result ≤ smaller input table
- 03 Alias sensibly — abbreviate the original table name (business_schools → bs)

### 13. Let's test your understanding on some new data (exercise, full-slide, EXERCISE badge, 2-column)
- Left (set-up): navigate to the `dvdrental` database in PGAdmin; browse tables and spot the primary keys
- Right (5 questions):
  1. List every film with its language name (e.g. "English")
  2. List all customers and the number of rentals each has made
  3. List every actor who has appeared in a film rated 'PG'
  4. List each customer with the city they live in
  5. How many films are in each category?

### 14. Solutions — skeleton queries (full-slide, 5 pink-title cards in a 3-col flex grid)
- Scaffolds for each of the 5 questions with `[?]` / `[bridge]` placeholders

### 15. Solutions — full queries (full-slide, 5 teal-title cards in a 3-col flex grid)
- Complete answers: INNER JOIN for films+languages; LEFT JOIN for rentals per customer; double JOIN with `film_actor`, filter on rating; double JOIN customer→address→city; double JOIN with `film_category`, GROUP BY

### 16. Break (navy bg, coffee icon, "10 minute break")

### 17. Section divider — "Subqueries" (section divider, Section 02, teal accent)
- Subtitle: "A query inside another query."

### 18. Subqueries (full-slide, concentric-circles SVG + bullets)
- Diagram: solid teal outer circle "PARENT QUERY · runs second · uses the result"; inner pink-bordered navy circle bottom-aligned with the outer, labelled "SUBQUERY · runs first"
- Bullets: subquery runs first; parent uses the result in WHERE/SELECT/FROM; handy for comparing rows against a summary

### 19. Subquery worked example (split code)
- Find schools with `weighted_salary_usd` above the overall average
- Code highlights the subquery inside the WHERE clause
- Annotations explain execution order and why it's cleaner than two separate queries

---

## TODO list (for later iteration)

- [ ] Fill in title date
- [ ] Add further subquery examples (SELECT-clause subquery, correlated subquery)
- [ ] Consider a CTEs section as a follow-on to subqueries
- [ ] Add a wrap-up / Q&A closing slide
