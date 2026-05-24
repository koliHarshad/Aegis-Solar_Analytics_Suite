# Aegis: Solar Analytics Suite ☀️🛰️

Aegis is a data analytics project focused on cleaning, transforming, and analyzing 24 years of daily space weather and solar activity metrics (2000–2024). This repository contains the end-to-end data pipeline, from raw data preprocessing using Python and Pandas to producing a highly optimized dataset prepared for interactive dashboarding.

🔗 **[View Interactive Tableau Dashboard](PASTE_YOUR_TABLEAU_PUBLIC_URL_HERE)** ---

## 📌 Project Overview
Space weather has significant implications for satellite operations, power grids, and communication systems. The goal of **Aegis** is to process noisy raw data from the OMNI daily space weather database, handle missing placeholders properly, analyze fundamental solar correlations, and engineer features suitable for a data visualization layer.

The cleaned dataset spans **9,132 days (24 years)** of continuous monitoring.

---

## 📊 Key Insights & Analytics
Initial correlation analysis reveals key behaviors in solar dynamics:
* **Solar Wind Speed vs. Kp Index:** A strong positive correlation (**0.67**) confirms that faster solar winds are primary drivers of intense geomagnetic activity on Earth.
* **Geomagnetic Direction (Bz) vs. Kp Index:** A negative correlation (**-0.35**) quantifies the phenomenon where a southward-pointing Interplanetary Magnetic Field ($Bz < 0$) destabilizes Earth's magnetosphere, triggering heightened storm indexes.
* **Sunspots:** Act as a leading structural indicator of long-term solar cycle intensity rather than isolated daily wind velocities.

---

## 🛠️ Data Pipeline & Cleaning Process
The raw data contained placeholder values (e.g., `999.9`, `9999`) representing missing instrumentation readings, which would distort any analytical models or visual aggregations. The `cleaning.ipynb` notebook implements the following pipeline:

1. **Schema Parsing:** Imported the raw tabular file using white-space delimiters, ignoring metadata comments, and structuring standard columns: `Year`, `Day`, `Hour`, `B_Mag`, `Bz`, `Density`, `Speed`, `Kp_Index`, `Sunspots`.
2. **Missing Value Isolation:** Handled systemic instrumentation gaps by replacing standard space-physics null placeholders (`999`, `999.9`, `99.9`, `9999`) with true `NaN` values.
3. **Feature Engineering (Datetime Conversion):** Converted independent `Year` and Day-of-Year (`Day`) integers into a single, standard unified `Date` index using julian/ordinal string parsing (`%Y%j`).
4. **Data Standardization:** Adjusted the `Kp_Index` values to their standard scientific decimal scale by normalizing them (divided by `10.0`).
5. **Feature Selection & Export:** Narrowed the dataset down to the core visual analytics features and exported it to `solarstorm_clean.csv` for immediate dashboard consumption.
