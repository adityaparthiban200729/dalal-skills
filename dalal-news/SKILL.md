---
name: dalal-news
description: >-
  Indian market news and filings watcher. Reads the NSE corporate
  announcements feed (results, board meetings, resignations, dividends,
  the Indian equivalent of an 8-K) plus Google News and Moneycontrol RSS
  headlines for every stock the user holds or names, and flags what
  touches them. Use when the user says "any news on my stocks", "what
  happened with RELIANCE today", "watch TCS announcements", "market
  news", or before any analysis of an Indian stock.
---

# dalal-news

Watches Indian company news and exchange filings so the user does not
have to. Analysis only: it never trades and never recommends a trade.
Always show the source and timestamp of every item. This is information,
not financial advice.

## Data sources (all free, no key, verified 21 Oct 2026)

1. NSE corporate announcements (official exchange feed):

```bash
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0 Safari/537.36"
curl -s -c /tmp/nse_ck.txt -A "$UA" "https://www.nseindia.com" -o /dev/null
curl -s -b /tmp/nse_ck.txt -A "$UA" -H "Accept: application/json" \
  "https://www.nseindia.com/api/corporate-announcements?index=equities"
```

Each row has `symbol`, `desc` (category like Financial Results / Board
Meeting / Dividend / Resignation), `attchmntText` (plain summary) and a
PDF link. Filter rows to the user's symbols. The cookie step is
required; if the feed returns HTML ("Access Denied"), re-fetch the
cookie and retry once.

2. Google News RSS (India edition):

```
https://news.google.com/rss/search?q=<COMPANY NAME>+NSE&hl=en-IN&gl=IN&ceid=IN:en
```

3. Moneycontrol market RSS:

```
https://www.moneycontrol.com/rss/marketreports.xml
```

Use a browser User-Agent for both. BSE's API blocks bots; if the user
needs a BSE-only filing, open https://www.bseindia.com/corporates/ann.html
in a browser instead.

## Workflow

1. Get the user's holdings/watchlist (ask, or read `dalal/portfolio.json`
   if it exists).
2. Pull the NSE announcements feed and keep rows matching those symbols.
3. Pull Google News RSS per holding (one request each, a second apart)
   and Moneycontrol once for market-wide items.
4. Report per stock: exchange filings first (official), then press
   headlines, each with date and source. Mark anything earnings-,
   dividend- or management-related as high priority.
5. Write results to `dalal/news.json` for the other skills.
