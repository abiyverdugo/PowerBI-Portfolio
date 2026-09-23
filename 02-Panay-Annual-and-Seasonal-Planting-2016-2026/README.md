# Panay & Guimaras Rice Planting Analytics (Annual & Seasonal Monitoring 2016–2026)

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Dynamic_Cross--Filtering-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-Automated_ETL-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas_(Panay_--_Guimaras)-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

A centralized Business Intelligence dashboard engineered for the Department of Agriculture Regional Field Office VI (Field Operations Division, Rice Program & Agricultural Statistics). This platform automates the ingestion, transformation, and comparative tracking of a decade of municipal planting accomplishments against physical rice areas across Panay and Guimaras.

---

## 📊 Live Interactive Dashboard

Explore the live, interactive Power BI report:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMTc0ZGFkMjEtMTZmOS00Zjg1LWI4ODYtMDc0ZDA3NTg0ZWM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

---

## 🎯 Executive Summary & Operational Challenge

Evaluating rice planting accomplishments across Western Visayas historically required aggregating municipal monthly submissions scattered across disparate Excel files, fluctuating column layouts, and irregular seed-type classifications.

### Operational Challenges Solved:
* **Fragmented Multi-Year Workbooks (2016–2026):** Transitioned from manually consolidating annual and seasonal sheets to an automated Power Query pipeline with schema unification.
* **Double-Counting Prevention:** Addressed regional reporting where aggregate `INBRED SEEDS` totals were reported alongside granular classes (`CERTIFIED SEEDS`, `GOOD SEEDS`, `FARMER SAVED SEEDS`). Applied explicit DAX filter criteria and Power Query filtering (`[Seed Type] <> "INBRED SEEDS"`) to ensure data accuracy.
* **Physical Area Benchmark Alignment:** Municipal physical boundaries remained static while cropping cycles repeated. Implemented dynamic DAX measures with bi-directional cross-filtering and multi-column filter overrides (`REMOVEFILTERS`) to calculate physical area baselines without duplication.

---

## 📸 Dashboard Visuals & Structure

### Page 1: Annual Planting Performance (2016–2026)
![Annual Planting 2016-2026](Annual%20Planting%202016-2026.jpg)

* **Top-Level KPI Strip:** Displays total cumulative planted area (5.09M ha), regional physical footprint (258K ha), and multi-year accomplishment rate.
* **Seed Class Adoption by Province:** Stacked visual breakdown analyzing the distribution of Certified Seeds (CS), Good Seeds (GS), Farmer Saved Seeds (FSS), and Hybrid Seeds across Aklan, Antique, Capiz, Guimaras, and Iloilo.
* **Provincial Planting Rankings:** Horizontal Pareto-style distribution highlighting Iloilo (2.68M ha) and Capiz (1.04M ha) as primary regional volume drivers.
* **Ecosystem Trajectory (Irrigated vs. Rainfed):** Monthly operational tracking showing planting distribution between gravity-fed irrigation systems and rainfed lowland/upland tracts.
* **Provincial Accomplishment Matrix:** Line-by-line accounting calculating accomplishment percentages against municipal physical baselines.

---

### Page 2: Seasonal Cropping Dynamics (Dry vs. Wet Season)
![Seasonal Planting 2016-2026](Seasonal%20Planting%202016-2026.jpg)

* **Dry Season vs. Wet Season Cycles:** Evaluates crop rotation shifts and compares seasonal performance against annual production targets.
* **Seasonal Planting Percentage Trends:** Year-over-year progression evaluating variance across cropping calendars.
* **Monthly Seasonal Curves:** Tracks operational ramp-up times, identifying planting peaks in wet-season months versus water-constrained dry-season operations.

---

## 🔬 Agricultural Insights Delivered

1. **Provincial Scale & Density:** Iloilo accounts for over 51% of regional planted area, followed by Capiz (~20%) and Antique (~16%), highlighting key zones for farm input allocation and machinery deployment.
2. **Seed Class Modernization:** Certified Seeds (CS) represent the largest share of planted hectares (51.47%), while Farmer Saved Seeds (FSS) comprise 22.4% and Good Seeds (GS) 15.93%, demonstrating adoption progress while pinpointing areas needing seed support.
3. **Ecosystem Exposure:** Over 55% of planting operations occur in rainfed ecosystems, making overall provincial accomplishment sensitive to monsoon onset schedules and dry spells.

---

## 🏗️ Data Architecture & ETL Pipeline

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

## 💻 Core DAX Formulas

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

## 🛠️ Tools & Technologies Used
* **Business Intelligence Platform:** Power BI Desktop, Power BI Service
* **Data Modeling:** Star Schema Design, Bi-directional Cross-filtering, Disconnected Benchmarking
* **ETL & Data Engineering:** Power Query (M Language), Web API Google Sheet Integration, Dynamic Column Unpivoting
* **Data Governance:** Standardized validation logic filtering non-administrative records and subtotal rows

---

## 📬 Contact & Inquiries
* **Lead Analyst:** Abegail Vanjo (Abiy) G. Verdugo
* **Designation:** Information Systems Analyst II / Data Analyst
* **Organization:** Department of Agriculture — Regional Field Office VI (Western Visayas)
* **LinkedIn:** [linkedin.com/in/abiyverdugo](https://www.linkedin.com/in/abiyverdugo/)
* **Portfolio Repository:** [github.com/abiyverdugo/PowerBI-Portfolio](https://github.com/abiyverdugo/PowerBI-Portfolio)
