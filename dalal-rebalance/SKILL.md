---
name: dalal-rebalance
description: >-
  Rebalancer for a small Indian portfolio. Compares current weights to
  the user's target weights and lists what to trim or add when drift
  passes the band, always as suggestions the user must approve before
  dalal-ticket places them live. Use when the user says "rebalance", "my portfolio drifted",
  "back to my targets", "too much in one stock".
---

# dalal-rebalance

Brings the portfolio back toward its target weights. Suggestions only:
the user approves, then dalal-ticket places the orders live on their
INDstocks account after their explicit yes. Not financial advice.

## Inputs

- `dalal/targets.json`: `{"RELIANCE": 30, "TCS": 30, "CASH": 40}` style
  target weights in percent (ask the user once; keep their numbers).
- `dalal/portfolio.json` current lots, `dalal/prices.json` current
  prices (refresh with dalal-alerts if stale).
- Drift band: default 5 percentage points unless the user sets one.

## Method

1. Compute current weight of each holding and of cash.
2. Compare to targets; anything outside the band gets a suggested trade
   (sell X shares of A, buy Y shares of B) sized to the band edge, not
   beyond.
3. Run every suggested trade through dalal-risk before presenting it.
4. Show the table: current % vs target %, drift, suggested action,
   approx trade value in rupees.
5. For very small portfolios, note when the drift fix is smaller than
   one share or when charges make rebalancing pointless - then suggest
   doing nothing, which is a valid answer.
