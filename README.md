# Boston Marathon — Pace Engineering Analysis

> **An engineering breakdown of how to race Boston** — based on real split data from 21,985 runners across the 2023 and 2025 editions.

[![YouTube EN](https://img.shields.io/badge/YouTube-@RunningEngineer23-red?logo=youtube)](https://www.youtube.com/@RunningEngineer23)
[![YouTube IT](https://img.shields.io/badge/YouTube-@RunningIngegnere-red?logo=youtube)](https://www.youtube.com/@RunningIngegnere)

---

## What is this?

This project analyzes official BAA (Boston Athletic Association) split data to answer one question: **how do real runners pace the Boston Marathon?**

The result is a single-file interactive website (`index.html`) that shows:

- Optimal pacing strategy for **41 time buckets** (men 2:40→5:00, women 2:55→5:00)
- Deviation from average pace across **4 course segments**
- Positive split trends, negative split rates, and age group analysis
- Bilingual interface (English / Italian) with metric/imperial toggle
- Men vs Women comparison

The site works entirely **offline** — no server, no dependencies, just open the HTML file in any browser.

---

## The 4 course segments

| Segment | Distance | Elevation | Character |
|---|---|---|---|
| Seg. 1 — Downhill start | 0 → 10 km (0–6.2 mi) | −91 m / −299 ft | Deceptively easy. Burns quads. |
| Seg. 2 — Flat section | 10 → 25 km (6.2–15.5 mi) | ±0 m | Where the race is built. |
| Seg. 3 — Newton Hills | 25 → 35 km (15.5–21.7 mi) | +58 m / +190 ft | Heartbreak Hill at mile 20.5. |
| Seg. 4 — Final downhill | 35 → 42.2 km (21.7–26.2 mi) | −38 m / −125 ft | Boston's paradox: downhill, but slowest. |

---

## Data sources

| Edition | Gender | Runners analyzed | Notes |
|---|---|---|---|
| Boston 2023 | Men + Women | ~14,500 | Normal conditions |
| Boston 2025 | Men + Women | ~7,500 | Normal conditions |
| Boston 2024 | — | **Excluded** | Anomalous weather (heat + headwind): positive splits nearly double vs 2023 |

Official results with 5 km splits from **BAA** (Boston Athletic Association): `registration.baa.org`.

Each runner record includes: `5K · 10K · 15K · 20K · Half · 25K · 30K · 35K · 40K · Finish`.

---

## How the analysis works

### Bucket definition
Runners are grouped into ±2:30 windows around each target finish time (e.g. the "2:50" bucket includes all runners finishing between 2:47:30 and 2:52:30). For the 15-minute buckets above 4:00, the window is ±7:30.

### Segment metrics
For each bucket and segment, the analysis computes:

```
pace_segment   = segment_time / segment_distance_km
pace_overall   = chip_finish / 42.195

deviation_%    = (pace_segment − pace_overall) / pace_overall × 100
deviation_s    = pace_segment − pace_overall   [sec/km or sec/mi]
```

### Positive split
```
positive_split = chip_finish − 2 × half_time
```

A positive value means the second half was slower than the first.

---

## Key findings

**The Seg. 4 paradox** — The final 7.2 km is a net downhill (−38 m), yet it is the slowest segment for every runner at every pace. Depleted glycogen and eccentric muscle fatigue from the opening descent override the elevation advantage.

**Positive split scales with finish time** — From +2:59 (men 2:40 bucket) to +25:05 (men 5:00 bucket). The early downhill temptation is the primary driver: runners who start too aggressively in Seg. 1 systematically pay a larger price in Seg. 4.

**Women pace Seg. 4 better** — At equivalent age-graded effort levels, women show systematically lower Seg. 4 deviation than men. One hypothesis: women run the opening downhill more conservatively on average, arriving at the final stretch with more glycogen and less eccentric muscle damage.

**Experience beats youth in slow buckets** — In the 3:15+ buckets, runners aged 18–29 lose up to +14% in Seg. 4, versus +3–5% for runners aged 50–59. Younger runners are more likely to be seduced by the fast early miles.

**Negative splits are rare by design** — Only 16% of men in the 2:40 bucket and 23% of women in the 2:55 bucket run a negative split. Above 4:30, under 5% do. Boston's course profile makes a perfectly even effort nearly impossible; a controlled positive split is the realistic optimal strategy.

**2024 was a weather outlier** — The 2024 edition is excluded from the model. Warm temperatures and headwinds caused positive splits nearly double those of 2023 across all buckets (e.g. men 2:50: +2:49 in 2023 vs +6:23 in 2024). The 2024 data is however valuable as a "worst-case scenario" reference.

---

## Tech stack

| Layer | Technology |
|---|---|
| Visualization | Chart.js 4.4.1 (CDN) |
| Typography | Barlow Condensed + Barlow (Google Fonts) |
| Frontend | Vanilla HTML/CSS/JS — single file, zero framework |

---

## Limitations

- Analysis covers 2023 and 2025 only (2024 excluded for weather). Adding future editions will improve robustness.
- Age-group analysis is available for select buckets where sub-group sample sizes exceed 20 runners.
- Segment boundaries are approximated using the nearest BAA checkpoint (10K, 25K, 35K), not GPS-exact course geography.
- The pacing model assumes "normal" weather conditions. Hot, cold, wet, or windy editions will deviate.

---

## About

Made by **Fabio** — Italian engineer based in Zurich, Switzerland.

I train every day while working full-time as an engineer and raising two small kids. I analyze everything: splits, gear, training load, race strategy. Engineering approach to running.

| Channel | Language | Content |
|---|---|---|
| [@RunningEngineer23](https://www.youtube.com/@RunningEngineer23) | 🇬🇧 English | Training, races, gear, analysis |
| [@RunningIngegnere](https://www.youtube.com/@RunningIngegnere) | 🇮🇹 Italian | Allenamenti, gare, attrezzatura, analisi |

---

## License

Data © Boston Athletic Association. Analysis and code © Fabio / RunningEngineer. For personal and educational use.
