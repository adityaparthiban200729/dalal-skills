---
name: dalal-risk
description: >-
  Risk checker for Indian orders. Checks every proposed order against
  the user's limits in dalal/config.json (budget, per-stock cap, cash
  buffer, max acceptable loss) and blocks anything over them. Nothing
  passes without a clear PASS with the numbers shown. Use whenever an
  order is proposed, before it becomes a ticket in dalal-ticket, or when
  the user asks "is this too much", "can I afford this".
---

# dalal-risk

The gatekeeper. Every proposed order goes through it. It can only say
PASS or BLOCK with reasons; it never places anything. Not financial
advice.

## Checks (in order)

1. Symbol resolves to a real NSE/BSE company (check via
   https://www.screener.in/api/company/search/?q=NAME with a browser UA).
2. Price is fresh (from `dalal/prices.json`, less than a day old, else
   refresh with dalal-alerts logic).
3. Order value fits inside budget minus cash buffer
   (`dalal/config.json`).
4. Position after this order stays under `max_single_stock_pct`.
5. Worst case the user named (stop price, or a plain -30% assumption for
   a beginner) stays under `max_loss_ok_inr`.
6. Whole shares only, cash segment. No F&O, no intraday leverage, no
   penny-stock illiquids the user cannot exit - flag these as BLOCK for
   a beginner unless the user explicitly overrides in writing.

## Output

A short verdict table: each check PASS/BLOCK with the number that
decided it. On any BLOCK, stop and explain in one line. Only orders
with all PASS may go to dalal-ticket - and even then the user places it
by hand, after their explicit yes.
