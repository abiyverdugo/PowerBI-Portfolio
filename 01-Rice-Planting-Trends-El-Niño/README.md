# Rice Planting Trends & Climate Variability (El Niño Analysis 2018–2026)

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Time_Series_Averaging-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-M_ETL_Pipeline-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas_(Region_VI)-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

A Business Intelligence and climate vulnerability reporting system built for the Department of Agriculture Regional Field Office VI (Rice Program & Agricultural Statistics). This analytical framework evaluates nine years of monthly planting records across Western Visayas to quantify delayed monsoon shifts and measure hectare losses triggered by recurring El Niño weather anomalies.

---

## 📊 Live Interactive Dashboard

Explore the live, interactive Power BI report:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

---

## 🎯 Executive Summary & Analytical Objective

Severe climatic shock events such as El Niño create major operational uncertainty for rice farmers across Western Visayas. When rainfall is delayed or curtailed, farmers delay field preparation and transplanting, concentrating harvesting operations into wet, typhoon-prone months.

### Core Problems Solved:
* **The Normal Baseline Benchmark Problem:** Comparing individual years directly against single prior years created volatility. By aggregating non-El Niño cropping years (`2020`, `2021`, `2022`) into an automated dynamic baseline (`Normal Year Average (2020–2022)`), regional decision-makers gained an objective benchmark to measure real crop shifts[cite: 33].
* **Dynamic Year-Level Aggregation:** Normal reporting summed multi-year areas into inflated numbers. An iterative `AVERAGEX` DAX measure dynamically computes true annual averages when multiple years are grouped while preserving exact figures when single years are selected.
* **Ecosystem Vulnerability Mapping:** Separated irrigated gravity systems from rainfed lowland and upland zones to pinpoint exactly where water shortages stop field work[cite: 33].

---

## 📸 Dashboard Visuals & Structure

### Page 1: El Niño Years Trends & Baseline Comparison
![Rice Planting Trends 1](Rice%20Planting%20Trends%201.png)

* **Multi-Year Line Trajectory:** Plots monthly planting progressions from January through December, benchmarking individual El Niño cycles (`2018`, `2019`, `2023`, `2024`, `2025`) and current operations (`2026`) against the `Normal Year Average (2020–2022)`[cite: 33].
* **Planting Share Distribution:** Proportional breakdown showing annual contribution shares and regional volume balances[cite: 33].
* **Ecosystem Matrix Table:** Granular accounting matrix evaluating Irrigated vs. Rainfed (Lowland/Upland) areas across Aklan, Antique, Capiz, Guimaras, and Iloilo[cite: 33].
* **Interactive Slicers:** Full dynamic slicing across Quarters (Q1–Q3), Months (Jan–Dec), Ecosystems, Sub-Ecosystems, and Seed Varieties[cite: 33].

---

## 🔬 Key Agricultural Insights

1. **Two-Month Planting Delay:** Under baseline conditions (`Normal Year Average 2020–2022`), peak regional planting occurs sharply in **June** (~120K ha)[cite: 33]. During El Niño shock periods (`2018`, `2019`, `2023`, `2024`), peak planting shifts two months backward into **August and September**[cite: 33].
2. **Rainfed Vulnerability:** Rainfed lowland areas show severe contraction between May and July during drought years, accounting for over 55% of total delayed planting volume in Western Visayas[cite: 33].
3. **Provincial Exposure:** Iloilo and Capiz report the highest absolute hectare shifts during severe dry events, driving regional demand for supplemental pump irrigation and adjusted seed distribution windows[cite: 33].

---

## 🏗️ Data Architecture & Pipeline

```text
+-------------------------------------------------------------------------------+
| Raw Data Sources                                                              |
| - Historical Archives: Disconnected annual master files (2018-2025)           |
| - Live Operational Feeds: Active 2026 data monitoring tab                     |
+---------------------------------------+---------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| Power Query (M) Automated ETL                                                 |
| - Table.Combine: Merging historical 2018-2025 with 2026 active records        |
| - Dynamic Year Classification: Segregates 2020-2022 into "Normal Year Average" |
| - Label Normalization: Clean regex replacements for Pie Chart legends         |
| - Text Cleansing: "FARMER SAVED SEEDS" -> "FARMERS HOME SAVED SEEDS"          |
+---------------------------------------+---------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| DAX Calculation Layer                                                         |
| - Dynamic Baseline Measure: AVERAGEX over VALUES('Year')                      |
| - Context-Aware Aggregation: Direct SUM on single select; Mean on grouped view |
| - Cross-filtering across Month, Ecosystem, and Seed Type dimensions           |
+-------------------------------------------------------------------------------+
```

---

## 💻 Core DAX & Power Query Implementation

### 1. Dynamic Adjusted Planting Area (DAX)
Solves the aggregation problem by evaluating whether the visual filter context contains a single year or a multi-year baseline cluster:

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

### 2. Multi-Year Append & Climate Labeling (Power Query M)
Ingests historical files, appends current-year operational records, tags climate events, and cleans chart legends:

```powerquery
let
    Source = Table.Combine({#"2018-2025", #"2026"}),
    #"Added Conditional Column" = Table.AddColumn(Source, "Year Type", each 
        if [Year] = 2020 then "Normal Year Average (2020-2022)" 
        else if [Year] = 2021 then "Normal Year Average (2020-2022)" 
        else if [Year] = 2022 then "Normal Year Average (2020-2022)" 
        else if [Year] = 2018 then "2018 (El Niño Year)" 
        else if [Year] = 2019 then "2019 (El Niño Year)" 
        else if [Year] = 2023 then "2023 (El Niño Year)" 
        else if [Year] = 2024 then "2024 (El Niño Year)" 
        else if [Year] = 2025 then "2025 (El Niño Year)" 
        else if [Year] = 2026 then "2026 (Current Year)" 
        else Text.From([Year])
    ),
    #"Filtered Rows" = Table.SelectRows(#"Added Conditional Column", each true),
    #"Renamed Columns" = Table.RenameColumns(#"Filtered Rows",{{"Year Type", "Year Label"}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Renamed Columns",{{"Year Label", type text}}),
    #"Added Conditional Column1" = Table.AddColumn(#"Changed Type", "Month Number", each 
        if [Month Short] = "Jan" then 1 
        else if [Month Short] = "Feb" then 2 
        else if [Month Short] = "Mar" then 3 
        else if [Month Short] = "Apr" then 4 
        else if [Month Short] = "May" then 5 
        else if [Month Short] = "Jun" then 6 
        else if [Month Short] = "Jul" then 7 
        else if [Month Short] = "Aug" then 8 
        else if [Month Short] = "Sep" then 9 
        else if [Month Short] = "Oct" then 10 
        else if [Month Short] = "Nov" then 11 
        else if [Month Short] = "Dec" then 12 
        else null
    ),
    #"Reordered Columns" = Table.ReorderColumns(#"Added Conditional Column1",{"Year", "Quarter", "Month Number", "Month", "Month Short", "Province", "Municipality", "Ecosystem", "Sub-Ecosystem", "Seed Type", "Area Planted (Ha)", "Year Label"}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Reordered Columns",{{"Month Number", Int64.Type}}),
    #"Replaced Value" = Table.ReplaceValue(#"Changed Type1","FARMER SAVED SEEDS","FARMERS HOME SAVED SEEDS",Replacer.ReplaceText,{"Seed Type"}),
    #"Replaced Value1" = Table.ReplaceValue(#"Replaced Value","","-",Replacer.ReplaceValue,{"Sub-Ecosystem"}),
    #"Filtered Rows1" = Table.SelectRows(#"Replaced Value1", each true),
    #"Reordered Columns1" = Table.ReorderColumns(#"Filtered Rows1",{"Year Label", "Year", "Quarter", "Month Number", "Month", "Month Short", "Province", "Municipality", "Ecosystem", "Sub-Ecosystem", "Seed Type", "Area Planted (Ha)"}),
    #"Duplicated Column" = Table.DuplicateColumn(#"Reordered Columns1", "Year Label", "Year Label - Copy"),
    #"Reordered Columns2" = Table.ReorderColumns(#"Duplicated Column",{"Year Label - Copy", "Year Label", "Year", "Quarter", "Month Number", "Month", "Month Short", "Province", "Municipality", "Ecosystem", "Sub-Ecosystem", "Seed Type", "Area Planted (Ha)"}),
    #"Renamed Columns1" = Table.RenameColumns(#"Reordered Columns2",{{"Year Label - Copy", "Pie Chart Legend"}}),
    #"Replaced Value2" = Table.ReplaceValue(#"Renamed Columns1","(El Niño Year)","",Replacer.ReplaceText,{"Pie Chart Legend"}),
    #"Replaced Value3" = Table.ReplaceValue(#"Replaced Value2"," (Current Year)","",Replacer.ReplaceText,{"Pie Chart Legend"}),
    #"Replaced Value4" = Table.ReplaceValue(#"Replaced Value3","Normal Year Average ","",Replacer.ReplaceText,{"Pie Chart Legend"}),
    #"Filtered Rows2" = Table.SelectRows(#"Replaced Value4", each true)
in
    #"Filtered Rows2"
```

---

## 🛠️ Tools & Technologies Used
* **Business Intelligence Platform:** Power BI Desktop, Power BI Service
* **Analytical Modeling:** Dynamic time-series baseline benchmarking, multi-year trend grouping
* **ETL Engineering:** Power Query (M Language), schema unification, conditional labeling, text normalization
* **Data Context:** Western Visayas Provincial Coverage (Aklan, Antique, Capiz, Guimaras, Iloilo)[cite: 33]

---

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
