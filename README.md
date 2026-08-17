# Kimia Farma Business Performance Analytics (2020 - 2023)

**Big Data Analyst - Project-Based Internship**
Rakamin Academy x Kimia Farma

## Overview

This project evaluates Kimia Farma's business performance from 2020 to 2023 using BigQuery for data warehousing and transformation, Python (pandas) for exploratory data analysis, and Looker Studio for dashboard visualization. The goal is to identify key drivers of revenue, profitability, and customer satisfaction across Kimia Farma's branch network in Indonesia.

## Tech Stack

- **Google BigQuery** — data warehousing, table joins, and SQL transformations
- **Google Cloud Shell** — bulk data loading (`bq load`) for large CSV files
- **Python (pandas, pandas-gbq)** — exploratory data analysis in Google Colab
- **Google Looker Studio** — interactive dashboard

## Dataset

Four raw datasets were provided, each imported as a BigQuery table:

| Table | Rows | Description |
|---|---|---|
| `kf_final_transaction` | 672,458 | Transaction-level records (price, discount, rating) |
| `kf_kantor_cabang` | 1,725 | Branch master data (location, category, rating) |
| `kf_product` | 150 | Product master data (name, category) |
| `kf_inventory` | 1,035,000 | Branch-level stock data |

## Data Preparation

Two small files (`kf_kantor_cabang`, `kf_product`) were imported directly via the BigQuery Web UI. The two large files (`kf_final_transaction`, `kf_inventory`), which exceed the UI's 10MB upload limit, were imported via Cloud Shell using `bq load` with an explicitly defined schema — the `date` column was kept as `STRING` (source format `M/D/YYYY`) to avoid misparsing during auto-detection.

Row counts for every imported table were validated against the original CSV files; all counts matched exactly, confirming no data loss during import.

## Analysis Table — `tabel_analisa`

A single analytical table was built by joining three of the four tables (`kf_inventory` was excluded — none of its columns are part of the required schema):
```
for full query code can check on code file
```
Resulting row count: **672,458** — identical to the source transaction table, confirming the joins introduced no row loss or duplication.

## Key Insights

1. **Revenue has been stagnant since 2020–2023.** Total nett sales stay flat around Rp80 billion per year, with year-over-year growth always under 1%.
2. **Jawa Barat's dominance is a volume effect, not a performance edge.** It leads all provinces in total transactions and sales, but ranks only #17 of 31 by average sales per branch — its lead comes purely from having the most branches (510).
3. **Satisfaction paradox.** Branches with a perfect branch rating (5.0) show an average transaction rating of only ~3.9–4.0. Correlation analysis confirms discount, branch rating, and profit are statistically independent (all coefficients near 0).
4. **51.9% of transactions fall in the highest profit tier** (>Rp500,000), dominated by everyday medicine categories (antihistamines, pain relievers, sleep aids) rather than specialty drugs.
5. **Branch category (Apotek / Klinik & Apotek / Klinik-Apotek-Laboratorium) shows no meaningful performance difference** across sales, profit, or rating.

## Dashboard

The Looker Studio dashboard includes:
- Title & summary scorecards (total nett sales, nett profit, transactions, average rating)
- Province and date range filter controls
- Year-over-year revenue trend
- Top 10 provinces by transaction count and nett sales
- Top 5 branches with highest branch rating but lowest transaction rating
- Indonesia geo map of total profit by province
- Branch category and product category breakdown

**Dashboard link:** [Link Here](https://datastudio.google.com/reporting/f32d1baa-26df-4d35-b2d4-f87c490c78ce)

## Repository Structure
```
├── README.md
├── Code/
│ └── Create_Tabel_Analyst.sql
│ └── Kimia_Farma_Analyst_EDA.ipynb
├── Data/
│ └── Raw_Data
│ └── Final_Data
└── Presentation
```

## Author

**Irsan Maulana Yusuf**

Big Data Analyst Intern - Rakamin Academy x Kimia Farma
