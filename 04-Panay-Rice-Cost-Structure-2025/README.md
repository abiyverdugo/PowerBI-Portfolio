<div align="center">

# Panay & Guimaras Rice Cost Structure & Farm Profitability 2025

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Financial_Modeling-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-ETL_Pipeline-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

<p>
An interactive farm economics dashboard built for the Department of Agriculture Regional Field Office VI (Rice Program). It tracks production expenses, farmgate palay pricing, break-even targets, and net earnings per hectare across all five provinces of Panay and Guimaras.
</p>

</div>

---

<h2 align="center">📊 Live Interactive Dashboard</h2>

<div align="center">

Try the live report here:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiNzcwMjE5MjUtODEwYy00ZDAzLTllZjUtYjk0OGIzOTFiNjc4IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

</div>

---

<h2 align="center">🎯 Project Overview & Why It Matters</h2>

Rice farmers face changing input costs for seeds, fertilizer, fuel, and field labor. Before this dashboard, production cost studies were handled in separate Google Sheets for each province, making it hard to compare profitability between planting methods like direct seeding and transplanting.

### Problems Solved:
* **Automated Data Gathering:** Created a Power Query pipeline using custom parsing functions (`fn_ParseItemized` and `fn_ParseProfitability`) that pulls live cost tables directly from Google Sheets across Iloilo, Aklan, Antique, Capiz, and Guimaras.
* **Cost Category Grouping:** Reorganized dozens of individual field expenses into three standardized main groups: **I. Inputs** (seeds, fertilizer, pest control), **II. Labor Cost** (land preparation, planting, harvesting), and **III. Miscellaneous & Other Costs** (irrigation fees, rentals, fuel, sacks).
* **Break-Even Analysis:** Calculated the minimum harvest yield (kg/ha) and minimum selling price (₱/kg) needed for farmers to cover expenses, helping regional leaders guide price support and mechanization efforts.

---

<h2 align="center">📸 Dashboard Overview</h2>

<div align="center">

### Panay Rice Cost Structure & Farm Economics (2025)

<p align="center">
  <img src="Cost%20Structure.png" alt="Panay Rice Cost Structure Dashboard Preview" width="100%" />
</p>

</div>

* **Top Expense Breakdown Cards:** Displays total regional cost per hectare split across Inputs (₱685,061.71), Labor (₱1,099,155.00), and Miscellaneous Expenses (₱160,131.00).
* **Farm Profitability KPI Ribbon:** Summarizes gross yield in cavans (99 bags), average cavan weight (44.94 kg), yield per hectare (4,443.06 kg/ha), average wet palay price (₱20.58/kg), production cost per hectare (₱62,720.89), net cash income (₱27,993.94), and return on investment (43.64%).
* **Break-Even Indicators:** Highlights the baseline financial targets required to avoid losses: **₱14.44/kg** selling price and **3,110.35 kg/ha** yield.
* **Costs by Establishment Method:** Compares net income and total costs across Mechanical Irrigated Hybrid TPR, Manual Irrigated Hybrid TPR, Irrigated Hybrid DSR, Irrigated Inbred DSR, and Rainfed Inbred DSR.
* **Hybrid vs. Inbred Returns:** Bar and line chart proving the profit gap between hybrid seeds and inbred seed varieties.
* **Detailed Expense & Metric Matrix:** Displays an itemized ledger of seed, chemical, and labor costs alongside dynamic metric definitions.

---

<h2 align="center">🔬 Key Findings</h2>

1. **Labor is the Biggest Expense:** Farm labor makes up **57%** of total rice production expenses, followed by material inputs at **35%**, and miscellaneous fees at **8%**. Land preparation, transplanting, and harvesting are the main drivers of labor costs.
2. **Hybrid Advantage:** Farms using hybrid seeds achieve higher yields (over 5,850 kg/ha) and bring in nearly double the net income per hectare compared to standard inbred seed fields.
3. **Machine Transplanting Saves Costs:** Using mechanical transplanters (Mechanical TPR) lowers labor costs and improves crop density, giving higher returns than traditional manual hand-transplanting.
4. **Safety Margin Above Break-Even:** With an average farmgate price of **₱20.58/kg** and a break-even price of **₱14.44/kg**, farmers maintained an average profit buffer of ₱6.14 per kilogram during the 2025 dry cropping season.

---

<h2 align="center">🏗️ How the Data Moves</h2>

<div align="center">

<table width="85%">
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📂 1. Provincial Cloud Spreadsheets</b><br/>
      <sub>Live Google Sheets for Iloilo, Aklan, Antique, Capiz, and Guimaras detailing itemized expenses and production returns</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>⚙️ 2. Power Query Ingestion & Categorization</b><br/>
      <sub>Custom parsing functions read sheets, standardize seed names, assign category sorting numbers, and create unique province-method keys</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📊 3. Power BI Financial Modeling & DAX</b><br/>
      <sub>Calculates category expense shares, evaluates break-even thresholds, and formats values with dynamic currency and weight symbols</sub>
    </td>
  </tr>
</table>

</div>

---

<h2 align="center">💻 Main DAX Calculations</h2>

### 1. Cost Category Grouping Measures
Calculates the exact expense sums for inputs, labor, and miscellaneous items from the itemized dataset:
```dax
I. INPUTS = 
CALCULATE(
    SUM(Cost_Structure_Master_Itemized[Amount (Php)]),
    Cost_Structure_Master_Itemized[Category] = "I. INPUTS"
)

II. LABOR COST = 
CALCULATE(
    SUM(Cost_Structure_Master_Itemized[Amount (Php)]),
    Cost_Structure_Master_Itemized[Category] = "II. LABOR COST"
)

III. MISCELLANEOUS & OTHER COSTS = 
CALCULATE(
    SUM(Cost_Structure_Master_Itemized[Amount (Php)]),
    Cost_Structure_Master_Itemized[Category] = "III. MISCELLANEOUS & OTHER COSTS"
)
```

### 2. Category Share Percentage
Calculates what portion of total spending goes into labor:
```dax
Labor % Share = 
DIVIDE([II. LABOR COST], [Total Production Costs], 0)
```

### 3. Dynamic Matrix Switch Measure
Formats matrix rows with their correct currency symbols (₱), weight units (kg, kg/ha), and percentages (%) based on the selected metric row:
```dax
Profitability Value = 
VAR SelectedMetric = SELECTEDVALUE('Profitability_Metrics_Ref'[Metric Name])
RETURN
    SWITCH(
        SelectedMetric,
        "Gross yield in cavans (No. of Bags)", FORMAT([Gross yield in cavans (No. of Bags)], "#,##0"),
        "Average weight in kg/Cavan",          FORMAT([Average weight in kg/Cavan], "#,##0") & " kg",
        "Yield (kg/ha)",                       FORMAT([Yield (kg/ha)], "#,##0") & " kg/ha",
        "Price per kg (Wet) Php/kg",           FORMAT([Price per kg (Wet) Php/kg], "₱#,##0.00") & "/kg",
        "Total Production Costs",              FORMAT([Total Production Costs], "₱#,##0.00"),
        "Gross Income",                        FORMAT([Gross Income], "₱#,##0.00"),
        "Net Cash Income",                     FORMAT([Net Cash Income], "₱#,##0.00"),
        "Return on Investment (%)",            FORMAT([Return on Investment (%)], "0.00%"),
        "Break-Even Price (Php/kg)",           FORMAT([Break-Even Price (Php/kg)], "₱#,##0.00") & "/kg",
        "Break-Even Yield (kg/ha)",            FORMAT([Break-Even Yield (kg/ha)], "#,##0.00") & " kg/ha"
    )
```

---

<h2 align="center">🛠️ Tools Used</h2>

* **Power BI Desktop & Service:** Built interactive visual models, financial KPI ribbons, and web-published reports.
* **Power Query (M):** Built custom functions to parse Google Sheets, normalized itemized costs, and mapped category sorting orders.
* **DAX:** Formatted break-even indicators, cost proportions, and dynamic matrix values.

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
