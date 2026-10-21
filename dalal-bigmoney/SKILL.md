---
name: dalal-bigmoney
description: >-
  Big-money tracker for India, the honest replacement for the Pelosi
  skill. India has no politician trade disclosures; what exists and is
  public: NSE bulk and block deals (any trade over 0.5% of a company,
  with the buyer/seller name), daily FII/DII buy-sell figures, and
  insider-trading disclosures company insiders file with the exchange.
  Use when the user says "what are FIIs doing", "big deals today", "any
  insider buying", "smart money India", "who bought this stock".
---

# dalal-bigmoney

Tracks the footprints big money must leave in India. Analysis only, not
financial advice. A big buyer does not make a stock good; report the
data, do not hype it.

## Sources (free, verified 21 Oct 2026)

NSE APIs, each after the cookie step:

```bash
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0 Safari/537.36"
curl -s -c /tmp/nse_ck.txt -A "$UA" "https://www.nseindia.com" -o /dev/null
```

1. Bulk and block deals (names the client, qty, price, buy/sell):

```bash
curl -s -b /tmp/nse_ck.txt -A "$UA" -H "Accept: application/json" \
  "https://www.nseindia.com/api/snapshot-capital-market-largedeal"
```

2. FII / DII daily flows (crores, market-wide):

```bash
curl -s -b /tmp/nse_ck.txt -A "$UA" -H "Accept: application/json" \
  "https://www.nseindia.com/api/fiidiiTradeReact"
```

3. Insider trades: promoters and designated employees must disclose
   trades to the exchange under SEBI's PIT rules. NSE's public insider
   endpoint is unreliable for scripts; when the user asks about a
   specific company, check the filings list in dalal-news output for
   insider-trading disclosures, or open
   https://www.nseindia.com/companies-listing/corporate-filings-insider-trading
   in a browser.

## Output

- Bulk/block deals: table of date, symbol, client name, buy/sell, qty,
  price. Highlight names that repeat across days.
- FII/DII: today's and the last few days' net buy/sell with the trend in
  one line (e.g. "FIIs net sellers 3 days running").
- Always with the trading date the data belongs to.
