# Deck: Python for MBAs · Session 03 — Pandas

**Subtitle**: avidLearning · Workshop (Part 3 of 4)
**Date**: [TODO: add date]

> Third of four 3-hour sessions. Builds on Sessions 01 and 02. Today: the
> DataFrame — selecting, filtering, transforming, aggregating; date handling;
> missing values; using Claude to navigate pandas's vast API. Dataset: full
> Maven Analytics Coffee Shop Sales (~150k rows). Layout-hint conventions
> follow [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "Python for MBAs · Pandas" (title slide, navy bg)
- Kicker: avidLearning · Workshop · Part 3 of 4
- Title: Python / for MBAs (teal accent)
- Subtitle line: Pandas for Data Analysis — Session 03
- Date: [TODO]
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2×3 numbered card grid + dashed break card)
- 01 Recap & today's aim
- 02 Meet pandas
- 03 Selecting & filtering
- (dashed) 10 minute break
- 04 Reshaping & aggregating
- 05 Errors, dates & Claude

### 3. Last time — recap (full-slide, `.bb` list of 6 keyword pills + tying line)
- `def / return` — your own functions
- `built-ins` — len, sum, min, max, sorted
- `list comprehensions` — `[x for x in list if cond]`
- `import` — math, random, datetime, statistics
- `tracebacks` — bottom-up rule
- `two-try rule` — yourself, yourself, then Claude
- Tying line: "Everything you wrote by hand last time, pandas does in **one line**. Today we cash that in."

### 4. Today's aim (full-slide, two stacked quote-style blocks with coloured left borders)
- THE GOAL (teal border): be able to **load, slice, filter, and aggregate** a real dataset — and recognise when to ask Claude for help
- NOT (grey border): memorise pandas's 600+ methods (nobody does — that's what Claude is for)

### 5. Section divider — "Meet pandas" (section divider, teal accent, Section 02)

### 6. What is pandas? (full-slide, two-column: light card + dark card)
- Left (light card): pandas is **the** Python library for working with tabular data. Think Excel sheet, think SQL table — same idea, but you can run any analysis on millions of rows in seconds.
- Right (dark card): It's the **industry standard**. Every data team, every analyst, every Kaggle notebook. Once you can read pandas, you can read 80% of the data code you'll ever see.

### 7. A DataFrame is just a table (full-slide, two-column: explanation + mock DataFrame visual)
- Left: A `DataFrame` is a **table** — rows and columns, with a name on each column. Each column has a type (int, float, str, datetime). The index is a row label — usually just 0, 1, 2…
- Right card (mock DataFrame in `.dt` style):
  - Header: `transaction_id` · `transaction_date` · `store_location` · `product_category` · `unit_price` · `transaction_qty`
  - 5 sample rows from coffee shop data
- Caption: "Read it like an Excel sheet. The whole table is one Python variable — call it `df`."

### 8. Our dataset — Coffee Shop Sales (full-slide, intro line + data table + meta)
- Intro: "We'll use the **Maven Analytics Coffee Shop Sales** dataset — every transaction across 3 stores, 6 months of trading. **149,116 rows.**"
- Sample rows table (`.dt`): 5 rows with columns above
- Meta caption (mono, muted):
  - File: `coffee-shop-sales.csv` · 149,116 rows · 10 columns
  - Stores: Astoria · Hell's Kitchen · Lower Manhattan
  - Date range: Jan 2023 – Jun 2023

### 9. Pandas Building Blocks (full-slide, `.bb` list, 6 items)
- `import pandas as pd` — get pandas, call it `pd`
- `pd.read_csv(...)` — load a file into a DataFrame
- `df.head()` / `.info()` / `.describe()` — peek at the data
- `df[col]` / `df.loc[...]` — select columns and rows
- `df[df[col] > x]` — boolean filter
- `df.groupby(...)` — aggregate by group

### 10. Loading the data (split code)
- Code (left):
  ```
  import pandas as pd
  
  df = pd.read_csv("coffee-shop-sales.csv")
  
  df.head()
  ```
- Question (right): "How do I get a CSV into pandas?"
- Annotations: (1) `import pandas as pd` — the universal alias; (2) `pd.read_csv(path)` reads any CSV — local or URL; (3) `df.head()` shows the first 5 rows — your sanity check

### 11. First look — head, tail, shape (split code)
- Code (left):
  ```
  df.head()      # first 5 rows
  df.tail(3)     # last 3 rows
  
  df.shape       # (149116, 10)  → rows, columns
  len(df)        # 149116
  ```
- Question (right): "What's actually in this thing?"
- Annotations: (1) `.head(n)` / `.tail(n)` — first/last n rows (default 5); (2) `.shape` is a `(rows, cols)` tuple; (3) `len(df)` is just the row count — easier to remember

### 12. First look — info & describe (split code)
- Code (left):
  ```
  df.info()
  # → column names + types + non-null counts
  
  df.describe()
  # → count, mean, std, min, max for each numeric column
  ```
- Question (right): "What are the columns and what's in them?"
- Annotations: (1) `.info()` shows **types** and how many values are present (useful for spotting missing data); (2) `.describe()` is your **30-second summary** of every number; (3) Run these two on every new dataset

### 13. Columns and dtypes (split code)
- Code (left):
  ```
  df.columns
  # → Index(['transaction_id', 'transaction_date', ...])
  
  df.dtypes
  # → transaction_id        int64
  #   transaction_date      object
  #   unit_price            float64
  #   transaction_qty       int64
  ```
- Question (right): "What does each column hold?"
- Annotations: (1) `int64` = whole numbers; (2) `float64` = decimals; (3) `object` = usually text (str); (4) `datetime64` = dates — **we'll convert `transaction_date` to this shortly**

### 14. Section divider — "Selecting & filtering" (section divider, Section 03)

### 15. Selecting one column (split code)
- Code (left):
  ```
  df["unit_price"]            # the whole price column
  df["unit_price"].head()     # first 5
  df["unit_price"].mean()     # average price → 3.38
  ```
- Question (right): "How do I grab one column?"
- Annotations: (1) `df["col_name"]` — square brackets, name in quotes; (2) A single column is a `Series` — like a list with an index; (3) Series have the same methods — `.mean()`, `.sum()`, `.max()`, `.value_counts()`

### 16. Selecting multiple columns (split code)
- Code (left):
  ```
  df[["product_category", "unit_price", "transaction_qty"]].head()
  ```
- Question (right): "How do I select a subset of columns?"
- Annotations: (1) Pass a **list of names** inside `df[…]` — note the **double brackets**; (2) Returns a smaller DataFrame; (3) Order of names in the list = order in the output

### 17. loc vs iloc (full-slide, two-column: explanation + side-by-side examples)
- Left card (teal border): **`.loc[]` — by label**. Use the actual values of the index and column names. Read it as "give me the rows where the index is X."
- Right card (pink border): **`.iloc[]` — by position**. Use integer positions. Read it as "give me row number 5."
- Code (under cards, two snippets):
  - `df.loc[0:4, "unit_price"]`     # rows 0..4 (inclusive) by label
  - `df.iloc[0:5, 3]`               # rows 0..4 by position, column 3
- Footer: "**90% of the time you'll use boolean filters** instead of either — next slide."

### 18. Boolean filtering — the workhorse (split code)
- Code (left):
  ```
  # All transactions in Hell's Kitchen
  hk = df[df["store_location"] == "Hell's Kitchen"]
  
  # All transactions over $10
  big = df[df["transaction_qty"] * df["unit_price"] > 10]
  
  hk.shape    # (49894, 10)
  big.shape   # (12831, 10)
  ```
- Question (right): "How do I keep only the rows I care about?"
- Annotations: (1) Inside `df[…]` write a **condition** — pandas keeps rows where it's True; (2) Reads exactly like SQL's `WHERE`; (3) The condition is itself a Series of True/False — useful to know when things break

### 19. Multiple conditions — the parens trap (split code)
- Code (left):
  ```
  # Hell's Kitchen AND lattes
  q = df[
      (df["store_location"] == "Hell's Kitchen")
      & (df["product_type"] == "Latte")
  ]
  
  # Coffee OR Tea
  q = df[
      (df["product_category"] == "Coffee")
      | (df["product_category"] == "Tea")
  ]
  ```
- Question (right): "How do I combine filters?"
- Annotations: (1) Use **`&`** for AND and **`|`** for OR (not `and` / `or` — pandas is different); (2) **Every condition must be in its own pair of parentheses** — this is the #1 pandas error; (3) `~` means NOT — `~(df["x"] == 5)`

### 20. Exercise: Filter the coffee data (split code, EXERCISE badge)
- Skeleton (left):
  ```
  # Find: all coffee transactions in Astoria
  # where the quantity is at least 2
  
  result = df[
      [?]
  ]
  
  print(result.shape)
  print(result.head())
  ```
- Hints (right): (1) Three conditions: category == "Coffee", store_location == "Astoria", transaction_qty >= 2; (2) Combine with `&`; (3) Each condition in its own parentheses; (4) Expected ~5,800 rows

### 21. value_counts — the free win (split code)
- Code (left):
  ```
  df["product_category"].value_counts()
  # Coffee    58416
  # Tea       45449
  # Bakery    22796
  # …
  
  df["store_location"].value_counts()
  # Hell's Kitchen     49894
  # Astoria            50599
  # Lower Manhattan    48623
  ```
- Question (right): "How many of each? — without writing groupby"
- Annotations: (1) `.value_counts()` is the **fastest way to summarise** a column; (2) Works on any Series; (3) Use `.value_counts(normalize=True)` for percentages

### 22. Break (navy bg, coffee icon, "10 minute break" + "Back soon" subtitle)

### 23. Section divider — "Reshaping & deriving" (section divider, Section 04)
- Subtitle: "Adding columns, vectorised maths, sorting."

### 24. Adding a column (split code)
- Code (left):
  ```
  df["revenue"] = df["transaction_qty"] * df["unit_price"]
  
  df[["product_type", "transaction_qty", "unit_price", "revenue"]].head()
  ```
- Question (right): "How do I add a derived column?"
- Annotations: (1) `df["new_col"] = expression` — that's it; (2) Pandas runs the expression on **every row at once** (more on this next slide); (3) The new column lives on the DataFrame from then on

### 25. Vectorisation — the "aha" moment (full-slide, two-column: wrong way + right way)
- Intro line above: "If you've used Excel, you've already used vectorisation."
- Left card (pink border, **The wrong way** ✗):
  ```
  revenue = []
  for i in range(len(df)):
      r = df["transaction_qty"][i] * df["unit_price"][i]
      revenue.append(r)
  df["revenue"] = revenue
  # ~12 seconds on 149k rows. Don't.
  ```
- Right card (teal border, **The right way** ✓):
  ```
  df["revenue"] = df["transaction_qty"] * df["unit_price"]
  # ~0.05 seconds. 240× faster.
  ```
- Caption: "Pandas does the loop in C, not Python. Multiply two columns directly — never loop unless you have to."

### 26. Sorting (split code)
- Code (left):
  ```
  # Sort one column, descending
  df.sort_values("revenue", ascending=False).head(10)
  
  # Sort by two columns
  df.sort_values(
      ["store_location", "revenue"],
      ascending=[True, False],
  ).head(10)
  ```
- Question (right): "How do I sort the table?"
- Annotations: (1) `.sort_values(col)` sorts ascending by default; (2) `ascending=False` for descending; (3) Pass a **list** to sort by multiple columns with a list of directions; (4) Default sort is non-destructive — assign back if you want it permanent

### 27. Dropping columns (split code)
- Code (left):
  ```
  df = df.drop(columns=["transaction_id"])
  
  # Or pick the ones to keep
  df = df[["transaction_date","store_location","product_category","revenue"]]
  ```
- Question (right): "How do I remove a column?"
- Annotations: (1) `.drop(columns=[…])` removes by name; (2) Sometimes simpler to **list the ones you want** and reassign; (3) Either way — the column you removed is gone from `df`

### 28. Section divider — "Dates & missing values" (continuation; or a smaller transition)

### 29. Parsing dates (split code)
- Code (left):
  ```
  df["transaction_date"] = pd.to_datetime(df["transaction_date"])
  
  df["hour"]    = pd.to_datetime(df["transaction_time"], format="%H:%M:%S").dt.hour
  df["weekday"] = df["transaction_date"].dt.day_name()
  df["month"]   = df["transaction_date"].dt.month_name()
  ```
- Question (right): "How do I work with dates?"
- Annotations: (1) `pd.to_datetime(col)` converts strings to real datetimes; (2) Once converted, `.dt.X` gives you year/month/day/hour/weekday for free; (3) **Always parse dates first** — most date bugs come from forgetting this step

### 30. Missing values (split code)
- Code (left):
  ```
  df.isna().sum()
  # transaction_id     0
  # unit_price         0
  # promo_code         142891   ← lots of missing
  
  # Drop rows where any required column is missing
  df.dropna(subset=["unit_price", "transaction_qty"])
  
  # Or fill with a default
  df["promo_code"] = df["promo_code"].fillna("none")
  ```
- Question (right): "What do I do about empty cells?"
- Annotations: (1) `.isna()` returns True where missing — `.sum()` totals them; (2) `.dropna(subset=[…])` drops rows missing in those columns; (3) `.fillna(x)` fills with a default; (4) Decide per column — sometimes empty means something specific

### 31. Section divider — "GroupBy & aggregate" (section divider, Section 05)
- Subtitle: "The pandas finale — your SQL `GROUP BY` muscle memory."

### 32. groupby — the workhorse (split code)
- Code (left):
  ```
  df.groupby("store_location")["revenue"].sum()
  # Astoria            199824.45
  # Hell's Kitchen     236511.17
  # Lower Manhattan    230057.34
  ```
- Question (right): "What's the daily takings by store?"
- Annotations: (1) `df.groupby("col")` segments rows by unique values; (2) Then pick the column to aggregate, then call `.sum()` / `.mean()` / `.count()`; (3) Result is a Series indexed by group; (4) Same idea as SQL's `GROUP BY`

### 33. Multiple aggregations (split code)
- Code (left):
  ```
  df.groupby("store_location")["revenue"].agg(["sum", "mean", "count"])
  # → table: store_location × [sum, mean, count]
  
  df.groupby("product_category").agg(
      total_revenue=("revenue", "sum"),
      avg_price=("unit_price", "mean"),
      n_transactions=("transaction_id", "count"),
  )
  ```
- Question (right): "How do I get sum + average + count in one go?"
- Annotations: (1) `.agg([…])` runs multiple aggregations at once; (2) Named-tuple form lets you **name the output columns** and pick which input each works on; (3) Result is a DataFrame — you can chain `.sort_values()` straight after

### 34. groupby + filter — the SQL `HAVING` equivalent (split code)
- Code (left):
  ```
  # Top 5 product types by revenue
  top5 = (
      df.groupby("product_type")["revenue"]
        .sum()
        .sort_values(ascending=False)
        .head(5)
  )
  print(top5)
  ```
- Question (right): "What are the top 5 products by revenue?"
- Annotations: (1) Chain methods on multiple lines — wrap in parentheses; (2) groupby → sum → sort → head — read top to bottom; (3) This is the canonical pandas idiom; you'll write it constantly

### 35. Exercise: Busiest hour at Hell's Kitchen (split code, EXERCISE badge)
- Skeleton (left):
  ```
  # Find: hour of day with the highest revenue at Hell's Kitchen
  # Use the `hour` column we created earlier
  
  hk = df[[?]]
  by_hour = hk.groupby([?])[[?]].sum().sort_values([?])
  
  print(by_hour.head(3))
  ```
- Hints (right): (1) Filter to Hell's Kitchen first; (2) groupby `hour`; (3) Aggregate `revenue` with `.sum()`; (4) Sort descending and take `.head(3)`; (5) Expected: morning rush hours dominate

### 36. Exercise: Revenue by weekday (split code, EXERCISE badge)
- Skeleton (left):
  ```
  # Average daily revenue by day of the week
  
  daily = df.groupby([[?], [?]])[[?]].sum().reset_index()
  by_weekday = daily.groupby([?])[[?]].mean().sort_values([?])
  
  print(by_weekday)
  ```
- Hints (right): (1) Group transactions by `transaction_date` + `weekday` to get a per-day total; (2) Then group those totals by weekday and take the mean; (3) Sort descending; (4) Expected: weekends busier than midweek

### 37. Section divider — "Errors & try/except" (section divider continuation, Section 06)

### 38. Pandas errors you'll meet (full-slide, operator table `.ot`)
- Header: Error · What it means · Likely fix
- Rows:
  - `KeyError: 'cust_id'` · Column doesn't exist · Check spelling — `df.columns` shows them all
  - `TypeError` after `.dt.hour` · Column isn't a datetime · You forgot `pd.to_datetime(...)` first
  - `SettingWithCopyWarning` · Pandas isn't sure what you mean · See next slide — usually safe to ignore
  - `ValueError: cannot convert…` · Type mismatch in a filter · Make sure both sides match (str vs int)

### 39. SettingWithCopyWarning — the most-Googled warning in data (full-slide, hero panel + Claude note)
- Hero card (navy): the warning text itself, in mono
- Card below (`.si`/`.st` bullets):
  - 80% of the time it's **harmless** — your code worked
  - 20% of the time you assigned to a copy of the data, not the original
  - The safe fix: use `.loc[...]` instead of chained brackets, or call `.copy()` after a filter
- Closing line (italic, muted): "If it's blocking your work, **paste it into Claude with your code**. It's a warning, not an error."

### 40. try / except — for known-bad cells (split code)
- Code (left):
  ```
  for value in df["unit_price"]:
      try:
          n = float(value)
      except ValueError:
          print(f"Skipping bad value: {value}")
  ```
- Question (right): "What if some values are unparseable?"
- Annotations: (1) `try:` runs the risky code; (2) `except ERROR_TYPE:` catches a specific failure; (3) Always catch a **specific** exception — never a bare `except:`; (4) Most pandas work doesn't need this — but it's there when you need it

### 41. Section divider — "Using Claude with pandas" (section divider, pink accent, Section 07)
- Subtitle: "Pandas has 600+ methods. Claude knows them all. Here's how to ask."

### 42. The two ways Claude helps with pandas (full-slide, 2-card grid)
- Card 1 (teal border): **Method finder** — "I have a DataFrame and I want to do X. What's the pandas method?"
- Card 2 (pink border): **Debugger** — "I got this error / unexpected output. Here's my code and what I expected. What's wrong?"
- Closing line (italic, muted): "Pandas is too big to memorise. The skill is **knowing what to ask** — and recognising the right answer."

### 43. Showing Claude your DataFrame (full-slide, mocked Claude chat panel)
- Mocked chat (light card):
  - User: "Here's the first 3 rows of my DataFrame as a dict: [paste `df.head(3).to_dict()`]. How do I find the average revenue per product category?"
  - Claude: "Use `df.groupby('product_category')['revenue'].mean().sort_values(ascending=False)`. This groups by category, averages revenue, and sorts highest first."
- Caption (italic, muted): "Paste the **shape** of your data, not all 150k rows. `.head(3).to_dict()` gives Claude exactly enough."

### 44. Ask better questions (full-slide, 3-card grid + maxim)
- Intro: "When Claude gives you pandas, **don't stop there** — the follow-up is where you actually learn."
- Card 1 (teal): **"Explain each line"** — ask Claude to comment every method call
- Card 2 (pink): **"Why is this the right shape?"** — ask whether the result is a Series or DataFrame, and why
- Card 3 (teal): **"Is there a more idiomatic way?"** — pandas often has 3 ways to do something; ask for the most readable
- Maxim (centred, italic): "The best Python answers come from asking the best pandas questions."

### 45. Exercise: Ask Claude for a chart-ready summary (split code, EXERCISE badge, 10 min)
- Step 1 (teal card): Paste 3 rows of your DataFrame and ask Claude: "Give me a one-line pandas expression for revenue by `product_category` per `month`, sorted by month."
- Step 2 (pink card): Run it in your notebook. Read the result. Does each row make sense?
- Step 3 (teal card): Ask Claude: "Now reshape this into a table with months as rows and categories as columns." (preview of `pivot` — Session 04 territory)

### 46. Section divider — "Wrap-up" (title-slide style, dark navy, Section 08)

### 47. Summary so far (full-slide, 2×3 keyword pill grid)
- Pill `read_csv / head / info`: Load and peek at any dataset.
- Pill `df[col] / df.loc`: Select columns and rows.
- Pill `df[df[col] > x]`: Filter rows with boolean conditions.
- Pill `to_datetime / .dt`: Parse dates, extract hour/weekday/month.
- Pill `groupby / agg`: Aggregate by group — SQL's GROUP BY in one line.
- Pill `Claude + df.head().to_dict()`: Get unstuck without memorising the API.

### 48. The art-of-the-possible breadcrumb (full-slide, two-column: pandas one-liner + caption)
- Hero line above: "You can already do this:"
- Code card (navy):
  ```
  (df.groupby("product_category")["revenue"]
     .sum()
     .sort_values(ascending=False)
     .to_excel("category_summary.xlsx"))
  ```
- Caption (italic, muted): "Four lines. Your boss gets a sorted Excel summary at any hour, on any data slice. You've automated yesterday's analyst."

### 49. You can all now… (full-slide, two-column: 5 checklist rows on left + image on right)
- Left column: 5 rows with teal check-circle icons
  - Load a real dataset into pandas
  - Inspect, select, and filter rows and columns
  - Add derived columns using vectorised maths
  - Parse dates and handle missing values
  - Aggregate by group and export the result
- Right: Purple_small.jpg (reuse) or Python image — TBD

### 50. Coming up next time — Visualisation & the art of the possible (full-slide, intro line + 2 preview cards)
- Intro: "Final session. We turn the numbers into pictures — and meet the **art of the possible**."
- Card 1 (teal): **Matplotlib, Seaborn, Plotly** — three charting libraries, three flavours
- Card 2 (pink): **Capstone** — build a coffee shop dashboard from scratch in 40 minutes
- Tease (italic, centred): "Plus: where Python takes you next — automation, scraping, ML, APIs."

### 51. Questions & Feedback (final slide, dark navy, two-column: heading + two QR cards)
- Left: heading + subtitle "Thanks — one to go!"
- Right: Feedback QR + LinkedIn QR
- Logo at bottom

---

## Notes for implementation
- Target ~54 slides — the densest deck of the four.
- `.merge` is **skipped** (only mentioned as "what's next" if at all).
- Vectorisation slide is the load-bearing "aha" — make sure the visual contrast is strong.
- Claude section (slides 41-45) is the dedicated AI segment for the whole 4-deck programme.
