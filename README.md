# 🏥 Hospital Admissions & Billing Dashboard — Power BI Capstone Project

## 📌 Overview
An interactive Power BI dashboard analyzing hospital admissions, billing performance, and patient outcomes. Built as a capstone project to demonstrate end-to-end data modeling, DAX measure design, and dashboard storytelling skills.

The dashboard helps hospital administration understand:
- Admission volumes and trends over time
- Billing performance across hospitals, insurance providers, and admission types
- Doctor and hospital workload
- Patient length of stay and test result outcomes

## 📊 Dataset
**Source:** [Healthcare Dataset — Prasad Patil (Kaggle)](https://www.kaggle.com/datasets/prasad22/healthcare-dataset)

A synthetic dataset (~55,500 rows) with no real patient information, containing:
`Name, Age, Gender, Blood Type, Medical Condition, Date of Admission, Doctor, Hospital, Insurance Provider, Billing Amount, Room Number, Admission Type, Discharge Date, Medication, Test Results`

## 🧱 Data Model — Star Schema
Built a star schema in Power Query from the flat source file:
                Dim Calendar
                      |
Dim Doctor --- Fact Admissions --- Dim Hospital
                      |
                Dim Condition

- **Fact Admissions**: one row per admission (grain), with `AdmissionID` as a surrogate key (added via Index column since the source has no unique ID)
- **Dim Doctor**, **Dim Hospital**, **Dim Condition**: deduplicated lookup tables
- **Dim Calendar**: built with `CALENDARAUTO()` and DAX-derived Year/Quarter/Month columns
- All relationships: 1-to-many, single-direction filter

## 🧮 Key DAX Measures
| Measure | Purpose |
|---|---|
| `Total Admissions` | Row count of Fact Admissions |
| `Total Billing Amount` | Sum of billing across all admissions |
| `Average Length of Stay` | Avg days between admission and discharge |
| `Abnormal Test Result %` | Share of admissions with abnormal test results |
| `Billing YoY Growth %` | Year-over-year billing trend using `PREVIOUSYEAR()` |
| `Billing % of Hospital` | Each hospital's share of total billing using `ALL()` |

Full DAX code is documented in the PBIX file's measure descriptions.

## 📈 Dashboard Pages

**Page 1 — Admissions Overview**
- KPI cards: Total Admissions, Total Billing Amount, Average Billing Amount, Average Length of Stay
- Admissions by Medical Condition (bar chart)
- Billing by Hospital (treemap)
- Admission Type split (donut chart)
- Test Results distribution (pie chart)
- Top 10 Doctors by Billing (Top N filter)
- Age Group breakdown (column chart)

**Page 2 — Trends & Financials**
- KPI cards: Admissions YTD, Billing YTD, Billing YoY Growth %, Abnormal Test Result %
- Admissions over time (line chart)
- Billing: current year vs previous year (line chart)
- Billing by Insurance Provider (matrix table)
- Length of Stay vs Billing Amount (scatter chart)
- Billing Tier split by Admission Type (stacked column)

## 🛠️ Tools Used
- Power BI Desktop
- Power Query (data cleaning, star schema modeling)
- DAX (measures, calculated columns, time intelligence)

## 💡 Key Insights
- *("Emergency admissions show a higher average billing amount and shorter average length of stay compared to Elective admissions.")*

## 📂 Repository Contents
- `healthcare_dashboard.pbix` — the full Power BI report file
- `healthcare_dashboard.pdf` — static export of both report pages
- `screenshots/` — dashboard page images

## 👤 Author
**[Ammara Desai]**
Capstone Project — Power BI
