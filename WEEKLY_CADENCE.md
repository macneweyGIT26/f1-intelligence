# F1 Intelligence — Weekly Cadence

**Last updated:** 2026-03-13

---

## Race Week Rhythm

| Day | Task | Output |
|-----|------|--------|
| **Sunday** | Race day. Capture data, write race analysis. | Race analysis → Vercel |
| **Mon/Tue** | R may share betting info (pics of odds). Identify arbitrage opportunities for race weekend. | Store + analyze. Betting analysis → email to R. |
| **Wednesday** | Pull tyre data from Pirelli (RSS/browser). Pull track data for similar circuits. | Tyre setup file + track comparison |
| **Thu/Fri** | FP1–FP3. Note odds shifts but practice ≠ race pace. | Update report with session data |
| **Qualifying** | Real signal. Odds shift here matters. Update analysis. | Qualifying analysis → Vercel |
| **Race Day** | Capture results. Write post-race analysis. | Post-race recap → Vercel |

## Key Rules

1. **Race analysis and betting analysis are always separate.** Never mix them.
2. **R may not submit bets every race.** May provide late or not at all. Race analysis always happens.
3. **Always anticipate.** Use the F1 calendar to prepare before race week starts.
4. **Update Vercel proactively.** R checks there first.
5. **Betting analysis → email** to neweyai@icloud.com + notify via Telegram.
6. **If R sends bet pics:** Inform of any odds changes since first submission.

## Delivery

| Content | Channel |
|---------|---------|
| Race analysis (public) | Vercel (f1-intelligence.vercel.app) |
| Betting analysis (private) | Email to neweyai@icloud.com |

## Off-Week

- Store any bet info R sends
- Build bare minimum prep for next race
- Start track/tyre research when race week approaches
- Check calendar for session times and timezone differences

## Seasonal Archive

This project is designed to persist across multiple seasons. Structure by round:
- `round-XX-[circuit]/` for each race
- Betting files in `betting/` subfolder
- Season-level files at project root
