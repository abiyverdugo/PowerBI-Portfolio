<div align="center">

# Rice Planting Trends & Climate Variability (El Niño Analysis 2018–2026)

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Time_Series_Averaging-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-M_ETL_Pipeline-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas_(Region_VI)-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

<p>
An executive Business Intelligence reporting system designed for the Department of Agriculture Regional Field Office VI (Rice Program & Agricultural Statistics). This platform models nine years of monthly planting records to evaluate delayed monsoon shifts, quantify seasonal planting contractions, and assess ecosystem vulnerability caused by recurring El Niño weather cycles across Western Visayas.
</p>

</div>

---

<h2 align="center">📊 Live Interactive Dashboard</h2>

<div align="center">

Explore the deployed Power BI Service report:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

</div>

---

<h2 align="center">🎯 Operational Background & Analytical Objective</h2>

Severe climatic shock events disrupt seasonal transplanting calendars across Western Visayas. When rainfall is curtailed, farmers postpone land preparation and nursery establishment, bunching harvesting schedules directly into high-risk monsoon and typhoon periods later in the year.

### Key Operational Challenges Solved:
* **The Normal Baseline Benchmark:** Comparing an individual drought year directly against a single preceding year creates high volatility due to irregular weather baselines. By isolating and aggregating non-drought cropping years (`2020`, `2021`, `2022`) into an automated dynamic benchmark (`Normal Year Average (2020–2022)`), regional executives gained a reliable standard for measuring crop delays.
* **Context-Aware DAX Aggregation:** Direct summation across multi-year cohorts distorts regional benchmarks. An iterative DAX engine dynamically computes an arithmetic mean (`AVERAGEX`) when multiple baseline years are selected together, while returning exact summations when single historical years are evaluated.
* **Ecosystem Disaggregation:** The data structure disaggregates irrigated gravity systems from rainfed lowland and upland tracts, highlighting where localized water shortages restrict field operations.

---

<h2 align="center">📸 Dashboard Architecture & Visual Walkthrough</h2>

<div align="center">

### Page 1: El Niño Years Trends & Baseline Comparison

<p align="center">
  <img src="Rice%20Planting%20Trends%201.png" alt="Page 1: El Niño Trends" width="100%" />
</p>

</div>

* **Multi-Year Time-Series Trajectory:** Tracks monthly progress from January through December. It plots historical El Niño cycles (`2018`, `2019`, `2023`, `2024`, `2025`) alongside current `2026` operational progress against the `Normal Year Average (2020–2022)` benchmark.
* **Planting Area Distribution by Year:** Proportional donut breakdown displaying annual contribution shares across all tracked historical cohorts.
* **Provincial Ecosystem Matrix:** Granular matrix comparing Irrigated and Rainfed (Lowland/Upland) areas across Aklan, Antique, Capiz, Guimaras, and Iloilo.
* **Global Dynamic Slicers:** Synchronized controls for Quarter, Month, Ecosystem, Sub-Ecosystem, and Seed Variety.

---

<div align="center">

### Page 2: El Niño Years Graphs (Comparative Visual Diagnostics)

<p align="center">
  <img src="Rice%20Planting%20Trends%202.png" alt="Page 2: El Niño Graphs" width="100%" />
</p>

</div>

* **Monthly Planting Variance Curves:** Direct area and trajectory comparisons illustrating month-by-month deficits and post-drought surges.
* **Rainfed vs. Irrigated Resilience Tracking:** Visualizes the resilience gap between secure irrigated perimeters and climate-exposed rainfed tracts.
* **Seed Variety Utilization Dynamics:** Analyzes how farmers adjust varietal choices (Certified Seeds, Hybrid, Farmers Home Saved Seeds) when drought delays seasonal planting windows.

---

<h2 align="center">🔬 Core Agricultural & Policy Insights</h2>

1. **Two-Month Peak Planting Lag:** Under normal conditions (`Normal Year Average 2020–2022`), peak planting activity across Western Visayas occurs in **June** (~120K ha). During acute El Niño cycles (`2018`, `2019`, `2023`, `2024`), peak planting shifts two months backward into **August and September**.
2. **Extreme Rainfed Sensitivity:** Rainfed lowland areas contract sharply between May and July during drought years, representing over 55% of all delayed planting volume regionally.
3. **Provincial Intervention Targeting:** Iloilo and Capiz report the largest absolute shifts in planted area during drought periods, establishing them as priority zones for pump distribution and adjusted certified seed allocation.

---

<h2 align="center">🏗️ Data Engineering & Analytical Logic</h2>

### 1. Power Query (M) Pipeline: Schema Unification & Tagging
The raw data combined archival annual reports (`2018–2025`) with active operational records (`2026`). 

* **Automated Cohort Classification:** Uses conditional column transformations to classify years into drought events (`2018`, `2019`, `2023`, `2024`, `2025 (El Niño Year)`), active tracking (`2026 (Current Year)`), or the baseline benchmark (`Normal Year Average (2020–2022)`).
* **Dimensional Cleansing:** Cleans missing text values, strips non-printable characters, standardizes seed terminology (e.g., standardizing `FARMER SAVED SEEDS` to `FARMERS HOME SAVED SEEDS`), and assigns calendar sorting attributes (`Month Number` 1–12) to ensure chronological ordering across visuals.

### 2. DAX Measure Logic: Context-Aware Averaging
Standard aggregation (`SUM`) causes baseline groups to inflate totals by summing 2020, 2021, and 2022 together. To prevent this, the `Adjusted Planting Area` measure evaluates visual filter context dynamically:

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

* **Single-Year Context:** When a specific year is filtered, it calculates the true sum of hectares.
* **Multi-Year / Baseline Context:** When viewing the baseline group (`Normal Year Average`), it iterates over the active years using `AVERAGEX` and calculates the accurate mean hectare value per month.

---

<h2 align="center">🛠️ Tools & Technologies Used</h2>

* **Business Intelligence Platform:** Power BI Desktop, Power BI Service
* **Analytical Modeling:** Time-series benchmark modeling, dynamic context-aware DAX
* **ETL Engineering:** Power Query (M Language), append operations, data hygiene & calendar sorting
* **Domain Scope:** Western Visayas (Aklan, Antique, Capiz, Guimaras, Iloilo)

---

<div align="center">

### 📫 Connect With Me

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

</div>
