# Deck: Python for MBAs · Session 02 — Functions & Standard Library

**Subtitle**: avidLearning · Workshop (Part 2 of 4)
**Date**: [TODO: add date]

> Second of four 3-hour sessions. Builds on Session 01 (variables, types,
> control flow, function teaser). Today: deeper into functions, list
> comprehensions, the standard library, reading errors, and using Claude
> as a debugger. Layout-hint conventions follow [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "Python for MBAs · Functions & Libraries" (title slide, navy bg)
- Kicker: avidLearning · Workshop · Part 2 of 4
- Title: Python / for MBAs (teal accent)
- Subtitle line: Functions & Libraries — Session 02
- Date: [TODO]
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2×3 numbered card grid + dashed break card)
- 01 Recap & today's aim
- 02 Why functions?
- 03 Built-in functions
- (dashed) 10 minute break
- 04 List comprehensions & libraries
- 05 Errors & Claude · Mini-project

### 3. Last time — recap (full-slide, `.bb` list of 6 keyword pills + one-line tying-in)
- `variables` — name → value
- `int / float / str / bool` — the four basic types
- `lists & dicts` — ordered items vs labelled records
- `if / elif / else` — branching
- `for / while` — repetition
- `def` — your first function (one tiny example)
- Tying line below: "Today we turn that one tiny `def` into the workhorse of your Python."

### 4. Today's aim (full-slide, two stacked quote-style blocks with coloured left borders)
- THE GOAL (teal border): write **reusable functions** that wrap your logic — and feel confident **reading errors**, with Claude on standby
- NOT (grey border): memorise every Python built-in or library

### 5. Section divider — "Why functions?" (section divider, teal accent, Section 02)

### 6. The DRY principle (full-slide, two-column: before/after code cards)
- Intro line above: "When you find yourself **pasting the same code** with one small change — it's time for a function."
- Left card (pink border, "Before"): 3 near-identical `print(f"{store} sold {n} cups")` lines for 3 stores
- Right card (teal border, "After"): one `def report(store, n): ...` followed by 3 one-line calls
- Caption below: "DRY — **Don't Repeat Yourself**. Same output, far less code, one place to fix bugs."

### 7. Defining a function — the building blocks (full-slide, `.bb` list, 5 items)
- `def` — the keyword that says "I'm defining a function"
- `name` — what you'll call it later (your choice)
- `(parameters)` — inputs the function expects
- `:` & indent — the body of the function
- `return` — the value sent back to the caller

### 8. Parameters & return (split code)
- Code (left):
  ```
  def revenue(qty, price):
      total = qty * price
      return total
  
  morning = revenue(3, 4.50)   # → 13.5
  evening = revenue(8, 5.95)   # → 47.6
  ```
- Question (right): "How do I take inputs and give back an answer?"
- Annotations: (1) `(qty, price)` are **parameters** — placeholders for inputs; (2) `return total` sends the result back; (3) Call with values — Python plugs them in; (4) Each call is independent

### 9. Named vs positional arguments (split code)
- Code (left):
  ```
  def report(store, product, cups):
      return f"{store} sold {cups} {product}s"
  
  # Positional — order matters
  report("Astoria", "Latte", 312)
  
  # Named — order doesn't matter
  report(cups=312, product="Latte", store="Astoria")
  ```
- Question (right): "Why give arguments names when calling?"
- Annotations: (1) Positional is fine for **2-3 args**; (2) Named (keyword) arguments are clearer when the function has many params; (3) You can mix — positional first, then named; (4) Named arguments make your code self-documenting

### 10. Default arguments (split code)
- Code (left):
  ```
  def revenue(qty, price, discount=0):
      total = qty * price * (1 - discount)
      return total
  
  revenue(10, 4.50)            # → 45.0
  revenue(10, 4.50, discount=0.1)  # → 40.5
  ```
- Question (right): "How do I have an optional input?"
- Annotations: (1) `discount=0` is a **default** — used if caller doesn't pass it; (2) Defaults must come **after** non-default params; (3) Keeps the simple case simple, the flexible case possible

### 11. Docstrings (split code)
- Code (left):
  ```
  def revenue(qty, price, discount=0):
      """Return total revenue after applying a discount.
      
      qty:      number of items sold
      price:    unit price
      discount: 0.1 = 10% off (default 0)
      """
      return qty * price * (1 - discount)
  ```
- Question (right): "How do I leave a note for future-me?"
- Annotations: (1) A **docstring** is a string at the top of a function in triple quotes; (2) Tools like `help(revenue)` will show it; (3) You don't need one for every function — write one when the inputs aren't obvious

### 12. Exercise: Write a discount function (split code, EXERCISE badge)
- Skeleton (left):
  ```
  def final_price(price, vat_pct=20):
      """[?]"""
      vat = [?]
      return [?]
  
  print(final_price(10.00))         # expect 12.0
  print(final_price(10.00, 5))      # expect 10.5
  ```
- Hints (right): (1) `vat = price * vat_pct / 100`; (2) Return `price + vat`; (3) Test both: default VAT (20%) and reduced rate

### 13. Section divider — "Built-in functions" (section divider, Section 03)

### 14. You've been using functions all along (full-slide, one-line message + 4 keyword pills)
- Centred message: "You've used functions in every cell so far. Here's the secret: most of Python's power is in its **built-in** functions."
- 4 pills (mono, on navy): `print()` · `len()` · `type()` · `range()`

### 15. Built-in functions reference (full-slide, operator table `.ot`)
- Header: Function · What it does · Example
- Rows:
  - `len()` · count items · `len(transactions)` → `4`
  - `sum()` · add up a list of numbers · `sum([1, 2, 3])` → `6`
  - `min()` · smallest value · `min([4.50, 3.00, 6.95])` → `3.00`
  - `max()` · largest value · `max([4.50, 3.00, 6.95])` → `6.95`
  - `sorted()` · return sorted list · `sorted([3, 1, 2])` → `[1, 2, 3]`
  - `range()` · sequence of numbers · `range(5)` → `0..4`
  - `enumerate()` · pair index with item · `for i, x in enumerate(list):`
  - `zip()` · pair up two lists · `for p, q in zip(prices, qtys):`

### 16. sum & len in practice (split code)
- Code (left):
  ```
  prices = [4.50, 3.00, 4.95, 2.50, 5.10]
  
  total = sum(prices)             # → 20.05
  avg   = sum(prices) / len(prices)  # → 4.01
  
  print(f"£{total:.2f} across {len(prices)} items, avg £{avg:.2f}")
  ```
- Question (right): "How do I get headline stats without writing a loop?"
- Annotations: (1) `sum()` adds every number in a list; (2) `len()` counts items; (3) Average = sum / len — a one-liner; (4) `:.2f` in an f-string rounds to 2 decimal places

### 17. enumerate — index and item together (split code)
- Code (left):
  ```
  products = ["Latte", "Espresso", "Mocha"]
  
  for i, product in enumerate(products):
      print(f"{i + 1}. {product}")
  # 1. Latte
  # 2. Espresso
  # 3. Mocha
  ```
- Question (right): "How do I get the index *and* the item in a loop?"
- Annotations: (1) `enumerate(list)` yields `(index, item)` pairs; (2) Unpack with `for i, x in …`; (3) Indexes start at 0 — add 1 if you want to count from 1

### 18. zip — walk two lists together (split code)
- Code (left):
  ```
  products = ["Latte", "Espresso", "Mocha"]
  prices   = [4.50, 3.00, 4.95]
  
  for product, price in zip(products, prices):
      print(f"{product}: £{price}")
  ```
- Question (right): "How do I loop two lists in parallel?"
- Annotations: (1) `zip` pairs items at the same index; (2) Stops at the **shorter** of the two; (3) Common pattern when two lists describe the same things

### 19. Exercise: Stats on the daily takings (split code, EXERCISE badge)
- Skeleton (left):
  ```
  takings = [842.50, 1241.20, 998.40, 1567.80, 1102.55]
  
  total   = [?]
  average = [?]
  best    = [?]
  worst   = [?]
  
  print(f"Total: £{total:.2f}")
  print(f"Average: £{average:.2f}")
  print(f"Best day: £{best:.2f}")
  print(f"Worst day: £{worst:.2f}")
  ```
- Hints (right): (1) `sum()` for total; (2) Average = total / `len()`; (3) `max()` and `min()` for best/worst

### 20. Section divider — "List comprehensions" (continuation of Section 03; or kept as part of the same section)

### 21. List comprehensions — the one-liner loop (split code)
- Code (left, before/after):
  ```
  # Before — explicit loop
  prices = [3.00, 4.50, 6.95, 2.50]
  in_pence = []
  for p in prices:
      in_pence.append(p * 100)
  
  # After — list comprehension
  in_pence = [p * 100 for p in prices]
  ```
- Question (right): "How do I express a loop in one line?"
- Annotations: (1) Read it left-to-right: **"for each p in prices, compute p × 100"**; (2) Result is a new list; (3) Once you see this, you'll see it everywhere — Pandas, NumPy, GenAI-generated code

### 22. List comprehension with a filter (split code)
- Code (left):
  ```
  prices = [3.00, 4.50, 6.95, 2.50, 5.10]
  
  expensive = [p for p in prices if p > 4]
  # → [4.50, 6.95, 5.10]
  ```
- Question (right): "How do I filter in a list comprehension?"
- Annotations: (1) Add `if CONDITION` at the end; (2) Only items where the condition is true survive; (3) Same logic as `for + if + append` — just compressed

### 23. Exercise: Discount the cheap items (split code, EXERCISE badge)
- Skeleton (left):
  ```
  prices = [3.00, 4.50, 6.95, 2.50, 5.10]
  
  # Halve every price below £4 — return a new list
  cheap_half = [[?] for p in prices if [?]]
  
  print(cheap_half)
  ```
- Hints (right): (1) The output expression is `p / 2`; (2) The filter is `p < 4`; (3) Expected output: `[1.5, 1.25]`

### 24. Break (navy bg, coffee icon, "10 minute break" + "Back soon" subtitle)

### 25. Section divider — "Python's standard library" (section divider, Section 04)
- Subtitle: "Batteries included — and you only have to know they exist."

### 26. What's a library? (full-slide, two-column: explanation + visual stack)
- Left: A **library** (or "module") is pre-written Python that someone else has packaged up. You use `import` to bring it in, then call its functions. Python ships with dozens of standard libraries — already installed, no setup.
- Right (stacked card visual): mock list of imports —
  - `import math`
  - `import random`
  - `import datetime`
  - `import statistics`
  - `import csv`
  - `import json`
- Caption: "These four are today's focus. The others — for another day."

### 27. import math (split code)
- Code (left):
  ```
  import math
  
  math.sqrt(16)        # → 4.0
  math.pi              # → 3.14159…
  math.ceil(4.2)       # → 5
  math.floor(4.8)      # → 4
  ```
- Question (right): "What's the syntax for using a library?"
- Annotations: (1) `import math` once at the top of the notebook; (2) Then call `math.FUNCTION(...)` — the dot says "from this library"; (3) Tab-complete in Colab will show you everything available

### 28. import random (split code)
- Code (left):
  ```
  import random
  
  random.randint(1, 10)          # → some int between 1 and 10
  random.choice(["A", "B", "C"]) # → "B" (this time)
  random.shuffle(["A","B","C"])  # mixes a list in place
  ```
- Question (right): "When would I ever need random?"
- Annotations: (1) Sampling — pick 5 random transactions from a dataset; (2) Simulation — model 1000 random customer orders; (3) Testing — generate fake data while you build

### 29. import datetime (split code)
- Code (left):
  ```
  from datetime import datetime
  
  now = datetime.now()
  print(now)              # → 2026-05-14 14:32:01.123
  print(now.year)         # → 2026
  print(now.strftime("%A"))  # → "Thursday"
  
  # Parse a string into a datetime
  d = datetime.strptime("2025-04-12", "%Y-%m-%d")
  print(d.month)          # → 4
  ```
- Question (right): "How do I work with dates?"
- Annotations: (1) `from X import Y` imports a specific tool — saves typing; (2) `.now()`, `.year`, `.month` are common; (3) **You'll meet this again in Session 03** — the coffee dataset has dates we'll need to parse

### 30. import statistics (split code)
- Code (left):
  ```
  import statistics as stats
  
  takings = [842.50, 1241.20, 998.40, 1567.80, 1102.55]
  
  stats.mean(takings)     # → 1150.49
  stats.median(takings)   # → 1102.55
  stats.stdev(takings)    # → 273.21
  ```
- Question (right): "What about basic statistics?"
- Annotations: (1) `import X as Y` gives the library a **short alias** (saves typing); (2) `mean / median / stdev` are the common three; (3) For anything heavier — pandas (next session)

### 31. Exercise: Random coffee picker (split code, EXERCISE badge)
- Skeleton (left):
  ```
  import random
  
  menu = ["Latte", "Espresso", "Mocha", "Flat White", "Cappuccino"]
  
  # Pick today's special — at random
  todays_special = [?]
  
  # Pick 3 random options for a flight
  flight = [?]
  
  print(f"Today's special: {todays_special}")
  print(f"Coffee flight: {flight}")
  ```
- Hints (right): (1) `random.choice(menu)` picks one; (2) `random.sample(menu, 3)` picks 3 without repeats; (3) Try running the cell a few times — different each time

### 32. Section divider — "Reading errors" (section divider, Section 05)
- Subtitle: "What Python is actually telling you — and how to ask Claude."

### 33. The shape of a traceback (full-slide, two-column: annotated traceback + reading guide)
- Left card (navy code panel): a real traceback with line numbers highlighted:
  ```
  Traceback (most recent call last):
    File "<cell line 3>", line 3, in <module>
      total = qty + price
  TypeError: unsupported operand type(s) for +: 'int' and 'str'
  ```
- Right (`.si`/`.st` list): The bottom-up rule —
  - **Read the last line first** — that's the actual error
  - **Then look at the line before** — where it happened
  - **Then look at the type** — `TypeError`, `NameError`, `KeyError` tell you what kind of mistake
- Footer: "Tracebacks look scary. They aren't — they always tell you exactly where and why."

### 34. The three errors you'll meet (full-slide, operator table `.ot`)
- Header: Error · What it means · Likely fix
- Rows:
  - `NameError` · Python doesn't know this name · You probably misspelled a variable, or forgot to define it
  - `TypeError` · Wrong type for the operation · Probably mixing str and int — try `int()` or `float()`
  - `KeyError` · Dict doesn't have that key · Check the spelling and capitalisation of the key
  - `IndentationError` · Wrong whitespace · Count your spaces — 4 per level
  - `SyntaxError` · The code isn't valid Python · Usually a missing `:`, `(`, or quote

### 35. Worked example — fixing a NameError (split code)
- Code (left):
  ```
  qty = 5
  price = 4.50
  
  total = qnty * price   # NameError: name 'qnty' is not defined
  
  # Fix: qty, not qnty
  total = qty * price    # → 22.5
  ```
- Question (right): "What does Python actually tell me?"
- Annotations: (1) `NameError: name 'qnty' is not defined` — the name doesn't exist; (2) Look — `qnty` is missing a `u`; (3) Fix the typo, run again

### 36. Using Claude as your debugger (full-slide, mocked Claude chat panel)
- Mocked chat card:
  - User: "I got this error: `TypeError: unsupported operand type(s) for +: 'int' and 'str'`. Here's my code: [paste 4 lines]. What's wrong?"
  - Claude: "On line 3 you're adding `qty` (an integer) to `price`, which is a string because you read it from a CSV. Wrap `price` in `float()`: `total = qty + float(price)`."
- Caption below (italic, muted): "Paste the code, paste the **whole** error, and the fix is usually one message away."

### 37. The two-try rule (revisited) (full-slide, hero card)
- Hero (teal border): **"Try it twice yourself before you ask Claude."**
- Supporting bullets `.si`/`.st`:
  - First try — write the code, run it, see what Python says
  - Second try — read the traceback bottom-up; change one thing; run again
  - Then — paste the code + error + what you expected into Claude
- Closing line: "The error message is Claude-readable. So is the question 'why did this break?' Asking blind isn't."

### 38. Section divider — "Mini-project" (section divider, Section 06)
- Subtitle: "Putting it all together — without pandas, yet."

### 39. The setup — yesterday's coffee shop data (full-slide, intro line + data preview as a list of dicts)
- Intro: "Imagine a tiny slice of yesterday's takings — 8 transactions, as a list of dicts. We'll write a few functions to interrogate it."
- Card (navy code panel) showing:
  ```
  transactions = [
      {"store": "Astoria",   "product": "Latte",     "qty": 2, "price": 4.50},
      {"store": "Astoria",   "product": "Espresso",  "qty": 1, "price": 3.00},
      {"store": "Hell's K",  "product": "Mocha",     "qty": 1, "price": 4.95},
      {"store": "Hell's K",  "product": "Latte",     "qty": 3, "price": 4.50},
      {"store": "Lower M.",  "product": "Tea",       "qty": 4, "price": 2.50},
      {"store": "Lower M.",  "product": "Latte",     "qty": 2, "price": 4.50},
      {"store": "Astoria",   "product": "Mocha",     "qty": 2, "price": 4.95},
      {"store": "Hell's K",  "product": "Tea",       "qty": 1, "price": 2.50},
  ]
  ```

### 40. Mini-project — task 1: total revenue function (split code, EXERCISE badge)
- Skeleton (left):
  ```
  def total_revenue(transactions):
      total = [?]
      for tx in transactions:
          total = total + [?]
      return total
  
  print(total_revenue(transactions))
  ```
- Hints (right): (1) Start `total = 0`; (2) Add `tx["qty"] * tx["price"]` each iteration; (3) Expected output: `73.85`

### 41. Mini-project — task 2: filter by store (split code, EXERCISE badge)
- Skeleton (left):
  ```
  def filter_by_store(transactions, store_name):
      return [[?] for tx in transactions if [?]]
  
  astoria_only = filter_by_store(transactions, "Astoria")
  print(astoria_only)
  print(len(astoria_only))   # expect 3
  ```
- Hints (right): (1) Output expression: just `tx` itself; (2) Filter: `tx["store"] == store_name`; (3) Should be 3 Astoria transactions

### 42. Mini-project — task 3: best-selling product (split code, EXERCISE badge)
- Skeleton (left):
  ```
  def cups_by_product(transactions):
      counts = {}
      for tx in transactions:
          product = tx["product"]
          if product in counts:
              counts[product] = counts[product] + [?]
          else:
              counts[product] = [?]
      return counts
  
  print(cups_by_product(transactions))
  ```
- Hints (right): (1) Both blanks are `tx["qty"]`; (2) Look up the key first — if it's there, add to it; otherwise set it; (3) Expected: `{'Latte': 7, 'Espresso': 1, 'Mocha': 3, 'Tea': 5}`

### 43. The pandas teaser (full-slide, two-column: hand-rolled code (left, faded) + pandas one-liner (right, highlighted))
- Intro line above: "Look at all the code you just wrote to count by product. Next session, pandas does this in **one line**:"
- Left card (faded grey): the full 8-line `cups_by_product` function from above
- Right card (teal highlight): a single line
  ```
  df.groupby("product")["qty"].sum()
  ```
- Caption below: "Same answer, 1/8th the code. That's why we learn pandas next."

### 44. Section divider — "Wrap-up & Claude" (section divider continuation, pink accent, Section 07)

### 45. Summary so far (full-slide, 4 cards in 2×2 grid with Python-keyword pills)
- Pill `def / return`: Wrap logic in a name and reuse it.
- Pill `built-ins`: `len`, `sum`, `min`, `max`, `sorted`, `range`, `enumerate`, `zip` — your daily drivers.
- Pill `list comprehensions`: `[expr for x in list if cond]` — loop + filter in one line.
- Pill `import`: Bring in batteries — `math`, `random`, `datetime`, `statistics`.

### 46. The art-of-the-possible breadcrumb (full-slide, hero card with 5-line code snippet)
- Hero line above: "What you can already do with what you learned today:"
- Code card (navy):
  ```
  import smtplib
  from email.message import EmailMessage
  
  msg = EmailMessage()
  msg["Subject"], msg["To"] = "Daily takings", "boss@cafe.com"
  msg.set_content(f"Total: £{total_revenue(transactions):.2f}")
  smtplib.SMTP("smtp.gmail.com", 587).send_message(msg)
  ```
- Caption (italic, muted): "5 lines. One function. Your boss gets the daily numbers without you opening Excel. We'll build the real version in Session 04."

### 47. You can all now… (full-slide, two-column: 5 checklist rows on left + image on right)
- Left column: 5 rows with teal check-circle icons
  - Write reusable functions with parameters and return values
  - Use Python's built-in functions to summarise data
  - Read and write list comprehensions
  - Import and use standard libraries
  - Read a traceback and ask Claude a sharp debugging question
- Right: Purple_small.jpg (reuse) or a Python image — TBD

### 48. Coming up next time — Pandas (full-slide, intro line + 2 preview cards)
- Intro: "Next week — we leave the list-of-dicts behind and meet **pandas**, the analyst's power tool."
- Card 1 (teal): **DataFrames** — every Excel sheet you've ever seen, but programmable
- Card 2 (pink): **GroupBy + filter + aggregate** — answer business questions in one line
- Tease (italic, centred): "And we'll bring in the **full** 150k-row coffee shop dataset."

### 49. Questions & Feedback (final slide, dark navy, two-column: heading + two QR cards)
- Left: heading + subtitle "Thanks — see you next week!"
- Right: Feedback QR + LinkedIn QR cards
- Logo at bottom

---

## Notes for implementation
- Target ~46 slides. Above outline is 49 numbered items including a stub — final deck will trim/merge.
- No tuple introduction. No `lambda`. No generator expressions.
- `try/except` deferred to Session 03 — by then students have hit errors organically.
