# Stock Market Research Workspace

Personal investing research environment built around **Cursor AI rules and skills**. This repo is not a trading app — it is a structured way to get consistent, evidence-based stock analysis tailored to your portfolio, track predictions over time, and pick up exactly where you left off.

**GitHub:** https://github.com/Sanchit1397/stock-market

---

## What this project does

| Goal | Where to look |
|------|---------------|
| Decide what US stocks to buy this month | `@us-stock-suggestions` rule + `@my-portfolio` |
| Decide what Indian stocks to research | `@india-stock-suggestions` rule + `@my-portfolio` |
| Analyze Europe, Japan, EM, global themes | `@global-stock-suggestions` rule |
| Find short-term / swing trade setups | `@swing-trading-suggestions` rule |
| Backtest “what would I have bought in 2024?” | `historical-time-machine` skill |
| Review past chat predictions | `predictions/` folder |
| Keep portfolio context current | Edit `.cursor/rules/my-portfolio.mdc` |

All rules fetch **live data** (prices, earnings, news) — they do not answer from stale memory.

---

## Quick start (new machine)

### 1. Clone the repo

If you use the Sanchit1397 GitHub account with a custom SSH host (see your `~/.ssh/config`):

```bash
git clone git@github.com-badrikidukan:Sanchit1397/stock-market.git
cd stock-market
```

Or via HTTPS:

```bash
git clone https://github.com/Sanchit1397/stock-market.git
cd stock-market
```

### 2. Open in Cursor

Open the cloned folder in **Cursor**. The rules and skills under `.cursor/` load automatically when you invoke them.

### 3. (Optional) Set up the price tracker venv

The virtualenv is **not** in git. Recreate it if you want to fetch live prices from the command line:

```bash
python3 -m venv .venv-tracker
source .venv-tracker/bin/activate
pip install yfinance
```

---

## Project structure

```
stock-market/
├── README.md                          ← you are here
├── .gitignore                         ← ignores .venv-tracker/
├── .cursor/
│   ├── rules/                         ← AI research personas (invoke with @ in chat)
│   │   ├── my-portfolio.mdc         ← YOUR holdings & monthly plan (update monthly)
│   │   ├── us-stock-suggestions.mdc ← US long-term research
│   │   ├── india-stock-suggestions.mdc
│   │   ├── global-stock-suggestions.mdc
│   │   ├── swing-trading-suggestions.mdc
│   └── skills/
│       └── historical-time-machine/ ← anti-hindsight backtesting mode
└── predictions/                       ← saved prediction snapshots from past chats
    ├── YYYY-MM-DD-ticker-tracker.md   ← human-readable tracker
    └── YYYY-MM-DD-ticker-tracker.json ← machine-readable tracker
```

---

## How to use Cursor rules

Rules are **not** always-on. In Cursor chat, type `@` and pick the rule you need, then ask your question.

### `@my-portfolio` — your personal context (update monthly)

**Purpose:** Living snapshot of your holdings, monthly SIP amounts, and cross-portfolio rules so other rules do not give advice in a vacuum.

**Current setup (as of Jun 2026):**

| Sleeve | ₹/month | Platform |
|--------|---------|----------|
| India stocks | 40,000 | Sharekhan (broker-managed) |
| US Nasdaq growth | 20,000 | Groww — Motilal Oswal Nasdaq 100 ETF |
| US direct stocks | 40,000 | INDmoney |
| Gold | ~12,000 | — |
| Silver | ~5,000 | — |

**When to update:** Start of each month, or whenever holdings change. Edit `.cursor/rules/my-portfolio.mdc` directly.

**Example prompts:**
- `@my-portfolio Update my India holdings — broker now holds X, Y, Z`
- `@my-portfolio @us-stock-suggestions Where should my ₹40k INDmoney go this month?`

---

### `@us-stock-suggestions` — US long-term research

**Purpose:** Deep fundamental analysis, valuation, portfolio review, hype detection for US equities. Thorough, institutional-style output.

**Use when:**
- Picking stocks for your INDmoney sleeve
- Weekly US check-in
- Analyzing a specific ticker (e.g. “Should I buy CRM?”)
- Portfolio review of US holdings

**Example prompts:**
- `@us-stock-suggestions @my-portfolio I have ₹40k for INDmoney this month. What should I buy given my Groww Nasdaq SIP and India book?`
- `@us-stock-suggestions Analyze BRK.B — bull case, bear case, conviction rating`
- `@us-stock-suggestions Weekly US check-in — macro, Groww stance, INDmoney thesis, one avoid call`
- `@us-stock-suggestions Is PLTR overhyped right now?`

**Output includes:** Bull/bear/neutral case, conviction rating, time horizon, risk level, valuation assessment, key catalysts and risks.

---

### `@india-stock-suggestions` — India long-term research

**Purpose:** NSE / BSE equity research, sector analysis, FII/DII flows, promoter checks, mutual fund context.

**Use when:**
- Researching Indian quality names (even though Sharekhan is broker-managed)
- Understanding sector overlap with your US book
- India macro / RBI / earnings season context

**Example prompts:**
- `@india-stock-suggestions @my-portfolio My broker holds heavy infra/rail names. What India sectors am I missing?`
- `@india-stock-suggestions Deep dive on HDFC Bank — valuation vs ICICI`
- `@india-stock-suggestions What are the best quality large-caps to watch this quarter?`

---

### `@global-stock-suggestions` — global / multi-market research

**Purpose:** Developed and emerging markets outside a single-country focus — Europe, Japan, China, EM, global ETFs, themes.

**Use when:**
- Exploring non-US, non-India opportunities
- Global sector or theme research (e.g. semiconductors globally)
- Diversification beyond your current sleeves

**Example prompts:**
- `@global-stock-suggestions Compare ASML vs TSMC for a 5-year hold`
- `@global-stock-suggestions Best global dividend ETFs right now`
- `@global-stock-suggestions What EM markets look attractive given current USD strength?`

---

### `@swing-trading-suggestions` — short-term / swing trades

**Purpose:** Multi-day to multi-week trade setups with entry, stop, target, and risk/reward. **Not** buy-and-hold advice.

**Use when:**
- Looking for trades over days/weeks, not years
- Want ranked setups with A+/A/ B conviction
- Need market regime read before trading

**Time horizons:**
- Short-term: 1–10 trading days
- Swing (default): ~2 days to ~6 weeks

**Example prompts:**
- `@swing-trading-suggestions Best swing setups in US tech right now`
- `@swing-trading-suggestions Setup on NVDA — entry, stop, target, R/R`
- `@swing-trading-suggestions Market regime check — should I be aggressive or in cash?`
- `@swing-trading-suggestions Scan NSE for momentum breakouts this week`

**Output includes:** Regime verdict, ranked trade cards, watchlist triggers, avoid list, stop/target levels, conviction A+ to Pass.

---

### `historical-time-machine` skill — backtest without hindsight

**Purpose:** Simulate what you would have invested on a **past date**, using only information available then. No “as we now know” cheating.

**Use when:**
- “What would you have bought on June 2, 2024?”
- “Which stock would you pick 2 years ago?”
- Testing whether your framework would have worked historically

**How to invoke:** Mention a past date, or combine with another rule:

```
@us-stock-suggestions Using historical-time-machine: pretend today is Jan 1, 2023.
What would you buy with $100k?
```

**Output includes:** Date assumed, top 10 candidates, $100k allocation, reasoning with period-appropriate data only, known risks at the time.

---

## Predictions folder — track and score past calls

When a research session produces actionable predictions, save a snapshot here so you can review accuracy later.

### Files per session

| File | Purpose |
|------|---------|
| `YYYY-MM-DD-ticker-tracker.md` | Human-readable tables — verdicts, prices, 1-month predictions, scoring rubric |
| `YYYY-MM-DD-ticker-tracker.json` | Same data in JSON for scripts or future automation |

### Current snapshot

- **Created:** 2026-06-02
- **Review date:** 2026-07-02
- **User confirmed US picks:** BRK.B, CRM, XOM, JPM
- **File:** `predictions/2026-06-02-ticker-tracker.md`

### Scoring on review day

Open the `.md` file and for each ticker mark:

| Result | Meaning |
|--------|---------|
| ✅ Right | Price moved within predicted band AND verdict matched |
| ⚠️ Mixed | Right direction, wrong magnitude |
| ❌ Wrong | Opposite move or wrong action |

Add a **“Review — YYYY-MM-DD”** section at the bottom with actual prices and scores.

### Refresh prices on review day

```bash
cd stock-market   # or your local path
source .venv-tracker/bin/activate   # if not already active

python -c "
import yfinance as yf
syms = ['BRK-B','CRM','XOM','JPM','MDLZ','PLTR','ZS','MU','ASML','PATH']
for s in syms:
    p = float(yf.Ticker(s).history(period='2d')['Close'].iloc[-1])
    print(s, round(p, 2))
"
```

Note: Yahoo uses `BRK-B` (hyphen) for Berkshire B shares.

### Creating a new prediction snapshot

After a big research chat, ask Cursor:

> Create a prediction tracker for today's session — save both `.md` and `.json` in `predictions/` with today's date, review date one month out, all tickers discussed, prices, verdicts, and 1-month predictions.

---

## Common workflows (“I want to…”)

### …decide where to invest this month’s US ₹40k

```
@my-portfolio @us-stock-suggestions
I have ₹40k for INDmoney this month. My Groww Nasdaq SIP continues.
What 2–4 names should I buy, and what should I avoid given my full portfolio?
```

### …do my weekly US check-in

```
@my-portfolio @us-stock-suggestions
Weekly US check-in: macro, Groww stance, INDmoney holdings thesis,
one stock to avoid/trim, and one cross-portfolio note for India + metals.
```

### …research a single stock deeply

```
@us-stock-suggestions
Full analysis on CRM — business quality, valuation, bull/bear case,
conviction rating, and fit with my portfolio.
```

### …find a swing trade this week

```
@swing-trading-suggestions
US market — best 3 swing setups right now with entry, stop, target, and regime read.
```

### …understand my India + US overlap

```
@my-portfolio @us-stock-suggestions @india-stock-suggestions
Given my Sharekhan holdings (infra, banks, auto), am I over-exposed to cyclicals?
What should my US sleeve tilt toward?
```

### …review last month’s predictions

1. Open `predictions/` — find the file whose **review date** is today or past.
2. Run the price refresh script above.
3. Score each row using the rubric in the file.
4. Add a review section at the bottom.

### …update my portfolio after broker changes

1. Edit `.cursor/rules/my-portfolio.mdc` — update the India holdings table and sector map.
2. Commit and push so other machines stay in sync:

```bash
git add .cursor/rules/my-portfolio.mdc
git commit -m "Update portfolio holdings — [month year]"
git push
```

### …backtest a historical decision

```
@us-stock-suggestions
Historical time-machine: pretend today is June 2, 2024.
What would you buy with $50k for a 2-year hold? No hindsight.
```

---

## Git workflow

### Push changes

```bash
git add .
git commit -m "Describe what changed"
git push
```

**Important:** This repo uses a custom SSH host for the Sanchit1397 account. Remote URL must be:

```
git@github.com-badrikidukan:Sanchit1397/stock-market.git
```

Not plain `git@github.com:...` — that will fail if you have multi-account SSH config.

Check your remote:

```bash
git remote -v
```

Fix if needed:

```bash
git remote set-url origin git@github.com-badrikidukan:Sanchit1397/stock-market.git
```

### Pull on another machine

```bash
git pull
```

Then recreate `.venv-tracker` if you need price fetching (see Quick start).

---

## Monthly maintenance checklist

Use this when you come back after a break:

- [ ] **Pull latest** — `git pull`
- [ ] **Update `my-portfolio.mdc`** — new monthly amounts, Sharekhan holdings, any SIP changes
- [ ] **Run monthly US allocation chat** — `@my-portfolio @us-stock-suggestions` with this month’s ₹40k
- [ ] **Check `predictions/`** — any review dates due? Score and append results
- [ ] **Save new predictions** — if you made calls this month, add a dated tracker file
- [ ] **Commit & push** — keep repo synced across machines

---

## Key principles (built into the rules)

- **Live data only** — rules search for current prices and news; they do not guess
- **Push back on bad ideas** — rules are designed to challenge FOMO and hype, not agree with you
- **Portfolio-aware** — always invoke `@my-portfolio` for allocation advice; US is not your whole book
- **No duplication** — Groww Nasdaq already gives US tech beta; INDmoney should complement, not duplicate
- **Separate investing vs trading** — use US/India/Global rules for long-term; Swing rule for short-term
- **Track predictions** — save snapshots in `predictions/` so you can learn from outcomes

---

## Disclaimer

This workspace is for **personal research and education only**. It is not licensed financial advice. Rules explicitly note tax considerations (LRS, W-8BEN, Schedule FA, India ITR) but you are responsible for your own compliance and decisions. Past chat predictions are directional estimates, not guarantees.

---

## Quick reference card

| I want to… | Invoke |
|------------|--------|
| Monthly US stock picks | `@my-portfolio` + `@us-stock-suggestions` |
| India stock research | `@india-stock-suggestions` |
| Global / non-US markets | `@global-stock-suggestions` |
| Swing / short-term trades | `@swing-trading-suggestions` |
| Historical backtest | Mention date + any rule above |
| Update my holdings | Edit `my-portfolio.mdc` |
| Score past predictions | `predictions/YYYY-MM-DD-*.md` |
| Fetch live prices | `.venv-tracker` + yfinance script |
