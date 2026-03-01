# F1 Strategic Intelligence — Architecture Blueprint

**Version:** 2.0 (Ranking Layer Upgrade)  
**Status:** Validation Phase  
**Last Updated:** March 1, 2026  
**Domain:** F1 Intelligence Demo Validation (Silverstone 2025, 2026 Engine Mapping Applied)

---

## CORE PRINCIPLE

**"Branch when domain changes. DO NOT branch when depth increases."**

The Ranking Layer upgrade adds depth to F1 Intelligence without changing domain. No path reorganization during validation phase. All builds stay in current structure until production hardening begins.

---

## LAYERED ARCHITECTURE

### Layer 1: Ranking (Top Priority — Data First)
Centralized view of driver/constructor/engine supplier performance across three time horizons:
- Last race result
- Current season standing
- Trend analysis

**Purpose:** Establish the competitive hierarchy before strategy analysis.

### Layer 2: Strategy (Analytical)
Circuit profile, team suitability, forecasts, betting value.

**Dependency:** Uses Ranking Layer output to weight probabilities (e.g., "McLaren rising in constructor rankings → higher win % confidence").

### Layer 3: Execution (Tactical)
Live updates, pit window calls, race morning alerts.

**Dependency:** Uses both Ranking + Strategy layers for decision-making.

---

## MONDAY MASTER RECAP — NEW STRUCTURE

**Total Sections: 13** (6 Ranking + 7 Strategy)

### SECTION 1: DRIVER RANKING MODE

#### A) Last Race — Top 10 Finishers

| Pos | Driver | Team | Engine Supplier | Gap to Winner | Tire Strategy | Notes |
|-----|--------|------|-----------------|---------------|---------------|-------|
| 1 | [Name] | [Team] | [Engine] | — | [Strategy] | Winner |
| 2 | [Name] | [Team] | [Engine] | +[Gap] | [Strategy] | [Notes] |
| ... | ... | ... | ... | ... | ... | ... |
| 10 | [Name] | [Team] | [Engine] | +[Gap] | [Strategy] | [Notes] |

**Data Sources:** FIA official race result, OpenF1 API (pit stops, tyre info)

#### B) Current Season — Top 10 Standings

| Rank | Driver | Team | Engine Supplier | Points | Trend | Notes |
|------|--------|------|-----------------|--------|-------|-------|
| 1 | [Name] | [Team] | [Engine] | [Points] | ↑/↓/— | [Momentum] |
| 2 | [Name] | [Team] | [Engine] | [Points] | ↑/↓/— | [Momentum] |
| ... | ... | ... | ... | ... | ... | ... |
| 10 | [Name] | [Team] | [Engine] | [Points] | ↑/↓/— | [Momentum] |

**Trend:** ↑ Rising (avg +X points/race last 3 races) | ↓ Falling (avg -X points/race) | — Stable

**Data Sources:** FIA official standings, Brave Search (verification)

#### C) Previous Race — Full Result Table (Complete Classification)

| Pos | Driver | Team | Engine | Laps | Time/Retired | DNF Reason | Tire Strategy |
|-----|--------|------|--------|------|--------------|-----------|---------------|
| 1 | [Winner] | [Team] | [Engine] | [Laps] | [Time] | Finished | [Strategy] |
| 2 | [2nd] | [Team] | [Engine] | [Laps] | +[Gap] | Finished | [Strategy] |
| ... | ... | ... | ... | ... | ... | ... | ... |
| DNF | [Driver] | [Team] | [Engine] | [Lap] | [Reason] | [Type] | [Last tire] |

**Purpose:** Complete competitive picture for modeling accuracy (who finished, who didn't, why).

**Data Sources:** FIA official race classification, OpenF1 API (retirements), Race control messages

---

### SECTION 2: CONSTRUCTOR RANKING MODE

#### A) Last Race — Top 10 Constructors

| Rank | Team | Engine Supplier | Points Scored | Both Cars Finished? | Avg Finishing Position |
|------|------|-----------------|----------------|-------------------|----------------------|
| 1 | [Team] | [Engine] | [Points] | Yes/No | [Avg Pos] |
| 2 | [Team] | [Engine] | [Points] | Yes/No | [Avg Pos] |
| ... | ... | ... | ... | ... | ... |
| 10 | [Team] | [Engine] | [Points] | Yes/No | [Avg Pos] |

**Data Sources:** FIA official race result (team points), OpenF1 API

#### B) Current Season — Top 10 Constructors

| Rank | Team | Engine Supplier | Points | Podiums | Wins | 3-Race Momentum | Reliability Score |
|------|------|-----------------|--------|---------|------|-----------------|------------------|
| 1 | [Team] | [Engine] | [Points] | [Count] | [Count] | ↑/↓/— | [Score %] |
| 2 | [Team] | [Engine] | [Points] | [Count] | [Count] | ↑/↓/— | [Score %] |
| ... | ... | ... | ... | ... | ... | ... | ... |
| 10 | [Team] | [Engine] | [Points] | [Count] | [Count] | ↑/↓/— | [Score %] |

**3-Race Momentum:** Avg points per race (last 3 races) → compare to season average

**Reliability Score:** (Races Completed / Races Entered) × 100%

**Data Sources:** FIA official standings, OpenF1 API

---

### SECTION 3: ENGINE SUPPLIER RANKING MODE (NEW CORE LAYER)

#### A) Previous Race — Engine Ranking

| Rank | Engine Supplier | Total Points | Avg Finishing Position | DNFs | Reliability % |
|------|-----------------|---------------|----------------------|------|--------------|
| 1 | [Engine] | [Points] | [Avg] | [Count] | [%] |
| 2 | [Engine] | [Points] | [Avg] | [Count] | [%] |
| 3 | [Engine] | [Points] | [Avg] | [Count] | [%] |
| 4 | [Engine] | [Points] | [Avg] | [Count] | [%] |
| 5 | [Engine] | [Points] | [Avg] | [Count] | [%] |

**Calculation:**
- Total Points: Sum of all team points using that engine
- Avg Finishing Position: Mean of all finishers using that engine (DNFs excluded from avg, but counted separately)
- DNFs: Count of retirements attributable to engine (power unit, ERS, fuel system)
- Reliability %: (Races Completed / Races Entered) × 100%

**Data Sources:** FIA race result, OpenF1 API, Race control messages

#### B) Current Race Snapshot (Live Mode, If Active)

| Rank | Engine Supplier | Avg Running Position | Reliability Alerts | Notes |
|------|-----------------|----------------------|-------------------|-------|
| 1 | [Engine] | [Avg Pos] | [Alert] | [Notes] |
| 2 | [Engine] | [Avg Pos] | [Alert] | [Notes] |
| ... | ... | ... | ... | ... |

**Reliability Alerts:** Flag any ERS issues, fuel system warnings, thermal management concerns (from team radio, race control messages)

**Usage:** Updated during race (Mode 2 live updates); helps interpret pit decisions, strategy changes

**Data Sources:** OpenF1 API (live positions), FIA race control, Team radio context

#### C) Season Ranking — Engine Suppliers

| Rank | Engine Supplier | Total Points | Podiums | Wins | Avg Finish | Reliability Score | Momentum (3-race) |
|------|-----------------|--------------|---------|------|-----------|------------------|------------------|
| 1 | [Engine] | [Points] | [Count] | [Count] | [Avg] | [%] | ↑/↓/— |
| 2 | [Engine] | [Points] | [Count] | [Count] | [Avg] | [%] | ↑/↓/— |
| ... | ... | ... | ... | ... | ... | ... | ... |

**Purpose:** Identify engine supplier performance trends across the season. Reveals which power units are improving/declining and reliability patterns.

**Data Sources:** FIA standings (season), OpenF1 API, cumulative race data

---

### SECTION 4: TOP 10 DRIVER PROFILE SNAPSHOT

**For each Top 10 Driver (ranked by season points):**

**Format:**

```
[Rank] [Driver Name] — [Team] | [Engine Supplier]
├─ Strength Type: [Quali/Tire Mgmt/Racecraft/Consistency/etc.]
├─ Current Form: [↑ Rising/↓ Falling/— Stable] (3-race momentum)
├─ Engine Partnership: [Engine] (reliability score vs team average)
├─ Track Suitability (Upcoming Race): [High/Medium/Low fit] + [Brief reason]
└─ Notes: [Any recent standout moments or concerns]
```

**Example:**

```
1. Max Verstappen — Red Bull Racing | Ferrari
├─ Strength Type: Racecraft + High-speed efficiency
├─ Current Form: ↑ Rising (+12 pts/race avg last 3)
├─ Engine Partnership: Ferrari (98% reliability vs team 96%)
├─ Track Suitability (Silverstone): High — RBR aero advantage, engine power + cooling strong
└─ Notes: Dominant on high-speed circuits; pit discipline excellent
```

**Data Sources:** FIA standings, OpenF1 API (lap times, tyre data), Brave Search (recent performance context)

---

### SECTION 5: TOP 3 CONSTRUCTOR STRATEGIC PROFILE

**For each Top 3 Team (ranked by constructor points):**

**Format:**

```
[Rank] [Team Name] — [Engine Supplier]
├─ Aero Strength: [Description of wing setup, downforce philosophy, wind sensitivity]
├─ Engine Characteristics: [Power deployment, ERS efficiency, thermal mgmt style]
├─ Tire Behavior: [Warm-up style, deg profile, pit strategy preference]
├─ Development Direction: [Recent updates, focus area, projected strength]
├─ Wind Sensitivity: [High/Medium/Low] + [Mechanism]
└─ Upcoming Race Suitability: [High/Medium/Low fit] + [Key factor]
```

**Example:**

```
1. Red Bull Racing — Ferrari
├─ Aero Strength: Extreme high-speed dominance (98/100); DRS straight +0.5 sec vs grid avg
├─ Engine Characteristics: Ferrari power deployment strong (0.2 sec/lap on straights); ERS efficiency good (95%)
├─ Tire Behavior: Prefers medium tire long-run management; deg control excellent
├─ Development Direction: Focus on low-speed grip upgrade (via suspension); aero efficient
├─ Wind Sensitivity: High (SW tailwind at Hangar = +0.3 sec advantage; headwind at Copse = -0.2 sec penalty)
└─ Upcoming Race (Silverstone): High fit — 70% aero-dominant lap; pit discipline historically strong
```

**Data Sources:** FIA data, OpenF1 API, Brave Search (team principal quotes, technical updates)

---

### SECTION 6: ALL ENGINE SUPPLIER STRATEGIC PROFILE

**For each engine supplier (Ferrari, Mercedes, Honda, Renault, Audi):**

**Format:**

```
## [Engine Supplier Name]

**Power Unit Philosophy:** [One sentence describing design approach]

**Strengths:**
- [Deployment style] (e.g., "Aggressive mid-range torque")
- [Efficiency characteristic] (e.g., "ERS recovery excellent in high-deg zones")
- [Reliability pattern] (e.g., "Rare thermal issues; strong failure prediction")

**Weaknesses:**
- [Issue] (e.g., "Cold-weather warm-up lag")
- [Limitation] (e.g., "ERS deployment limited in fuel-save mode")

**Track Archetype Fit:**
- **High-speed circuits** (e.g., Silverstone, Monza): [Fit level + reason]
- **Technical circuits** (e.g., Hungary, Singapore): [Fit level + reason]
- **High-degradation circuits** (e.g., Spain): [Fit level + reason]
- **Cold-climate circuits** (e.g., Canada): [Fit level + reason]

**Momentum:** [Season ranking + trend]
```

**Example:**

```
## Ferrari

**Power Unit Philosophy:** Maximum straight-line speed via aggressive deployment; trade reliability for peak power.

**Strengths:**
- Straight-line acceleration (top speed +2 km/h vs Mercedes avg)
- High-load corner power delivery (Monza strong)
- Grid power advantage in qualifying

**Weaknesses:**
- Thermal management (runs hot, limits deployment duration in races)
- Cold-weather lag (needs 2–3 more laps to reach peak in cool temps)
- ERS efficiency lower (5% below Mercedes avg)

**Track Archetype Fit:**
- High-speed (Silverstone, Monza): High fit — straight-line speed dominant
- Technical (Hungary, Singapore): Medium fit — thermal constraints limit deploy
- High-degradation (Spain): Low fit — cooling challenged; deg control harder
- Cold-climate (Canada): Low fit — warm-up lag costly

**Momentum:** 3rd season ranking; ↓ Falling (-8 pts/race avg vs season avg)
```

**Data Sources:** FIA data, Brave Search (team engineering articles), OpenF1 API (lap data by engine)

---

## SECTIONS 7–13: STRATEGY LAYERS (Existing)

After Ranking Layer (Sections 1–6), proceed with existing 7 strategy sections:

7. **Circuit Technical Profile**
8. **Team/Car Suitability Matrix** (now weighted by Ranking Layer insights)
9. **Regulation Reality Check**
10. **Forecasts** (Win/Podium/Top 6 + SC likelihood)
11. **Strategy Baseline + Alternates**
12. **Value Lens** (Betting discipline)
13. **Post-Race Evaluation** (Accuracy validation)

---

## 2026 ENGINE SUPPLIER MAPPING (Demo Mode)

**For 2025 Silverstone Demo with 2026 logic applied:**

| Engine Supplier | 2025 Grid Teams (Demo Mapping) | 2026 Actual |
|-----------------|--------------------------------|------------|
| **Ferrari** | Ferrari, Haas | Ferrari, Haas, Sauber |
| **Mercedes** | Mercedes, Aston Martin, McLaren (partial) | Mercedes, Aston Martin, McLaren, Williams |
| **Honda** | Red Bull, AlphaTauri | Red Bull, RB (formerly AlphaTauri) |
| **Renault** | (2025: None; relabeled Alpine) | Alpine, Renault Sport |
| **Audi** | (2025: None; future) | **Sauber (2026 entry)** |

**Demo Instruction:** Use above mapping for 2025 Silverstone demo (even if not historically accurate for 2025). Purpose: Build framework, not historical accuracy. Framework validates; mapping can shift later.

---

## DATA INTEGRITY RULES

### Flagging Criteria

**Critical Threshold: >2 lap gap** between data sources

**Action:**
1. Flag: "Data integrity concern"
2. Reduce confidence to LOW
3. Pause predictive modeling
4. Cross-check against secondary source (F1.com, ESPN)

### Allowed Data Sources

✅ **Permitted:**
- Brave Search API (primary for context/news)
- OpenF1 API (primary for telemetry)
- FIA official timing archives (post-race validation)
- Internal dashboard data (prior week builds, trend data)

❌ **Not Allowed:**
- ESPN (delayed, secondary only)
- Twitter/X (unverified, social noise)
- Unverified social sources (random accounts, speculation)

### Conflict Resolution

**If classification differs between sources:**
- Use FIA official (most authoritative)
- Flag source of discrepancy
- Reduce confidence accordingly
- Document in notes section

---

## VALIDATION CHECKPOINT

**Silverstone 2025 Demo (Current Validation Build):**

- [ ] Ranking Layer (6 sections) implemented
- [ ] 2026 engine mapping applied to 2025 grid
- [ ] All tables populated with real Silverstone data
- [ ] Driver profile snapshot (top 10) completed
- [ ] Constructor strategic profile (top 3) completed
- [ ] Engine supplier profile (all 4–5) completed
- [ ] Data integrity checks passed (no >2 lap gaps)
- [ ] Forecast accuracy validated against actual result

**Status:** TBD (rebuilding demo with new architecture)

---

## DEPLOYMENT SEQUENCE

### Phase 1: Validation (Current)
- Rebuild Silverstone 2025 demo with Ranking Layer
- Validate architecture against real race data
- Document any refinements needed

### Phase 2: Production (Australia 2026)
- Deploy full architecture to Round 1 template
- Use validated Ranking Layer for all future reports

### Phase 3: Hardening (Post-Season)
- Reorganize files to production paths (`/frameworks/`, `/live/`, `/round-01-australia/`)
- Lock file references + skill triggers
- Establish cron schedule for weekly reports

---

## NOTES FOR IMPLEMENTATION

1. **Ranking Layer First:** Complete Ranking Layer data before Strategy analysis. Don't skip to forecasts without establishing competitive hierarchy.

2. **Engine Supplier Relevance:** Especially important for:
   - Reliability forecasts (predict DNF risk by engine)
   - Track suitability weighting (which engines suit upcoming circuit?)
   - Momentum tracking (which power units improving/declining?)

3. **Time Horizons:** Each ranking section has 3 time views:
   - Last race (recent form signal)
   - Current season (trend over multiple races)
   - Previous race full table (complete picture for modeling)

4. **Data Refresh Cadence:**
   - Last race rankings: Updated Sunday PM (post-race)
   - Current season: Updated Monday AM (final standings)
   - Engine supplier profiles: Updated Monday AM (cumulative)

5. **Confidence Calibration:** Ranking Layer outputs inform Strategy Layer confidence levels. Example:
   - If driver "↑ Rising" in rankings (3-race trend) → increase win % forecast by 1–2%
   - If engine supplier "↓ Falling" in reliability → increase DNF probability in forecasts

---

**Status:** ✅ **ARCHITECTURE BLUEPRINT COMPLETE**  
**Validation Phase:** Active (Silverstone 2025 demo rebuild pending)  
**Next:** Rebuild demo with 6-section Ranking Layer + 2026 engine mapping

---

**Document Type:** Architecture (Framework, not demo report)  
**Domain:** F1 Intelligence (Validation phase, no reorganization yet)  
**Audience:** System prompt reference + framework builder
