# F1 INTELLIGENCE — DEMO TAB ARCHITECTURE (SILVERSTONE 2025)

**Version:** 2.0 (Specification)  
**Status:** Architecture Blueprint (UI Guidance Only — Do NOT Implement Yet)  
**Date:** March 1, 2026  
**Scope:** Silverstone 2025 Demo Tabs Only

---

## PURPOSE

Define tab structure for Silverstone 2025 demo build. Test information density, switching friction, table readability, and engine ranking clarity.

**Do NOT:**
- Implement season navigation yet
- Reorganize file structure yet
- Create category tabs (Drivers, Constructors, Engines)

---

## TOP-LEVEL DEMO TABS (Silverstone Only)

```
[ Overview ]  [ Rankings ]  [ Engine View ]  [ Strategy ]
```

---

## TAB 1 — OVERVIEW (Executive Layer)

**Purpose:** Default landing tab. Board-ready narrative view.

**Default Open:** YES (when viewer loads)

**Content:**

1. **Monday Recap Summary**
   - Championship snapshot (leader, gap, momentum)
   - Previous race winner + podium
   - Key talking point (1–2 sentences)

2. **Previous Race Podium (Top 3)**
   - P1, P2, P3 finishers
   - Gap to winner
   - Tire strategy used

3. **Top 10 Drivers (Current Season Standings)**
   - Rank, Driver, Team, Engine Supplier, Points, Trend

4. **Top 3 Constructors (Current Season Standings)**
   - Rank, Team, Engine, Points, Momentum

5. **All Engine Suppliers Summary**
   - Short profile per supplier (1–2 bullets each)
   - Power philosophy
   - Current season rank

6. **Key Strategic Takeaways (5 bullets max)**
   - What matters for next race
   - Emerging patterns
   - Risk factors

**Format:** Narrative + embedded tables. High-level, digestible.

---

## TAB 2 — RANKINGS (Structured Data Only)

**Purpose:** Pure structured comparison layer. Tables only, no narrative.

**Default Open:** NO (click to activate)

**Content:**

1. **Last Race — Top 10 Drivers**
   | Pos | Driver | Team | Engine | Gap | Tire Strategy |

2. **Current Season — Top 10 Drivers**
   | Rank | Driver | Team | Engine | Points | Trend |

3. **Last Race — Top 10 Constructors**
   | Rank | Team | Engine | Points | Both Finished? |

4. **Current Season — Top 10 Constructors**
   | Rank | Team | Engine | Points | Podiums | Wins | Momentum |

5. **Engine Supplier Ranking — Previous Race**
   | Rank | Engine | Total Points | Avg Finish | DNFs | Reliability % |

6. **Engine Supplier Ranking — Current Season**
   | Rank | Engine | Total Points | Podiums | Wins | Avg Finish | Reliability Score |

**Format:** Tables only. No commentary. Pure data.

---

## TAB 3 — ENGINE VIEW (Power Unit Intelligence Layer)

**Purpose:** Dedicated engine analysis. Power-unit competitive lens.

**Default Open:** NO

**Content:**

1. **Race Ranking by Engine Supplier**
   - Combined team points
   - Average finishing position
   - DNF count + causes
   - Reliability %

2. **Season Ranking by Engine Supplier**
   - Total points (cumulative)
   - Podiums + Wins
   - Reliability trend (improving/declining)
   - Momentum (3-race average)

3. **Reliability Comparison**
   - Engine-by-engine DNF analysis
   - Failure types (thermal, ERS, fuel, mechanical)
   - Season trend

4. **Performance Characteristics Summary**
   - Straight-line speed delta (vs reference)
   - ERS efficiency
   - Thermal management profile
   - Cold-weather response

5. **Track Archetype Fit Notes**
   - High-speed circuits: Which engines excel?
   - Technical circuits: Which engines struggle?
   - High-degradation: Thermal constraint impact?
   - Cold-climate: Warm-up lag by engine?

**Format:** Tables + short analytical notes. Engine-centric narrative.

---

## TAB 4 — STRATEGY (Technical Layer)

**Purpose:** Deep technical analysis. Strategist brain mode.

**Default Open:** NO

**Content:**

1. **Track Technical Breakdown**
   - Corner-speed mix (% high-speed, medium, technical)
   - Overtake difficulty (DRS zones)
   - Tire degradation profile by compound

2. **Suitability Matrix (Team vs Track)**
   - High-speed aero strength
   - Low-speed grip
   - Tire management capability
   - Engine power match
   - Overall track fit score (0–10)

3. **Forecast vs Actual Comparison**
   - Qualifying deltas (forecast vs actual)
   - Win probabilities (forecast vs result)
   - Podium predictions (correct/miss)
   - Betting value calls (edge, outcome)

4. **Weather Impact Analysis**
   - Wind sensitivity (which cars vulnerable?)
   - Temperature effects (tire warm-up lag by setup)
   - Rain scenario (probability + impact)

5. **Lessons Learned**
   - What the ranking model got right
   - What it got wrong (refinements)
   - Confidence calibration updates
   - New variables to track

**Format:** Tables + analytical narrative. Strategic depth.

---

## INFORMATION FLOW

**Typical User Journey:**

1. **Enter viewer** → Lands on Overview tab (executive summary)
2. **Want more detail?** → Click Rankings tab (data verification)
3. **Engine question?** → Click Engine View tab (power-unit analysis)
4. **Deep dive needed?** → Click Strategy tab (technical full picture)

---

## DESIGN PRINCIPLES

### 1. Layer by Intelligence Type (NOT Category)

❌ **Wrong:** [ Drivers ] [ Constructors ] [ Engines ]
- Fragments workflow
- Forces navigation jump between related concepts

✅ **Right:** [ Overview ] [ Rankings ] [ Engine View ] [ Strategy ]
- Flows by analytical depth
- User stays in coherent journey
- No topic jumping

### 2. Minimize Switching Friction

- Tab bar always visible (top of page)
- Instant switching (no page reload)
- URL updates (shareable tabs: `?tab=rankings`)
- Scroll position resets (new tab = fresh view)

### 3. Table-First for Rankings Tab

- No prose in Rankings tab
- Pure comparison layer
- User scans quickly
- Copy/paste friendly for external reports

### 4. Narrative-First for Overview Tab

- Summary statistics
- Key insights
- Strategic context
- "Send to CEO" ready

---

## VALIDATION GOALS

This demo tab structure tests:

1. **Information Density** — Can 4 tabs hold Silverstone complexity?
2. **Switching Friction** — Is clicking between tabs natural or annoying?
3. **Table Readability** — Are tables easy to scan? Cols legible?
4. **Engine Ranking Clarity** — Does Engine View explain power-unit competition?
5. **Layer Coherence** — Does Overview → Rankings → Engine View → Strategy flow logically?

---

## FILE SOURCE MAPPING

**Data pulled from existing REBUILD_v2_RANKING_LAYER.md:**

| Tab | Source Section |
|-----|-----------------|
| Overview | Sections 1–6 summary + Section 10 (Forecasts) |
| Rankings | Sections 1–3 (all ranking tables) |
| Engine View | Section 3 (Engine Supplier Ranking full) |
| Strategy | Sections 7–13 (Circuit, Suitability, Forecasts, Strategy, Betting, Post-Race) |

**No new data generation needed.** Extract + reformat existing REBUILD_v2 content into tab structure.

---

## IMPLEMENTATION NOTES (When Ready)

1. **Extract data** from REBUILD_v2_RANKING_LAYER.md
2. **Create 4 tab panel sections** in `viewer.html`
3. **Add CSS** for tab styling (active/inactive)
4. **Add JavaScript** for tab switching
5. **Test navigation** (all tabs, URL params)
6. **Deploy to Vercel**

**NOT YET:** Do this later. This is architecture guidance only.

---

## SCOPE BOUNDARIES

**This demo focuses on Silverstone 2025 only.**

**Do NOT yet:**
- Build Australia 2026 tabs
- Create season-wide navigation
- Reorganize `/projects/f1-intelligence/` structure
- Add per-race tab groups

**Future (after Silverstone demo validated):**
- Expand to Australia, Bahrain, etc.
- Build season-wide comparison tabs
- Add dynamic race selector
- Create live race view tabs (FP2, Quali, Race)

---

## SUMMARY

**4 Tabs, 1 Demo, 1 Purpose:**

1. **Overview** — Executive summary (board-ready)
2. **Rankings** — Data verification (tables only)
3. **Engine View** — Power-unit intelligence
4. **Strategy** — Technical deep-dive

**Flow:** Shallow → Deep → Specialized → Comprehensive

**Status:** Architecture defined. Ready for implementation when approved.

---

**Document Type:** UI Architecture Specification  
**Audience:** Implementation team (when building `viewer.html` tabs)  
**Do NOT Implement Yet:** This is guidance. Demo validation still in progress.
