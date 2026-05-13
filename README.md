# ICP Fit × Intent Dashboard

A two-axis B2B account scoring dashboard for sales prioritization, built as a single self-contained HTML file.

**[View the live demo →](https://ashleymillan.github.io/icp-dashboard/)**

---

## What it does

Each of 175 simulated B2B accounts is scored on two independent axes:

**Fit Score — A · B · C · D · 0–100 points**
Built from concrete firmographic, financial, technographic, and growth data. Stable across time.

**Intent Score — Hot · Warm · Cold · 0–100 points**
Built from live intent signals: 6sense research surge, buying stage, hiring postings, leadership changes, funding events, and tech replacement windows. Decays over time.

The combination answers the operational question every revenue team asks every Monday: **who should we call first?** Accounts that are A-tier *and* Hot are the priority segment. Accounts at D-Hot are flagged as churn risk.

---

## Highlights

- **Five clickable KPI tiles** — each opens a drill-down drawer with distributions and an account list
- **4 × 3 Fit × Intent heatmap** — written sales recommendations for each cell ("Call first", "Caution — churn risk", "Top-of-funnel", etc.)
- **Industry leaderboard** sorted by average fit score
- **Growth quadrant** — revenue YoY × employee YoY scatter with four labeled regions (Hyper-growth, Hiring through downturn, Efficiency play, Contracting)
- **Sortable, filterable account table** — text search plus fit-tier and intent-band filters
- **Slide-in account drawer** with full per-dimension Fit and Intent breakdowns, 4-quarter growth sparklines, D&B financial health, active intent keywords, and tech-stack overlap (with target matches highlighted)
- **Drill-down filtering** — every distribution bar in every drawer is itself clickable, with a back button to walk back up the stack
- **Annotated methodology** — full scoring rubric plus an exemplar account drawer with numbered callouts explaining every section and its data source

---

## Simulated data sources

Modeled after the kind of enrichment a real sales-ops team would pull from:

| Source | Drives |
| --- | --- |
| ZoomInfo | Firmographics, employee count + YoY, exec depth, hiring postings, intent + buying stage |
| HG Insights | Installed tech stack, tech spend tier, recent installs / replacements / pilots |
| 6sense | Keyword intent surge, buying stage classification, web + content engagement |
| D&B Hoovers | D-U-N-S, revenue + YoY, credit / risk / stress ratings, ownership type, location count |

Data is deterministic across reloads (seeded PRNG, seed `1337`), so the same account scores the same way every time.

---

## Stack

- **Vanilla JavaScript** — no framework
- **D3.js v7** — all five charts built from scratch (donut, matrix heatmap, horizontal bar, scatter, sparklines)
- **GSAP + ScrollTrigger** — entrance animations, count-up tweens, scroll-triggered reveals
- **Lenis** — smooth scroll
- **Google Fonts (Quicksand)**

All dependencies load from CDN. No build step, no `package.json`, no `node_modules` — just drop `index.html` anywhere and it runs.

---

## Running locally

```bash
open index.html        # macOS
```

Or double-click it in Finder. That's it.

---

## Scoring model

### Fit Score (100 points)

| Dimension | Max | Source |
| --- | ---: | --- |
| Industry match (target / adjacent / non-target) | 12 | ZoomInfo, D&B |
| Revenue band (sweet spot $1B–$5B) | 12 | D&B Hoovers |
| Employee size (sweet spot 1k–10k) | 10 | ZoomInfo |
| Financial health (credit, risk, stress) | 12 | D&B Hoovers |
| Technographic overlap + spend tier | 16 | HG Insights |
| Growth trajectory (employee + revenue YoY) | 14 | ZoomInfo, D&B |
| Geographic fit (HQ tier + multinational) | 10 | D&B, ZoomInfo |
| Org structure (ownership, locations, age) | 8 | D&B |
| Decision-maker depth (execs + recent hires) | 6 | ZoomInfo |

Tier cutoffs: **A ≥ 80**, **B ≥ 65**, **C ≥ 45**, **D < 45**.

### Intent Score (100 points)

| Signal | Max | Source |
| --- | ---: | --- |
| 6sense intent surge (keyword research) | 30 | 6sense |
| Buying stage (Awareness → Purchase) | 20 | 6sense |
| Web + content engagement | 15 | 6sense, ZoomInfo |
| Hiring for relevant target-function roles | 10 | ZoomInfo |
| Recent leadership changes (target function) | 10 | ZoomInfo |
| Funding event in last 12 months | 10 | D&B, ZoomInfo |
| Tech change-of-status (install / replacement) | 5 | HG Insights |

Band cutoffs: **Hot ≥ 70**, **Warm ≥ 40**, **Cold < 40**.

The full rubric — plus an annotated example drawer explaining every UI element and its data source — is also available inside the dashboard under the *Scoring methodology* expander.

---

© 2026 Ashley Millan. All rights reserved. Published as a portfolio piece — not licensed for reuse, redistribution, or derivative works.
