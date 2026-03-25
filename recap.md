# F1 Intelligence — Project Status

**Last Updated:** 2026-03-23 18:00 EDT  
**Current Season:** Formula 1, 2026  
**Status:** Active, Japan race week in progress

---

## Current Round

- **Round:** R3 — Japan (Suzuka)
- **Weekend:** Mar 27–29, 2026
- **Format:** Standard (FP1/FP2/FP3 → Qualifying → Race)
- **Status:** Pre-race (practice sessions TBD)
- **Working file:** `rounds/2026-r03-japan.md`

---

## Next Active Race

- **Round:** R6 — Miami
- **Weekend:** May 1–3, 2026
- **Status:** Scheduled (no prep started)

---

## Cancelled / Non-Running

- **R4 Bahrain** (Apr 10–12) — Listed on public calendar, NOT running
- **R5 Saudi Arabia** (Apr 17–19) — Listed on public calendar, NOT running

---

## Project Structure

```
projects/f1-intelligence/
├── recap.md                          (this file — project status)
├── canon/
│   └── race_week.md                 (operating canon: rules, schedule, mandate)
├── templates/
│   ├── public_race_analysis.md      (public analysis template)
│   └── private_betting_memo.md      (private betting template)
├── rounds/
│   └── 2026-r03-japan.md            (current round working file)
└── [skills/f1-race-week/ linked externally]
```

---

## Content Separation

### Public (Vercel)
- Race recaps (session summaries, results, analysis)
- Regulation notes (FIA changes, directives, penalties)
- Performance tables (pace rankings, tyre data, team form)
- Strategy forecasts (non-betting predictions)
- Dashboard updates (visuals, signal cards, tables)

### Private (Internal Only)
- Betting memo (odds, positions, cash-out rules, P&L)
- Odds screenshots (never published)
- Position sizing logic
- Bankroll notes
- Variance play rationale

**Rule:** Betting analysis NEVER published externally.

---

## Open Items

### Japan Round
- [ ] Official tyre compounds — pending Pirelli confirmation
- [ ] Operator odds screenshots — awaiting user submission
- [ ] Monday trigger automation — not yet built
- [ ] Friday/Saturday odds updates — pending live session data
- [ ] Post-race debrief template — ready, awaiting results

### Vercel UI / Dashboard Enhancement
- [ ] Add track layout + tyre compound block to Vercel race pages
- [ ] Fetch official F1 circuit SVG assets per round (start with Japan)
- [ ] Display alongside tyre compounds as static reference card
- [ ] Repeat for all 2026 rounds (automated acquisition)

### Post-Japan / Miami Prep
- [ ] Miami tyre compounds — TBD
- [ ] Miami market baseline — TBD

---

## Automation Status

**Ready:**
- ✅ Betting memo template (templates/private_betting_memo.md)
- ✅ Public analysis template (templates/public_race_analysis.md)
- ✅ Canon rules + schedule (canon/race_week.md)
- ✅ SKILL.md triggers documented

**Not yet built:**
- ❌ Monday cron trigger (verify round, fetch tyres, create memo, prompt for odds)
- ❌ Post-practice trigger (prompt for mid-week update)
- ❌ Post-quali trigger (prompt for pre-race final note)
- ❌ Post-race trigger (prompt for debrief within 24h)

---

## Betting Budget

**Weekly F1 racing betting budget:** $30–40

**Early-week budget (Mon/Tue):** $30–40 for stale market prices before line movement

**Allocation per race week:**
- Early week (Mon/Tue): $30–40 (stale market prices — main opportunity)
- Mid-week (Wed/Fri): Adjustments within weekly total (practice/sprint updates)
- Saturday (Quali): Final refinements within budget
- Sunday (Race): First lap, hedges, buffer (if budget allows)

**Some weeks may skip** if travel, timing, or lack of edge.

---

## Key Rules (Short Reference)

For detailed rules, see `canon/race_week.md`.

- **One canonical truth per concept** (no duplication)
- **Templates are reusable forms** (not live data)
- **Rounds are working files** (deleted after race)
- **Screenshots don't count until converted to markdown**
- **Betting analysis NEVER published externally**
- **User-confirmed race status overrides public calendar**

---

## Next Steps

1. **Operator provides Japan odds screenshots** → convert to markdown in R03 memo
2. **Pirelli confirms tyre compounds** → update canon + R03 memo
3. **Friday FP1/FP2 complete** → populate mid-week update
4. **Saturday qualifying done** → populate pre-race final note
5. **Sunday race complete** → populate post-race review within 24h
6. **Debrief logged** → start Miami prep (or skip if cancelled)

---

**Authority:** User (2026-03-23)  
**Questions:** See canon/race_week.md or skills/f1-race-week/SKILL.md
