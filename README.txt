# Does Athletic Testing Predict NFL Success? A Position-by-Position Analysis

*An applied analysis of NFL Combine data with implications for the 2026 Chicago Bears Draft Class*

---

## Overview

The NFL Combine has been a fixture of pre-draft evaluation for decades. But how much does raw athleticism — as measured by the 40-yard dash, vertical jump, broad jump, and other drills — actually predict success at the NFL level?

This project builds a position-normalized Athletic Composite Score from historical combine data, correlates it against career performance outcomes across 1,760 drafted players, and applies those findings to the 2026 Chicago Bears draft class — which by RAS (Relative Athletic Score) was the most athletic class of the entire draft.

---

## Hypothesis

Athletic testing captures physical traits that should theoretically translate to NFL performance. But the degree to which that translation occurs likely varies significantly by position. A cornerback's ability to mirror and recover depends heavily on elite movement skills. A quarterback's success depends on decision-making, accuracy, and football IQ — traits the combine does not measure.

---

## Data Sources

- **Combine Data:** nflverse combine dataset (2000–2024), accessed via GitHub
- **Career Stats:** nflverse player stats (regular season only), aggregated to career totals
- **2026 Bears Draft Class:** RAS scores via ras.football / Yahoo Sports

---

## Methodology

### Athletic Composite Score
Rather than relying on a third-party metric, this project builds an original composite score from raw combine measurements:

- **Speed metrics** (40 time, 3-cone, shuttle): normalized 0-10 within position group, inverted so lower time = higher score
- **Power metrics** (vertical, broad jump, bench press): normalized 0-10 within position group
- **Final score**: average of all available normalized metrics per player

Normalization is done within position group to ensure fair comparison — a 4.55 forty means something different for a cornerback than an offensive tackle.

### Career Outcome Variables
- **QB:** Career passing yards
- **RB:** Career rushing yards
- **WR/TE:** Career receiving yards
- **CB, S, OL, LB, DL:** Career seasons played (longevity as proxy for NFL viability)

### Statistical Method
Pearson correlation coefficient between Athletic Composite Score and career outcome variable, calculated separately for each position group. Significance threshold: p < 0.05.

---

## Findings

| Position | Outcome | n | r | r² | Significant |
|----------|---------|---|---|----|-------------|
| CB | Seasons Played | 24 | 0.487 | 0.237 | Yes |
| TE | Receiving Yards | 303 | 0.272 | 0.074 | Yes |
| RB | Rushing Yards | 467 | 0.138 | 0.019 | Yes |
| WR | Receiving Yards | 676 | 0.075 | 0.006 | No |
| QB | Passing Yards | 212 | 0.026 | 0.001 | No |

### Key Takeaways

**Cornerback** shows the strongest relationship between athleticism and career success (r=0.487). At a position where elite movement skills are required just to survive in the NFL, this makes intuitive sense — the floor for athletic ability is simply higher here than anywhere else on the field.

**Tight End** shows a meaningful and statistically significant relationship (r=0.272). The dual demand of blocking physicality and receiving athleticism means combine performance captures something real about TE potential.

**Running Back** has a small but statistically significant athletic signal (r=0.138). Scheme, offensive line quality, and usage likely explain more variance than athleticism alone.

**Wide Receiver** is essentially noise (r=0.075, p=0.051). Route running, hands, and football IQ — none of which the combine measures — appear to matter far more than raw athleticism at the position.

**Quarterback** shows virtually zero correlation (r=0.026). Tom Brady's career — 89,214 passing yards on a 2.88 Athletic Composite Score — is the single most dramatic illustration of this finding. The most important position in football is the least predictable from combine testing.

---

## Visualizations

### Athletic Composite vs Career Performance by Position
![Position Scatter](athletic_composite_by_position.png)

### Correlation Coefficients by Position
![Correlation Chart](correlation_by_position.png)

### 2026 Chicago Bears Draft Class — Athletic Percentile by Position
![Bears Draft Class](bears_2026_draft_class.png)

---

## Implications for the 2026 Chicago Bears

The Bears' 2026 draft class ranked as the most athletic in the entire draft by RAS. Every player in their class scored above the 85th percentile athletically compared to historical draftees at their respective positions.

Critically, the Bears concentrated elite athleticism at the positions where this analysis suggests it matters most:

- **Sam Roush (TE, RAS 9.94)** — Tight end is the position with the second-strongest athletic-to-production correlation in this dataset. A near-perfect athletic profile at TE has historically translated to meaningful production.
- **Malik Muhammad (CB, RAS 9.51)** — Cornerback shows the strongest correlation between athleticism and career longevity. Elite CB athleticism is not just a nice-to-have — it's the closest thing to a predictive signal this dataset contains.

This does not guarantee success. Athleticism explains at most 23% of variance in career outcomes even at the positions where it matters most. But it does suggest the Bears' approach was analytically grounded, not just aesthetically appealing.

---

## Limitations

- Name matching between combine and career stats datasets is imperfect — some players may be missing from the merged dataset
- Combine data has significant missing values for certain metrics (bench press, 3-cone, shuttle), which affects the composite score calculation
- The CB sample size (n=24) is small and should be interpreted cautiously
- Career outcomes reflect total accumulation, not efficiency or peak performance
- Players drafted before 2000 or after 2020 may have incomplete career data

---

## Tools

Python | pandas | numpy | matplotlib | seaborn | scipy | nflverse

---

*Built as part of an ongoing sports analytics portfolio. All data sourced from publicly available datasets.*
