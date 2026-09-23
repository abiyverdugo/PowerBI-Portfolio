# Rice Planting Trends & Climate Variability (El Niño Analysis)

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Calculations-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Region](https://img.shields.io/badge/DA_RFO_VI-Western_Visayas-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

Interactive monitoring dashboard developed for the Department of Agriculture Regional Field Office VI (Field Operations Division, Rice Program). This report evaluates rice planting patterns across Western Visayas to quantify planting delays, shifts in seasonal peaks, and vulnerability during El Niño episodes compared to baseline normal crop years (2018–2026).

---

## Live Interactive Dashboard

Explore the live, interactive Power BI report:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

---

## Executive Summary & Operational Challenge

Western Visayas (Region VI) serves as a primary rice production hub in the Philippines, encompassing Aklan, Antique, Capiz, Guimaras, and Iloilo. Climate shocks, particularly recurring El Niño dry spells, disrupt seasonal rainfall and compromise rainfed and upland farming systems.

### Operational Challenges Faced:
* **Manual Cross-Year Tracking**: Field data submitted across municipal agriculture offices was isolated across separate yearly spreadsheets (2018 to 2026), preventing fast comparative historical assessments.
* **Lack of Baseline Benchmarks**: Program officers needed an automated way to compare current-year planting progress against a standardized baseline (`Normal Year Average (2020–2022)`) versus confirmed El Niño years (`2018`, `2019`, `2023`, `2024`, and `2025`).
* **Spatial & Ecosystem Blind Spots**: Decision-makers required instant drill-downs to determine whether planting delays were concentrated in rainfed lowland ecosystems or extended into irrigated networks.

---

## Dashboard Visuals & Structure

### Page 1: El Niño Years Trends (Temporal & Baseline Comparison)
![Rice Planting Trends 1](Rice%20Planting%20Trends%201.png)

* **Monthly Planting Area Trend Line**: Compares monthly trajectories across each El Niño year, current year (2026), and the 3-year baseline normal average (2020–2022).
* **Planting Area Distribution Donut**: Summarizes the volume of total hectares tracked across all evaluated cycles.
* **Provincial & Ecosystem Breakdown Matrix**: Line-by-line accounting of total planted area categorized by Province, Ecosystem (Irrigated vs. Rainfed), and Sub-Ecosystem (Lowland vs. Upland).
* **Multi-Attribute Filter Slicers**: Dynamic slicing by Quarter, Month, Ecosystem, Sub-Ecosystem, and Seed Type (Certified, Hybrid, Good, Farmer Saved).

### Page 2: El Niño Geospatial & Distribution Profile
![Rice Planting Trends 2](Rice%20Planting%20Trends%202.png)

* **Geospatial Concentration**: Visualizes regional distribution of planting operations across the Panay-Guimaras area.
* **Ecosystem Shift Bars**: Highlights the planting balance between irrigated areas and climate-vulnerable rainfed systems.

---

## Key Agricultural Insights Delivered

1. **Shift in Wet Season Planting Peak**: Historical baseline trends demonstrate a peak in June–July. During severe El Niño cycles (such as 2018 and 2024), peak planting shifted late into August and September due to delayed monsoon onset.
2. **Rainfed Vulnerability Ratio**: Over 55% of the total regional planted area falls under rainfed ecosystems, making overall provincial rice targets heavily reliant on seasonal weather patterns.
3. **Provincial Resilience**: Iloilo represents the largest share of regional planted area, where irrigated districts cushioned production drops during prolonged dry spells.

---

## Data Pipeline & Modeling Architecture

### 1. Power Query ETL Pipeline
* **Source Integration**: Appended historical tabular datasets covering 2018–2025 with active 2026 operational records into a unified fact table: `Annual Planting 2018-2026`.
* **Data Transformation**:
  * Normalized inconsistent municipality naming conventions across provincial submissions.
  * Extracted and standardized `Month`, `Month Short`, `Month Number`, `Quarter`, and `Year`.
  * Added conditional columns classifying specific years into defined climate tags (`El Niño Year`, `Normal Baseline`, `Current Year`).

### 2. Core DAX Logic

#### Dynamic Adjusted Planting Area & Benchmark Measure:
This calculation dynamically returns actual planted hectares when evaluating an individual year, or automatically aggregates the monthly average across the reference baseline years when no single year is filtered:

```dax
Adjusted Planting Area = 
IF(
    HASONEVALUE('Annual Planting 2018-2026'[Year]),
    COALESCE(SUM('Annual Planting 2018-2026'[Area Planted (Ha)]), 0),
    AVERAGEX(
        VALUES('Annual Planting 2018-2026'[Year]),
        CALCULATE(SUM('Annual Planting 2018-2026'[Area Planted (Ha)]))
    )
)
```

---

## Technologies Used

* **Business Intelligence**: Power BI Desktop, Power BI Service (Fabric Cloud Workspace)
* **Data Transformation**: Power Query (M Language)
* **Calculations**: Data Analysis Expressions (DAX)
* **Data Sourcing**: Department of Agriculture Regional Field Office VI Master Planting Datasets
* **Domain**: Rice Sector Analytics, Agristat Climate Impact Assessment

---

## 📬 Connect With Me

<p align="center">
  <a href="https://www.linkedin.com/in/abiyverdugo/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
  &nbsp;
  <a href="https://github.com/abiyverdugo" target="_blank">
    <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
  </a>
  &nbsp;
  <a href="mailto:abegailvanjoverdugo@gmail.com">
    <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" />
  </a>
</p>

<p align="center">
  <b>Abegail Vanjo (Abiy) G. Verdugo</b><br/>
  <i>Information Systems Analyst II / Data Analyst</i><br/>
  Department of Agriculture — Regional Field Office VI (Western Visayas)
</p>

<p align="center">
  <sub>© 2026 Abegail Vanjo G. Verdugo. All rights reserved.</sub>
</p>
