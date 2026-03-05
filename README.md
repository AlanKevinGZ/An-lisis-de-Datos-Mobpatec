Readme · MD
Copiar

#  Mobpatec Sales Data Analysis

A complete end-to-end data analysis pipeline built with Python and Pandas for Mobpatec, a company specializing in office furniture and technological devices. This project covers the full data science workflow: ingestion, cleaning, transformation, and business insights.

---

##  Project Overview

As the company's Data Scientist, the goal was to consolidate data from multiple sources — internal SQL exports and publicly available web data — to answer key business questions around sales performance, profitability, customer behavior, and market expansion strategy.

---

##  Data Sources

### Internal (Excel exports from SQL database)
| DataFrame | Description |
|---|---|
| `df_ventas` | Sales transactions per item |
| `df_clientes` | Customer information |
| `df_productos` | Product catalog |

### External (Web scraping)
| DataFrame | Source |
|---|---|
| `df_pob` | Country population — Wikipedia |
| `df_pib` | GDP by country — Worldometers |
| `df_rpc` | Average wage / per capita income — Wikipedia |

---

##  Workflow

### Step 1 — Data Import
- Loaded 3 Excel files into Pandas DataFrames
- Scraped 3 external HTML tables using `pd.read_html()`
- Verified dimensions and identified NaN values across all sources

### Step 2 — Data Cleaning
- Removed records with missing purchase dates (business rule: no date = invalid record)
- Detected and dropped duplicate rows
- Fixed data type issues: replaced `","` decimal separators, stripped `"$"` symbols and whitespace, and cast columns to `float`/`int` as needed

### Step 3 — Statistical Cleaning
- Used `.describe()` to inspect distributions
- Identified outliers: orders with more than 13 units were flagged as invalid per business policy and removed
- Imputed missing shipping dates using: `Purchase Date + median(Shipping Date − Purchase Date)`

### Step 4 — Analysis & Insights
- Merged `df_ventas`, `df_productos`, and `df_clientes` into a single master table `df_global` using inner joins
- Computed a `Beneficio` (Profit) column: `(Unit Price − Unit Cost) × Units Sold`
- Joined with external data for macroeconomic correlation analysis

---

##  Business Questions Answered

| # | Question |
|---|---|
| Q1 | Dimensions (rows × columns) of each DataFrame |
| Q2 | Presence of NaN values in each source |
| Q3 | Number of records removed due to missing purchase date |
| Q4 | Duplicate records detected and removed |
| Q5 | Columns requiring data type transformation |
| Q6 | Median sale value |
| Q7 | Units threshold at the 75th percentile of orders |
| Q8 | Number of orders exceeding 13 units |
| Q9 | New dimensions of `df_ventas` after outlier removal |
| Q10 | Imputation method for missing shipping dates |
| Q11 | Country with the highest sales volume |
| Q12 | Year with the highest number of sales |
| Q13 | Product category generating the highest profit |
| Q14 | Correlation between country profit and per capita income |
| Q15 | Correlation between number of orders per country and per capita income |
| Q16 | Correlation between GDP, population, and per capita income |
| Q17 | Countries recommended for new production plant locations |
| Q18 | Excel report export: profit by category and country |

---

##  Technologies Used

- **Python 3.x**
- **Pandas** — data manipulation and analysis
- **NumPy** — numerical operations
- **Matplotlib / Seaborn** — data visualization
- **openpyxl** — Excel file export
- **requests / lxml** — web scraping

---

##  Output

A final Excel report `Reporte Beneficios.xlsx` is generated with a sheet named `Beneficios_cat_pais`, summarizing profit broken down by **product category** and **country** — ready for executive review.

---
