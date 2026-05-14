# Deck: Python for MBAs · Session 01 — Foundations

**Subtitle**: avidLearning · Workshop (Part 1 of 4)
**Date**: [TODO: add date]

> First of four 3-hour sessions in the Python for MBAs programme. Starts from
> zero Python knowledge; ends with students writing useful loops over real data
> in a Colab notebook. Runtime: Google Colab. Dataset: Maven Analytics Coffee
> Shop Sales (~150k rows). Layout-hint conventions follow [../../CLAUDE.md](../../CLAUDE.md).

## Slides

### 1. Title — "Python for MBAs · Foundations" (title slide, navy bg)
- Kicker: avidLearning · Workshop · Part 1 of 4
- Title: Python / for MBAs (teal accent on "for MBAs")
- Subtitle line: Foundations — Session 01
- Date: [TODO]
- avidLearning logo at bottom

### 2. Agenda (full-slide, 2×3 numbered card grid + dashed break card)
- 01 Intro & expectations
- 02 What is Python?
- 03 Variables & data types
- (dashed) 10 minute break
- 04 Collections & control flow
- 05 Functions & Claude · Wrap-up

### 3. Workshop Expectations (full-slide, 3 cards with teal top borders)
- Cameras on — "If at all possible"
- Double-screen works best — "Slides on one screen, Colab on the other"
- Ask questions — "Just come off mute and shout out"

### 4. Who am I? (full-slide, 3 horizontal rows with teal numerals + divider + company logos)
- 01 Ex-data scientist — >2 years at Deliveroo (`shared/assets/deliveroo.png`)
- 02 Ex-consultant — >4 years at Strategy& (`shared/assets/strategy.png`) — data and analytics specialty
- 03 Experienced instructor — >5 years teaching analytics

### 5. Today's aim (full-slide, two stacked quote-style blocks with coloured left borders)
- THE GOAL (teal border): become **comfortable** writing simple Python in a notebook — and confident enough to **read** what Claude gives you
- NOT (grey border): to become a software engineer or memorise the entire language

### 6. The programme — 4 sessions (full-slide, 4-card horizontal grid)
- Intro line: "Today is the first of four 3-hour sessions. Here's where we're going:"
- Card 1 (teal): **01 Foundations** — variables, loops, your first function (TODAY)
- Card 2 (teal): **02 Functions & libraries** — reusable code, errors, the standard library
- Card 3 (teal): **03 Pandas** — data analysis at scale
- Card 4 (pink): **04 Visualisation** — charts, dashboards & the art of the possible

### 7. Section divider — "What is Python?" (section divider, teal accent, Section 02)

### 8. What is Python? (full-slide, two-column: light card + dark card)
- Left (light card): Python is a **general-purpose programming language**. We write instructions in plain text, the computer runs them. No compiling, no setup magic.
- Right (dark card): Python is **the lingua franca of data**. Almost every data team, ML team, and analytics function uses it. If you ever want to peek inside what an analyst does — this is the language they're typing.

### 9. Why do you care? (full-slide, intro line + 4 cards in 2×2 grid, alternating teal/pink left borders)
- Intro: "Python doesn't make you a programmer. It makes you **fluent in what your team is doing** — and unlocks what's possible."
- More leverage — Automate the spreadsheet drudgery that eats your week.
- Less reliant on analysts — Self-serve a 'quick look' instead of waiting for someone's queue.
- Sharper with GenAI — Read, run, and verify what Claude writes for you.
- The art of the possible — See what data, automation, and AI can actually do — beyond Excel's ceiling.

### 10. But can't I just use Excel? (full-slide, two-column comparison: Excel card light + Python card dark)
- Excel (light card): ✗ Single user, single laptop; ✗ Manual every time; ✗ Limited charting & no real automation; ✓ Good for ad-hoc small data
- Python (dark card): ✓ Runs the same analysis on **any size dataset**; ✓ **Automatable** — same code, run on a schedule; ✓ **Thousands of libraries** for stats, ML, viz, APIs, scraping; ✓ Pairs perfectly with **GenAI**

### 11. Section divider — "Getting set up" (section divider, Section 03 placeholder — actually Section 03 in numbering — keep as part of Section 02 of agenda)
- Actually: Continue under Section 02 of the agenda. Use a smaller setup transition rather than a full divider.
- (Implementation note: drop this and treat the Colab/notebook intro as continuation of "What is Python?")

### 11. Where we'll write Python — Google Colab (full-slide, terminal-window card with URL + steps)
- Intro: "We're using **Google Colab** — Python running in your browser, no install."
- URL card (mac-style window chrome): https://colab.research.google.com
- Steps below the card: (1) Sign in with any Google account · (2) File → New notebook · (3) Type code into a cell · (4) Press **Shift+Enter** to run

### 12. What's a notebook? (full-slide, two-column: explanation text + mock notebook screenshot/diagram on right)
- Left: A Colab notebook is a stack of **cells**. Some hold code, some hold notes. You run each cell and the output appears underneath — like a conversation with the computer.
- Right card: mock notebook with two cells — Cell 1 `2 + 2` → output `4`; Cell 2 `print("Hello, MBAs")` → output `Hello, MBAs`. Caption: "Type → Shift+Enter → output."

### 13. Section divider — "Variables & data types" (section divider, Section 03)

### 14. Python Building Blocks (full-slide, `.bb` list, 5 items)
- **variable** — A name that holds a value
- **type** — Whether the value is text, a number, true/false, or a list
- **operator** — What we do with values (+, -, ==, in, etc.)
- **statement** — A single instruction the computer runs
- **comment** — A note for humans (starts with `#`), ignored by Python

### 15. Variables (split code)
- Code (left):
  ```
  store_name = "Astoria"
  daily_revenue = 1842.50
  is_open = True
  ```
- Question (right): "How do I save a value for later?"
- Annotations: (1) `=` means **assign** — read it as "becomes"; (2) The **name** on the left is yours to choose; (3) The **value** on the right can be text, a number, True/False, or anything else

### 16. Data types (full-slide, operator table `.ot`)
- Header: Type · Example · What it's for
- Rows:
  - `int` · `7` · whole numbers
  - `float` · `4.95` · decimals (prices, percentages)
  - `str` · `"Latte"` · text in quotes
  - `bool` · `True` / `False` · yes/no flags
  - `list` · `["A","B","C"]` · ordered collection (covered next section)
  - `dict` · `{"city": "London"}` · key-value pairs (covered next section)
- Footer: `type(x)` tells you what type a value is — useful when Python complains

### 17. Type conversion (split code)
- Code (left):
  ```
  price = "4.95"          # str
  price_num = float(price) # → 4.95
  qty = 3
  total = price_num * qty  # → 14.85
  ```
- Question (right): "Why does adding `"4.95"` to a number fail?"
- Annotations: (1) Numbers as **text** can't be added — Python won't guess; (2) `int(x)`, `float(x)`, `str(x)` convert between types; (3) Mixing types is the #1 beginner error

### 18. f-strings — putting values into text (split code)
- Code (left):
  ```
  store = "Astoria"
  cups = 312
  print(f"{store} sold {cups} cups today")
  # Astoria sold 312 cups today
  ```
- Question (right): "How do I print a sentence with values in it?"
- Annotations: (1) An **f-string** starts with `f"..."`; (2) Anything in `{...}` gets replaced with the value; (3) Use these for any output you'd want a human to read

### 19. Exercise: Your first variables (split code, EXERCISE badge)
- Question: "Create three variables and print a sentence using them."
- Skeleton (left):
  ```
  product = "[?]"
  unit_price = [?]
  qty_sold = [?]
  total = [?]
  print(f"We sold {qty_sold} {product}s for £{total}")
  ```
- Hints (right): (1) Pick a coffee product (e.g. "latte"); (2) Set a price and quantity; (3) Multiply to get the total; (4) Run with Shift+Enter

### 20. Indentation matters (full-slide, two-column: explanation + before/after code cards)
- Left: Python is **whitespace-sensitive** — indentation defines which lines belong inside `if`, `for`, or `def`. No curly braces. **4 spaces** per level is the standard.
- Right (two stacked cards — Good ✓ and Bad ✗):
  - Good (teal border):
    ```
    if cups > 100:
        print("Busy day")
    ```
  - Bad (pink border):
    ```
    if cups > 100:
    print("Busy day")   # IndentationError
    ```
- Footer: Colab auto-indents — let it. If you get `IndentationError`, count your spaces.

### 21. Operators reference (full-slide, operator table `.ot`)
- Header: Operator · Meaning · Example
- Rows:
  - `+ - * /` · arithmetic · `price * qty`
  - `==` · equal to · `store == "Astoria"`
  - `!=` · not equal · `category != "Tea"`
  - `>` `<` `>=` `<=` · comparison · `qty >= 10`
  - `and` · both must be true · `qty > 5 and price < 10`
  - `or` · either must be true · `city == "LDN" or city == "NYC"`
  - `in` · membership · `"Latte" in product_list`

### 22. Section divider — "Collections & control flow" (section divider, Section 04 — placed AFTER the break in numbering)

### NOTE — Section 04 collections section comes BEFORE the break per the design rule (break after Collections). Renumber accordingly in the implementation. The next slides are still part of "variables/types and now collections."

### 23. Lists (split code)
- Code (left):
  ```
  products = ["Latte", "Espresso", "Mocha", "Cappuccino"]
  print(products[0])      # → Latte
  print(products[-1])     # → Cappuccino
  print(len(products))    # → 4
  products.append("Flat White")
  ```
- Question (right): "How do I hold a list of things?"
- Annotations: (1) Use **square brackets** with comma-separated values; (2) Index starts at **0** — `[0]` is the first item; (3) `[-1]` is a shortcut for the last item; (4) `len(list)` returns the count; (5) `.append(x)` adds to the end

### 24. List slicing (split code)
- Code (left):
  ```
  products = ["Latte","Espresso","Mocha","Cappuccino","Flat White"]
  products[0:3]      # → first 3
  products[-2:]      # → last 2
  ```
- Question (right): "How do I grab a chunk of a list?"
- Annotations: (1) `[start:stop]` — stop is **exclusive**; (2) Empty start = "from the beginning"; (3) Negative numbers count from the end

### 25. Dictionaries — the workhorse (split code)
- Code (left):
  ```
  store = {
      "name": "Astoria",
      "city": "New York",
      "open": True,
      "daily_cups": 312,
  }
  print(store["name"])     # → Astoria
  print(store["daily_cups"]) # → 312
  store["manager"] = "Sam"
  ```
- Question (right): "How do I hold labelled information?"
- Annotations: (1) A **dict** is a collection of **key → value** pairs; (2) Look up with `dict["key"]`; (3) Add a new pair with `dict["new_key"] = value`; (4) Far more useful than lists for real-world records

### 26. Exercise: Build a coffee dictionary (split code, EXERCISE badge)
- Skeleton (left):
  ```
  drink = {
      "name": "[?]",
      "price": [?],
      "category": "[?]",
      "in_stock": [?],
  }
  print(f"{drink['name']} costs £{drink['price']}")
  ```
- Hints (right): (1) Fill in any coffee product; (2) Use a float for the price; (3) Use True/False for in_stock; (4) Try changing the print to show category instead

### 27. Lists of dicts — modelling real data (split code)
- Code (left):
  ```
  transactions = [
      {"store": "Astoria",  "product": "Latte",     "qty": 2, "price": 4.50},
      {"store": "Astoria",  "product": "Espresso",  "qty": 1, "price": 3.00},
      {"store": "Hell's K", "product": "Mocha",     "qty": 1, "price": 4.95},
  ]
  print(transactions[0]["product"])  # → Latte
  ```
- Question (right): "How do I represent a table of transactions?"
- Annotations: (1) A list of dicts ≈ a table — each dict is a **row**, each key is a **column**; (2) This is **exactly** how pandas thinks about data internally; (3) Get row 0's product with `transactions[0]["product"]`

### 28. Break (navy bg, coffee icon, "10 minute break" + "Back soon" subtitle)

### 29. Section divider — "Control flow" (section divider, Section 04)
- Subtitle: "Making the computer choose, and making it repeat."

### 30. Comparison & logic (full-slide, operator table `.ot`)
- Header: Operator · Question it asks · Example
- Rows:
  - `==` · "are these equal?" · `category == "Coffee"`
  - `!=` · "are these different?" · `store != "Astoria"`
  - `>` `<` · numeric comparison · `price > 5`
  - `and` · "both true?" · `qty > 0 and in_stock`
  - `or` · "either true?" · `city == "NYC" or city == "LDN"`
  - `not` · "flip it" · `not in_stock`

### 31. if / elif / else (split code)
- Code (left):
  ```
  price = 4.95
  if price > 6:
      label = "Premium"
  elif price > 3:
      label = "Standard"
  else:
      label = "Cheap"
  print(label)   # → Standard
  ```
- Question (right): "How does the computer choose a path?"
- Annotations: (1) `if` checks the first condition; (2) `elif` (else-if) checks the next, only if previous were false; (3) `else` catches everything left; (4) Mind the **colons** and **indentation**

### 32. Exercise: Pay category (split code, EXERCISE badge, 3 coloured hint boxes)
- Question: "Label a transaction by its size."
- Skeleton (left):
  ```
  total = qty * price
  if total > [?]:
      size = "[?]"
  elif total > [?]:
      size = "[?]"
  else:
      size = "[?]"
  print(size)
  ```
- Coloured hint boxes (right):
  - Amber: **"Large"** if total > 20
  - Blue: **"Medium"** if total > 5
  - Grey: **"Small"** otherwise

### 33. For loops — repeating yourself (split code)
- Code (left):
  ```
  products = ["Latte", "Espresso", "Mocha"]
  for product in products:
      print(f"Today's special: {product}")
  ```
- Question (right): "How do I do something for every item in a list?"
- Annotations: (1) `for X in LIST:` walks through each item; (2) `X` is a new variable name **you choose** — it holds the current item; (3) Indent the body — that's what's inside the loop; (4) Print runs **once per item**

### 34. Looping with range (split code)
- Code (left):
  ```
  for i in range(5):
      print(i)
  # → 0, 1, 2, 3, 4
  
  for i in range(1, 6):
      print(i)
  # → 1, 2, 3, 4, 5
  ```
- Question (right): "How do I loop a specific number of times?"
- Annotations: (1) `range(n)` gives you 0 to n-1; (2) `range(a, b)` gives you a to b-1; (3) Stop is **exclusive** — same rule as list slicing

### 35. Looping over a dict (split code)
- Code (left):
  ```
  store = {"name": "Astoria", "city": "NYC", "cups": 312}
  
  for key, value in store.items():
      print(f"{key}: {value}")
  # name: Astoria
  # city: NYC
  # cups: 312
  ```
- Question (right): "How do I walk through a dictionary?"
- Annotations: (1) `.items()` gives you key/value pairs; (2) `for key, value in …` unpacks them in one step; (3) Use this to inspect any dict

### 36. Loop + if (split code)
- Code (left):
  ```
  prices = [3.00, 4.50, 6.95, 2.50, 5.10]
  expensive = []
  
  for price in prices:
      if price > 5:
          expensive.append(price)
  
  print(expensive)   # → [6.95, 5.10]
  ```
- Question (right): "How do I filter a list?"
- Annotations: (1) Start with an **empty list** to collect results; (2) Loop over prices; (3) If the condition is true, `.append()` it; (4) This is the same idea as SQL's `WHERE` — now you've written it from scratch

### 37. Exercise: Filter the transactions (split code, EXERCISE badge)
- Skeleton (left):
  ```
  transactions = [
      {"product": "Latte",    "qty": 2, "price": 4.50},
      {"product": "Espresso", "qty": 1, "price": 3.00},
      {"product": "Mocha",    "qty": 1, "price": 4.95},
      {"product": "Tea",      "qty": 3, "price": 2.50},
  ]
  
  big_orders = []
  for tx in transactions:
      total = [?]
      if [?]:
          big_orders.append(tx)
  
  print(big_orders)
  ```
- Hints (right): (1) `total = tx["qty"] * tx["price"]`; (2) Keep orders where total > 7; (3) Run and check — you should see 2 orders

### 38. Answer: Filter the transactions (split code)
- Full code with `total = tx["qty"] * tx["price"]` and `if total > 7:`
- Annotations: (1) Multiply qty by price for each row; (2) `if total > 7:` keeps only big ones; (3) Print the result — Python returned the matching dictionaries

### 39. While loops (briefly) (split code)
- Code (left):
  ```
  cups = 0
  while cups < 5:
      cups = cups + 1
      print(f"Pouring cup {cups}")
  ```
- Question (right): "What if I want to loop *until* something is true?"
- Annotations: (1) `while CONDITION:` keeps repeating until the condition is false; (2) **Must** change the variable inside, or you loop forever; (3) Use `for` 90% of the time — `while` only when you don't know how many iterations in advance

### 40. Summary so far (full-slide, 4 cards in 2×2 grid with Python-keyword pills)
- Pill: `variables` — Names that hold values. Types: int, float, str, bool.
- Pill: `lists & dicts` — Lists are ordered; dicts hold key→value pairs.
- Pill: `if / elif / else` — Choose a path based on a condition.
- Pill: `for loops` — Do something for every item.

### 41. Section divider — "Functions & Claude" (section divider, Section 05)

### 42. Functions — a name for some code (split code)
- Code (left):
  ```
  def total_for(qty, price):
      return qty * price
  
  print(total_for(3, 4.50))   # → 13.5
  print(total_for(1, 6.95))   # → 6.95
  ```
- Question (right): "How do I name a chunk of logic and reuse it?"
- Annotations: (1) `def NAME(args):` defines a function; (2) Indented body holds the logic; (3) `return` sends the result back; (4) Call with `NAME(values)` — Python plugs them in

### 43. Why functions matter (full-slide, two-column: explanation text + card)
- Left: "You **already use** functions all the time — `print(...)`, `len(...)`, `type(...)`. Writing your own means you can name *your* logic and reuse it everywhere — instead of pasting the same code into 8 cells."
- Right (teal sidebar card): "Why write your own?" `.si`/`.st` list:
  - Reuse — write once, call many times
  - Read — `total_for(3, 4.50)` says what it does; `3 * 4.50` doesn't
  - Refactor — fix the function once, every caller benefits
  - Claude-friendly — easier to ask for help when logic is wrapped in a function

### 44. Exercise: Write your first function (split code, EXERCISE badge)
- Skeleton (left):
  ```
  def revenue_for(transactions):
      total = [?]
      for tx in transactions:
          total = total + [?]
      return [?]
  
  print(revenue_for(transactions))
  ```
- Hints (right): (1) Start `total = 0`; (2) Add `tx["qty"] * tx["price"]` each iteration; (3) Return `total`; (4) The previous transactions list still works

### 45. Section divider — "Working with Claude" (section divider continuation, pink accent, Section 06)
- Subtitle: "Your coding partner — not your replacement."

### 46. How to prompt Claude when you're stuck (full-slide, 3-card grid + maxim)
- Intro: "When something doesn't work, Claude can help — but **how** you ask matters."
- Card 1 (teal): **Show your code** — paste the cell that's misbehaving in full, not just a summary
- Card 2 (pink): **Show the error** — paste the **entire** traceback, including the last line (that's the actual error)
- Card 3 (teal): **Say what you expected** — "I expected this to print 5 cups but it printed 0" — gives Claude the goal, not just the symptom
- Maxim (centred italic): "The clearer your question, the better Claude's answer."

### 47. A good Claude prompt (full-slide, mocked Claude chat panel)
- Mocked chat (light card with rounded corners):
  - User prompt block: "I'm trying to count how many transactions are over £5. Here's my code: [paste 5 lines]. I expected 3 but got 0. What am I doing wrong?"
  - Claude response block: "Your loop is comparing `tx` (a dict) to a number. You meant `tx['price']`. Here's the fix: [3 corrected lines]. Try this — it should give you 3."
- Caption below: Notice — code, expectation, and the **specific question** — Claude responded with a targeted fix, not a guess.

### 48. The two-try rule (full-slide, hero card with rule + supporting bullets)
- Hero card (teal border): **"Try it twice yourself before you ask Claude."**
- Supporting `.si`/`.st` bullets:
  - First try — write the code as best you can
  - Second try — read the error, change one thing
  - Then — paste it into Claude with context
- Closing line: "Reaching for Claude before thinking means you never learn the syntax. The rule keeps Claude as a partner, not a crutch."

### 49. Section divider — "Wrap-up" (title-slide style, dark navy, Section 07)

### 50. You can all now… (full-slide, two-column: 5 checklist rows on left + Purple_small.jpg on right)
- Left column: 5 rows with teal check-circle icons
  - Open a Colab notebook and write code
  - Use variables, lists, and dictionaries
  - Filter and transform data with `if` and `for`
  - Write a basic function
  - Ask Claude a question that actually helps
- Right: `../sql-for-mbas/assets/Purple_small.jpg` (reuse) or a Python-themed image — TBD asset

### 51. Coming up next time — Functions & libraries (full-slide, intro line + 2 preview cards)
- Intro: "Next session we'll go deeper:"
- Card 1 (teal): **Functions in depth** — parameters, defaults, list comprehensions, error reading
- Card 2 (pink): **Python's standard library** — `math`, `random`, `datetime`, `statistics` — and the Claude-as-debugger workflow
- Tease (centred, italic): "By Session 4, you'll have built a coffee shop dashboard from scratch."

### 52. Questions & Feedback (final slide, dark navy, two-column: heading + two QR cards)
- Left: "Questions & Feedback" heading (teal accent on "Feedback") + pink underline + "Thanks for joining — see you next week!" subtitle
- Right: two white rounded cards side-by-side
  - Feedback QR: pink small-caps label "Feedback" + `../sql-for-mbas/assets/feedback-qr.png` (reuse for now)
  - LinkedIn QR: teal small-caps label "Let's connect" + `../../shared/assets/LinkedIn.png`
- Logo at bottom

---

## Notes for implementation
- Slide numbering above includes 1 "ignore this stub" marker — final HTML will have 52 slides as planned.
- Break sits between collections (slide 27) and control flow (slide 29) — natural cognitive break.
- Function teaser (Section 05) is **light** — one definition slide, one motivation slide, one exercise. Session 2 deepens.
- Reuse Purple_small.jpg and feedback-qr.png from sql-for-mbas/assets/ until Python-specific imagery is created.
