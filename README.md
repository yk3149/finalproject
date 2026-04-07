# Final Project: Heat Waves, Data Centers, and Regional Electricity Demand

## Scientific Question

How do extreme heat events affect peak electricity demand across different PJM regions, and are these effects stronger in regions with high concentrations of data centers?

## Hypothesis

Extreme heat events increase electricity demand due to higher cooling needs. Regions with high data center density (such as the Dominion zone in Northern Virginia) will experience larger increases in peak electricity demand during heat waves compared to other PJM regions.

## Datasets

* **PJM Electricity Load Data (hourly load by zone):**
  https://dataminer2.pjm.com/feed/hrl_load_metered/definition

* **NOAA Temperature Data (daily maximum temperature):**
  https://www.ncei.noaa.gov/

* **Global Cloud / Data Center Location Data (GeoJSON for mapping):**
  https://github.com/lwieske/cloud-datacenter-locations

* **Virginia Data Center Map:**
  https://www.pecva.org/region/loudoun/existing-and-proposed-data-centers-a-web-map/

## Analysis Plan

I will combine electricity load data and temperature data to identify extreme heat events and calculate daily peak electricity demand for multiple PJM regions. Using Pandas, I will group and aggregate the data to compare peak demand during heat wave periods versus non-heat periods across regions. I will analyze whether regions with higher data center concentration exhibit stronger increases in demand during extreme heat.

In addition, I will use a global dataset of data center locations to create a geographic visualization of major data center clusters worldwide. This will provide broader context for understanding how concentrated digital infrastructure may influence electricity demand patterns.

## Planned Figures

This project will include six figures:
1. **Global Map of Data Centers:** A map showing major data center locations worldwide (highlighting major clusters).
2. **Time Series Plot:** Daily peak electricity demand and temperature over time for a selected region (e.g., Dominion).
3. **Scatter Plot:** Relationship between temperature and electricity demand, showing how demand scales with heat.
4. **Boxplot:** Comparison of electricity demand on heat wave days versus non-heat days.
5. **Bar Chart (Regional Comparison):** Average increase in peak demand during heat waves across different PJM regions.
6. **Geographic or Multi-Panel Figure:** A geographic or comparative visualization highlighting regional differences in demand response.

## Tools and Methods

This project will use Python with Pandas for data processing and Matplotlib (and optionally Cartopy) for visualization. Key techniques will include time series analysis, grouping and aggregation, merging datasets, and spatial visualization of geographic data.
