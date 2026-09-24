<div align="center">

# Western Visayas Rice Price Monitoring Analytics 2026

[![Power BI](https://img.shields.io/badge/Power_BI-Desktop_%26_Service-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Price_Intelligence-045C36)](https://learn.microsoft.com/en-us/dax/)
[![Power Query](https://img.shields.io/badge/Power_Query-Buffer_ETL-238636)](https://learn.microsoft.com/en-us/power-query/)
[![Region](https://img.shields.io/badge/Region-Western_Visayas-0A5C36)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

<p>
A weekly price monitoring dashboard built for the Department of Agriculture Regional Field Office VI (Rice Program). It tracks farmgate palay buying prices and retail commercial rice prices across Aklan, Antique, Capiz, Guimaras, and Iloilo to protect farmer incomes and watch market price changes.
</p>

</div>

---

<h2 align="center">📊 Live Interactive Dashboard</h2>

<div align="center">

Try the live report here:

👉 **[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMWFhOWIxNGItOGMyMC00ZGUyLWE4MDgtZWQ0ZmJjMTU2NTI4IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)**

</div>

---

<h2 align="center">🎯 Project Overview & Why It Matters</h2>

Rice prices change every week depending on harvest seasons, local supply, and transport costs. Before this dashboard, field price monitors recorded data across wide, complex spreadsheets with stacked headers for months, weeks, and grain qualities. Comparing farmgate prices to wet market retail prices required manual calculations.

### Problems Solved:
* **Reading Complex Multi-Header Sheets:** Built an automated Power Query ETL pipeline that unpivots multi-tier headers (Month, Week Period, Grain Category, and Quality Grade) from live Google Sheets into a clean fact table.
* **Separating Palay from Milled Rice:** Cleaned seed categories so that farmgate palay (Fresh and Dry) is analyzed separately from market retail rice (Regular Milled, Well Milled, Premium, and Fancy), making it easy to track the price gap between farm and consumer.
* **Guaranteed Date & Week Sorting:** Created a custom numeric sort key formula `(Month Number * 100) + StartDay` in Power Query. This ensures that weekly tracking labels like `Jan (1-2)` and `Sep (7-11)` always sort chronologically instead of alphabetically.

---

<h2 align="center">📸 Dashboard Overview</h2>

<div align="center">

### Western Visayas Rice Price Monitoring (2026)

<p align="center">
  <img src="Price%20Monitoring.png" alt="Price Monitoring Dashboard Preview" width="100%" />
</p>

</div>

* **Top Price KPI Ribbon:** Displays regional benchmark prices for Fresh Palay (₱18.93/kg), Dry Palay (₱22.82/kg), Regular Milled Rice (₱45.49/kg), Well Milled Rice (₱49.56/kg), Premium Rice (₱54.30/kg), and Fancy Rice (₱61.49/kg).
* **Price by Province:** Stacked bar chart comparing local price levels across Aklan, Antique, Capiz, Guimaras, and Iloilo.
* **Monthly Price Trajectory Area Chart:** Tracks how market prices rise or fall across months, showing seasonality shifts and peak harvest adjustments.
* **Price Distribution by Statistic Type:** Analyzes market pricing across Mode (most frequent price), Minimum, Maximum, and Average benchmarks.
* **Weekly Price Matrix Table:** Detailed grid displaying weekly prices across provinces, sectors, and grain classifications.

---

<h2 align="center">🔬 Key Findings</h2>

1. **The Farmgate to Retail Price Gap:** Dry palay sells at an average farmgate price of **₱22.82/kg**, while Regular Milled Rice (RMR) retails at **₱45.49/kg** and Well Milled Rice (WMR) at **₱49.56/kg**. This shows a steady milling and retail margin of approximately ₱23 to ₱27 per kilogram.
2. **Fresh vs. Dry Palay Difference:** Freshly harvested wet palay sells at **₱18.93/kg**, compared to **₱22.82/kg** for dry palay. The **₱3.89/kg** premium demonstrates the economic value of regional solar and mechanical drying facilities.
3. **Provincial Price Consistency:** Aklan and Iloilo maintain the highest trading volumes, while island transport logistics in Guimaras create slight price premiums for commercial retail rice grades.

---

<h2 align="center">🏗️ How the Data Moves</h2>

<div align="center">

<table width="85%">
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📂 1. Live Google Sheets Monitoring Feeds</b><br/>
      <sub>Field-submitted weekly price tracking sheets with multi-row headers for months, weeks, and rice categories</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>⚙️ 2. Power Query In-Memory ETL Pipeline</b><br/>
      <sub>Uses Table.Buffer to load sheets fast, matches headers by column position, extracts dates, and assigns chronological week sort numbers</sub>
    </td>
  </tr>
  <tr>
    <td align="center">⬇️</td>
  </tr>
  <tr>
    <td align="center" style="padding: 14px;">
      <b>📊 3. Power BI Price Intelligence Measures</b><br/>
      <sub>Filters grain qualities dynamically, powers KPI cards, and evaluates price variance across provinces</sub>
    </td>
  </tr>
</table>

</div>

---

<h2 align="center">💻 Core DAX Formulas & Price Intelligence</h2>

### 1. Farmgate Palay Price Isolation (Fresh vs. Dry)
Farmers need to know whether selling wet palay at harvest is fair compared to drying it first. These measures isolate buying prices for both types:

```dax
Fresh = 
CALCULATE(
    AVERAGE(Fact_Weekly_Price_Monitoring[Price (Php/kg)]),
    Fact_Weekly_Price_Monitoring[Sub-Category] = "Fresh"
)

Dry = 
CALCULATE(
    AVERAGE(Fact_Weekly_Price_Monitoring[Price (Php/kg)]),
    Fact_Weekly_Price_Monitoring[Sub-Category] = "Dry"
)
```
* **How it solves the problem:** Isolates the farmgate buying rate for wet palay (₱18.93/kg) versus dried palay (₱22.82/kg), giving field officers exact data to determine if drying support is paying off for farmers.

---

### 2. Commercial Retail Rice Monitoring (RMR & WMR)
Regular Milled Rice and Well Milled Rice are staple purchases for families. Monitoring these grades helps detect unexpected market spikes:

```dax
RMR = 
CALCULATE(
    AVERAGE(Fact_Weekly_Price_Monitoring[Price (Php/kg)]),
    Fact_Weekly_Price_Monitoring[Sub-Category] = "RMR"
)

WMR = 
CALCULATE(
    AVERAGE(Fact_Weekly_Price_Monitoring[Price (Php/kg)]),
    Fact_Weekly_Price_Monitoring[Sub-Category] = "WMR"
)
```
* **How it solves the problem:** Separates common consumer rice grades from farm palay, allowing market inspectors to compare farmgate increases directly against consumer price tags.

---

### 3. Specialty & High-End Rice Grades (Premium & Fancy)
Specialty varieties sell at higher price points for specific culinary markets:

```dax
Premium = 
CALCULATE(
    AVERAGE(Fact_Weekly_Price_Monitoring[Price (Php/kg)]),
    Fact_Weekly_Price_Monitoring[Sub-Category] = "Premium"
)

Fancy = 
CALCULATE(
    AVERAGE(Fact_Weekly_Price_Monitoring[Price (Php/kg)]),
    Fact_Weekly_Price_Monitoring[Sub-Category] = "Fancy"
)
```
* **How it solves the problem:** Tracks price ceilings in the market (reaching up to ₱61.49/kg), providing guidance for farmers considering higher-value seed varieties.

---

<h2 align="center">🛠️ Tools Used</h2>

* **Power BI Desktop & Power BI Service:** Built multi-tier card ribbons, price trend areas, and cloud-shared dashboards.
* **Power Query (M):** Used memory buffering (`Table.Buffer`), matrix unpivoting, and custom sorting keys to structure messy field surveys.
* **DAX:** Filtered price categories dynamically across weekly and monthly time frames.

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
