# NEVI EV Charging Infrastructure Optimization

**Mixed Integer Programming model for optimizing California's federal EV charging site selection and port allocation under equity and budget constraints.**

Built for DESC 605 (Prescriptive Analytics) at Pepperdine Graziadio School of Business — Team JCT.

---

## The Problem

The National Electric Vehicle Infrastructure (NEVI) program is deploying $5 billion in federal funding across all 50 states. California must decide where to place charging stations and how many ports to install at each — a decision currently made without a systematic, reproducible framework. Site selection decisions are actively contested.

This project builds a data-driven MIP model that answers: **given a $10M budget and federal Justice40 equity mandates, which 11 sites across 400 candidates should be selected, and how many ports should each have?**

---

## Approach

### Three-Layer Analytics Stack

**Descriptive** — Regression analysis on 89 months of CA DMV ZEV registration data. Key finding: population density has near-zero predictive power for EV adoption (R² = 0.008), invalidating the most common siting heuristic.

**Predictive** — Multiple linear regression with time trend, COVID-19 structural break indicator, and 11 monthly seasonal dummies. Applied to all 400 candidate sites to estimate forward-looking ZEV demand.

**Prescriptive** — Mixed Integer Programming with:
- Binary variable `yᵢ ∈ {0,1}` — is site i selected?
- Integer variable `xᵢ ∈ ℤ⁺` — how many ports at site i?
- Objective: maximize weighted utility across population coverage, ZEV demand, and equity score
- Constraints: $10M budget cap, ≥40% DAC investment (Justice40), 4–12 ports per site (NEVI standard)

### Three Strategies Modeled

| Strategy | w₁ (Population) | w₂ (ZEV Demand) | w₃ (Equity) |
|---|---|---|---|
| A — Population Focus | 0.8 | 0.1 | 0.1 |
| B — Demand Focus ⭐ | 0.1 | 0.8 | 0.1 |
| C — Equity Baseline | 0.1 | 0.1 | 0.8 |

---

## Results

All three strategies selected 11 sites and spent $9.95M (99.5% budget utilization). All cleared the 40.2% DAC investment threshold.

| Metric | Population Focus | Demand Focus | Equity Baseline |
|---|---|---|---|
| ZEV Coverage | 46,399 | **168,751** | 99,505 |
| ZEVs per Site | 4,218 | **15,341** | 9,045 |
| DAC Investment | 40.2% | 40.2% | 40.2% |
| Justice40 Compliant | ✓ | ✓ | ✓ |
| **Recommended?** | — | **YES** | Backup |

**Demand Focus delivers 3.6× more ZEVs served per site at identical cost.** Equity and efficiency are not in conflict — all strategies meet Justice40 requirements.

Sensitivity analysis across $8M–$30M budgets shows linear coverage scaling with no diminishing returns, supporting the case for expanded federal allocation.

---

## Data Sources

| Dataset | Source |
|---|---|
| NEVI Candidate Sites (400 locations) | CA Energy Commission |
| ZEV Registration Data | CA DMV |
| CalEnviroScreen 4.0 (DAC classification) | OEHHA / CalEPA |
| US Census ACS (population) | U.S. Census Bureau |
| NEVI Federal Port Standards | FHWA |
| Cost Assumptions | DOE / Industry benchmarks |

---

## Tech Stack

- **Python** — PuLP / Google OR-Tools for MIP solving
- **Pandas / NumPy** — data wrangling and regression
- **Folium** — interactive maps with site-level tooltips (strategy, ports, DAC status)
- **Matplotlib / Seaborn** — static visualizations
- **Google Colab** — development and execution environment

---

## Files

```
├── DESC_605_Midterm_NEVI_Charger_Quantity_Location_Optimization_team_JCT.ipynb
│   └── Full analysis notebook — regression, MIP formulation, all three strategies,
│       sensitivity analysis, and geographic visualization
├── NEVI_Charging_Optimization_JCT.pptx
│   └── 14-slide presentation deck with methodology, results, and managerial insights
└── README.md
```

---

## Key Findings for Policy Makers

1. **Use demand-weighted siting, not population density.** Population explains less than 1% of EV adoption variance. Infrastructure built on demographic density systematically misallocates resources.

2. **Equity and efficiency are compatible.** The Justice40 DAC constraint is binding but not costly — meeting it doesn't require sacrificing ZEV coverage.

3. **Advocate for more budget.** Coverage scales linearly up to $30M+ with no saturation in the current candidate pool. Each incremental $2M produces proportional ZEV coverage gains.

4. **The model is reproducible.** Weights, constraints, and candidate site data are all adjustable — this framework generalizes to any state's NEVI allocation problem.

---

## Author

**Cayden Campbell** — Pepperdine Graziadio MSBA 2025–26 · 4.0 GPA  
[LinkedIn](https://linkedin.com/in/cayden-campbell) · [Portfolio](https://caydencampbell-9.github.io)

*Team JCT — DESC 605 Prescriptive Analytics Midterm*
