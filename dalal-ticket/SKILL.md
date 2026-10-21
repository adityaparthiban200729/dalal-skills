---
name: dalal-ticket
description: >-
  Order ticket writer. Turns an approved, risk-checked order into an
  exact paper ticket (symbol, exchange, qty, order type, limit price)
  for the user to place BY HAND in their own broker app (INDmoney,
  Zerodha, Groww, etc.). It never connects to a broker, never places or
  modifies an order, and records the user's explicit yes. Use after
  dalal-risk says PASS and the user says yes to a specific order.
---

# dalal-ticket

The last step before the user's own hands. This skill cannot trade.
There is no broker connection and there must never be one. Not
financial advice.

## Hard rules

1. Only runs on an order that passed dalal-risk AND the user explicitly
   approved ("yes, buy 2 shares of TCS"). No approval, no ticket.
2. Output is a paper ticket for manual placement. Nothing else exists.
3. Defaults for a beginner: cash segment (CNC/delivery), LIMIT order
   with a stated price from the latest quote, day validity. No market
   orders on illiquid small caps; no F&O; no intraday margin.
4. The ticket states the exact steps: open your broker app, search the
   symbol, buy, quantity, limit price, review the charges shown by the
   broker, then confirm - and to screenshot the confirmation back.
5. Log the ticket and the user's yes to `dalal/orders.json` with a
   timestamp so dalal-tax and dalal-rebalance can use it later.

## Ticket format

```
TICKET 2026-10-21
BUY  TCS (NSE: TCS)  x 2 shares
Type: delivery (CNC), LIMIT Rs 3,xxx.xx, valid today
Approx cost: Rs x,xxx + charges
Placed by: YOU, by hand, in your broker app
Approved: yes - <user's words, time>
```
