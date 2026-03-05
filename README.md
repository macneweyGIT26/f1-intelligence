# F1 Strategic Intelligence System

A data-driven Formula 1 analysis platform for strategic insights, race predictions, and technical breakdown.

**Status:** Production Ready (2026 Season)  
**Latest:** Australia GP Round 1 (Mar 6–8, 2026)

---

## Overview

F1 Intelligence is a technical analysis system that combines live race data with strategic modeling to deliver:
- **Race strategy analysis** — Pit window modeling, undercut/overcut opportunities, tyre management
- **Driver & team rankings** — Competitiveness assessment based on multi-metric scoring
- **Engine & power unit insights** — Performance signatures, reliability patterns, advantage quantification
- **Pre-race strategy frameworks** — Decision trees for pit calls, tyre selection, aggressive vs. conservative approaches
- **Weekly championship recaps** — Post-race momentum, points trends, upcoming circuit profiles

Built for **decision-grade accuracy**, not fan commentary.

---

## Quick Start

### Web Dashboard
Visit the live dashboard (deployed on Vercel):
```
https://f1-intelligence-vercel-link.com  [UPDATE WITH ACTUAL URL]
```

Features:
- Interactive circuit previews
- Strategy simulations
- Live race feeds (when available)
- Archive of past rounds

### Local Development

**Prerequisites:**
- Node.js 18+
- Python 3.10+ (optional, for data processing scripts)

**Setup:**
```bash
git clone https://github.com/yourusername/f1-intelligence.git
cd f1-intelligence
npm install  # if needed for web assets
```

**Data Integration:**
```bash
# Fetch latest session data from OpenF1
# [Example script path or API call here]
```

---

## Architecture

### Data Flow

```
OpenF1 API / F1.com → Data Parser → Analysis Engine → Web Dashboard
     ↑                                                         ↓
   Primary Source                                   Strategic Output
   (Live/Telemetry)                              (Reports, Rankings, Viz)
```

### Key Files

| File/Folder | Purpose |
|-------------|---------|
| `round-01-australia/` | Australia GP analysis (practice, strategy, race) |
| `frameworks/` | Reusable analysis templates & decision models |
| `data_sources.md` | Complete data integration reference |
| `TYRE_WEEK_MONITORING.md` | Pirelli tyre nomination tracking |
| `skill_f1_intelligence.md` | System prompt & analysis rules |
| `index.html` / `viewer.html` | Web UI components |
| `vercel.json` | Deployment configuration |

---

## Features

### 1. **Tyre Week Monitoring**
Automatically tracks Pirelli compound nominations (soft/medium/hard) and assesses strategic implications for each circuit.

**Workflow:**
- Tuesday/Wednesday check during race weeks
- Extract compound nominations from Pirelli press releases
- Assess qualifying vs. race tradeoffs
- Auto-update TYRE_WEEK_SETUP in race dashboard

**File:** `TYRE_WEEK_MONITORING.md`

### 2. **Race Strategy Analysis**
Multi-level strategy modeling:
- **Pit window optimization** — Undercut/overcut windows with ±2 sec precision
- **Tyre strategy** — 1-stop, 2-stop, or aggressive variants based on circuit + weather
- **Pace delta modeling** — Expected gap per tyre age/compound
- **Safety car contingencies** — SC/VSC triggers and re-strategy rules

**Example:** Silverstone 2025 demo analysis in `round-08-silverstone-2025-demo/`

### 3. **Driver & Team Rankings**
Composite scoring across:
- Recent race pace (last 3 races, weighted)
- Head-to-head matchups (driver quality)
- Engine power (horsepower signature)
- Reliability (DNF rate, mechanical issues)
- Strategic execution (pit calls, tire management)

Outputs ranked lists with confidence levels.

### 4. **Power Unit / Engine Analysis**
Signature-based assessment of engine performance:
- Top speed clusters (DRS zone comparisons)
- Acceleration profiles (0–100 km/h)
- Thermal management (overtemp risk zones)
- Relative advantage vs. competitors (±2–5 hp range)

### 5. **Pre-Race Strategic Frameworks**
Decision trees for key strategic moments:
- Should we undercut? (go early / stay out)
- Should we switch tyre strategy? (if SC/VSC hits)
- Should we be aggressive or conservative? (risk/reward matrix)
- What's our contingency if the leader pits early?

---

## Data Sources

### Primary: OpenF1 API
- **URL:** https://api.openf1.org
- **Coverage:** All 2026 session data (FP1, FP2, Quali, Race)
- **Latency:** ~3 sec (acceptable for strategic analysis)

**Available endpoints:**
```
GET /sessions?year=2026&round=1
GET /laps?session_key=9158
GET /pit_stops?session_key=9158
GET /weather?session_key=9158
GET /race_control?session_key=9158
```

### Secondary: F1.com Live Timing
- **URL:** https://www.f1.com/live
- **Coverage:** Real-time feeds when OpenF1 lags
- **Latency:** <2 sec

### Supplementary: Pirelli Insights
- **Source:** press.pirelli.com (RSS feed)
- **Usage:** Tyre compound nominations, strategy guidance

For full data reference, see `data_sources.md`.

---

## Analysis Outputs

### Weekly Reports (Post-Race)
```
📊 Championship Snapshot
  - Drivers' & Constructors' standings
  - Momentum trends (last 3 races)

🏁 Race Recap (Strategy Lens)
  - Podium + key strategy story
  - Pit window execution
  - Tyre behavior analysis
  - Reliability notes

🏎️ Upcoming Circuit Profile
  - Technical corner breakdown
  - Tyre strategy archetypes
  - Strategic decision framework
```

### Interactive Dashboard
- Circuit previews (3D/2D layout)
- Strategy simulations (pit window calculator)
- Live race feeds (with commentary layer)
- Archive search

---

## Usage Examples

### Scenario 1: Assessing Undercut Opportunity
```
Input: Current pit window (Laps 18–24), track temp 45°C, medium→soft tyre swap
Output: Undercut gain +0.6 sec/lap (viable window = Lap 20–22)
Confidence: MEDIUM-HIGH (recent baseline confirmed)
```

### Scenario 2: Predicting Race Strategy
```
Input: Circuit type (high-downforce), weather (stable), field (tight midfield)
Output: Recommended 2-stop with medium→hard→soft progression
Alternative: 1-stop aggressive (medium→hard) if leading
Decision point: SC/VSC at Lap 25–35 triggers contingency evaluation
```

### Scenario 3: Engine Performance Assessment
```
Input: Top speed data from qualifying (Silverstone)
Output: Mercedes engine +3.2 hp over Ferrari (straight-line advantage)
Track impact: +0.15 sec on DRS zones
Risk: Thermal concern in hot corners (monitor coolant temps)
```

---

## Project Structure

```
f1-intelligence/
├── README.md                          # This file
├── data_sources.md                    # Data integration guide
├── TYRE_WEEK_MONITORING.md            # Automated tyre tracking workflow
├── skill_f1_intelligence.md           # System prompt & analysis rules
├── PROJECT_PROMPT.md                  # Project charter
│
├── round-01-australia/                # Australia GP (Round 1, 2026)
│   ├── halo.html                      # Executive summary dashboard
│   ├── overview.md                    # Circuit profile + grid analysis
│   ├── rankings.md                    # Team & driver rankings
│   ├── strategy.md                    # Strategic frameworks
│   ├── engines.md                     # Power unit analysis
│   ├── betting-edge.md                # Value/odds analysis
│   └── ... (additional analysis)
│
├── round-08-silverstone-2025-demo/    # Demo analysis (2025 archive)
│   ├── overview.md
│   ├── strategy.md
│   ├── rankings.md
│   └── ...
│
├── frameworks/                        # Reusable analysis templates
│   ├── circuit_template.md
│   ├── strategy_decision_tree.md
│   └── ranking_methodology.md
│
├── prompts/                           # LLM prompts for analysis tasks
├── reports/                           # Generated reports (archive)
│
├── index.html                         # Web dashboard (main entry)
├── viewer.html                        # Markdown viewer component
├── vercel.json                        # Vercel deployment config
└── .gitignore                         # Git exclusions
```

---

## Deployment

### Vercel (Live)
The project is deployed on Vercel for live access to dashboards.

**Deploy steps:**
```bash
# Push to main branch
git push origin main

# Vercel auto-deploys via webhook
# Check deployment status: vercel.com/dashboard
```

**Environment variables:** (if needed)
```
OPENF1_API_KEY=          # Optional if OpenF1 adds auth
F1COM_SESSION_TOKEN=     # If F1.com integration requires auth
```

---

## Methodology

### Confidence Levels
All outputs include explicit confidence ratings:
- **VERY HIGH** — Data verified + tested; multiple signal sources
- **HIGH** — Data confirmed; established pattern
- **MEDIUM-HIGH** — Data consistent; some uncertainty
- **MEDIUM** — Early indicator; needs confirmation
- **LOW** — Speculative; avoid major decisions

### Data Integrity Rules
- Discrepancy >2 laps → Flag "Data integrity concern" + reduce confidence
- Missing data → Use last reliable value + note gap
- Conflicting sources → Resolve via majority vote or recency

### Seasonality
- **2026 data only** for car competitiveness & power rankings
- **2024 data only** for circuit geometry & strategy archetypes
- No cross-season extrapolation

---

## Contributing

This project is maintained as a personal analysis tool. Community contributions welcome:

1. **Report bugs:** Open an issue with session data + observed discrepancy
2. **Suggest features:** Circuit-specific frameworks, new data sources, visualization improvements
3. **Submit PRs:** Improvements to analysis logic, dashboard, documentation

**Guidelines:**
- Keep analysis outputs decision-grade (avoid speculation)
- Reference data sources explicitly
- Test against 2–3 prior races before generalizing
- Document methodology changes

---

## License

**Status:** Personal project (learning & analysis)  
**Usage:** Non-commercial analysis only

Not affiliated with FIA, F1, or team IP. All race data from public sources (OpenF1, F1.com, Pirelli).

---

## References

- **OpenF1 API:** https://api.openf1.org (open-source, community-maintained)
- **Pirelli F1:** https://press.pirelli.com (tyre compounds, strategy guides)
- **F1.com:** https://www.f1.com (official FIA source)
- **2024 Circuit Data:** Formula1.com archives

---

## Roadmap

- [ ] Real-time race control integration (SC/VSC auto-trigger)
- [ ] Multi-season competitive tracking (2025→2026 carry-forward)
- [ ] Advanced weather modeling (wind, rain probability forecasting)
- [ ] Predictive AI ranking (machine learning on historical data)
- [ ] Mobile dashboard (iOS / Android)
- [ ] Slack/Discord bot for live race alerts

---

## Support

For questions or issues:
1. Check `data_sources.md` for data integration help
2. Review `skill_f1_intelligence.md` for analysis methodology
3. See `TYRE_WEEK_MONITORING.md` for Pirelli compound tracking
4. Open an issue on GitHub

---

**Last Updated:** March 4, 2026  
**Version:** 1.0 (Production Ready)  
**Maintainer:** [@neweyAI](https://github.com/neweyAI)
