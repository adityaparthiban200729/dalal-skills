# Dalal Skills - Indian market pack (adapted from trader-skill)

11 skills for NSE/BSE, adapted for India from
github.com/Jakeschincariol/trader-skill (MIT). Original US data sources
(SEC EDGAR, Congress PTRs, NYSE calendar) were swapped for free public
Indian sources verified working on 21 Oct 2026:

- Yahoo Finance chart JSON (.NS / .BO tickers) - delayed quotes
- NSE public JSON APIs (announcements, bulk/block deals, FII/DII,
  holidays, shareholding patterns) - needs the cookie step, see each skill
- Screener.in - fundamentals and screens
- Google News RSS + Moneycontrol RSS - headlines
- AMFI NAVAll + AMC monthly portfolio sheets - mutual fund data

SAFETY: every skill except dalal-ticket is analysis only - it cannot
place an order, connect to a broker, or move money. dalal-ticket
places LIVE orders on the user's own INDstocks account, and only when
ALL of these hold: dalal-risk said PASS, the round-trip fee math
clears, and the user confirmed the exact stock, quantity, price and
total in writing. Login OTP is approved by the user on his own phone.
Cash segment and limit orders only; no F&O, no borrowed money. Nothing
here is financial advice; no outcome is promised.

Install (Cue): Settings > Skills > Add > Import from GitHub, one folder
per import. Or paste a single SKILL.md into a Cue chat to run it as a mode.

## Bonus: website animation skills

Four usage skills from the 20 Oct reel tools (all repos verified live):
webanim-lenis, webanim-gsap, webanim-vanta, webanim-reactbits. These are
guides Cue uses to add the libraries into your website code - they are
not the libraries themselves.
