# SalesData-ETL: Azure Data Factory ETL Pipeline for Retail Sales Analytics

## Overview

**SalesData-ETL** is an end-to-end cloud ETL project built with **Azure Data Factory (ADF)** and **Azure Data Lake Storage Gen2 (ADLS Gen2)**.

The pipeline ingests raw Superstore sales data (CSV), applies business-focused transformations and data quality checks through **Mapping Data Flows**, and writes curated output for downstream analytics and reporting.

---

## Problem Statement

Raw retail sales data often contains:
- Inconsistent discount representation
- Missing customer information
- Invalid sales records
- Limited business-ready metrics for decision-making

This project solves these issues by creating a reliable, analytics-ready processed dataset with derived KPIs and standardized business categories.

---

## Solution Architecture

### High-Level Flow

```text
Raw Sales CSV (Superstore dataset)
        ↓
ADLS Gen2 (raw container)
        ↓
Azure Data Factory Pipeline
        ↓
Mapping Data Flow Transformations
   - Data quality filtering
   - Derived KPI creation
   - Discount standardization and categorization
        ↓
ADLS Gen2 (processed container)
        ↓
Curated Sales Dataset for BI / Reporting
```

---

## Tech Stack

- **Azure Data Factory (ADF)**
- **Azure Data Lake Storage Gen2 (ADLS Gen2)**
- **Mapping Data Flows**
- **GitHub**
- **ARM Templates** (for deployment and infra backup)
- **CSV Data Source (Superstore Sales Dataset)**

---

## Dataset

Source: **Superstore Sales Dataset**  
Contains retail attributes such as:
- Order details
- Customer details
- Product details
- Sales, Profit, Discount, Quantity
- Region/Geography fields

---

## ETL Pipeline Stages

## 1) Extract
- Source file read from `raw` container in ADLS Gen2.
- Connected through ADF linked services and datasets.

## 2) Transform (Mapping Data Flow)

### Data Quality Rules
1. **Filter invalid sales records**
   - Keep records where `Sales > 0`
2. **Remove incomplete customer records**
   - Exclude rows where required customer fields (e.g., `Customer Name`) are null

### Business Transformations
1. **Profit Margin (%)**
   - Formula: `(Profit / Sales) * 100`
   - Rounded to **2 decimal places**

2. **Discount Standardization**
   - Convert discount from decimal to percentage scale  
   - Example: `0.2 → 20`, `0.4 → 40`

3. **Discount Category**
   - Bucket records into:
     - No Discount
     - Low Discount
     - Medium Discount
     - High Discount

4. **Revenue Per Unit**
   - Formula: `Sales / Quantity`

5. **Profit Per Unit**
   - Formula: `Profit / Quantity`

## 3) Load
- Transformed data written to the `processed` container in ADLS Gen2.
- Output file is analytics-ready for BI tools and SQL-based analysis.

---

## Repository Structure

```text
SalesData-ETL/
│
├── adf/                      # ADF artifacts (pipelines, dataflows, datasets, linked services)
├── data/
│   └── raw/
│       └── superstore_sales.csv
├── deployment/               # ARM templates
├── docs/
│   └── project-architecture.md
├── screenshots/
└── README.md
```

---

## Azure Resources

- **Resource Group:** `rg-salesdata-etl`
- **Storage Account:** `salesdataetl_1781609692282`
- **Data Factory:** `salesdata-etl`

---

## Key Business Outcomes

- Improved data reliability via quality filters
- Standardized discount metrics for easier reporting
- Added unit-level and margin KPIs for profitability insights
- Produced clean curated data for dashboards and analytics

---

## Deployment

Infrastructure and ADF assets can be redeployed using ARM templates under:

```text
deployment/
```

---

## Future Enhancements

- Event-triggered ingestion (file arrival-based automation)
- Parameterized pipelines for multi-file processing
- Incremental load strategy (watermark-based)
- Load curated data into Azure SQL / Synapse
- Power BI dashboard layer for executive reporting

---

## Author

Built by **Shreyansh** as a practical cloud data engineering project focused on ETL design, transformation logic, and analytics-ready data modeling.
