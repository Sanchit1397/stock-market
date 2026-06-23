---
name: historical-time-machine
description: >-
  Simulate historical investment decisions using only information available on
  or before a specified past date, with zero hindsight bias. Use when the user
  asks what stock/portfolio they would have picked at a past date (e.g. "Which
  stock would you have picked 2 years ago?", "What would you buy if today's date
  was June 2, 2024?", "What would your portfolio look like on January 1, 2023?"),
  or asks for any historical investment recommendation. Also use prices,
  earnings, and conditions as they were on the simulated date when this skill is
  run alongside other stock skills or rules.
---

# HISTORICAL TIME-MACHINE MODE (ANTI-HINDSIGHT BIAS)

When I ask questions such as:

* "Which stock would you have picked 2 years ago?"
* "What would you buy if today's date was June 2, 2024?"
* "What would your portfolio look like on January 1, 2023?"
* "What would you recommend before AI became mainstream?"
* Any similar historical investment question

you must enter **Historical Time-Machine Mode**.

### Core Principle

You must behave as though you are physically living on the specified date.

You must be completely unaware of anything that happened after that date.

Treat all future events as unknown.

### Strict Rules

1. Do NOT use information published after the specified date.
2. Do NOT use future stock prices.
3. Do NOT use future earnings reports.
4. Do NOT use future product launches.
5. Do NOT use future analyst upgrades/downgrades.
6. Do NOT use future geopolitical developments.
7. Do NOT use future economic data.
8. Do NOT use future market reactions.
9. Do NOT use future Reddit discussions.
10. Do NOT use future knowledge of winners and losers.

### Required Mental Model

If the date is June 2, 2024:

You must genuinely believe:

* It is June 2, 2024.
* The future has not happened yet.
* You do not know what stocks will outperform.
* You only know what was publicly available on or before June 2, 2024.

### Research Method

For each candidate investment:

Evaluate only:

* Financial statements available at that time
* Macroeconomic conditions known at that time
* Geopolitical risks known at that time
* Management quality known at that time
* Valuation known at that time
* Competitive landscape known at that time
* Industry trends known at that time

### Output Format

For historical simulations provide:

#### Date Assumed

Explicitly state the date being simulated.

#### Available Information

List only information available up to that date.

#### Top 10 Candidates

Rank the stocks you would most likely purchase.

#### Portfolio Construction

Show how you would allocate $100,000.

#### Why These Stocks

Provide reasoning using only historical information.

#### Known Risks At The Time

List risks that were visible at the time.

#### Confidence Level

State your confidence based only on historical evidence.

### Mandatory Integrity Check

Before finalizing your answer, perform a self-audit:

"Am I using any information that became available after the simulated date?"

If yes:

Remove it.

### Forbidden Phrases

Do NOT say:

* "As we now know..."
* "This stock later became..."
* "The stock eventually..."
* "In hindsight..."
* "Looking back..."
* "Afterward..."
* "Subsequently..."

These phrases reveal future knowledge and violate Historical Time-Machine Mode.

### Goal

The purpose is to determine what the highest-quality investment decision would have been using only the information available at that point in history, exactly as a professional investor would have done in real life.

### When Combined With Other Skills Or Rules

When this skill is run alongside another skill or rule, this mode takes precedence for time context: use prices, valuations, fundamentals, and all data as they stood on the simulated date, not the present day.
