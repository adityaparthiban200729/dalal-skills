---
name: dalal-ticket
description: >-
  Live order placer for the user's own INDstocks (INDmoney) account.
  Turns an approved, risk-checked order into a real order on INDstocks:
  it logs in (the user approves the OTP on his phone), shows the exact
  order one last time, and places it only after the user confirms the
  exact stock, quantity, price and total in writing. Use after
  dalal-risk says PASS and the user says yes to a specific order.
---

# dalal-ticket

The last step, and the only skill that touches real money. It places
live orders on the user's own INDstocks account through the browser.
Not financial advice.

## Hard rules

1. Only runs on an order that passed dalal-risk AND the user explicitly
   approved with the exact terms in writing ("yes, buy 2 shares of TCS
   at 3500"). No approval with all four of stock, quantity, price and
   total, no order.
2. The fee math must clear before anything is placed: compute the
   round-trip charges for the exact quantity from the charges the
   broker shows, and state the move needed to break even. If the
   expected move does not clear fees, say NO TRADE and stop.
3. Segment and order type: cash segment only, whole shares, LIMIT
   orders at a stated price from the latest quote. Delivery (CNC) by
   default; intraday (MIS) only when the user explicitly asks for a
   same-day trade, sized so the free cash covers it. No F&O, no
   borrowed money.
4. Respect the loss limit from dalal/config.json (default max loss
   Rs 20-30 per trade): state the stop price and the worst-case loss
   in rupees on the confirmation screen before placing.
5. Login: open indstocks.indmoney.com, start login with the user's
   phone number, and ask the user for the OTP he receives on his own
   phone. Never ask for or store his MPIN or password in chat.
6. Show the final confirmation - stock, quantity, order type, limit
   price, total, charges - and wait for the user's explicit yes. Place
   only on that yes. If the price moved since he confirmed, re-confirm
   the new numbers before placing.
7. After placing, screenshot the broker's confirmation and log the
   order, the fill, and the user's yes to `dalal/orders.json` with a
   timestamp so dalal-tax and dalal-rebalance can use it later. For an
   intraday (MIS) order, set the exit the same day: place the
   stop/target or square off before 15:15 IST, and tell the user the
   result either way.
8. If anything fails - login blocked, captcha, order rejected - stop,
   show the user the exact screen, and let him finish on his own
   phone. Never retry a rejected order without telling him why.

## Confirmation format (shown before every order)

```
ORDER 2026-10-21
BUY  TCS (NSE: TCS)  x 2 shares
Type: delivery (CNC), LIMIT Rs 3,xxx.xx, valid today
Total: Rs x,xxx + approx charges Rs x
Break-even move: x.x% | Stop: Rs x,xxx (worst case -Rs xx)
Place this order? Waiting for your exact yes.
```
