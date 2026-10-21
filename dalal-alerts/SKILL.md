---
name: dalal-alerts
description: >-
  Price alerts for NSE/BSE stocks. Rings when a price target, a stop or
  the NSE opening bell hits: above / below / stop rules and percent moves
  from the previous close, each ringing once so the user is not spammed.
  Knows NSE hours (9:15-15:30 IST) with the official exchange holiday
  list, and fetches free delayed quotes from Yahoo Finance one ticker at
  a time. Use when the user says "alert me when", "tell me if RELIANCE
  hits", "set a stop", "price target", "watch my stocks", "is the market
  open", "get me prices", or to refresh prices before sizing, risk or tax.
---

# dalal-alerts

Watches the numbers so the user does not have to. An alert is
information, never an order: when a stop rings, nothing is sold. If the
user wants to act, the normal path runs (dalal-budget, dalal-risk, their
yes, then they place the order by hand in their own app). Not financial
advice.

## Quotes (free, delayed, verified 21 Oct 2026)

Yahoo Finance chart JSON, one request per ticker, about a second apart,
with a browser User-Agent:

```bash
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0 Safari/537.36"
curl -s -A "$UA" "https://query1.finance.yahoo.com/v8/finance/chart/RELIANCE.NS?interval=1d&range=5d"
```

- NSE stocks: append `.NS` (RELIANCE.NS, TCS.NS, UJJIVANSFB.NS).
- BSE stocks: append `.BO`.
- Price is at `.chart.result[0].meta.regularMarketPrice`, previous close
  at `.meta.previousClose` (or chartPreviousClose).
- If Yahoo returns "Too Many Requests", wait 30-60 s and retry once.
  Free quotes are delayed up to 15 min; fine for alerts, not for timing
  an order. The broker's price is the one that fills.
- Do NOT use nseindia.com/api/quote-equity: it blocks automated access.

## The NSE clock

Regular session 9:15 a.m. to 3:30 p.m. IST, Monday-Friday. Holidays are
published by the exchange; fetch the live list instead of hardcoding:

```bash
curl -s -c /tmp/nse_ck.txt -A "$UA" "https://www.nseindia.com" -o /dev/null
curl -s -b /tmp/nse_ck.txt -A "$UA" -H "Accept: application/json" \
  "https://www.nseindia.com/api/holiday-master?type=trading"
```

## Rule types

| type | rings when |
| --- | --- |
| `above` | price at or above target |
| `below` / `stop` | price at or below target |
| `pct_move` | moved N percent from previous close |
| `opening_bell` | NSE opens (9:15 IST, not a holiday) |

Keep rules in `dalal/alerts.json`, which rules already rang in
`dalal/state/alerts.json` (each rings once until reset), and write the
latest quotes to `dalal/prices.json` as
`{"as_of": "...", "prices": {"RELIANCE": 2451.10}}` for dalal-budget,
dalal-risk, dalal-tax and dalal-rebalance.
