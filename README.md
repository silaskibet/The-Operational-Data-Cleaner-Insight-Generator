# Week 2: Operations Sensor Data Wrangler

**Author:** Silas Kibet   
**Role:** Statistician

## 📌 Project Overview
This repository contains a complete data wrangling and time-series analysis pipeline built to sanitize, process, and analyze a week of simulated "dirty" sensor data from a processing plant. 

Raw industrial sensor logs are notoriously noisy, frequently suffering from missing values, degraded sensor misfires, and formatting inconsistencies. The objective of this project is to construct a robust, modular Python pipeline that transforms chaotic operational logs into clean, actionable business intelligence for plant management.

## 🛠️ Tools & Libraries Used
* **Language:** Python
* **Data Manipulation:** `pandas`, `numpy`
* **Visualization:** `matplotlib.pyplot`, `seaborn`, `missingno`
* **Environment:** Jupyter Notebook

## 📂 Repository Contents
* `week2_data_wrangler.ipynb`: The core Jupyter Notebook containing the ingestion, profiling, cleaning, and time-series aggregation code.
* `Week2_Insight_Report_Silas_Kibet.pdf`: A 1-page executive summary for the Plant Manager, translating the statistical findings into a "Context-Insight-Action" business narrative.
* `raw_vs_cleaned_trend.png`: The finalized visualization proving the efficacy of the cleaning pipeline.

## ⚙️ The Data Wrangling Pipeline
The core of this project is the `clean_ops_data()` function, which executes the following sanitization steps:
1. **Datetime Standardization:** Parses inconsistent strings into sortable `datetime` objects.
2. **Structural Cleaning:** Drops duplicate sensor firings and removes rows with fundamentally missing location tags (`Zone`).
3. **Categorical Standardization:** Strips whitespace and standardizes casing for categorical variables.
4. **Shift Allocation:** Programmatically assigns operational shifts (Morning, Afternoon, Night) based on the timestamp hour.
5. **Physical Outlier Bounding:** Filters out impossible physical phenomena (e.g., negative pressures and extreme positive anomalies > 1000 PSI) caused by sensor degradation.
6. **Chronological Interpolation:** Utilizes linear interpolation to fill missing gaps in the continuous time-series data.

## 📊 Analytics & Business Impact
After cleaning, the data was resampled to an hourly frequency and smoothed using a **24-hour rolling average**. 

**Key Finding:** Visualizing the raw data alongside the smoothed 24-hour trend line revealed that perceived extreme volatility in `ZONE_WEST` was actually an illusion caused by severe sensor degradation. The physical system pressure is highly stable (holding at ~200 PSI). This statistical insight allows plant management to confidently schedule preventative sensor maintenance without unnecessarily shutting down the physical pipeline.

## 🚀 How to Run the Code
1. Clone this repository to your local machine.
2. Ensure you have the required libraries installed (`pip install pandas numpy matplotlib seaborn missingno`).
3. Place the `ops_sensor_log_dirty.csv` file in the root directory.
4. Run all cells in `week2_data_wrangler.ipynb`.
