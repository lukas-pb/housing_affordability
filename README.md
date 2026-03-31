# 🏠 Australian Housing Affordability

Interactive analysis of house price affordability across Australia's capital cities, using CPI-adjusted ABS data.

**[View live →](https://lukas-pb.github.io/housing_affordability)**

---

## What it shows

Three views, toggleable by city and dwelling type (house vs attached):

| View | Description |
|------|-------------|
| **Price-to-income ratio** | Median house price ÷ annual earnings. How many years of gross income to buy. |
| **Growth index** | House prices and earnings rebased to 100 at the start of the series. Shows how much faster prices have grown than wages. |
| **Real house prices** | CPI-adjusted median transfer prices in today's dollars. |

## Data sources

| Dataset | Source |
|---------|--------|
| Residential property prices | ABS 6416.0 — Residential Property Price Indexes |
| Average weekly earnings | ABS 6302.0 — Ordinary time cash earnings, full-time adults |
| CPI | ABS 6401.0 — Consumer Price Index |

All price series are adjusted to the latest CPI quarter per city using the formula:

```
real_value = nominal_value × (CPI_latest / CPI_period)
```

## Repo structure

```
housing_affordability/
├── docs/
│   ├── index.html      # Interactive chart (GitHub Pages entry point)
│   └── data.csv        # Full dataset — all cities, all quarters
├── notebooks/
│   └── analysis.ipynb  # Data cleaning, CPI adjustment, PTI calculations
├── README.md
└── .gitignore
```

## Running locally

No server needed — just open `docs/index.html` in a browser. If you get a CORS error loading the CSV, run a simple local server:

```bash
cd docs
python -m http.server 8000
# then open http://localhost:8000
```

## Methodology notes

- **Price-to-income** uses annual earnings (`weekly_earnings × 52`) as the denominator
- **Earnings** are state-level averages (ABS 6302.0), not city-specific — capital city workers typically earn above the state average, so PTI ratios may be slightly overstated
- **Dwelling types**: "House" = detached house transfers; "Attached" = units, townhouses, and semi-detached dwellings
- Affordability thresholds follow the [Demographia International Housing Affordability](http://www.demographia.com/dhi.pdf) methodology: ≤3× affordable, 3–5× moderate, 5–10× seriously unaffordable, >10× severely unaffordable

## License

MIT
