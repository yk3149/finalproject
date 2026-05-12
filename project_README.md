# Final Project: Heat Waves, Data Centers, and Regional Electricity Demand

**Columbia Climate School — Computing and Research Methods for Climate Data Science**
**yk3149**

---

## Scientific Question

> How do extreme heat events affect peak electricity demand across different PJM regions, and are these effects stronger in regions with high concentrations of data centers?

## Hypothesis

> Extreme heat events increase electricity demand due to higher cooling needs. Regions with high data center density (such as the Dominion zone in Northern Virginia) will experience larger increases in peak electricity demand during heat waves compared to other PJM regions.

---

## Datasets

### 1. PJM Hourly Metered Load
- **Source:** [PJM DataMiner2](https://dataminer2.pjm.com/feed/hrl_load_metered/definition)
- **Coverage:** 2018–2023, hourly resolution, five zones: DOM, PSEG, PPL, BGE, PECO
- **Usage:** Aggregated to daily peak load (MW) per zone using Pandas `groupby`

### 2. NOAA GHCNd Station Temperature
- **Source:** [NOAA Climate Data Online API](https://www.ncdc.noaa.gov/cdo-web/api/v2/)
- **Variable:** TMAX — daily maximum temperature (°F)
- **Stations:** One representative station per PJM zone (Richmond VA, Newark NJ, Harrisburg PA, Baltimore MD, Philadelphia PA)
- **Access:** Fetched directly in the notebook via the NOAA CDO API (see setup instructions below)

### 3. Global Data Center Locations *(contextual only)*
- **Source:** [lwieske/cloud-datacenter-locations](https://github.com/lwieske/cloud-datacenter-locations)
- **Usage:** Approximate cluster centroids used for Figure 1 (global map) only — not used in quantitative analysis

---

## Analysis Plan

PJM hourly electricity load data and NOAA GHCNd daily maximum temperature observations are combined to identify extreme heat events and calculate daily peak electricity demand for five PJM zones. Using Pandas, data are grouped and aggregated to compare peak demand on heat wave days (≥ 3 consecutive days with TMAX ≥ 95°F) versus normal days across regions. Mann–Whitney U tests and OLS regression are used to assess whether regions with higher data center concentration — particularly the Dominion zone in Northern Virginia — exhibit a significantly stronger increase in peak demand during extreme heat.

---

## Figures

| # | Figure | Description |
|---|--------|-------------|
| 1 | Global Data Center Map | Cartopy world map showing approximate locations of major cloud and colocation data center clusters; highlights Dominion zone |
| 2 | Time Series | Daily peak load and TMAX for the Dominion zone (2018–2023), with heat wave periods highlighted |
| 3 | Scatter Plot | Temperature vs. daily peak load by zone (summer months), with OLS regression lines and R² values |
| 4 | Boxplot | Distribution of peak load on heat wave vs. normal days, with Mann–Whitney U significance brackets |
| 5 | Bar Chart | Average absolute and relative increase in peak demand during heat waves by PJM zone, with 95% bootstrap confidence intervals |
| 6 | Multi-Panel | Four-panel summary: seasonal load profiles, demand-response curves by temperature bin, annual heat wave day counts, and summer load duration curves |

---

## Tools and Methods

- **Python** — pandas, numpy, matplotlib, scipy, requests
- **Pandas** — datetime indexing, `groupby`, `merge`, daily peak aggregation, rolling averages
- **SciPy** — `mannwhitneyu` (hypothesis testing), `linregress` (OLS regression)
- **Matplotlib** — all six figures
- **Cartopy** *(optional)* — Robinson projection for Figure 1; Matplotlib fallback used if unavailable

---

## How to Run

### 1. Get a free NOAA API token
Register at https://www.ncdc.noaa.gov/cdo-web/token — tokens are issued instantly by email.

### 2. Set your token
In the notebook, find the NOAA data cell and either:

**Option A — paste directly into the notebook:**
```python
NOAA_TOKEN = "your_token_here"
```

**Option B — set as an environment variable before launching Jupyter:**
```bash
export NOAA_TOKEN=your_token_here
jupyter notebook
```

### 3. Run all cells
`Kernel → Restart & Run All`

All data is loaded automatically inside the notebook — no manual downloads required. If no NOAA token is provided, the notebook falls back to a synthetic temperature dataset calibrated to NOAA 1991–2020 climatological normals for each station.

### Optional: install Cartopy for the map projection in Figure 1
```bash
conda install -c conda-forge cartopy
```

---

## Repository Structure

```
finalproject/
├── README.md
└── heat_waves_datacenter_electricity.ipynb
```
