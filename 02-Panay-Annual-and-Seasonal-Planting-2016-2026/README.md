<div align="center">

# Western Visayas Rice Planting Analytics (Annual & Seasonal Monitoring 2016–2026)

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Dynamic_Cross--Filtering-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-Automated_ETL-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas_(Panay_--_Guimaras)-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

<p>
A centralized Business Intelligence dashboard engineered for the Department of Agriculture Regional Field Office VI (Field Operations Division, Rice Program & Agricultural Statistics). This platform automates the ingestion, transformation, and comparative tracking of a decade of municipal planting accomplishments against physical rice areas across Panay and Guimaras.
</p>

</div>

---

<h2 align="center">📊 Live Interactive Dashboard</h2>

<div align="center">

Explore the live, interactive Power BI report:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMTc0ZGFkMjEtMTZmOS00Zjg1LWI4ODYtMDc0ZDA3NTg0ZWM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

</div>

---

<h2 align="center">🎯 Executive Summary & Operational Challenge</h2>

Evaluating rice planting accomplishments across Western Visayas historically required aggregating municipal monthly submissions scattered across disparate Excel files, fluctuating column layouts, and irregular seed-type classifications.

### Operational Challenges Solved:
* **Fragmented Multi-Year Workbooks (2016–2026):** Transitioned from manually consolidating annual and seasonal sheets to an automated Power Query pipeline with schema unification.
* **Double-Counting Prevention:** Addressed regional reporting where aggregate `INBRED SEEDS` totals were reported alongside granular classes (`CERTIFIED SEEDS`, `GOOD SEEDS`, `FARMER SAVED SEEDS`). Applied explicit DAX filter criteria and Power Query filtering (`[Seed Type] <> "INBRED SEEDS"`) to ensure data accuracy.
* **Physical Area Benchmark Alignment:** Municipal physical boundaries remained static while cropping cycles repeated. Implemented dynamic DAX measures with bi-directional cross-filtering and multi-column filter overrides (`REMOVEFILTERS`) to calculate physical area baselines without duplication.

---

<h2 align="center">📸 Dashboard Visuals & Structure</h2>

<div align="center">

### Page 1: Annual Planting Performance (2016–2026)

<p align="center">
  <img src="Annual%20Planting%202016-2026.png" alt="Annual Planting 2016-2026" width="100%" />
</p>

</div>

* **Top-Level KPI Strip:** Displays total cumulative planted area (5.09M ha), regional physical footprint (258K ha), and multi-year accomplishment rate.
* **Seed Class Adoption by Province:** Stacked visual breakdown analyzing the distribution of Certified Seeds (CS), Good Seeds (GS), Farmer Saved Seeds (FSS), and Hybrid Seeds across Aklan, Antique, Capiz, Guimaras, and Iloilo.
* **Provincial Planting Rankings:** Horizontal Pareto-style distribution highlighting Iloilo (2.68M ha) and Capiz (1.04M ha) as primary regional volume drivers.
* **Ecosystem Trajectory (Irrigated vs. Rainfed):** Monthly operational tracking showing planting distribution between gravity-fed irrigation systems and rainfed lowland/upland tracts.
* **Provincial Accomplishment Matrix:** Line-by-line accounting calculating accomplishment percentages against municipal physical baselines.

---

<div align="center">

### Page 2: Seasonal Cropping Dynamics (Dry vs. Wet Season)

<p align="center">
  <img src="Seasonal%20Planting%202016-2026.png" alt="Seasonal Planting 2016-2026" width="100%" />
</p>

</div>

* **Dry Season vs. Wet Season Cycles:** Evaluates crop rotation shifts and compares seasonal performance against annual production targets.
* **Seasonal Planting Percentage Trends:** Year-over-year progression evaluating variance across cropping calendars.
* **Monthly Seasonal Curves:** Tracks operational ramp-up times, identifying planting peaks in wet-season months versus water-constrained dry-season operations.

---

<h2 align="center">🔬 Agricultural Insights Delivered</h2>

1. **Provincial Scale & Density:** Iloilo accounts for over 51% of regional planted area, followed by Capiz (~20%) and Antique (~16%), highlighting key zones for farm input allocation and machinery deployment.
2. **Seed Class Modernization:** Certified Seeds (CS) represent the largest share of planted hectares (51.47%), while Farmer Saved Seeds (FSS) comprise 22.4% and Good Seeds (GS) 15.93%, demonstrating adoption progress while pinpointing areas needing seed support.
3. **Ecosystem Exposure:** Over 55% of planting operations occur in rainfed ecosystems, making overall provincial accomplishment sensitive to monsoon onset schedules and dry spells.

---

<h2 align="center">🏗️ Data Architecture & ETL Pipeline</h2>

```text
+--------------------------------------------------------------------------------+
| Master Data Storage: OneDrive / Google Drive Regional Repositories             |
| - 12 Monthly Tabs / Workbook (2016-2025 Annual & Seasonal Directories)         |
| - Live 2026 Wet Season Google Sheet Feed (Published Cloud Endpoint)            |
+---------------------------------------+----------------------------------------+
                                        |
                                        v
+--------------------------------------------------------------------------------+
| Power Query (M Language) Automated Data Ingestion                              |
| - Schema transpose & header extraction (Skipping metadata lines)                |
| - Location standardization: Strict validation for 5 Western Visayas provinces  |
| - Dynamic unpivoting of 16 seed/ecosystem matrix headers                       |
| - Live 2026 append with historical records; deduplication by business keys     |
+---------------------------------------+----------------------------------------+
                                        |
                                        v
+--------------------------------------------------------------------------------+
| Dimensional Modeling & DAX Calculation Engine                                 |
| - Tables: 'Planting Annual', 'Planting Seasonal', 'Municipality Physical Area' |
| - Dynamic DAX Accomplishment Measures ([Planted Area] / [Physical Area])       |
| - Dynamic YoY growth calculation and conditional indicator formatting          |
+--------------------------------------------------------------------------------+
```

---

<h2 align="center">💻 Core DAX Formulas</h2>

### 1. Accomplishment Rate
```dax
Accomplishment Rate = 
DIVIDE([Planted Area (ha)], [Physical Area (ha)], 0)
```

### 2. Area Planted (ha) with Double-Count Prevention
```dax
Area Planted (ha) = 
IF(
    ISFILTERED('Planting Seasonal 2016-2026'[Seed Type]),
    SUM('Planting Seasonal 2016-2026'[Area Planted (ha)]),
    CALCULATE(
        SUM('Planting Seasonal 2016-2026'[Area Planted (ha)]),
        'Planting Seasonal 2016-2026'[Seed Type] <> "INBRED SEEDS"
    )
)
```

### 3. Dynamic Physical Area Baseline (Bi-directional Cross-Filter)
```dax
Physical Area (ha) = 
VAR RawPhysicalSum = 
    CALCULATE(
        SUM('Municipality Physical Area'[Physical Area (ha)]),
        CROSSFILTER(
            'Planting Annual 2016-2026 (Normalized)'[Municipality_Year], 
            'Municipality Physical Area'[Municipality_Year], 
            Both
        ),
        REMOVEFILTERS(
            'Planting Annual 2016-2026 (Normalized)'[Month],
            'Planting Annual 2016-2026 (Normalized)'[Month Number],
            'Planting Annual 2016-2026 (Normalized)'[Month Short],
            'Planting Annual 2016-2026 (Normalized)'[Quarter],
            'Planting Annual 2016-2026 (Normalized)'[Seed Type],
            'Planting Annual 2016-2026 (Normalized)'[Ecosystem],
            'Planting Annual 2016-2026 (Normalized)'[Sub-Ecosystem]
        )
    )
VAR ActiveYears = 
    CALCULATE(
        DISTINCTCOUNT('Planting Annual 2016-2026 (Normalized)'[Year]),
        REMOVEFILTERS(
            'Planting Annual 2016-2026 (Normalized)'[Month],
            'Planting Annual 2016-2026 (Normalized)'[Month Number],
            'Planting Annual 2016-2026 (Normalized)'[Month Short],
            'Planting Annual 2016-2026 (Normalized)'[Quarter],
            'Planting Annual 2016-2026 (Normalized)'[Seed Type],
            'Planting Annual 2016-2026 (Normalized)'[Ecosystem],
            'Planting Annual 2016-2026 (Normalized)'[Sub-Ecosystem]
        )
    )
RETURN
DIVIDE(RawPhysicalSum, ActiveYears, 257922.88)
```

### 4. Dynamic Year-over-Year Accomplishment Indicator
```dax
Planting Percentage YoY Label = 
VAR MinYr = MIN('Planting Annual 2016-2026 (Normalized)'[Year])
VAR MaxYr = MAX('Planting Annual 2016-2026 (Normalized)'[Year])
VAR StartVal = 
    CALCULATE(
        [Accomplishment Rate],
        'Planting Annual 2016-2026 (Normalized)'[Year] = MinYr
    )
VAR EndVal = 
    CALCULATE(
        [Accomplishment Rate],
        'Planting Annual 2016-2026 (Normalized)'[Year] = MaxYr
    )
VAR Growth = DIVIDE(EndVal - StartVal, StartVal, 0)
RETURN
IF(
    MinYr = MaxYr,
    "--",
    IF(
        Growth > 0, 
        "▲ +" & FORMAT(Growth, "0.0%"), 
        IF(
            Growth < 0, 
            "▼ " & FORMAT(Growth, "0.0%"), 
            "0.0%"
        )
    )
)
```

---

<h2 align="center">🛠️ Tools & Technologies Used</h2>

* **Business Intelligence Platform:** Power BI Desktop, Power BI Service
* **Data Modeling:** Star Schema Design, Bi-directional Cross-filtering, Disconnected Benchmarking
* **ETL & Data Engineering:** Power Query (M Language), Web API Google Sheet Integration, Dynamic Column Unpivoting
* **Data Governance:** Standardized validation logic filtering non-administrative records and subtotal rows

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
