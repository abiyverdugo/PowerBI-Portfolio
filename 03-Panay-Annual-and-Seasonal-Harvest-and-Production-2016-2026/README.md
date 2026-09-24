<div align="center">

# Western Visayas Rice Harvest & Production Analytics (2016–2026)

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Calculations-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-Data_Cleaning-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

<p>
An interactive Business Intelligence reporting system built for the Department of Agriculture Regional Field Office VI (Rice Program). It tracks 10 years of municipal rice harvesting, crop yields (MT/ha), and production volumes (MT) across Panay and Guimaras.
</p>

</div>

---

<h2 align="center">📊 Live Interactive Dashboard</h2>

<div align="center">

Try the live report here:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiYWMzM2I1OWEtYzhkZS00OWNiLWE2ZTMtNzU2MzY5OTdiYTRlIiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

</div>

---

<h2 align="center">🎯 Project Overview & Why It Matters</h2>

Monitoring regional rice harvest performance previously required manually consolidating dozens of monthly Excel files from different towns and field offices. Because formatting changed between cropping years, regional managers found it difficult to quickly compare real farm yields and harvest totals.

### Problems Solved:
* **Combining Historical Files with Live Data:** Built an automated Power Query pipeline that merges 10 years of archived municipal records (2016–2025) with a live 2026 Google Sheet feed without manual copying.
* **Fixing Double-Counted Inbred Seeds:** Original reports placed broad "Inbred Seeds" totals in the same column list as detailed seed types (Certified Seeds, Good Seeds, and Farmer Saved Seeds). Custom DAX measures filter out the summary line so harvest areas and production tons are not counted twice.
* **Tracking Real Farmland Productivity:** Standardized the calculation for average yield (`Production (MT) / Area Harvested (ha)`) so team leaders can evaluate farm performance across irrigated plains, rainfed lowlands, and upland areas.

---

<h2 align="center">📸 Dashboard Pages</h2>

<div align="center">

### Page 1: Annual Harvest & Production Performance (2016–2026)

<p align="center">
  <img src="Annual%20Harvest%202016-2026.png" alt="Annual Harvest 2016-2026" width="100%" />
</p>

</div>

* **Top Summary KPIs:** Displays cumulative area harvested (4.98M ha), average yield (4.03 MT/ha), and total regional rice production (20.07M metric tons).
* **Harvest Area by Seed Type & Province:** Compares the usage of Certified Seeds (CS), Good Seeds (GS), Farmers Home Saved Seeds (FSS), and Hybrid Seeds across Aklan, Antique, Capiz, Guimaras, and Iloilo.
* **Production vs. Yield Progression:** Dual-axis visual charting harvest volume trends against average crop yields over a 10-year span.
* **Provincial Harvest Rankings:** Highlights total output per province, led by Iloilo (2.62M ha harvested) and Capiz (1.03M ha harvested).
* **Detailed Municipal Matrix:** Table detailing area harvested, average yield, and production across ecosystems and seed categories.

---

<div align="center">

### Page 2: Seasonal Harvest Dynamics (Dry Season vs. Wet Season)

<p align="center">
  <img src="Seasonal%20Harvest%202016-2026.png" alt="Seasonal Harvest 2016-2026" width="100%" />
</p>

</div>

* **Seasonal Production Balance:** Compares harvest outputs between dry-season and wet-season cropping calendars.
* **Harvest Pace Curves:** Maps which months experience the largest harvest peaks to guide post-harvest drying facility operations.
* **Ecosystem Yield Comparison:** Analyzes yield differences between irrigated farms and rainfed farms across seasons.

---

<h2 align="center">🔬 Key Findings</h2>

1. **Regional Production Center:** Iloilo accounts for more than half of the region's total rice harvest, producing over 10.4 million metric tons between 2016 and 2026.
2. **Hybrid Seed Yield Advantage:** Hybrid rice varieties consistently reach average yields above **5.14 MT/ha**, compared to 4.49 MT/ha for Certified Seeds (CS) and 3.65 MT/ha for Farmer Saved Seeds (FSS).
3. **Irrigation Stability:** Irrigated rice farms maintain consistent yields averaging **4.38 MT/ha**, while rainfed upland tracts fluctuate near **3.30 MT/ha**, showing high vulnerability to dry weather periods.

---

<h2 align="center">🏗️ How the Data Moves</h2>

<div align="center">

<table width="85%">
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📂 1. Multi-Source Raw Files</b><br/>
      <sub>Folder archives of 2016–2025 monthly harvest workbooks combined with a live 2026 Google Sheet feed</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>⚙️ 2. Automated Power Query Data Ingestion</b><br/>
      <sub>Unpivots complex 30-column matrix sheets, extracts area and production figures, standardizes town names, and builds time attributes</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📊 3. Power BI Modeling & DAX Calculation Engine</b><br/>
      <sub>Removes double counting, computes crop yields (MT/ha), and calculates dynamic year-over-year comparison indicators</sub>
    </td>
  </tr>
</table>

</div>

---

<h2 align="center">💻 Main DAX Calculations</h2>

### 1. Average Yield (MT/ha)
Calculates true yield by dividing total volume in metric tons by harvested area:
```dax
Ave. Yield (MT/ha) = 
DIVIDE([Total Production (MT)], [Total Area Harvested (ha)], 0)
```

### 2. Harvested Area (Double-Count Prevention)
Sums area while filtering out the generic "Inbred Seeds" aggregate row unless explicitly selected:
```dax
Total Area Harvested (ha) = 
IF(
    HASONEVALUE('Harvest & Production Annual 2016-2026 (Normalized)'[Seed Type]),
    SUM('Harvest & Production Annual 2016-2026 (Normalized)'[Area Harvested (ha)]),
    CALCULATE(
        SUM('Harvest & Production Annual 2016-2026 (Normalized)'[Area Harvested (ha)]),
        KEEPFILTERS('Harvest & Production Annual 2016-2026 (Normalized)'[Seed Type] <> "INBRED SEEDS")
    )
)
```

### 3. Total Production (Double-Count Prevention)
Sums production metric tons safely without duplicating inbred sub-varieties:
```dax
Total Production (MT) = 
IF(
    HASONEVALUE('Harvest & Production Annual 2016-2026 (Normalized)'[Seed Type]),
    SUM('Harvest & Production Annual 2016-2026 (Normalized)'[Production (MT)]),
    CALCULATE(
        SUM('Harvest & Production Annual 2016-2026 (Normalized)'[Production (MT)]),
        KEEPFILTERS('Harvest & Production Annual 2016-2026 (Normalized)'[Seed Type] <> "INBRED SEEDS")
    )
)
```

### 4. Dynamic Year-over-Year Production Indicator
Finds growth between the earliest and latest active years and formats it with indicator arrows:
```dax
Production YoY Label = 
VAR MinYr = MIN('Harvest & Production Annual 2016-2026 (Normalized)'[Year])
VAR MaxYr = MAX('Harvest & Production Annual 2016-2026 (Normalized)'[Year])
VAR StartVal = 
    CALCULATE(
        [Total Production (MT)],
        'Harvest & Production Annual 2016-2026 (Normalized)'[Year] = MinYr
    )
VAR EndVal = 
    CALCULATE(
        [Total Production (MT)],
        'Harvest & Production Annual 2016-2026 (Normalized)'[Year] = MaxYr
    )
VAR Growth = DIVIDE(EndVal - StartVal, StartVal, 0)
RETURN
IF(
    MinYr = MaxYr,
    "--",
    IF(Growth >= 0, "▲ +" & FORMAT(Growth, "0.0%"), "▼ " & FORMAT(Growth, "0.0%"))
)
```

---

<h2 align="center">🛠️ Tools Used</h2>

* **Power BI Desktop & Power BI Service:** For data modeling, visual analytics, and cloud reporting.
* **Power Query (M):** For unpivoting complex matrices, merging web feeds, and standardizing locations.
* **DAX:** For yield ratios, growth measures, and seed variety deduplication.

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
