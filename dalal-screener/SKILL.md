---
name: dalal-screener
description: >-
  Screen Indian stocks against the user's own rules and rank what
  passes. Uses Screener.in's public screens and company data
  (PE, ROCE, growth, debt) plus delayed Yahoo quotes for current prices.
  Use when the user says "find me cheap stocks", "screen for", "good
  companies under Rs X", "shortlist NSE stocks".
---

# dalal-screener

Screens Indian companies against rules the user sets. Analysis only,
not financial advice. Passing a screen means "worth a closer look",
never "buy".

## How

1. Turn the user's words into concrete rules: max PE, min ROCE, max
   debt-to-equity, min sales growth, market-cap floor. Confirm the rules
   back in one line before running.
2. Data: Screener.in (browser UA, one page at a time). Its public
   screens gallery (https://www.screener.in/screens/) already encodes
   common rule sets; the company pages carry every ratio needed to apply
   custom rules to a shortlist. For a handful of named companies, fetch
   each page and filter locally.
3. Prices: Yahoo chart JSON (`.NS`), see dalal-alerts. Screener
   ratios are computed off recent prices anyway; refresh only if the
   user asks for today's price.
4. Rank the passes by the rule the user cares most about, show the
   table with the numbers that decided each rank, and note the data
   date. Hand any pick to dalal-analyst for a closer read, then
   dalal-budget and dalal-risk if the user wants to size it.

## Limits to state

Fundamentals data lags (last reported quarter/year). A screen cannot
see fraud, governance problems or one-off results - that is what
dalal-analyst and dalal-news are for.
