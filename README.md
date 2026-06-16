# Sales Data ETL Pipeline using Azure Data Factory

## Overview

This project demonstrates the development of an end-to-end ETL (Extract, Transform, Load) pipeline using Azure Data Factory (ADF) and Azure Data Lake Storage Gen2 (ADLS Gen2).

The pipeline ingests raw sales data from CSV files, performs data quality checks and transformations, and stores the processed data in a separate location for downstream analytics and reporting.

---

## Project Architecture

```text
Raw Sales CSV
      ↓
Azure Data Lake Storage Gen2 (raw)
      ↓
Azure Data Factory Pipeline
      ↓
Mapping Data Flow
    • Filter invalid sales records
    • Remove records with missing customer information
    • Create Profit Margin metric
    • Categorize sales transactions
      ↓
Azure Data Lake Storage Gen2 (processed)
      ↓
Processed Sales Dataset
```

---

## Technologies Used

* Azure Data Factory (ADF)
* Azure Data Lake Storage Gen2 (ADLS Gen2)
* GitHub
* ARM Templates
* CSV Dataset

---

## Dataset

Source dataset: Superstore Sales Dataset

The dataset contains retail sales information including:

* Orders
* Customers
* Products
* Sales
* Profit
* Geographic information

---

## ETL Process

### Extract

* Read source CSV file from the `raw` container in ADLS Gen2.
* Import data through Azure Data Factory datasets and linked services.

### Transform

The Mapping Data Flow performs the following transformations:

#### 1. Sales Validation

Removes records with invalid sales values.

```text
Sales > 0
```

#### 2. Null Handling

Removes records with missing customer information.

```text
Customer Name IS NOT NULL
```

#### 3. Derived Metric

Creates a Profit Margin column.

```text
ProfitMargin = (Profit / Sales) * 100
```

#### 4. Sales Categorization

Creates a business-friendly sales category.

```text
High Value
Regular
```

### Load

Stores transformed data in the `processed` container of ADLS Gen2.

Output file:

```text
superstore_sales_transformed.csv
```

---

## Azure Resources

### Resource Group

```text
rg-salesdata-etl
```

### Storage Account

```text
salesdataetl_1781609692282
```

### Azure Data Factory

```text
salesdata-etl
```

---

## Repository Structure

```text
SalesData-ETL/
│
├── adf/
├── data/
│   └── raw/
│       └── superstore_sales.csv
│
├── deployment/
│
├── docs/
│   └── project-architecture.md
│
├── screenshots/
│
└── README.md
```

---

## Screenshots

### Pipeline

Add screenshot:

```text
screenshots/pipelineCanvas.png
```

### Data Flow

Add screenshot:

```text
screenshots/dataflowCanvas.png
```

### Monitoring

Add screenshot:

```text
screenshots/PipelineRunSuccessful.png
```

### Storage

Add screenshot:

```text
screenshots/storageAccount.png
```

---

## Deployment

The repository includes ARM templates for redeploying Azure Data Factory resources.

Location:

```text
deployment/
```

These templates can be used to recreate the Data Factory environment in another Azure subscription.

---

## Key Learnings

* Azure Data Factory Pipelines
* Linked Services
* Datasets
* Mapping Data Flows
* Data Transformation Techniques
* Azure Data Lake Storage Gen2
* Monitoring and Debugging ETL Workflows
* Infrastructure Backup using ARM Templates
* Source Control Integration with GitHub

---

## Future Enhancements

* Event-based triggers for automatic file ingestion
* Dynamic file processing through parameterized datasets
* Loading transformed data into Azure SQL Database
* Power BI dashboard integration
* Incremental data processing

---
