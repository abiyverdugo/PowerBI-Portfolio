# Agricultural Business Intelligence & Power BI Portfolio

### **Abegail Vanjo (Abiy) G. Verdugo**
*Information Systems Analyst II / Data Analyst*  
**Department of Agriculture RFO VI — Rice Program & Agricultural Statistics**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/abiyverdugo/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/abiyverdugo)
[![Email](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:abegailvanjoverdugo@gmail.com)

---

## 🛠️ Technical Skills & Tools

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-045C36?style=for-the-badge&logo=dax&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-238636?style=for-the-badge&logo=powerquery&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)
![Microsoft Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Zapier](https://img.shields.io/badge/Zapier-FF4A00?style=for-the-badge&logo=zapier&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)

---

## 👤 About the Author

I am an **Information Systems Analyst II / Data Analyst** at the Department of Agriculture Regional Field Office VI (Western Visayas). My primary focus involves architecting automated data pipelines, developing executive Business Intelligence reports, and performing climate shock and economic viability evaluations across Panay and Guimaras (Aklan, Antique, Capiz, Guimaras, and Iloilo).

* **Education:** B.S. in Computer Science
* **Domain:** Agricultural Statistics, Climate Impact Analysis, Farmgate Economics, and Production Benchmarking
* **Data Sources:** Cleaned and normalized from regional master datasets including historical production records (2016–2026), cost-of-production structures, and weekly palay price monitoring systems.

---

## 🌾 Featured Projects

---

### [01. Rice Planting Trends & Climate Variability (El Niño Analysis)](./01-Rice-Planting-Trends-El-Ni%C3%B1o/)

[![View Live Dashboard](https://img.shields.io/badge/Power_BI_Live_Report-View_Interactive_Dashboard-0A5C36?style=for-the-badge&logo=powerbi)](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)
[![Read Case Study](https://img.shields.io/badge/Documentation-Read_Full_Case_Study-blue?style=for-the-badge&logo=github)](./01-Rice-Planting-Trends-El-Ni%C3%B1o/)

#### 📸 Dashboard Preview
<p align="center">
  <a href="./01-Rice-Planting-Trends-El-Ni%C3%B1o/">
    <img src="./01-Rice-Planting-Trends-El-Ni%C3%B1o/Rice%20Planting%20Trends%201.png" alt="Rice Planting Trends Dashboard Preview" width="100%"/>
  </a>
</p>

#### 📌 Overview & Operational Value
* **Business Problem:** Municipal-level rice planting submissions were recorded across disconnected yearly sheets (2018–2026), making it difficult for regional executives to detect seasonal planting shifts or calculate delays caused by recurring El Niño cycles.
* **The Analytics Solution:** Built a 2-page time-series monitoring dashboard appending 9 years of regional data, establishing an automated 3-year baseline benchmark (`Normal Year Average 2020–2022`) against historical and active El Niño years (`2018`, `2019`, `2023`, `2024`, and `2025`).
* **Key Findings:** Revealed that severe drought pushed seasonal peak planting back by two months (from June/July into August/September), with rainfed systems bearing more than 55% of total climate vulnerability across Western Visayas.

👉 **[Explore Full Project Case Study & DAX Code →](./01-Rice-Planting-Trends-El-Ni%C3%B1o/)**

---

### [02. Panay & Guimaras Rice Planting Analytics (Annual & Seasonal 2016–2026)](./02-Panay-Annual-and-Seasonal-Planting-2016-2026/)

[![View Live Dashboard](https://img.shields.io/badge/Power_BI_Live_Report-View_Interactive_Dashboard-0A5C36?style=for-the-badge&logo=powerbi)](https://app.powerbi.com/view?r=eyJrIjoiMTc0ZGFkMjEtMTZmOS00Zjg1LWI4ODYtMDc0ZDA3NTg0ZWM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D)
[![Read Case Study](https://img.shields.io/badge/Documentation-Read_Full_Case_Study-blue?style=for-the-badge&logo=github)](./02-Panay-Annual-and-Seasonal-Planting-2016-2026/)

#### 📸 Dashboard Preview
<p align="center">
  <a href="./02-Panay-Annual-and-Seasonal-Planting-2016-2026/">
    <img src="https://raw.githubusercontent.com/abiyverdugo/PowerBI-Portfolio/main/02-Panay-Annual-and-Seasonal-Planting-2016-2026/Annual%20Planting%202016-2026.png" alt="Annual Planting Dashboard Preview" width="100%"/>
  </a>
</p>

#### 📌 Overview & Operational Value
* **Business Problem:** Assessing annual and seasonal planting efficiency required aggregating 10+ years of municipal reporting while accounting for repeated cropping cycles across a static physical rice area footprint (258K ha).
* **The Analytics Solution:** Developed an end-to-end data pipeline combining historical Excel archives with a live 2026 Google Sheet feed. Implemented DAX cross-filtering and double-count prevention measures to benchmark progress across 5 provinces, 4 seed types, and 2 ecosystems.
* **Key Findings:** Mapped regional planting patterns, demonstrating that Certified Seeds lead overall adoption (51.47%), while Iloilo represents over 51% of total planting volume across Western Visayas.

👉 **[Explore Full Project Case Study & DAX Code →](./02-Panay-Annual-and-Seasonal-Planting-2016-2026/)**

---

### [03. Panay Rice Cost Structure & Profitability 2025](#) *(In Development)*
* **Domain:** Agricultural Economics, Break-Even Analysis, Farm Profitability
* **Summary:** Evaluates production methods (Irrigated vs. Rainfed, Hybrid vs. Inbred, Mechanical TPR vs. Direct Wet Seeding) across unit costs, break-even thresholds (₱/kg and kg/ha), and Return on Investment (ROI %).
* **Core Technique:** Disconnected metric matrix tables, Dynamic Format Strings (`/kg`).

---

### [04. Panay Rice Price Monitoring 2026](#) *(In Development)*
* **Domain:** Market Intelligence & Weekly Farmgate Price Fluctuations
* **Summary:** Real-time tracking of fresh palay, dry palay, regular milled rice (RMR), and well-milled rice (WMR) across all 5 Panay-Guimaras provinces.
* **Core Technique:** Multi-card visual layouts, price spread variance measures.

---

## 📋 Comprehensive Project Catalog

| # | Project Name | Primary Focus | Modeling Architecture | Case Study | Interactive Demo |
| :---: | :--- | :--- | :--- | :---: | :---: |
| **01** | **Rice Planting Trends & El Niño Variability** | Climate shock analysis, delayed monsoon peaks, baseline benchmarking | Multi-year append, dynamic baseline DAX | [View Project](./01-Rice-Planting-Trends-El-Ni%C3%B1o/) | [Live Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODdlYmRiMDMtNDI0MS00NmRiLTk0YTItNmViNWE4NGRiZTM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D) |
| **02** | **Annual & Seasonal Planting Analytics (2016–2026)** | 10-year trend monitoring, accomplishment rates, seed class adoption | Bi-directional cross-filtering, live Google Sheet append | [View Project](./02-Panay-Annual-and-Seasonal-Planting-2016-2026/) | [Live Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMTc0ZGFkMjEtMTZmOS00Zjg1LWI4ODYtMDc0ZDA3NTg0ZWM2IiwidCI6IjI1MzYzMDI3LTUyNjQtNGE1Mi04MmRjLTgzYWNiZTMwY2M4YiIsImMiOjEwfQ%3D%3D) |
| **03** | **Panay Rice Cost Structure 2025** | Production unit costs, ROI ranking, break-even benchmarks | Disconnected matrix, dynamic `/kg` formatting | *In Development* | *Coming Soon* |
| **04** | **Rice Price Monitoring 2026** | Weekly farmgate palay & retail milled rice dynamics | Multi-card layout, dynamic format strings | *In Development* | *Coming Soon* |

---

## 🔒 Data Source & Governance
The analytical models in this portfolio are developed using regional agricultural statistics and operational records provided by the **Department of Agriculture Regional Field Office VI (Rice Program & Agricultural Statistics)**.

> *Note: In compliance with government data management and privacy standards, raw operational datasets and internal administrative drives are restricted and not publicly accessible. Public interactive reports display aggregated, non-sensitive summary indicators for analytical demonstration.*

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
