---
name: dalal-copycat
description: >-
  Copy a big investor or fund in India. India has no 13F filings, so this
  reads the closest public equivalents: NSE shareholding patterns
  (promoter / FII / DII / big public holders, quarterly), mutual fund
  monthly portfolio disclosures (every AMC must publish them), and bulk
  deal history. Rebuilds the target's known holdings as weights the user
  can compare against their own portfolio. Use when the user says "copy
  this fund", "what does HDFC Flexicap hold", "what are FIIs buying",
  "follow a big investor", "copycat portfolio India".
---

# dalal-copycat

Reverse-engineers what the big money in India holds, from public
disclosures. Honest limits first: India has nothing like the US 13F.
Holdings data is quarterly (shareholding patterns) or monthly (mutual
funds), always delayed, and big investors are under no obligation to
explain themselves. Say the as-of date on every number. Analysis only,
not financial advice.

## What you can copy, from where (all free, verified 21 Oct 2026)

1. A listed company's shareholding pattern (who owns it):

```bash
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0 Safari/537.36"
curl -s -c /tmp/nse_ck.txt -A "$UA" "https://www.nseindia.com" -o /dev/null
curl -s -b /tmp/nse_ck.txt -A "$UA" -H "Accept: application/json" \
  "https://www.nseindia.com/api/corporate-share-holdings-master?index=equities&symbol=RELIANCE"
```

Gives promoter / public split by quarter. Screener.in's company page
shows the same history plus FII/DII trend in one table (easier to read):
`https://www.screener.in/company/<TICKER>/consolidated/`.

2. A mutual fund's portfolio (what the fund owns): every AMC publishes a
   monthly portfolio disclosure sheet (XLS) on its own website, linked
   from AMFI. AMFI NAVs for all schemes:
   `https://portal.amfiindia.com/spages/NAVAll.txt`.
   Pick the fund on AMFI, then download the AMC's latest monthly
   portfolio sheet and read the top holdings with weights.

3. Big-ticket recent trades: NSE bulk/block deal data (see
   dalal-bigmoney) shows when a named big investor or fund actually
   bought or sold 0.5%+ of a company.

## Workflow

1. Ask what to copy: a fund (route 2), a famous investor (routes 1+3:
   find companies where they appear in >1% holders or bulk deals), or
   "foreign money" (FII/DII flows in dalal-bigmoney).
2. Rebuild the holdings as a weights table: stock, % of portfolio,
   as-of date, source.
3. Compare two periods if available and call out what was bought,
   added, trimmed, sold.
4. Hand the list to dalal-budget / dalal-risk if the user wants to size
   anything. Copying a disclosure means copying a trade that is weeks
   old - say so every time.
