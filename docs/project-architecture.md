# Sales Data ETL Pipeline

## Source
Superstore Sales CSV

## Storage
Azure Data Lake Storage Gen2

Containers:
- raw
- processed

## Processing
Azure Data Factory

Transformations:
- Remove null values
- Remove duplicates
- Standardize date formats
- Filter invalid sales records

## Output
Processed sales dataset stored in ADLS Gen2

## Automation
ADF Schedule Trigger
