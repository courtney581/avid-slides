# Deck: SQL for MBAs

**Subtitle**: avidLearning · Workshop
**Date**: Friday 24th April 2026

> This is the bullet outline the deck was built from. It doubles as the canonical
> `source.md` example for other decks — every layout-hint convention used here
> (e.g. "(split code)", "(3 cards)", "(section divider)") is understood by the
> Claude instructions in [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "SQL for MBAs" (title slide)
- Kicker: avidLearning · Workshop
- Date: Friday 24th April 2026
- avidLearning logo + copyright at bottom

### 2. Agenda (full-slide, 2×3 card grid + dashed break card)
- 01 Intro & expectations
- 02 What is SQL?
- 03 How does SQL work?
- 04 Why is it useful?
- 05 Wrap-up & questions
- (dashed) 10 minute break

### 3. Workshop Expectations (full-slide, 3 cards with colored top borders)
- Cameras on — interactive environment
- Double-screen works best — slides on one screen, SQL tool on other
- Ask questions — no silly questions, come off mute

### 4. Why listen to me? (full-slide, 3 horizontal rows with big numerals)
- 01 Ex-data scientist — 2+ years Deliveroo (pre-IPO), RVU (PE)
- 02 Ex-consultant — 4+ years at Strategy&
- 03 Experienced instructor — 5+ years B2B cohorts at large enterprises

### 5. Today's aim (full-slide, two stacked quote-style blocks)
- THE GOAL: become a more sophisticated and better-informed user of data
- NOT: to become a data analyst or data scientist

### 6. Section divider — "What is SQL?" (section divider, teal accent, labelled Section 02)

### 7. What is SQL? (full-slide, two-column: light card + dark card)
- Left (light card): Stands for Structured Query Language — we use it to query large datasets
- Right (dark card): SQL is **ubiquitous** — almost every large business employs analysts to use SQL

### 8. Why do you care? (full-slide, 4 cards in 2×2 grid, alternating teal/pink left borders)
- Better informed — data-driven decisions, not guesswork
- Less reliant on analysts — self-serve answers
- More confident — understand the data behind dashboards
- More 'dangerous' in meetings — spot when numbers don't add up

### 9. But can't I just use Excel? (full-slide, two-column comparison: Excel vs SQL)
- Excel cons: only as fast as your computer, can't handle big data, max 1.1m rows
- Excel pros: good for small data viz
- SQL pros: millions of records, cloud-based, production-scale, relational

### 10. Why Excel doesn't scale (full-slide, two image cards + navy stats strip)
- Intro line: Excel leads to redundancy; relational DBs eliminate it by storing each entity once and linking tables by keys
- Left card (pink accent): "The Excel way — one flat table, repeated data" with `assets/Excel.png` and caption about customer details repeated on every row
- Right card (teal accent): "The relational way — normalised tables linked by keys" with `assets/RelationalData.png` and caption about tables linked by IDs
- Bottom navy strip: Excel limit 1.1m rows (pink) · SQL ∞ (green)

### 11. Section divider — "How does SQL work?" (section divider, Section 03)

### 12. Let's get connected (full-slide, terminal-window card with URL/user/password)
- URL: http://51.44.8.109/pgadmin4/browser/
- Username: student@mbadata.com
- Password: dataformbas

### 13. Our dataset: FT MBA Rankings (full-slide, data table `.dt` with 5 sample rows)
- Columns: school_rank, school_name, weighted_salary_usd, female_students_pct, primary_location, value_for_money_rank
- Caption: Table: business.business_schools · 100 rows

### 14. SQL Building Blocks (full-slide, `.bb` list)
- SELECT — the columns to analyse
- FROM — the table
- WHERE — the filter(s)
- ORDER BY — the column(s) to use for sorting

### 15. SELECT * (split code)
- Question: Show me the first 10 rows of data
- Code: `SELECT * FROM business.business_schools LIMIT 10;`
- Annotations: SELECT * = all columns; FROM = this table; LIMIT 10 = first 10 rows

### 16. COUNT(*) (split code)
- Question: How many rows are in my data?
- Code: `SELECT COUNT(*) FROM business.business_schools;`
- Expected result box: 100

### 17. Exercise: Select specific columns (split code, EXERCISE badge)
- Question: I only care about salary data for now
- Task: modify query to select school_rank, school_name, weighted_salary_usd

### 18. Answer: Select specific columns (split code)
- Code: `SELECT school_rank, school_name, weighted_salary_usd FROM ... LIMIT 10;`
- Annotations: name each column; comma-separated; leading commas are a stylistic preference

### 19. WHERE clause (split code)
- Question: I only want to see schools in the US
- Code: `... WHERE primary_location = 'US' LIMIT 10;`
- Annotations: WHERE filters rows; = exact match; text needs single quotes

### 20. Comparison Operators (full-slide, operator table `.ot`)
- =, <> / !=, >, >=, BETWEEN, ILIKE, AND, OR — each with example

### 21. Exercise: UK + Salary (split code, EXERCISE badge)
- Question: Show me schools in the UK with salaries > $180k
- Hint: use AND to combine two conditions

### 22. Exercise: US or UK + female % (split code, EXERCISE badge)
- Question: US or UK schools with > 50% female students
- Hint: use OR for location, AND for female %; wrap ORs in parens

### 23. BETWEEN operator (split code)
- Question: US/UK schools, >50% female, salary $120k–$170k
- Annotations: BETWEEN is inclusive; parens control precedence; multiple ANDs all true

### 24. ILIKE pattern matching (split code with wildcard reference block)
- Question: schools containing "University of"
- Code: `... WHERE school_name ILIKE '%University of%';`
- Reference: `%london%` contains, `london%` starts-with, `%london` ends-with
- Annotations: ILIKE = case-insensitive; % = wildcard; LIKE = case-sensitive

### 25. SQL Building Blocks — ORDER BY highlighted (full-slide, `.bb` list, ORDER BY row highlighted)

### 26. ORDER BY example (split code)
- Question: top 5 schools by earning potential
- Code: `... ORDER BY weighted_salary_usd DESC LIMIT 5;`
- Annotations: ORDER BY sorts; DESC = highest first; LIMIT 5 = top 5

### 27. Exercise: highest salary (split code, EXERCISE badge)
- Question: which school has the highest weighted average salary?
- Hints: select school_name + weighted_salary_usd; ORDER BY DESC; LIMIT 1

### 28. DISTINCT (split code with "expected result" box)
- Two code blocks: `SELECT DISTINCT primary_location ...` and `SELECT COUNT(DISTINCT ...)`
- Expected result: 18 countries

### 29. Part 1 Summary (full-slide, 4 cards in 2×2 grid with SQL-keyword pills)
- SELECT / FROM, WHERE, ORDER BY, COUNT / DISTINCT

### 30. Break slide (inline dark, coffee icon, "10 minute break")

### 31. Section divider — "Aggregate Functions" (section divider, with tagline "SUM, AVG, COUNT, MAX, MIN")

### 32. AVG function intro (split code)
- Question: what's the average salary for an MBA grad from a top 100 school?
- Code: `SELECT AVG(weighted_salary_usd) FROM ...`
- Note: introduces concept of summary statistics vs individual rows

### 33. SQL Building Blocks — GROUP BY highlighted (full-slide, `.bb` list, GROUP BY row added and highlighted)

### 34. GROUP BY example (split code)
- Question: how do salaries compare across countries?
- Code: `SELECT primary_location, AVG(...) ... GROUP BY primary_location ORDER BY AVG(...) DESC;`
- Annotations: GROUP BY groups then aggregates; non-aggregated cols must appear in GROUP BY; think PivotTable

### 35. Aggregate functions reference (full-slide, operator table)
- COUNT, AVG, SUM, MAX, MIN — with descriptions and examples

### 36. Exercise: MAX by country (split code, EXERCISE badge)
- Question: max salary per country?
- Hints: use MAX(); GROUP BY primary_location; order by max DESC

### 37. MAX with AS alias (split code)
- Code introduces `AS max_sal` and then uses the alias in ORDER BY
- Annotations: AS gives a shorter name; reusable in ORDER BY; improves readability

### 38. Aliasing explained (full-slide, two columns: two code snippets + "why alias?" sidebar)
- Basic alias example
- With aggregation example
- Sidebar: easier to read, required for computed cols, reuse in ORDER BY, shortens long names

### 39. Exercise: COUNT by country (split code, EXERCISE badge, with 3 category hint boxes)
- Question: how many schools in each country?
- Hints: COUNT(*); GROUP BY primary_location; alias as num_schools

### 40. Answer: COUNT by country (split code)
- Full query with annotations

### 41. CASE WHEN intro (full-slide, two-column: explanation + IF/ELSE pseudocode card)
- Motivation: dataset doesn't have "US vs International" but has primary_location
- CASE WHEN = manipulate data beyond what exists

### 42. CASE WHEN: US vs International (split code)
- Code: CASE WHEN primary_location != 'US' THEN 'International' ELSE primary_location END AS region
- Annotations: CASE WHEN row-by-row; THEN = if true; ELSE = fallback; END AS names the column

### 43. CASE WHEN + GROUP BY (split code, with "expected output" box)
- Combines CASE WHEN with GROUP BY on the aliased region
- Expected: US · 51 schools, International · 49 schools

### 44. Exercise: Pay category (split code, EXERCISE badge, with 3 category hint boxes)
- Build a CASE WHEN that labels schools Elite Pay (>$200k) / Strong Pay ($160–200k) / Lower Pay (otherwise)

### 45. Answer: Pay category (split code)
- Full query + annotations about multiple WHEN clauses, ELSE as catch-all, alias in GROUP BY

### 46. Wrap-up (title-slide style, dark, with 6 keyword pill grid)
- Section 05 kicker
- Grid: SELECT·FROM, WHERE, ORDER BY, GROUP BY, COUNT·AVG·MAX…, AS (alias)

### 47. You can all now… (full-slide, 4 rows with teal check circles)
- Interrogate the data
- Investigate and challenge hypotheses
- Check for discrepancies in the data
- Select and manipulate the relevant variables

### 48. Speak purple (full-slide, two-column: single statement + image card)
- Left: one sentence — "If business people speak **blue** and tech people speak **red**, being able to speak **purple** makes you the most valuable person in the room." ('blue'/'red'/'purple' inline-coloured)
- Right: `assets/Purple_small.jpg` + small-caps caption "That's what we're here to do"

### 49. Section divider — "What about GenAI?" (section divider, **pink accent** instead of teal, kicker "A note on")

### 50. What about GenAI? (full-slide, 3 cards with colored top borders, mix of light + dark card)
- Always been normal — analysts always Googled / StackOverflowed
- GenAI is not infallible — sycophantic, can give answers that never work
- Know the basics first — GenAI makes you 10× faster if you know SQL; 10× slower if you don't

### 51. What's next? (full-slide, 2 cards with teal / pink top borders, penultimate slide)
- Intro + "Continue your journey with avidLearning"
- Card 1 (teal): Intermediate SQL — JOINs, CTEs, window functions, query optimisation
- Card 2 (pink): Intro to Python for Business — Python fundamentals, pandas, matplotlib, automating Excel
- Footer CTA: "Register your interest — avidlearning.com"

### 52. Questions & Feedback (final slide, dark, minimal)
- Logo + copyright at bottom
