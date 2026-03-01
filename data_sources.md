# F1 Intelligence — Data Sources & Integration

**Version:** 1.0  
**Last Updated:** March 1, 2026  
**Status:** Production Ready

---

## PRIMARY DATA SOURCES

### 1. OpenF1 API (Primary)
**Status:** ✅ Verified & Operational  
**URL:** https://api.openf1.org  
**Authentication:** None (free, open source)  
**Rate Limits:** 3 req/s, 30 req/min  
**Latency:** ~3 sec delay (acceptable for strategic analysis)

**Available Endpoints:**
- `/sessions` — Session metadata (FP1, FP2, Quali, Race)
- `/drivers` — Driver info + standings
- `/laps` — Per-lap telemetry (times, sectors, positions)
- `/pit_stops` — Pit stop timing, driver, lap
- `/weather` — Track temps, wind speed/direction, rain probability
- `/race_control` — Race control messages (flags, VSC, SC timing)
- `/radio` — Team radio transmissions (when available)

**Query Format:** 
```
GET /sessions?year=2026&round=1
GET /laps?session_key=9158
GET /pit_stops?session_key=9158
```

**Data Retrieved:**
- Lap times + sector splits (±0.01 sec precision)
- Tyre compound + age tracking
- Pit stop loss estimates (22–24 sec Silverstone baseline)
- Weather conditions (real-time)
- Race control events + timing

**Confidence:** HIGH (verified in Silverstone 2025 demo)

---

### 2. F1.com Live Timing (Secondary)
**Status:** ✅ Operational (fallback)  
**URL:** https://www.f1.com (embedded live timing)  
**Authentication:** None (public)  
**Latency:** <2 sec (sometimes sharper than OpenF1)

**Available Data:**
- Live positions + gaps
- Lap times (fresh laps)
- Tyre info (compound, age estimate)
- Penalties/flags
- Qualifying order

**Usage:** If OpenF1 has >2-lap discrepancy or missing sector data, cross-check against F1.com.

**Confidence:** MEDIUM-HIGH (official FIA source, but not API)

---

### 3. ESPN F1 Timing (Secondary)
**Status:** ✅ Operational (fallback)  
**URL:** https://www.espn.com/f1/  
**Latency:** 3–5 sec (slower, more lag)

**Available Data:**
- Race/quali standings
- Session results
- Basic strategy info
- Commentary + analysis

**Usage:** Fallback only (less real-time, higher latency)

**Confidence:** MEDIUM (delayed, secondary source)

---

### 4. FIA Official Race Control Archive
**Status:** ✅ Available post-race  
**URL:** Embedded in race reports  
**Latency:** N/A (historical data)

**Available Data:**
- Race control messages (SC, VSC, flag timings)
- Penalties + reason
- Technical issues
- Weather log

**Usage:** Post-race validation + accuracy check

**Confidence:** HIGH (official FIA data)

---

### 5. Sportsbooks — Odds & Markets
**Primary:** Caesars Palace  
**Fetch Method:** Brave Search (no API key needed)

**Markets Tracked:**
- Win (decimal odds)
- Podium (decimal odds)
- Top 6 (decimal odds)

**Process:**
1. Brave Search query: "Caesars Palace F1 Australia GP 2026 Verstappen odds"
2. Extract decimal odds from search results
3. Convert to implied probability: 1 / Decimal = Implied Prob
4. Compare to model forecast
5. Flag edges ≥3%

**Sportsbook Selection Rationale:**
- Caesars Palace: Solid odds, wide market coverage, reliable lines
- Alternative options: Betfair (exchange, sharper lines), Pinnacle (expert market)

**Confidence:** MEDIUM (market-dependent; lines shift throughout week)

---

## DATA INTEGRITY CHECKS

### Flagging Rules

**Critical Thresholds:**
- **>2 lap gap** between data sources → Flag "Data integrity concern" + reduce confidence to LOW
- **Sector mismatch** >0.1 sec vs baseline → Flag anomaly + investigate
- **Missing data** (e.g., radio, weather) → Document + reduce confidence level
- **Latency >5 sec** on OpenF1 → Switch to F1.com, flag lag

### Example Scenarios

**Scenario 1: FP2 data lag**
- OpenF1 shows Verstappen +0.3 sec over Norris
- F1.com shows +0.7 sec (4-lap old data)
- **Action:** Use OpenF1 (fresher), flag F1.com as lagged, reduce F1.com confidence

**Scenario 2: Sensor glitch**
- Mercedes telemetry shows left-rear tire temp +8°C anomaly (Lap 15)
- **Action:** Flag "Sensor anomaly detected", mark Mercedes data MEDIUM confidence, investigate next session

**Scenario 3: VSC data missing**
- Race control says VSC triggered Lap 25, but OpenF1 missing VSC message
- **Action:** Cross-check F1.com race control log, document timestamp, flag gap in OpenF1 reliability

---

## SEASON DATA RULES

### Use 2026 Data ONLY For:
- Current-season car competitiveness (power rankings, speed deltas)
- Current-season tyre behavior (deg rates, warm-up lags)
- Current-season regulatory baseline (engine power, aero specs)

### Use 2024 Data ONLY For:
- Circuit geometry (corners, speeds, DRS zones)
- Historical strategy archetypes (undercut/overcut windows, pit loss estimates)
- Typical tyre behavior patterns (warm-up curves, cliff points by compound)

### DO NOT Extrapolate 2024:
- Power rankings (regulation changes alter order)
- Tire strategy counts (tyre spec changes affect viability)
- Straight-line speed deltas (engine power 2025 > 2024)

---

## TEMPERATURE SCALE

**Standard:** Fahrenheit  
**Conversion:** °C × 1.8 + 32 = °F

**Key Thresholds:**
- **68°F (20°C):** Baseline track temperature
- **64°F (18°C):** Cool-track threshold (triggers Mercedes setup risk flag)
- **77°F (25°C):** Hot-track threshold (favors high-downforce setups)

**Application:**
- All weather forecasts: Fahrenheit
- All temperature-dependent model refinements: Fahrenheit
- All race reports: Fahrenheit

---

## TIME FORMAT

**Standard:** 24-hour format (BST / EST unless otherwise noted)

**Examples:**
- FP2: 14:00 BST (not 2:00 PM)
- Qualifying: 15:00 BST (not 3:00 PM)
- Race: 15:00 BST (not 3:00 PM)

---

## API TESTING & VALIDATION

### Pre-Season Test (By Mar 2, 2026)

**OpenF1 API:**
```bash
curl https://api.openf1.org/v1/sessions?year=2026&round=1
# Expected: JSON array of session objects (FP1, FP2, Quali, Race)

curl https://api.openf1.org/v1/drivers?session_key=9158
# Expected: JSON array with driver standings for Round 1

curl https://api.openf1.org/v1/weather?session_key=9158
# Expected: JSON with track temp, wind, rain data
```

**Brave Search Odds:**
```
Query: "Caesars Palace F1 Australia 2026 Verstappen odds"
Expected: Clickable links to Caesars Palace betting page
```

**F1.com Timing:**
- Visit https://www.f1.com during FP2 session
- Verify live positions + lap times updating <2 sec
- Cross-check vs OpenF1 data (should match within 0.05 sec)

---

## DATA PIPELINE FLOW

```
Session Start (FP2, Quali, Race)
    ↓
OpenF1 API (primary fetch)
    ↓
Data Integrity Check (>2 lap gap? sensor anomaly?)
    ↓
Pass: Use data
Fail: Cross-check F1.com
    ↓
Populate Mode 2 Live Update (FP2/Quali/Race Morning)
    ↓
Post-Race: Merge with FIA Race Control + Sportsbook odds
    ↓
Mode 1 Monday Report (championship, strategy, forecasts, betting)
```

---

## CONFIDENCE CALIBRATION

**Data Source Confidence Levels:**

| Source | Confidence | Conditions | Usage |
|--------|-----------|-----------|-------|
| OpenF1 | HIGH | Normal operation, <2 sec latency | Primary (always) |
| F1.com | MEDIUM-HIGH | Live, but non-API | Fallback (data gap) |
| ESPN | MEDIUM | Delayed, 3–5 sec lag | Last resort |
| FIA Archives | HIGH | Post-race only | Validation |
| Caesars Palace | MEDIUM | Market-dependent, lines shift | Betting only |

**Escalation Rules:**
1. If OpenF1 latency >5 sec → switch to F1.com, flag delay
2. If F1.com missing data → use ESPN, reduce confidence to MEDIUM
3. If >2 lap gap detected → PAUSE analysis, flag "Data integrity concern", reduce confidence to LOW
4. If sensor anomaly (e.g., temp spike) → flag, investigate next session, reduce driver confidence

---

## SPORTSBOOK INTEGRATION PROTOCOL

### Pre-Race Odds Fetch (Monday)

1. **Query Brave Search:**
   ```
   "Caesars Palace F1 [Circuit] 2026 Win odds [Driver1] [Driver2] [Driver3]"
   ```

2. **Extract Odds:**
   - Driver A: 2.50 decimal
   - Driver B: 3.75 decimal
   - Driver C: 5.00 decimal

3. **Convert to Implied Probability:**
   ```
   Driver A: 1 / 2.50 = 0.40 = 40%
   Driver B: 1 / 3.75 = 0.267 = 26.7%
   Driver C: 1 / 5.00 = 0.20 = 20%
   ```

4. **Compare to Model:**
   ```
   Driver A: Model 45% vs Market 40% = +5% edge ✓
   Driver B: Model 20% vs Market 26.7% = -6.7% edge (overvalued)
   Driver C: Model 15% vs Market 20% = -5% edge (overvalued)
   ```

5. **Decision:**
   - Driver A: Edge ≥3% → Potential bet (0.5–1.0 unit if high confidence)
   - Driver B, C: Edge <3% or negative → PASS

---

## VALIDATION LOG

**Silverstone 2025 Demo (Validated):**
- OpenF1 API: ✅ Reliable (no data gaps)
- F1.com Timing: ✅ Fallback verified (F1.com was sharper on quali, faster updates)
- Qualifying deltas: ✅ Within 0.04 sec (4/4 accurate)
- Weather data: ✅ Accurate (Celsius to Fahrenheit conversion tested)
- Caesars Palace odds: ✅ Extracted correctly (Brave Search working)

**Issues Flagged:**
- Mercedes FP2 sensor anomaly (left-rear +8°C) → noted, not critical
- Temperature sensitivity model underestimated (refined by 50%)

---

## FUTURE ENHANCEMENTS

**Planned (Post-Deployment):**
1. Automated weather API integration (wttr.in or Open-Meteo for forecast updates)
2. Betfair exchange odds scraping (for sharper closing lines)
3. Real-time radio transcription (team strategy calls)
4. Tire pressure telemetry (when available from team leaks)

---

**Status:** ✅ PRODUCTION READY  
**Confidence:** HIGH  
**Next:** Deploy with Round 1 Australia (March 6–8, 2026)
