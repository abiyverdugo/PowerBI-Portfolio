# 🌾 Agricultural Business Intelligence & Power BI Portfolio
**Department of Agriculture RFO VI — Rice Program & Agricultural Statistics**  
*Lead Analyst:* **Abegail Vanjo G. Verdugo** | *Information Systems Analyst II*

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Advanced_Modeling-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-ETL_%26_M_Code-238636)](https://learn.microsoft.com/en-us/power-query/)
[![DA-RFO VI](https://img.shields.io/badge/Agency-DA_RFO_VI_Western_Visayas-0A5C36)](#)

Welcome to my Power BI Portfolio. This repository showcases interactive Business Intelligence dashboards, dimensional data modeling, and custom DAX solutions developed for agricultural statistics, climate resilience, and operational monitoring across Western Visayas (Aklan, Antique, Capiz, Guimaras, and Iloilo).

---

## 🚀 Featured Projects

---

### [01. Rice Planting Trends & Climate Variability (El Niño)](./01-Rice-Planting-Trends-El-Niño/)

[![View Live Dashboard](https://img.shields.io/badge/Power_BI_Live_Report-View_Interactive_Dashboard-0A5C36?style=for-the-badge&logo=powerbi)](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)
[![Read Case Study](https://img.shields.io/badge/Documentation-Read_Full_Case_Study-blue?style=for-the-badge&logo=github)](./01-Rice-Planting-Trends-El-Niño/)

#### 📸 Dashboard Preview
[![Rice Planting Trends Full Preview](./01-Rice-Planting-Trends-El-Niño/Rice%20Planting%20Trends%201.png)](./01-Rice-Planting-Trends-El-Niño/)

#### 📌 Overview & Business Value
* **Operational Problem:** Field data from municipal agriculture offices was isolated across fragmented yearly sheets (2018–2026), preventing program officers from tracking monsoon delays and planting disruptions during recurring El Niño episodes.
* **The Solution:** A centralized multi-year monitoring dashboard establishing an automated 3-year baseline benchmark (`Normal Year Average 2020–2022`) against confirmed El Niño cycles (`2018`, `2019`, `2023`, `2024`, and `2025`).
* **Key Findings:** Revealed an approximate two-month lag in peak planting during extreme dry spells, with rainfed farming systems sustaining over 55% of the overall regional climate risk exposure.

#### 🛠️ Tech Stack & Implementation
* **Tools:** Power BI Desktop, Power BI Service, Power Query (M Language), DAX
* **Data Transformations:** Multi-year append across heterogeneous yearly schemas, province/municipality cross-referencing, conditional climate epoch flags
* **Featured DAX Logic:** Dynamic baseline switching (`AVERAGEX`, `CALCULATE`, `HASONEVALUE`, `COALESCE`)

👉 **[Explore Full Project Documentation & DAX Breakdown →](./01-Rice-Planting-Trends-El-Niño/)**

---

### 02. Panay Rice Cost Structure 2025 *(Coming Next)*
* **Focus:** Cost of production per kilogram, line-item cost drivers, break-even thresholds, and return on investment (ROI) ranking across production methods (Irrigated vs Rainfed, Hybrid vs Inbred, TPR vs DSR).
* **Core Technique:** Disconnected metric matrix tables, custom dynamic currency format strings (`/kg`).

---

### 03. Rice Price Monitoring 2026 *(Coming Next)*
* **Focus:** Weekly palay farmgate and retail milled rice price dynamics across 5 provinces in Region VI.
* **Core Technique:** Clustered variance tracking, KPI callouts, dynamic price trend visual containers.

---

## 📋 Portfolio Catalog

| Project | Domain | Key Tech | Live Demo | Case Study |
| :--- | :--- | :--- | :---: | :---: |
| **01. Rice Planting Trends & El Niño** | Climate shock impact, monthly planting shifts, baseline benchmarking | Power Query, DAX, Time Series | [Live Report](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D) | [View Case Study](./01-Rice-Planting-Trends-El-Niño/) |
| **02. Panay Rice Cost Structure 2025** | Unit costs, ROI ranking, break-even benchmarks | Disconnected Matrix, Dynamic Formatting | *Pending Upload* | *Pending Upload* |
| **03. Rice Price Monitoring 2026** | Weekly palay & milled rice farmgate / market tracking | Multi-card layout, Dynamic `/kg` strings | *Pending Upload* | *Pending Upload* |

---

## 📬 Contact & Credentials
* **Analyst:** Abegail Vanjo G. Verdugo
* **Role:** Information Systems Analyst II / Data Analyst
* **Organization:** Department of Agriculture Regional Field Office VI (Western Visayas)
* **GitHub Profile:** [@abiyverdugo](https://github.com/abiyverdugo)
