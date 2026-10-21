---
name: dalal-analyst
description: >-
  Earnings and fundamentals analyst for Indian companies. India has no
  free SEC-XBRL-style API, so this reads Screener.in (the standard free
  fundamentals site: sales, profit, EPS, ROCE, PE, shareholding,
  quarterly results tables) plus the official results announcement from
  the NSE feed. Use when the user says "analyse this company", "how are
  TCS results", "is this stock expensive", "fundamentals of", "quarterly
  results".
---

# dalal-analyst

Reads an Indian company's reported numbers and presents them plainly.
Analysis only, not financial advice. Numbers come from public filings
aggregated by Screener.in; when a number matters, cross-check the
company's results PDF on the exchange.

## Sources (free, verified 21 Oct 2026)

1. Find the company:

```bash
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
curl -s -A "$UA" "https://www.screener.in/api/company/search/?q=tata%20steel"
```

2. Fundamentals page (use a browser UA):
   `https://www.screener.in/company/<TICKER>/consolidated/`
   Tables on it: market cap, PE, book value, dividend yield, ROCE, ROE,
   quarterly results, profit & loss years, balance sheet, cash flow,
   shareholding pattern trend. Screener.in has no official API; fetch
   pages politely, one at a time, for personal use.

3. Official confirmation: the results announcement and PDF from the NSE
   corporate announcements feed (see dalal-news). This is the primary
   document; Screener is the convenient summary.

## Output

A one-page brief: what the company does in one line, latest quarter
(sales, profit, YoY change), valuation vs its own history and sector,
debt level, shareholding trend (promoter/FII/DII rising or falling),
and 2-3 plain risks. Every number with its period. End with what you
could not verify, not with a buy/sell call.
