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

- The dashboard covers **56,000 admissions** totaling **₹1.42 billion** in billing, 
  with an average billing amount of **₹25.54K** per admission and an average 
  length of stay of **15.5 days**.

- Admissions are spread almost evenly across all six medical conditions 
  (Arthritis, Diabetes, Hypertension, Obesity, Cancer, Asthma), each accounting 
  for roughly 9,000-9,500 admissions — indicating no single condition dominates 
  hospital load in this dataset.

- Test results are split nearly evenly three ways: **33.6% Normal, 33.4% Abnormal, 
  33.1% Inconclusive** — with no strong skew toward any single outcome.

- Admission Type is similarly balanced: **Elective 33.6%, Emergency 33.5%, 
  Urgent 32.9%** of total admissions, suggesting the hospital's caseload isn't 
  concentrated in any one admission category.

- Across all five insurance providers, billing is remarkably consistent — each 
  provider accounts for roughly **20% of total admissions** (10,900-11,250 each) 
  and a near-identical average billing amount (**₹25.4K-25.6K**), with **Cigna** 
  handling the most admissions (11,249) and **Blue Cross** the highest per-patient 
  average (₹25,613).

- Total admissions and billing both show a sharp drop in **2024**, which reflects 
  a partial year of data in the source dataset rather than an actual decline in 
  hospital activity.

- Average length of stay shows minimal variation across medical conditions 
  (15.4-15.7 days), and billing amount shows no strong correlation with length 
  of stay — consistent with this being a synthetically generated dataset rather 
  than one reflecting real clinical cost drivers.

## 📂 Repository Contents
- `healthcare_dashboard.pbix` — the full Power BI report file
- `healthcare_dashboard.pdf` — static export of both report pages
- `screenshots/` — dashboard page images

## 👤 Author
**[Ammara Desai]**
Capstone Project — Power BI
