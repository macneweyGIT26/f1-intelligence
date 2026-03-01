# Tyre Week Monitoring Workflow

**Purpose:** Auto-populate TYRE WEEK SETUP section in Halo tab when Pirelli releases compound nominations.

**Frequency:** Every Tuesday/Wednesday (during F1 race weekends)

**Source:** Pirelli F1 RSS Feed (official)

---

## Workflow Steps

### Step 1: Check Pirelli RSS Feed
**URL:** `https://www.pirelli.com/en-EN/rss/formula1` (or current Pirelli F1 RSS endpoint)

**Timing:** Tuesday or Wednesday morning (compounds usually released midweek before Friday qualifying)

**Search for keywords in new items:**
- "tyre range" OR "compound choices"
- Track name: "Australia" OR "Melbourne" OR "Albert Park" (varies by race)
- Confidence check: Pirelli official source, dated this week

### Step 2: Extract Compound Nominations
When found, extract **three compounds:**
- Soft (red)
- Medium (yellow)
- Hard (white)

**Format captured:**
```
Soft: RED
Medium: YELLOW
Hard: WHITE
```

### Step 3: Assess Strategic Implications

Fill in the Halo TYRE WEEK SETUP section:

| Field | Source |
|-------|--------|
| **Compound nominations** | Pirelli press release |
| **Strategy bias** | Analyze qual pace (soft advantage) vs race durability (hard advantage) |
| **Warm-up vs deg risk** | Soft = quick warm-up, high deg; Hard = slower warm-up, low deg |
| **Qualifying vs race tradeoff** | Soft for pole, hard for longevity; medium = balanced |

**Quick assessment template:**
- If **soft advantage >0.8 sec in qual**: Expect pole-sitter to run soft in Q3
- If **hard compound durable >10 laps vs medium**: Teams may run hard first stint
- If **medium is "Goldilocks"**: Balanced quali pace + race pace likely

### Step 4: Update Halo Tab
**File:** `/round-01-australia/halo.html`

**Section to update:** "Tyre Week Setup (Pirelli)" table

**Replace placeholder "—" with:**
- Soft nomination + strategic note
- Medium nomination + strategic note
- Hard nomination + strategic note

**Example:**
```html
<tr>
    <td><strong>Soft</strong></td>
    <td>RED (aggressive compound)</td>
    <td>Qualifying pace edge; ~0.8 sec/lap advantage. High degradation (est. 3-4 laps race-sim). Pole strategy likely.</td>
</tr>
```

### Step 5: Add Press Release Link
**Add below the tyre table:**
```markdown
**Source:** [Pirelli Official Press Release — Australia 2026 Tyre Range](https://pirelli-press-link-here)  
**Released:** 2026-03-__ (date)
```

### Step 6: Commit & Deploy
```bash
git add round-01-australia/halo.html
git commit -m "UPDATE: Pirelli tyre nominations (Soft/Medium/Hard) — Strategy bias + qual/race tradeoff added"
git push origin main
```

**Live Update:** Vercel auto-deploys; changes live within 60 seconds.

---

## Quick Reference: Compound Characteristics

| Compound | Char | Qual Pace | Race Durability | Warm-up | Deg |
|----------|------|-----------|-----------------|---------|-----|
| **Soft** | Aggressive | +0.6–0.8 sec | Low (3–4 laps) | Fast | High |
| **Medium** | Balanced | Baseline | Medium (8–12 laps) | Medium | Medium |
| **Hard** | Durable | -0.3–0.5 sec | High (15+ laps) | Slow | Low |

---

## Checklist (Weekly)

- [ ] **Tuesday morning:** Check Pirelli RSS feed for Australia/Melbourne tyre range announcement
- [ ] **If found:**
  - [ ] Extract Soft / Medium / Hard nominations
  - [ ] Assess strategy bias (qual pace vs race durability)
  - [ ] Note warm-up vs deg risks
  - [ ] Update Halo TYRE WEEK SETUP table with nominations + implications
  - [ ] Add press release link + release date
  - [ ] Commit & push to GitHub
- [ ] **If not found by Wednesday:**
  - [ ] Check again Thursday morning (rare delay)
  - [ ] If still not available, keep placeholder "— (Awaiting Pirelli release)"

---

## Storage Location
- **Master source:** `/round-01-australia/halo.html` (Tyre Week Setup section)
- **Tracking:** This file (TYRE_WEEK_MONITORING.md)
- **History:** Git commit history (all updates versioned)

---

## Notes
- Pirelli typically releases compounds **4–5 days before race Friday** (Tuesday/Wednesday for Sunday races)
- Compounds vary by track (soft/medium/hard always; sometimes "intermediate" if wet expected)
- **Do NOT use tyre choice data for momentum/trend calculations** (week-specific context only)
- **Rule:** Tyre strategy is tactical input, not strategic prediction tool

---

**Last Updated:** 2026-03-01T18:06 EST  
**Next Check:** Tuesday (during Australia race week, ~2 weeks away)
