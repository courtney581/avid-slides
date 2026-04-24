# Deck: SQL for MBAs

**Subtitle**: avidLearning · Workshop
**Date**: Friday 24th April 2026

> This is the bullet outline the deck was built from. It doubles as the canonical
> `source.md` example for other decks — every layout-hint convention used here
> (e.g. "(split code)", "(3 cards)", "(section divider)") is understood by the
> Claude instructions in [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "SQL for MBAs" (title slide, navy bg)
- Kicker: avidLearning · Workshop
- Title: SQL / for MBAs (teal accent on "for MBAs")
- Date: Friday 24th April 2026
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2×3 card grid with dashed break card)
- 01 Intro & expectations
- 02 What is SQL?
- 03 How does SQL work?
- (dashed) 10 minute break
- 04 Aggregate functions
- 05 Wrap-up & questions

### 3. Workshop Expectations (full-slide, 3 cards with teal top borders)
- Cameras on — "If at all possible"
- Double-screen works best — "Keep these slides on one screen and PGAdmin on the other, if possible"
- Ask questions — "Just come off mute and shout out"

### 4. Who am I? (full-slide, 3 horizontal rows with teal numerals + divider + company logos)
- 01 Ex-data scientist — >2 years at Deliveroo (inline `shared/assets/deliveroo.png` logo)
- 02 Ex-consultant — >4 years at Strategy& (inline `shared/assets/strategy.png` logo) - data and analytics specialty
- 03 Experienced instructor — >5 years teaching analytics

### 5. Today's aim (full-slide, two stacked quote-style blocks with coloured left borders)
- THE GOAL (teal border): become a more **sophisticated** and **better-informed** user of data
- NOT (grey border): to become a data analyst or data scientist

### 6. Speak purple (full-slide, two-column: single statement + image card)
- Left: one sentence — "If business people speak **blue** and tech people speak **red**, being able to speak **purple** makes you the **most valuable person in the room**." ('blue'/'red'/'purple' inline-coloured blue/red/purple)
- Right: `assets/Purple_small.jpg` + small-caps caption "That's what we're here to do"

### 7. Section divider — "What is SQL?" (section divider, teal accent, labelled Section 02)

### 8. What is SQL? (full-slide, two-column: light card + dark card)
- Left (light card): Stands for Structured Query Language. A language we use to **query** and ask for information from large datasets.
- Right (dark card): SQL is **ubiquitous** — almost every large business employs analysts to answer business questions using SQL. It's the universal language of data.

### 9. Why do you care? (full-slide, intro line + 4 cards in 2×2 grid, alternating teal/pink left borders)
- Intro: "SQL enables **you** to interrogate how a business is actually performing. A basic understanding makes you:"
- Better informed — Make data-driven decisions with confidence, not guesswork.
- Less reliant on analysts — Self-serve answers to common data questions without waiting in the queue.
- More confident — Understand the data behind the dashboards your team presents.
- More 'dangerous' in meetings — Know when the numbers don't add up — and be able to ask the right questions.

### 10. But can't I just use Excel? (full-slide, two-column comparison: Excel card light + SQL card dark)
- Excel (light card): ✗ Only as fast as your computer; ✗ Cannot handle 'big data'; ✗ Max 1.1 million rows; ✓ Good for small data visualisation
- SQL (dark card): ✓ Easily retrieves millions of records; ✓ Cloud-based — not limited by laptop specs; ✓ Handles production-scale datasets; ✓ Works on relational databases

### 11. Why Excel doesn't scale (full-slide, two cards with inline HTML comparison tables)
- Intro line: "Excel spreadsheets lead to **redundancy**. Relational databases eliminate it — storing each entity once and linking tables by keys."
- Left card (pink accent): "The Excel way — One flat table, repeated data". Rendered orders table (order_id, customer_name, customer_city, product_name, product_category, product_price) with duplicated customer rows highlighted pink. Caption: "Customer details are repeated on every order row — storage balloons and updates are error-prone."
- Right card (teal accent): "The SQL way — Related tables, stored once". Three stacked tables (Orders with primary key order_id + foreign keys customer_id/product_id; Customers; Products) + legend showing teal = primary key, pink = foreign key. Caption: "Each entity lives in one table. Primary keys identify rows; foreign keys link tables — cheaper, cleaner, scales to billions of rows."

### 12. Section divider — "How does SQL work?" (section divider, Section 03)

### 13. Let's get connected (full-slide, terminal-window card with URL/user/password, mac-style window chrome)
- URL: http://51.44.8.109/pgadmin4/browser/
- Username: student@mbadata.com
- Password: dataformbas

### 14. Our dataset: FT MBA Rankings (full-slide, data table `.dt` with 5 sample rows)
- Intro: "We'll use SQL to interrogate this dataset — the **Financial Times Global MBA Rankings**"
- Preview note (mono italic): "Preview — the full table in the database has additional columns"
- Columns shown: school_rank, school_name, weighted_salary_usd, primary_location
- Sample rows: Wharton (US, $245,772), Insead (France, $198,904), Columbia (US, $232,760), SDA Bocconi (Italy, $202,534), London Business School (UK, $192,331)
- Caption: Table: business.business_schools · 100 rows

### 15. SQL Building Blocks (full-slide, `.bb` list, 5 items)
- SELECT — The columns to analyse
- FROM — The table
- WHERE — The filter(s)
- ORDER BY — The column(s) to use for sorting
- LIMIT — The maximum number of rows to return

### 16. SELECT * (split code)
- Table label: business.business_schools
- Question: Show me the first 10 rows of data
- Code: `SELECT * FROM business.business_schools LIMIT 10;`
- Annotations: SELECT * = Retrieve all of the columns; FROM business.business_schools = From this specific table; LIMIT 10 = Return only the first 10 rows

### 17. COUNT(*) (split code, with expected-result box)
- Question: How many rows are in my data?
- Code: `SELECT COUNT(*) FROM business.business_schools;`
- Annotations: COUNT(*) counts total rows; result is a single number
- Expected result box: 100

### 18. Exercise: Select specific columns (split code, EXERCISE badge)
- Question: How do the top 100 schools compare on salary?
- Task: Modify the query to select only — school_rank, school_name, weighted_salary_usd (shown as 3 mono pill rows)

### 19. Answer: Select specific columns (split code)
- Question: How do the top 100 schools compare on salary?
- Code: `SELECT school_rank, school_name, weighted_salary_usd FROM ... LIMIT 10;` (leading-comma style)
- Annotations: name each column; comma-separated; leading commas are a stylistic preference (easier to comment out individual columns)

### 20. WHERE clause (split code)
- Question: How do the US schools compare on salary?
- Code: `... WHERE primary_location = 'US' LIMIT 10;`
- Annotations: WHERE is a row filter; = checks for exact match; text values go in single quotes — numbers don't

### 21. Comparison Operators (full-slide, operator table `.ot`)
- =, <> / !=, >, >=, BETWEEN, ILIKE, AND, OR — each with meaning + code example (example column uses mono font with pink string literals and orange numeric literals)

### 22. Exercise: UK + Salary (split code, EXERCISE badge)
- Question: Show me schools in the UK with average salaries > $180k
- Hint: Use AND to combine two conditions

### 23. Exercise: US or UK + female % (split code, EXERCISE badge)
- Question: Show me schools in the US or UK with > 50% female students
- Hints: Use OR for location and AND for female %; wrap OR conditions in parentheses to control operator precedence

### 24. BETWEEN operator (split code)
- Question: US or UK schools with >50% female students and salaries between $120–$170k
- Annotations: BETWEEN is inclusive; parentheses control operator precedence (AND evaluates before OR without them); multiple ANDs all must be true simultaneously

### 25. ILIKE pattern matching (split code with wildcard reference block in lower-left)
- Question: Show me schools with names containing the phrase 'University of'
- Code: `... WHERE school_name ILIKE '%University of%';`
- Wildcard reference: `'%london%'` contains, `'london%'` starts with, `'%london'` ends with
- Annotations: ILIKE is case-insensitive; % is a wildcard; LIKE is case-sensitive

### 26. SQL Building Blocks — ORDER BY highlighted (full-slide, same 5-item `.bb` list, ORDER BY row highlighted teal)

### 27. ORDER BY example (split code)
- Question: Show me the top 5 schools in terms of earning potential
- Code: `... ORDER BY weighted_salary_usd DESC LIMIT 5;`
- Annotations: ORDER BY sorts by the specified column; DESC = highest first (ASC for ascending); LIMIT 5 = top 5 rows

### 28. Exercise: highest salary (split code, EXERCISE badge)
- Question: Which school has the highest weighted average salary?
- Hints: Select school_name + weighted_salary_usd; Sort by weighted_salary_usd DESC; Limit to 1 row

### 29. DISTINCT (split code, two code blocks, with expected-result box)
- Question: Which unique countries made the list of top 100 schools?
- Code block 1: `SELECT DISTINCT primary_location FROM ... ORDER BY primary_location;` (with `-- Unique values` comment)
- Code block 2: `SELECT COUNT(DISTINCT primary_location) FROM ...;` (with `-- Count unique values` comment)
- Annotations: DISTINCT removes duplicates; combine COUNT and DISTINCT to count unique values
- Expected result box ("How many unique countries?"): 18 countries

### 30. Part 1 Summary (full-slide, 4 cards in 2×2 grid with SQL-keyword pills)
- SELECT / FROM — Every query needs these two. Use `*` for all, or name columns.
- WHERE — Filters rows. Use comparison operators: =, !=, >, BETWEEN, ILIKE
- ORDER BY — Sorts results. Add DESC for descending, ASC for ascending.
- COUNT / DISTINCT — Aggregators enable summary statistics. DISTINCT returns unique entries.

### 31. Break slide (inline dark navy bg, coffee icon, "10 minute break" + "Back soon" subtitle)

### 32. Section divider — "Aggregate Functions" (section divider, Section 04, with tagline "SUM, AVG, COUNT, MAX, MIN")

### 33. AVG function intro (split code)
- Question: What is the average salary for an MBA graduate from a top 100 school?
- Code: `SELECT AVG(weighted_salary_usd) FROM business.business_schools;` (with `-- Average salary across all schools` comment)
- Lead-in on right panel: "When querying a dataset we're often interested in **summary statistics** rather than individual rows. This is where aggregators come in."
- Annotations: returns the average (mean) of a numeric column; works like Excel's AVERAGE()

### 34. SQL Building Blocks — GROUP BY highlighted (full-slide, `.bb` list, GROUP BY row inserted after WHERE and highlighted teal; full 6-item list now: SELECT, FROM, WHERE, GROUP BY, ORDER BY, LIMIT)

### 35. GROUP BY example (split code)
- Question: How do average post-MBA salaries compare across different countries?
- Code: `SELECT primary_location, AVG(weighted_salary_usd) ... GROUP BY primary_location ORDER BY AVG(weighted_salary_usd) DESC;`
- Annotations: GROUP BY groups then aggregates each group; non-aggregated SELECT cols must appear in GROUP BY; think PivotTable — one row per unique value

### 36. Aggregate functions reference (full-slide, operator table `.ot`)
- COUNT(), AVG(), SUM(), MAX(), MIN() — each with description and example (green function names)
- Footer line: "These functions operate on a column and return a **single summary value**, or one value per group when used with GROUP BY."

### 37. Exercise: MAX by country (split code, EXERCISE badge)
- Question: What is the maximum salary for schools in different countries?
- Hints: Use MAX() to find the highest salary; use GROUP BY primary_location; order so highest-salary country appears first

### 38. MAX with AS alias (split code)
- Question: What is the maximum salary for schools in different countries?
- Code introduces `AS max_sal` and reuses the alias in `ORDER BY max_sal DESC`
- Annotations: AS max_sal gives a shorter, cleaner name; alias reusable in ORDER BY; improves readability (especially with long expressions)

### 39. Aliasing explained (full-slide, two-column: two stacked code snippets + "Why alias?" teal sidebar card)
- Lead-in: "In SQL it is possible to **alias** a column (or a table) — simply giving it a **more descriptive name** which can then be used throughout the rest of the query."
- BASIC ALIAS snippet: `SELECT weighted_salary_usd AS salary FROM ...`
- WITH AGGREGATION snippet: `SELECT primary_location AS country, AVG(weighted_salary_usd) AS avg_sal ... GROUP BY country ORDER BY avg_sal DESC`
- Sidebar "Why alias?": easier to read, required for computed columns, reuse in ORDER BY, shortens long expression names

### 40. Exercise: COUNT by country (split code, EXERCISE badge)
- Question: How many schools are in each country?
- Hints: Use COUNT(*) to count schools per group; GROUP BY primary_location; alias as num_schools

### 41. Answer: COUNT by country (split code)
- Full query with `COUNT(*) AS num_schools`, `GROUP BY primary_location`, `ORDER BY num_schools DESC`
- Annotations for each clause

### 42. CASE WHEN intro (full-slide, two-column: explanation text + IF/ELSE pseudocode card on navy)
- Left: "The **business.business_schools** dataset doesn't natively include a 'US vs International' field — but it does include **primary_location**." + "Using **CASE WHEN** logic allows us to **manipulate the data** beyond what natively exists — like creating new derived columns on the fly."
- Right card (navy): "Think of it as IF/ELSE" label + pseudocode with coloured tokens — `CASE WHEN condition / THEN result / ELSE fallback / END AS column_name`

### 43. CASE WHEN: US vs International (split code)
- Question: How many schools are in the US versus everywhere else in the world?
- Code: `CASE WHEN primary_location != 'US' THEN 'International' ELSE primary_location END AS region`
- Annotations: CASE WHEN row-by-row; THEN = value if true; ELSE = fallback; END AS names the new column

### 44. CASE WHEN + GROUP BY (split code, with expected-output box)
- Question: How many schools are in the US versus everywhere else?
- Code: combines CASE WHEN with `GROUP BY region` on the aliased CASE WHEN column
- Annotations: you can GROUP BY the aliased CASE WHEN column; creates US/International split on the fly with no new data
- Expected output: US · 43 schools, International · 57 schools

### 45. Exercise: Pay category (split code, EXERCISE badge, with 3 coloured category hint boxes)
- Question: How many schools fall into each pay category?
- Task: build a CASE WHEN that labels schools — "Elite Pay" (>$200k, amber box), "Strong Pay" ($160k–$200k, blue box), "Lower Pay" (otherwise, grey box)

### 46. Answer: Pay category (split code)
- Full query with multiple WHEN clauses + `COUNT(*) AS num_schools`, `GROUP BY pay_category`, `ORDER BY num_schools DESC`
- Annotations: multiple WHEN clauses evaluated in order (first match wins); ELSE catches everything else; aliased column can be used in GROUP BY

### 47. Wrap-up (title-slide style, dark navy, with 2×3 keyword pill grid)
- Section 05 kicker
- Title: Wrap-up
- Grid: SELECT·FROM (choose tables & columns), WHERE (filter rows), ORDER BY (sort results), GROUP BY (aggregate & pivot), COUNT·AVG·MAX… (summary statistics), AS (alias) (rename columns)
- Logo at bottom

### 48. You can all now… (full-slide, two-column: 4 checklist rows on left + Purple_small.jpg on right)
- Left column: 4 rows with teal check-circle icons
  - Interrogate the data
  - Investigate and challenge hypotheses
  - Check for discrepancies in the data
  - Select and manipulate the relevant variables
- Right column: `assets/Purple_small.jpg`

### 49. Section divider — "What about GenAI?" (section divider, **pink accent** instead of teal, kicker "A note on", teal underline bar)

### 50. What about GenAI? (full-slide, 3 cards in a row with coloured top borders; mix of light + dark)
- Card 1 (grey top border, light): **Always been normal** — Even before GenAI, analysts always used Google & StackOverflow. Literally no one knows all commands by heart — and they never have.
- Card 2 (pink top border, light): **GenAI is not infallible** — It's not uncommon to get responses that just don't work at all. Models are trained to be sycophantic — if you ask something wrong, it may keep giving answers that will never work.
- Card 3 (teal top border, dark navy): **Know the basics first** — If you can write basic SQL yourself, GenAI will make you 10× faster (green). If you only use GenAI, it can make you 10× slower (pink).

### 51. What's next? (full-slide, intro line + 2 course cards with teal / pink top borders)
- Intro: "Keep learning with us"
- Card 1 (teal top border) — Course 01: **Intermediate SQL** / tagline "From comfortable to confident." / You'll learn: JOINs (INNER, LEFT, RIGHT & FULL); Subqueries & Common Table Expressions; Window functions (RANK, LAG, LEAD); Query optimisation with AI / `shared/assets/courseinterest.png` in bottom-right
- Card 2 (pink top border) — Course 02: **Intro to Python for MBAs** / tagline "Automate, analyse, accelerate." / You'll learn: Python fundamentals (syntax & data types); Pandas for data analysis & wrangling; Automating Excel & reporting workflows; Automate your life admin / `shared/assets/courseinterest.png` in bottom-right

### 52. Questions & Feedback (final slide, dark navy, two-column: heading + two QR cards)
- Left: "Questions & Feedback" heading (teal accent on "Feedback") + pink underline + "Thanks for joining!" subtitle
- Right: two white rounded cards side-by-side
  - Feedback QR: pink small-caps label "Feedback" + `assets/feedback-qr.png`
  - LinkedIn QR: teal small-caps label "Let's connect" + `shared/assets/LinkedIn.png`
- Logo at bottom
