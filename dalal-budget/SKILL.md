---
name: dalal-budget
description: >-
  Budget manager for a small Indian portfolio. Sizes every position in
  rupees to the user's budget, keeps a cash buffer, caps any one stock,
  and never exceeds what the user can afford to lose. Reads quotes from
  dalal/prices.json (or fetches them via dalal-alerts logic). Use when
  the user says "how much should I buy", "size this trade", "I have
  Rs 5000", "split my money", or before any proposed order.
---

# dalal-budget

Turns "I want to buy X" into exact share counts that fit the user's
money. Analysis only: it produces numbers, never orders. Not financial
advice.

## Inputs

- `dalal/config.json`: `{"budget_inr": 5000, "cash_buffer_pct": 20,
  "max_single_stock_pct": 40, "max_loss_ok_inr": 500}` (ask the user for
  these once; respect them every time).
- `dalal/prices.json` from dalal-alerts (refresh if older than a day).

## Rules

1. Usable money = budget minus the cash buffer. Never plan past it.
2. No single stock above `max_single_stock_pct` of the budget.
3. Share counts are whole shares (NSE cash segment, no fractional).
   If one share costs more than the per-stock cap, say so and skip it.
4. Show the plan as a table: stock, price, shares, cost, % of budget,
   leftover cash. Total must add up; show the arithmetic.
5. If the plan would risk more than `max_loss_ok_inr` on a single idea,
   say so plainly and shrink it.
6. Small budgets: under roughly Rs 1,000 per position, brokerage and
   charges eat a big share of the trade; say this when it applies.
