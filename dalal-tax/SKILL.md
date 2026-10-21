---
name: dalal-tax
description: >-
  Indian capital-gains tracker for shares. Tracks buy lots, works out
  short-term vs long-term for listed equity (12-month line), current
  rates (STCG 20%, LTCG 12.5% above the Rs 1.25 lakh yearly exemption),
  unrealised gains/losses, and tax-loss harvesting candidates before the
  financial year ends 31 March. India has no wash-sale rule. Use when the
  user says "tax on my stocks", "how much gain", "sell before March",
  "tax loss harvesting", "STCG LTCG".
---

# dalal-tax

Keeps the user's lot book and shows the tax angle of selling. Analysis
and record-keeping only; it never tells the user to sell and never
trades. Not tax advice - for filing, the broker's P&L statement and a
CA win over anything here. Say that when it matters.

## Indian rules applied (per incometaxindia.gov.in, post 23 Jul 2024)

- Listed equity with STT paid:
  - Held under 12 months: short-term, 20% (plus cess/surcharge).
  - Held 12 months or more: long-term, 12.5% on total LTCG above
    Rs 1,25,000 per financial year.
- First-in-first-out for matching sells to buy lots.
- No wash-sale rule in India (unlike the US): selling at a loss and
  rebuying is allowed; the loss still counts. Tax-loss harvesting near
  31 March is legal and common - still the user's decision, not yours to
  push.
- Financial year runs 1 April to 31 March.

## Data

- `dalal/portfolio.json` lots: symbol, buy date, qty, buy price (ask the
  user or read their broker statement they paste in).
- Current prices: `dalal/prices.json` (dalal-alerts).

## Output

- Lot table: symbol, buy date, qty, cost, current value, gain/loss,
  ST or LT today, days until it turns LT.
- If sold today: STCG and LTCG split and the rough tax at the rates
  above, shown as an estimate with the rate and year stated.
- Harvesting list: lots currently at a loss with the loss amount, noting
  the 31 March deadline when it is near.
