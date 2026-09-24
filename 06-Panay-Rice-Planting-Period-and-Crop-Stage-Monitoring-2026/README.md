<div align="center">

# Western Visayas Rice Planting Period & Crop Growth Stage Monitoring 2026

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Crop_Stage_Modeling-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-Bi--Weekly_ETL-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

<p>
An operational rice monitoring dashboard built for the Department of Agriculture Regional Field Office VI (Rice Program). It tracks bi-weekly planting progress, counts participating farmers, and dynamically models live crop growth stages (Vegetative, Reproductive, and Ripening) based on days after planting.
</p>

</div>

---

<h2 align="center">📊 Live Interactive Dashboard</h2>

<div align="center">

Try the live report here:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiNzU4NTVjMDUtMDI2NC00OTliLWIxZWUtNTJiNTg5NDZiMWZkIiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

</div>

---

<h2 align="center">🎯 Project Overview & Why It Matters</h2>

Agricultural officers need to know not only how much land has been planted, but also which growth phase the standing crop is currently in. If a typhoon or pest infestation occurs, response teams need to know immediately how many hectares are in the vulnerable vegetative stage versus the ripening harvest phase.

### Problems Solved:
* **Dynamic Days After Planting (DAP) Calculation:** Normal spreadsheets only record static planting dates. Using dynamic DAX date logic tied to an evaluation calendar slicer (`[As of Date]`), the model calculates crop age in real time and automatically reclassifies standing hectares into Vegetative (0 to 60 days), Reproductive (61 to 90 days), or Ripening (91 to 120 days).
* **Double-Counting Unique Farmers:** Individual farmers often plant across multiple seed varieties and bi-weekly windows. Standard summation inflates headcounts. An iterated `SUMX(SUMMARIZE(...))` DAX measure extracts the true count of unique participating rice farmers (157,408 farmers) without duplication.
* **Bi-Weekly Calendar Sorting:** Field survey intervals such as `January 1 - 15` and `January 16 - 31` default to alphabetical order in standard charts. Power Query builds a dedicated mathematical index `(Month - 1) * 2 + Option` that guarantees strict chronological ordering across all visuals.

---

<h2 align="center">📸 Dashboard Overview</h2>

<div align="center">

### Planting Period & Crop Growth Stage Monitoring (2026)

<p align="center">
  <img src="Planting%20Period.png" alt="Planting Period Dashboard Preview" width="100%" />
</p>

</div>

* **Top Summary Ribbon:** Displays total planted land (234,829.58 ha), total physical rice farmland (257,922.88 ha), regional accomplishment rate (91.05%), and total verified participating farmers (157,408).
* **Crop Stage Area Breakdown Table:** Summarizes standing crop areas, percentage of physical land reached, and active farmers categorized across vegetative, reproductive, and ripening windows.
* **Crop Growth Stage Distribution Chart:** Visualizes standing rice volume across growth periods, illustrating how crops mature across successive bi-weekly cycles.
* **Planting Method Share:** Donut chart showing the operational divide between Direct Seeded Rice (DSR) at 92.6% and Transplanted Rice (TPR) at 7.4%.
* **Ecosystem Share:** Donut chart comparing Rainfed fields (58.42%) against Irrigated perimeters (41.58%).
* **Provincial Planting Trajectory:** Evaluates accomplishment percentages across Aklan, Antique, Capiz, Guimaras, and Iloilo.
* **Detailed Bi-Weekly Variety Matrix:** Granular matrix detailing certified seeds, good seeds, farmer-saved seeds, and hybrid seeds split by planting method.

---

<h2 align="center">🔬 Key Findings</h2>

1. **Direct Seeding Dominance:** Over **92.6%** (217.46K ha) of planted rice across the region is established via direct seeding, while transplanting accounts for only **7.4%** (17.37K ha). This highlights widespread farmer reliance on broadcasting methods to reduce labor costs.
2. **Rainfed Fragility:** Rainfed farmland accounts for **58.42%** of all planted area. Because these crops lack gravity canal irrigation, monitoring vegetative-stage timing is critical to prevent drought damage during mid-season dry spells.
3. **High Regional Target Completion:** Western Visayas reached **91.05%** accomplishment against its physical rice area baseline of 257,922.88 hectares, with Iloilo driving the majority of regional volume.

---

<h2 align="center">🏗️ How the Data Moves</h2>

<div align="center">

<table width="85%">
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📂 1. Field Reporting Spreadsheets</b><br/>
      <sub>Live Google Sheets collecting municipal bi-weekly planting reports, farmer counts, and seed breakdowns</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>⚙️ 2. Power Query Ingestion & Mapping Pipeline</b><br/>
      <sub>Splits reporting intervals into calendar dates, unpivots seed columns, joins farmer headcounts, and creates numerical sort indexes</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📊 3. Dynamic DAX Growth Stage Modeling</b><br/>
      <sub>Calculates days after planting from a dynamic evaluation date, categorizes growth phases, and deduplicates farmer totals</sub>
    </td>
  </tr>
</table>

</div>

---

<h2 align="center">💻 Core DAX Formulas & Growth Stage Modeling</h2>

### 1. Dynamic Evaluation Date & Growth Phase Calculation
Field teams need to evaluate standing crop stages as of any arbitrary inspection date or today's date. These measures dynamically calculate Days After Planting (DAP) and assign each planting cohort to its corresponding physiological stage.

```dax
As of Date = 
IF(
    ISFILTERED('Evaluation Calendar'[Date]), 
    MAX('Evaluation Calendar'[Date]), 
    TODAY()
)

Dynamic Growth Stage = 
VAR PDate = MAX('Planting PERIOD (Area)'[Planting Date])
VAR AsOf = [As of Date]
VAR DAP = DATEDIFF(PDate, AsOf, DAY)
RETURN
SWITCH(
    TRUE(),
    DAP >= 0 && DAP <= 60, "Vegetative Stage (0-60 Days)",
    DAP > 60 && DAP <= 90, "Reproductive Stage (61-90 Days)",
    DAP > 90 && DAP <= 120, "Ripening Stage (91-120 Days)",
    BLANK()
)
```
* **How it solves the problem:** Eliminates outdated reports. When an agricultural officer selects an evaluation date, the model recalculates the age of crops across all municipalities automatically.

---

### 2. Stage-Specific Area Aggregators
Disaster risk management requires knowing the exact number of hectares currently in vulnerable growth stages to estimate potential storm damage.

```dax
Vegetative Stage (60 Days) = 
VAR CurrentAsOfDate = [As of Date]
RETURN
    SUMX(
        'Planting PERIOD (Area)',
        VAR PlantedDate = 'Planting PERIOD (Area)'[Planting Date Ref]
        VAR DAP = INT(CurrentAsOfDate - PlantedDate)
        RETURN
            IF(
                NOT(ISBLANK(PlantedDate)) && DAP >= 0 && DAP <= 60,
                'Planting PERIOD (Area)'[Area Planted (Ha)],
                BLANK()
            )
    )

Reproductive Stage (30 Days) = 
VAR CurrentAsOfDate = [As of Date]
RETURN
    SUMX(
        'Planting PERIOD (Area)',
        VAR PlantedDate = 'Planting PERIOD (Area)'[Planting Date Ref]
        VAR DAP = INT(CurrentAsOfDate - PlantedDate)
        RETURN
            IF(
                NOT(ISBLANK(PlantedDate)) && DAP >= 61 && DAP <= 90,
                'Planting PERIOD (Area)'[Area Planted (Ha)],
                BLANK()
            )
    )

Ripening Stage (30 Days) = 
VAR CurrentAsOfDate = [As of Date]
RETURN
    SUMX(
        'Planting PERIOD (Area)',
        VAR PlantedDate = 'Planting PERIOD (Area)'[Planting Date Ref]
        VAR DAP = INT(CurrentAsOfDate - PlantedDate)
        RETURN
            IF(
                NOT(ISBLANK(PlantedDate)) && DAP >= 91 && DAP <= 120,
                'Planting PERIOD (Area)'[Area Planted (Ha)],
                BLANK()
            )
    )
```
* **How it solves the problem:** Iterates through individual field planting entries and sums only the hectares that fall strictly within the chosen day window, giving operational commanders accurate area numbers for emergency assistance.

---

### 3. Unique Farmer Deduplication
Farmer counts submitted across multiple seed programs and bi-weekly cycles can easily be overcounted if simply summed together.

```dax
Total No. of Farmers = 
SUMX(
    SUMMARIZE(
        'Planting PERIOD (Area)',
        'Planting PERIOD (Area)'[Province],
        'Planting PERIOD (Area)'[Municipality],
        'Planting PERIOD (Area)'[Reporting Period -],
        "UniquePeriodFarmers", MAX('Planting PERIOD (Area)'[No. of Farmers])
    ),
    [UniquePeriodFarmers]
)
```
* **How it solves the problem:** Summarizes data by province, municipality, and reporting period first, taking the unique maximum count per period before aggregating. This prevents multiplying farmer counts across multiple seed types.

---

### 4. Physical Area & Accomplishment Rate
Accomplishment percentages must be calculated against the true municipal land boundary without duplicating baseline land sizes across multiple reporting periods.

```dax
Total Physical Area (Ha) = 
SUMX(
    VALUES('Planting PERIOD (Area)'[Municipality]),
    CALCULATE(MAX('Planting PERIOD (Area)'[Physical Area]))
)

Planting Percentage = 
DIVIDE([Total Area Planted (Ha)], [Total Physical Area (Ha)], 0)
```
* **How it solves the problem:** Ensures each municipality's physical farmland baseline is counted only once, producing an accurate 91.05% accomplishment rate across the region.

---

<h2 align="center">🛠️ Tools Used</h2>

* **Power BI Desktop & Service:** Dynamic crop calendar modeling, interactive filter ribbons, and cloud deployment.
* **Power Query (M):** Cleaned complex bi-weekly periods, generated chronological sort keys, and unified mapping tables.
* **DAX:** Dynamic Days After Planting (DAP) logic, multi-stage area aggregations, and unique farmer deduplication.

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
