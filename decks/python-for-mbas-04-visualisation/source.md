# Deck: Python for MBAs · Session 04 — Visualisation & The Art of the Possible

**Subtitle**: avidLearning · Workshop (Part 4 of 4)
**Date**: [TODO: add date]

> Final session of the 4-part programme. Builds on Sessions 01–03. Today:
> matplotlib, seaborn, and plotly for visualisation; a guided capstone build;
> then the inspirational "what else can Python do" tour. Closes the programme
> on the "art of the possible" framing. Layout-hint conventions follow
> [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "Python for MBAs · Visualisation" (title slide, navy bg)
- Kicker: avidLearning · Workshop · Part 4 of 4
- Title: Python / for MBAs (teal accent)
- Subtitle line: Visualisation & The Art of the Possible — Session 04
- Date: [TODO]
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2×3 numbered card grid + dashed break card)
- 01 Recap & today's aim
- 02 Matplotlib basics
- 03 Seaborn
- (dashed) 10 minute break
- 04 Plotly & capstone build
- 05 The art of the possible · Wrap-up

### 3. Last time — recap (full-slide, `.bb` list of 6 keyword pills + tying line)
- `read_csv` — load
- `df.head() / .info()` — peek
- `df[df[col] > x]` — filter
- `df["new"] = a * b` — vectorise
- `groupby / agg` — summarise
- `to_excel / to_csv` — export
- Tying line: "Last week we got the numbers out. Today we turn them into **pictures** — and then you take Python wherever you want to go next."

### 4. Today's aim (full-slide, two stacked quote-style blocks with coloured left borders)
- THE GOAL (teal border): build **clear, attractive charts** from a real dataset — and leave with a clear sense of where Python can take you next
- NOT (grey border): become a data viz designer or master every plotting library

### 5. Section divider — "Why visualise?" (section divider, teal accent, Section 02)

### 6. Why visualise? (full-slide, two-column: light card + dark card)
- Left (light card): A table of 12 numbers is hard to read. A chart of 12 numbers tells a story in **half a second**. Visualisation is how you make your analysis **persuasive** in a meeting.
- Right (dark card): MBAs spend half their lives in decks. **Knowing how to make a chart that says one clear thing** — without an analyst — is leverage.

### 7. Picking the right chart (full-slide, `.bb` list, 4 items as decision tree)
- `Bar chart` — Compare **categories** (e.g. revenue by store)
- `Line chart` — Show **change over time** (e.g. daily revenue Jan → Jun)
- `Histogram` — See the **distribution** of a single number (e.g. transaction size)
- `Scatter plot` — Show the **relationship** between two numbers (e.g. price vs quantity)

### 8. Section divider — "Matplotlib basics" (section divider, Section 03)
- Subtitle: "The original Python plotting library. Ugly by default — but everyone uses it."

### 9. Your first chart (split code)
- Code (left):
  ```
  import matplotlib.pyplot as plt
  
  by_store = df.groupby("store_location")["revenue"].sum()
  
  plt.bar(by_store.index, by_store.values)
  plt.title("Revenue by store")
  plt.show()
  ```
- Question (right): "How do I make a chart?"
- Annotations: (1) `import matplotlib.pyplot as plt` — the universal alias; (2) `plt.bar(labels, values)` — bar chart; (3) `plt.show()` displays it in Colab; (4) **One chart per cell** — keeps things simple

### 10. Adding titles, labels, sizing (split code)
- Code (left):
  ```
  plt.figure(figsize=(10, 5))
  plt.bar(by_store.index, by_store.values, color="#2899A4")
  plt.title("Revenue by store · Jan–Jun 2023", fontsize=16)
  plt.xlabel("Store")
  plt.ylabel("Revenue (USD)")
  plt.show()
  ```
- Question (right): "How do I make it not embarrassing?"
- Annotations: (1) `figsize=(w, h)` sets the size — bigger is usually better; (2) `color` accepts hex codes — match your brand; (3) `.title()`, `.xlabel()`, `.ylabel()` — never ship a chart without these

### 11. Line chart — revenue over time (split code)
- Code (left):
  ```
  daily = (
      df.groupby("transaction_date")["revenue"]
        .sum()
        .sort_index()
  )
  
  plt.figure(figsize=(12, 5))
  plt.plot(daily.index, daily.values, color="#2899A4")
  plt.title("Daily revenue · Jan–Jun 2023")
  plt.ylabel("Revenue (USD)")
  plt.show()
  ```
- Question (right): "Is the business growing?"
- Annotations: (1) Use `.sort_index()` so dates plot in order; (2) `plt.plot(x, y)` — same shape as `plt.bar`; (3) Already useful — you can spot weekly cycles and a clear trend

### 12. Histogram — what does a typical transaction look like (split code)
- Code (left):
  ```
  plt.figure(figsize=(10, 5))
  plt.hist(df["revenue"], bins=40, color="#E05FA0")
  plt.title("Distribution of transaction sizes")
  plt.xlabel("Revenue per transaction (USD)")
  plt.ylabel("Count")
  plt.show()
  ```
- Question (right): "What does a 'normal' coffee transaction look like?"
- Annotations: (1) `plt.hist(values, bins=N)` — N is the number of buckets; (2) Use histograms when you want to know **shape, not exact values**; (3) Long-tail distributions are everywhere in business data

### 13. Exercise: Top 10 product types (split code, EXERCISE badge)
- Skeleton (left):
  ```
  # Bar chart: top 10 product types by revenue
  
  top10 = (
      df.groupby("product_type")["revenue"]
        .sum()
        .sort_values(ascending=False)
        .head(10)
  )
  
  plt.figure(figsize=([?], [?]))
  plt.barh([?], [?], color="#2899A4")
  plt.title("[?]")
  plt.xlabel("[?]")
  plt.show()
  ```
- Hints (right): (1) `plt.barh` is horizontal — better for long product names; (2) Fill in `top10.index` and `top10.values`; (3) `figsize=(10, 6)` works well; (4) Don't forget a clear title

### 14. Section divider — "Seaborn" (section divider, pink accent, Section 04)
- Subtitle: "Same plots, fewer keystrokes, defaults that don't embarrass you."

### 15. Why seaborn (full-slide, two-column: text + side-by-side comparison)
- Left: **Seaborn** is built on top of matplotlib. Same plot types, but with smarter defaults, prettier colours, and one-liners for things matplotlib makes you write 5 lines for.
- Right (two stacked cards):
  - Card 1 ("matplotlib"): 4-line `plt.bar(...)` setup with hardcoded colour
  - Card 2 ("seaborn"): 1-line `sns.barplot(data=df, x="store_location", y="revenue")`
- Caption (italic, muted): "When you can use seaborn, use seaborn. Drop back to matplotlib for fine control."

### 16. sns.barplot (split code)
- Code (left):
  ```
  import seaborn as sns
  sns.set_theme(style="whitegrid")
  
  plt.figure(figsize=(10, 5))
  sns.barplot(
      data=df,
      x="store_location",
      y="revenue",
      estimator="sum",
      palette="crest",
  )
  plt.title("Total revenue by store")
  plt.show()
  ```
- Question (right): "What does the seaborn equivalent look like?"
- Annotations: (1) `data=df` — pass the whole DataFrame; (2) `x` and `y` are **column names** (strings); (3) `estimator="sum"` — seaborn defaults to mean; (4) Palettes — try `crest`, `flare`, `mako`

### 17. sns.boxplot — distributions per group (split code)
- Code (left):
  ```
  plt.figure(figsize=(12, 5))
  sns.boxplot(
      data=df,
      x="product_category",
      y="revenue",
      palette="crest",
  )
  plt.title("Transaction size by product category")
  plt.show()
  ```
- Question (right): "Which categories have the biggest *and* most variable transactions?"
- Annotations: (1) Box = middle 50%; line = median; dots = outliers; (2) Tells you **far more** than just the average; (3) Common in finance/ops dashboards

### 18. sns.heatmap — pivot tables, visualised (split code)
- Code (left):
  ```
  pivot = (
      df.assign(weekday=df["transaction_date"].dt.day_name())
        .pivot_table(
            index="weekday",
            columns="hour",
            values="revenue",
            aggfunc="sum",
        )
  )
  
  plt.figure(figsize=(14, 6))
  sns.heatmap(pivot, cmap="crest", linewidths=0.5)
  plt.title("Revenue heatmap — weekday × hour")
  plt.show()
  ```
- Question (right): "When are people actually buying coffee?"
- Annotations: (1) `pivot_table` reshapes the data — weekday on rows, hour on columns; (2) `sns.heatmap(pivot)` colours by value; (3) The morning rush jumps out instantly — that's the power of viz

### 19. Exercise: Seaborn the daily takings (split code, EXERCISE badge)
- Skeleton (left):
  ```
  # Average daily revenue by weekday — as a seaborn barplot
  
  daily = (
      df.groupby([[?], [?]])["revenue"]
        .sum()
        .reset_index()
  )
  
  plt.figure(figsize=(10, 5))
  sns.barplot(
      data=daily,
      x=[?],
      y=[?],
      estimator="mean",
      order=["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"],
  )
  plt.title("Average daily revenue by weekday")
  plt.show()
  ```
- Hints (right): (1) Group by `transaction_date` AND `weekday` to get a per-day total; (2) `x="weekday"`, `y="revenue"`; (3) `order=` forces Mon→Sun on the x-axis (otherwise seaborn alphabetises)

### 20. Break (navy bg, coffee icon, "10 minute break" + "Back soon" subtitle)

### 21. Section divider — "Plotly — interactive charts" (section divider, Section 05)
- Subtitle: "The 'wow' moment."

### 22. Plotly Express (split code)
- Code (left):
  ```
  import plotly.express as px
  
  daily = (
      df.groupby(["transaction_date","store_location"])["revenue"]
        .sum()
        .reset_index()
  )
  
  fig = px.line(
      daily,
      x="transaction_date",
      y="revenue",
      color="store_location",
      title="Daily revenue by store",
  )
  fig.show()
  ```
- Question (right): "What if I want the user to hover and zoom?"
- Annotations: (1) `plotly.express` — same family as seaborn (one-liners over a DataFrame); (2) `color=` automatically separates lines per category; (3) Hover, zoom, toggle legend — all free; (4) Great for dashboards and stakeholder share

### 23. Section divider — "Capstone — Coffee Shop Dashboard" (section divider, Section 06, pink accent)
- Subtitle: "30 minutes. 5 charts. One story."

### 24. Capstone — the brief (full-slide, 5-card grid: 5 chart targets)
- Intro: "Your job: build five charts that tell the story of these three coffee shops to the CEO. Open a fresh cell for each. Claude is your safety net."
- Card 1 (teal): **Headline number** — total revenue, in a styled text box
- Card 2 (pink): **Store comparison** — revenue per store (bar)
- Card 3 (teal): **Time trend** — daily revenue, all stores (line)
- Card 4 (pink): **Top products** — revenue by top 10 product types (horizontal bar)
- Card 5 (teal): **When are we busy?** — weekday × hour heatmap

### 25. Capstone — chart 1: total revenue (split code, with answer)
- Code (left):
  ```
  total = df["revenue"].sum()
  print(f"Total revenue: ${total:,.2f}")
  # → Total revenue: $666,392.96
  ```
- Annotations: (1) `:,` formats with thousands separators; (2) `.2f` rounds to 2 decimals; (3) Set the stage with a single, well-formatted number

### 26. Capstone — chart 2: store comparison (split code, with answer)
- Code (left):
  ```
  by_store = df.groupby("store_location")["revenue"].sum().sort_values()
  
  plt.figure(figsize=(8, 4))
  plt.barh(by_store.index, by_store.values, color="#2899A4")
  plt.title("Revenue by store")
  plt.xlabel("Revenue (USD)")
  plt.show()
  ```
- Annotations: (1) `.sort_values()` so the bars order largest at top; (2) `plt.barh` = horizontal; (3) Brand colour applied

### 27. Capstone — chart 3: daily trend (split code, with answer)
- Code (left):
  ```
  daily = df.groupby("transaction_date")["revenue"].sum().sort_index()
  
  plt.figure(figsize=(12, 4))
  plt.plot(daily.index, daily.values, color="#2899A4")
  plt.title("Daily revenue · Jan–Jun 2023")
  plt.ylabel("Revenue (USD)")
  plt.show()
  ```
- Annotations: (1) Spot the upward trend across months; (2) Wider `figsize` for time series; (3) Try adding a 7-day rolling average — `daily.rolling(7).mean()` — as a follow-up

### 28. Capstone — chart 4: top product types (split code, with answer)
- Code (left):
  ```
  top10 = (
      df.groupby("product_type")["revenue"]
        .sum()
        .sort_values()
        .tail(10)
  )
  
  plt.figure(figsize=(10, 6))
  plt.barh(top10.index, top10.values, color="#E05FA0")
  plt.title("Top 10 product types by revenue")
  plt.show()
  ```
- Annotations: (1) `.sort_values()` ascending + `.tail(10)` gives smallest-to-largest in the right order for `.barh`; (2) Switch to pink for visual variety

### 29. Capstone — chart 5: when are we busy (split code, with answer)
- Code (left):
  ```
  df["weekday"] = df["transaction_date"].dt.day_name()
  df["hour"]    = pd.to_datetime(df["transaction_time"]).dt.hour
  
  pivot = df.pivot_table(
      index="weekday", columns="hour",
      values="revenue", aggfunc="sum",
  ).reindex([
      "Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"
  ])
  
  plt.figure(figsize=(14, 5))
  sns.heatmap(pivot, cmap="crest", linewidths=0.5)
  plt.title("Revenue heatmap — weekday × hour")
  plt.show()
  ```
- Annotations: (1) Build the pivot, then reindex weekdays in calendar order; (2) Heatmap visualises a 2D summary in one glance; (3) Add this to your slide and the story tells itself

### 30. Capstone — the takeaway (full-slide, 3-card grid + maxim)
- Intro: "Five cells. One narrative. Same dataset you couldn't even read four weeks ago."
- Card 1 (teal): **Total revenue: $666k** across 3 stores, 6 months
- Card 2 (pink): **Hell's Kitchen leads**, but barely — all three stores within 15%
- Card 3 (teal): **Mornings 7–10am** are when this business is made
- Maxim (italic, centred): "This is what 'data fluency' looks like — a story you built yourself."

### 31. Section divider — "The art of the possible" (section divider, pink accent, Section 07)
- Subtitle: "What else can you do with Python?"

### 32. Possibility — automate an Excel workflow (split code)
- Code (left):
  ```
  import pandas as pd
  
  df = pd.read_csv("monthly-sales.csv")
  summary = df.groupby("region")["revenue"].sum()
  summary.to_excel("region_summary.xlsx")
  ```
- Question (right): "What was an hour in Excel?"
- Annotations: (1) Three lines; (2) Run it on a schedule — your boss gets the summary every Monday at 8am; (3) Multiply by every recurring report you currently do by hand

### 33. Possibility — scrape a webpage (split code)
- Code (left):
  ```
  import pandas as pd
  
  # Read all tables from any Wikipedia page
  tables = pd.read_html(
      "https://en.wikipedia.org/wiki/List_of_S%26P_500_companies"
  )
  sp500 = tables[0]
  print(sp500.head())
  ```
- Question (right): "What if I want data from a website?"
- Annotations: (1) `pd.read_html(url)` grabs every table from a page; (2) One line; (3) Combine with pandas + matplotlib — instant report on any public data

### 34. Possibility — call an API (split code)
- Code (left):
  ```
  import requests
  
  r = requests.get("https://api.exchangerate.host/latest?base=GBP")
  rates = r.json()["rates"]
  
  print(f"1 GBP = {rates['USD']} USD")
  print(f"1 GBP = {rates['EUR']} EUR")
  ```
- Question (right): "What if I want live data?"
- Annotations: (1) `requests.get(url)` fetches anything HTTP; (2) `.json()` parses the response; (3) Use this to pull from Stripe, HubSpot, your CRM, Slack — any API your business uses

### 35. Possibility — fit a model (split code)
- Code (left):
  ```
  from sklearn.linear_model import LinearRegression
  
  X = df[["unit_price", "transaction_qty"]]
  y = df["revenue"]
  
  model = LinearRegression().fit(X, y)
  print(model.coef_, model.intercept_)
  ```
- Question (right): "What if I want to predict?"
- Annotations: (1) `scikit-learn` is the Python ML library; (2) Fit a model in 3 lines; (3) Replace `LinearRegression` with any of 50+ algorithms — the API is identical

### 36. Possibility — Python + GenAI together (split code)
- Code (left):
  ```
  import anthropic
  
  client = anthropic.Anthropic()  # uses your API key
  
  msg = client.messages.create(
      model="claude-opus-4-7",
      max_tokens=200,
      messages=[{"role": "user", "content": f"Summarise this in one line: {df.head().to_dict()}"}],
  )
  print(msg.content[0].text)
  ```
- Question (right): "Can I call Claude from Python?"
- Annotations: (1) `pip install anthropic` once; (2) Claude reads your DataFrame and writes prose; (3) Imagine a script that runs nightly, summarises yesterday's data, and emails the result; (4) **This is the multiplier** — Python gives Claude eyes and hands

### 37. Section divider — "Where to next" (section divider, Section 08)

### 38. Where to go from here (full-slide, intro line + 2 course cards)
- Intro: "Keep learning with us:"
- Card 1 (teal top border) — **Coming soon: Python for Automation** — "Make Python do your admin." You'll learn: scheduled scripts, Excel automation, email & Slack notifications, scraping & APIs at scale, working with files at scale.
- Card 2 (pink top border) — **Recommended further reading**: free Kaggle courses (Python, Pandas, Data Viz); the official pandas tutorials; Python Crash Course (book); "Python for Data Analysis" by Wes McKinney (creator of pandas).

### 39. Section divider — "A note on GenAI" (section divider, pink accent, Section 09)
- Subtitle: "The art of the possible — amplified."

### 40. GenAI and the art of the possible (full-slide, hero headline + 2-card split)
- Hero line (centred, 52px): "Python is what lets you see **the art of the possible**. GenAI is what makes it **happen**."
- 2-card split:
  - Card 1 (teal top border, light): **YOU CAN SEE IT** — "With Python literacy, you know what's possible — automation, scraping, ML, API mash-ups — and you can ask Claude to build it." `.si`/`.st` bullets: "You see the opportunity" / "You ask the right question" / "You judge the answer"
  - Card 2 (navy, pink top border): **WITHOUT IT** — "Someone who's never written a line of Python doesn't even know what to ask. They wait for IT to build a script they can't read." `.si`/`.st` bullets: "Opportunities go un-asked" / "AI output goes un-checked" / "Excel hours go un-saved"
- Footer line (small, italic, muted): "Python literacy is the **multiplier** on AI fluency — not a substitute for it."

### 41. Section divider — "Wrap-up" (title-slide style, dark navy, Section 10)

### 42. The 4-session arc (full-slide, 4-card horizontal grid with checkmarks)
- Intro: "Look at what you've done in 12 hours:"
- Card 1 (teal, checkmark): **01 Foundations** — variables, loops, your first function
- Card 2 (teal, checkmark): **02 Functions & libraries** — reusable code, errors, the standard library
- Card 3 (teal, checkmark): **03 Pandas** — real data analysis, GroupBy, your boss's monthly report
- Card 4 (pink, checkmark): **04 Visualisation** — a dashboard from scratch, plus the road ahead

### 43. You can all now… (full-slide, two-column: 6 checklist rows on left + image on right)
- Left column: 6 rows with teal check-circle icons
  - Open a Colab notebook and run Python
  - Wrangle real data with pandas
  - Build charts that tell a story
  - Read and verify Claude's Python output
  - Spot when Python is the right tool
  - Take any of this further on your own
- Right: Purple_small.jpg (reuse) — TBD asset

### 44. Final word (full-slide, hero card with closing maxim)
- Hero card (teal border):
  > "You came in not knowing Python. You're leaving able to see, ask for, and verify what Python and Claude can do for your work.
  >
  > That's the art of the possible."
- Below (muted, small caps): "Thank you · avidLearning"

### 45. Questions & Feedback (final slide, dark navy, two-column: heading + two QR cards)
- Left: heading "Questions & Feedback" (teal accent on "Feedback") + pink underline + "Thanks for completing the programme!" subtitle
- Right: Feedback QR + LinkedIn QR cards
- Logo at bottom

---

## Notes for implementation
- Target ~48 slides — capstone section earns its airtime in **live coding**, not slide count.
- Capstone slides 25-29 show working code so the room has a fallback if they fall behind.
- The "art of the possible" section is the closing arc — keep each possibility slide to ~5 lines of code that *do something*.
- The GenAI closing slide is the rhyme of sql-for-mbas slide 50, but reframed around "the art of the possible" (per user feedback on plan).
- Recommend follow-on course: **Python for Automation only** — no other teases.
