# Dalal Skills - Indian market pack (adapted from trader-skill)

11 analysis-only skills for NSE/BSE, adapted for India from
github.com/Jakeschincariol/trader-skill (MIT). Original US data sources
(SEC EDGAR, Congress PTRs, NYSE calendar) were swapped for free public
Indian sources verified working on 21 Oct 2026:

- Yahoo Finance chart JSON (.NS / .BO tickers) - delayed quotes
- NSE public JSON APIs (announcements, bulk/block deals, FII/DII,
  holidays, shareholding patterns) - needs the cookie step, see each skill
- Screener.in - fundamentals and screens
- Google News RSS + Moneycontrol RSS - headlines
- AMFI NAVAll + AMC monthly portfolio sheets - mutual fund data

SAFETY: every skill is analysis only. No skill can place an order,
connect to a broker, or move money. Any order is written as a paper
ticket for the user to place by hand in his own app. Nothing here is
financial advice; no outcome is promised.

Install (Cue): Settings > Skills > Add > Import from GitHub, one folder
per import. Or paste a single SKILL.md into a Cue chat to run it as a mode.

## Bonus: website animation skills

Four usage skills from the 20 Oct reel tools (all repos verified live):
webanim-lenis, webanim-gsap, webanim-vanta, webanim-reactbits. These are
guides Cue uses to add the libraries into your website code - they are
not the libraries themselves.
