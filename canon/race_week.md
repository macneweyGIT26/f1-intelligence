# F1 RACE WEEK OPERATING CANON

**Last Updated:** 2026-03-23 17:57 EDT  
**Status:** Active, locked  
**Authority:** User-confirmed operating truth

---

## 2026 F1 Schedule (Operating Truth)

### Active Rounds
- **R3: Japan (Suzuka)** — Mar 27–29, 2026 — ACTIVE ✅
- **R6: Miami** — May 1–3, 2026 — NEXT ACTIVE RACE ✅

### Cancelled / Non-Operating (Public Calendar Only)
- **R4: Bahrain** — Apr 10–12, 2026 — LISTED publicly, NOT RUNNING
  - Note: May appear on FIA calendars for legal/contractual reasons
  - No race-week workflow
  - No betting memo
  - Do NOT prepare analysis unless user reactivates
- **R5: Saudi Arabia** — Apr 17–19, 2026 — LISTED publicly, NOT RUNNING
  - Note: May appear on FIA calendars for legal/contractual reasons
  - No race-week workflow
  - No betting memo
  - Do NOT prepare analysis unless user reactivates

### Source Priority Rule
1. **User-confirmed operating status** (highest authority)
2. **Actual event scheduling** (what races actually happen)
3. **Public calendar listings** (legal/contractual reference only, not operational truth)

**When public calendar conflicts with user-confirmed status:**
- Canon uses user-confirmed status for workflow/automation
- Public listings noted for transparency, not action

---

## 2026 Regulation Context

**Regulation Era:** New power unit era (2026+)

**Key principles:**
- Cars and strategy treated as fresh regime
- Reduced reliance on pre-2026 historical comparisons
- Prioritize current 2026 session data

**Historical data weight:**
- ✅ Track characteristics (overtaking, tyre stress, weather patterns)
- ✅ Similar-track archetypes
- ❌ Race pace expectations (new regulation)
- ❌ Reliability patterns (new power units)
- ❌ Energy/recharge strategy (new regulations)

---

## Race Week Mandate

### Two Parallel Tracks

**Track 1: Public F1 Analysis**
- Purpose: Strategic analysis, competitive reads, predictions
- Output: Vercel + public-facing markdown
- Content: Pace reads, strategy forecasts, race recaps, regulation notes
- **NEVER includes:** Odds, betting, wager sizing, sportsbook references

**Track 2: Private Betting Analysis**
- Purpose: Market analysis, position management, edge hunting
- Output: Internal-only markdown (never published)
- Content: Odds, positions, cash-out rules, P&L tracking
- **NEVER publish externally under any circumstances**

---

## Race Format Logic

**Standard Weekend:**
- FP1 / FP2 (Fri) → FP3 / Qualifying (Sat) → Race (Sun)
- Workflow: Three practice → qualifying → race

**Sprint Weekend:**
- Compressed FP (Fri) → Sprint Qualifying (Sat AM) → Sprint (Sat PM) → Qualifying (Sat PM) → Race (Sun)
- Workflow: Limited practice → sprint result informs race expectations

**Rule:** Explicitly classify weekend format before executing workflow.

---

## Tyre Workflow

**At start of each race week:**
1. Fetch official Pirelli / F1 tyre compounds
2. Log compounds in race-week prep note
3. Compare to previous rounds and similar archetypes
4. Update likely degradation / strategy scenarios
5. Revise forecasts after practice long runs

**Rule:** Do NOT assume tyre compounds. Mark as "pending" if not yet confirmed.

---

## Data Hierarchy for Predictions

**Highest weight:**
1. 2026 current season results
2. Current round session data (FP1/FP2/FP3, qualifying, sprint)
3. Tyre compounds (official confirmation)
4. Current regulation / reliability state
5. Weather + penalties

**Medium weight:**
- Similar-track results from 2026
- Same-team, same-driver recent form
- Current market movement

**Lower weight:**
- Pre-2026 comparable tracks (reference only, not prediction)

---

## Betting Operation Rules

**Budget:** $40–50 per race week (some weeks may skip)

**Early-week objective:** Attack stale Mon/Tue prices before line movement

**Position structure:** Double-bet approach (selective cash-out vs. upside riding)

**Cash-out rules:** Defined BEFORE placing (not reactive)

**Betting disclaimer:** All analysis is internal model opinion only, NOT gambling advice. User makes all decisions.

---

## Automation Triggers

**Monday:** Verify round, format, tyres; create race-week memo; prompt for odds screenshots

**Post-Practice:** Prompt for mid-week pace update

**Post-Qualifying:** Prompt for pre-race final note

**Post-Race:** Prompt for debrief within 24h

---

## Storage Paths (Reference Only)

For actual locations, see `/Users/newey/.openclaw/workspace/projects/f1-intelligence/` structure:
- Canon: `canon/` (source of truth)
- Templates: `templates/` (public + private)
- Rounds: `rounds/` (current round working files)
- Betting: `betting/` (archived memo files)

---

## Quality Standards

- Pace reads account for fuel load artifact
- Strategy forecasts explain pit windows + undercut/overcut logic
- Betting rationale states edge clearly
- Signal confidence always stated
- Tables preferred over text blocks
- External sources linked where appropriate

---

**Authority:** User (2026-03-23)  
**Next review:** Post-Japan debrief  
**Questions:** See SKILL.md (skills/f1-race-week/SKILL.md)
