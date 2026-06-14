# TravelTide — Customer Segmentation & Reward Strategy

![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-K--Means-F7931E?logo=scikitlearn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-data-150458?logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-interactive%203D-3F4F75?logo=plotly&logoColor=white)
![Status](https://img.shields.io/badge/status-complete-2A9D8F)
![Project](https://img.shields.io/badge/Masterschool-ML%20Mastery%20Project-1F3A5F)

> An end-to-end **unsupervised machine-learning** project that segments TravelTide's customers by booking
> behaviour and designs a **tailored rewards programme** to drive repeat, revenue-generating bookings.

---

<iframe src="https://0xbrenpa.github.io/ML-Mastery-Project-Customer-Segmenation/clusters_3d_offline.html"
        width="800" height="600" frameborder="0"></iframe>

---

## Table of contents

- [Project description](#project-description)
- [Project summary](#project-summary)
  - [Key points](#key-points)
  - [The six customer segments](#the-six-customer-segments)
  - [Key insights](#key-insights)
  - [Deliverables & visualizations](#deliverables--visualizations)
- [Repository structure](#repository-structure)
- [Installation](#installation)
- [Data](#data)
- [Usage](#usage)
- [Example usage](#example-usage)
- [Dependencies](#dependencies)
- [Methodology in brief](#methodology-in-brief)
- [Limitations](#limitations)
- [Author & license](#author--license)

---

## Project description

**TravelTide** is an online travel platform (flights + hotels) with a large browsing audience but a
comparatively small booking base — **65.5 % of all sessions end without a booking**. The business needs a
**retention / loyalty programme**, but a single blanket reward wastes margin on customers who would book
anyway and fails the customers who need a different nudge.

This project answers two questions:

1. **Who are TravelTide's customers, behaviourally?** — discovered with unsupervised clustering, letting the
   data decide how many segments exist rather than fixing the number in advance.
2. **What reward should each segment receive?** — a perk matched to each segment's dominant behaviour and its
   specific churn risk, plus a measurement framework (a retention KPI and an A/B test) to prove, net of cost,
   which perks actually work.

The analysis runs on four raw platform tables (`users`, `sessions`, `flights`, `hotels`), engineers a
behavioural feature set, and produces six actionable segments, a per-segment reward strategy, and a complete
set of presentation-ready deliverables.

---

## Project summary

### Key points

- **Scope:** ~5,746 customers / 46,863 cleaned sessions over a 29-week window (Jan–Jul 2023).
- **Method:** feature engineering → `log1p` + RobustScaler preprocessing → **two-stage K-Means** clustering →
  per-segment reward design → retention KPI + A/B-test design.
- **Outcome:** **6 segments** — two mainstream tiers (≈75 % of customers) plus four well-separated niches —
  each with a tailored reward and a back-tested retention baseline.
- **Headline finding:** for TravelTide, **conversion and bundling — not raw loyalty — are the biggest levers**.

### The six customer segments

| Segment | Share | Defining behaviour | Headline reward |
|---|---|---|---|
| **Engaged mainstream bookers** | 37.8 % | Active, multi-product core; books & bundles often, rarely cancels (~$4,794 LTV) | Loyalty / points programme + bundle free-night |
| **Light / occasional mainstream** | 37.5 % | Same profile at lower intensity; lower spend, mostly solo | Time-limited “comeback” offer + low-cost sweetener |
| **Premium far-advance planners** | 7.7 % | Highest fares & spend; book `~`145 days ahead; international (`~`$7,868 LTV) | No cancellation fees + premium service |
| **Browse-only non-bookers** | 7.0 % | Engage but never convert — intent present, a barrier blocking | Bold first-booking offer + risk removal |
| **International long-stay hotel** | 5.3 % | Book hotels abroad but flights elsewhere; long stays | Bundle free-night to win the flight leg |
| **High-engagement budget hunters** | 4.7 % | Most engaged & price-driven; bundle most; cancel most (12 %) | Members-only deals; reward completed trips |

### Key insights

- **Sessions rarely convert, and bundles are the value** — 65.5 % browse-only; bundle-dominant customers spend
  **2.2× more** (median `$`5,233 vs `$`2,424).
- **Engagement is double-edged** — the most engaged quartile books 2.5× more (47 % vs 19 %) but also cancels far
  more (4.8 % vs ~0 %); the engagement↔cancellation correlation (0.83) is the strongest link in the data.
- **Two distinct trip types** — booking lead time is sharply **bimodal**: ~95 % book last-minute (~7 days,
  ~`$`371) while a separate ~5 % book ~224 days ahead at ~$1,775 (71 % international), with almost nobody between.
- **No airline owns our customers** — only **24 %** of flyers stay loyal to one airline; 76 % comparison-shop
  across two or more, and the more they spread, the more they spend — an opening for a platform loyalty programme.
- **Never-bookers are a behavioural, not demographic, problem** — they look identical to bookers; a friction
  barrier, not the wrong audience.

### Deliverables & visualizations

| Deliverable                      | File                                                                                                                                    |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| 📄 **Executive summary + detailed report** | [`./TravelTide_Project_Summary.pdf`](output/TravelTide_Project_Summary.pdf)                                                             |
| 🖥️ **Main presentation deck**   | [`./TravelTide_Segmentation.pptx`](output/TravelTide_Segmentation.pptx)                                                                 |
| 🔎 **CSV file with users assigned to perks** | [`./data/users_assigned_to_perks.csv`](output/TravelTide_Customer_Insights.pptx) · [transcript](output/transcript_customer_insights.md) |
| 🌐 **Interactive 3-D cluster visualization** | [`clusters_3d_offline.html`](https://0xbrenpa.github.io/segment-charts/clusters_3d_offline.html) (open in a browser)                            |
| 🧾 **Analysis notebook** (source of truth) | [`./ipynb/Mastery_Project.ipynb`](mastery_project.ipynb)                                                                                |

---

## Repository structure

```
Masterschool - Mastery Project - Customer Segmentation/
├── README.md                       # You are here
├── ipynb/                           
│   └── Mastery_Project.ipynb       # ⭐ The live analysis notebook (clean → cluster → perks → KPI → A/B)
├── requirements.txt                # Python dependencies for the notebook
├── clusters_3d_offline.html        # Interactive 3-D cluster projection (Plotly)
│
├── data/                           
│   ├── users_assigned_to_perks.csv # Output: user_id → segment → assigned perk  
│   ├── users_raw_table.csv  
│   ├── sessions_raw_table.csv  
│   ├── flights_raw_table.csv
│   └── hotels_raw_table.csv
│
├── TravelTide_Project_Summary.pdf        # 4-page exec summary + detailed report
└── TravelTide_Segmentation.pptx          # Main 22-slides deck
```
---

## Installation

> Requires **Python 3.11+** (developed on 3.13).

```bash
# 1. Download the Jupyter notebook 
Mastery_Project.ipynb

# 2. Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 3. Install all dependencies (analysis + reporting tooling)
pip install -r requirements.txt
```

---

## Data

The four source tables are **included** in the repository (≈1.3 GB combined). They originate from the
TravelTide PostgreSQL database; the notebook's DB-pull cells are commented out and the analysis reads cached
CSVs from `data/` instead. To run the project end-to-end you need:

```
data/users_raw_table.csv      data/sessions_raw_table.csv      data/flights_raw_table.csv      data/hotels_raw_table.csv
```

**Schema (essentials):**

| Table | Grain | Key fields |
|---|---|---|
| `users` | one row per customer | birthdate, gender, household, home location, sign-up date |
| `sessions` | one row per visit | start/end, `page_clicks`, booking flags, discounts, `cancellation`, `trip_id` |
| `flights` | one row per booked flight | `seats`, `checked_bags`, `base_fare_usd`, route, airline, departure/return |
| `hotels` | one row per booked hotel | `rooms`, `nights`, `hotel_per_room_usd`, check-in/out, hotel name |

To pull the data yourself, uncomment the database cells near the top of `Mastery_Project.ipynb` and supply your
own connection string.

---

## Usage

### 1) Run the analysis

Open the notebook and run all cells:

```bash
jupyter lab Mastery_Project.ipynb      # or: jupyter notebook
```

The notebook proceeds top-to-bottom: **clean → join → feature-engineer → select features → preprocess →
select k → two-stage cluster → assemble segments → design perks → design retention KPI → design A/B test**.

### 2) View the visualizations

- Open [`clusters_3d_offline.html`](https://0xbrenpa.github.io/segment-charts/clusters_3d_offline.html) in any browser to explore the clusters in 3-D.
- Read the [4-page summary PDF](./TravelTide_Project_Summary.pdf).

---

## Example usage

Run the Jupyter notebook in the `./ipynb` directory to reproduce the analysis.

---

## Dependencies

All dependencies are pinned in [`requirements.txt`](requirements.txt) and install with a single command:

```bash
pip install -r requirements.txt
```

**Core analysis:**
`numpy` · `pandas` · `scipy` · `scikit-learn` · `matplotlib` · `seaborn` · `plotly` · `kaleido` ·
`SQLAlchemy` · `psycopg2-binary` · `duckdb`

---

## Methodology in brief

1. **Cleaning** — distinguish *structurally missing* values (no booking ⇒ blank) from data errors; drop 2,121
   under-18 sessions; recompute hotel `nights` from check-in/out dates.
2. **Feature engineering** — build session-level behaviour (booking type, lead time, spend, discount depth,
   international flag), aggregate to 57 customer features, then select **19** across five behavioural dimensions.
3. **Preprocessing** — zero-impute structural NaNs, `log1p` the right-skewed magnitudes (so a few extreme
   values don't dominate distance), then RobustScaler.
4. **Clustering** — K-Means with **k = 5** (the last *k* before the silhouette cliff: 0.429 → 0.186), then a
   **second stage** that splits the dominant ~75 % mainstream cluster into two actionable tiers.
5. **Reward design** — one perk package per segment, matched to behaviour and churn risk.
6. **Measurement** — a **90-day repeat-booking rate (RBR-90)** KPI (back-tested per segment) and a six-arm,
   segment-stratified **A/B test** with cost guardrails and a strict ship/no-ship decision rule.

---

## Limitations

- **Snapshot data** — a single 29-week window; retention is reconstructed via a historical back-test.
- **The mainstream split is business-driven**, not a natural data gap (a transparent modelling choice).
- **Small niches are statistically underpowered** for modest A/B effects, even with variance reduction.
- **Perk economics are not yet quantified** — the net-revenue-after-cost guardrail needs per-perk margins
  before the A/B test reads as a profit decision.

---

## Author & license

**Author:** PB — Masterschool *ML Mastery* capstone project.

This is an **educational project**. The TravelTide dataset is course-provided.
Code may be reused for learning purposes; please credit the author.
