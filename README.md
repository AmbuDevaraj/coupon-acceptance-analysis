# Coupon Acceptance Analysis

## Overview

This project analyzes a dataset of driving scenarios to determine what factors influence whether a driver accepts a coupon delivered to their phone. Using visualizations and probability distributions, we distinguish between customers who accepted coupons versus those who did not.

**Notebook:** [`coupon_acceptance_analysis.ipynb`](coupon_acceptance_analysis.ipynb)

---

## Dataset

- **Source:** UCI Machine Learning Repository (collected via Amazon Mechanical Turk)
- **File:** `data/coupons.csv`
- **Size:** ~12,007 rows after cleaning, 25 columns

### Coupon Types
- Restaurant (< $20)
- Coffee House
- Carry Out & Take Away
- Bar
- Restaurant ($20–$50)

### Key Attributes

| Category | Attributes |
|---|---|
| User | Gender, Age, Marital Status, Children, Education, Occupation, Income |
| Frequency | Bar, Coffee House, Carry Away, Restaurant visits per month |
| Context | Destination, Weather, Temperature, Time, Passenger |
| Coupon | Type, Expiration (2h or 1d) |
| Target | `Y` — 1 = Accepted, 0 = Declined |

---

## Project Structure

```
coupon-acceptance-analysis/
├── data/
│   └── coupons.csv                          # Raw dataset
├── plots/                                   # Saved plot images
│   ├── 01_coupon_distribution.png
│   ├── 02_temperature_distribution.png
│   ├── 03_bar_acceptance_by_frequency.png
│   ├── 04_bar_acceptance_age_over25.png
│   ├── 05_bar_target_vs_others.png
│   ├── 06_bar_three_groups.png
│   ├── 07_coffee_acceptance_by_frequency.png
│   ├── 08_coffee_acceptance_by_passenger.png
│   ├── 09_coffee_acceptance_by_time.png
│   └── 10_coffee_frequent_vs_infrequent.png
├── coupon_acceptance_analysis.ipynb         # Main analysis notebook
└── README.md                                # This file
```

---

## How to Run

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd coupon-acceptance-analysis
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
3. Launch Jupyter:
   ```bash
   jupyter notebook
   ```
4. Open `coupon_acceptance_analysis.ipynb` and run all cells. Plots are automatically saved to the `plots/` folder.

---

## Summary of Findings

### Overall Acceptance Rate: 56.84%

The overall coupon acceptance rate is **56.84%**. Acceptance varies significantly by coupon type, existing habits, and trip context.

---

### Part 1 — Bar Coupon Analysis (Acceptance: 41.19%)

Bar coupons have a notably lower acceptance rate than average. Key findings:

| Segment | Acceptance Rate |
|---|---|
| Bar visits ≤ 3x/month | ~37% |
| Bar visits > 3x/month | ~77% |
| Frequent bar-goer, age > 25 | ~69% |
| Frequent bar-goer, no kids, not farming | ~71% |
| Bar > 1x/month, no kids, not widowed | ~71% |
| Bar > 1x/month, age < 30 | ~72% |

**Hypothesis:** Bar coupon acceptance is driven by existing bar-going habit. Drivers who visit bars more than once a month accept at nearly double the rate of infrequent visitors. The presence of child passengers and certain occupations (farming, fishing, forestry) significantly reduce acceptance.

**Actionable Items:**
- Target frequent bar-goers (>1x/month) as the primary audience
- Avoid targeting drivers with children as passengers
- Focus on ages 21–30 for highest yield
- Send bar coupons in the evening to match typical bar-going hours
- Use 1-day expiry to give flexibility for evening plans

---

### Part 2 — Coffee House Coupon Analysis (Acceptance: 49.57%)

Coffee house coupons are the most frequently issued type but still fall below the overall average. Key findings:

| Segment | Acceptance Rate |
|---|---|
| Frequent visitors (>1x/month) | ~65% |
| Infrequent visitors (never / <1x) | ~38% |
| Passengers: Friends or Partner | ~58–60% |
| Passengers: Alone or Kids | ~43–47% |
| Time: 10AM | ~65% |
| Time: 2PM | ~50% |
| Time: 6PM | ~43% |

**Hypothesis:** Coffee coupon acceptance is strongly tied to existing coffee habit. Time of day is the second strongest predictor — morning delivery aligns with natural coffee-drinking behavior. Social trips (with friends or a partner) further boost acceptance.

**Actionable Items:**
- Prioritize frequent coffee visitors (>1x/month) in targeting
- Send coupons in the morning (10AM) for highest acceptance
- Target social trips (passengers = friends or partner)
- Deprioritize evening delivery windows
- Combine habit + timing: frequent visitor + 10AM = ideal profile

---

### Next Steps

1. **Expand to other coupon types** — Carry Out, cheap restaurants, and mid-range restaurants remain unexplored.
2. **Build a predictive model** — Use visit frequency, passenger type, time, and age as features for a logistic regression or decision tree classifier.
3. **Analyze expiration impact** — Compare 2-hour vs 1-day acceptance rates across all coupon types.
4. **Investigate weather and destination** — Explore whether weather or trip destination interacts with coupon type acceptance.
5. **Demographic deep-dive** — Analyze income and education as additional targeting filters.

---

## Dependencies

| Library | Version |
|---|---|
| pandas | >= 1.3 |
| numpy | >= 1.21 |
| matplotlib | >= 3.4 |
| seaborn | >= 0.11 |
| jupyter | >= 1.0 |

---

## Author

Ambu Devaraj
AIML Program — Module 5 Assignment
