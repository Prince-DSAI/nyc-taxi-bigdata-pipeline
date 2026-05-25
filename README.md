NYC Taxi Big Data Pipeline — LDS7005M Component 1
A Scalable Azure-Based Big Data Pipeline for Urban Taxi Mobility Analytics Using NYC TLC Trip Records
Module: LDS7005M — Big Data and Cloud Computing | York St John University
Level: 7 | Component: 1 of 2 (60% weighting)
Submission Deadline: 28 May 2026
---
Project Overview
This repository contains the supporting artefacts for a cloud-based big data pipeline built on Microsoft Azure to analyse 79.5 million NYC Yellow Taxi trip records spanning 2023–2024. The pipeline implements ingestion, distributed processing, exploratory analytics, anomaly detection and machine learning fare prediction using Azure Data Factory, ADLS Gen2 and Azure Databricks.
---
Repository Structure
```
├── notebooks/
│   └── NYC_Taxi_Analysis.ipynb       # Full PySpark analysis notebook (12 cells)
├── data/
│   └── sample/
│       └── nyc_taxi_sample_cleaned.parquet   # 1% sample of cleaned dataset (~712K rows)
├── docs/
│   └── taxi_zone_lookup.csv          # NYC TLC taxi zone reference table
├── README.md
└── requirements.txt
```
---
Dataset
Full Dataset (External Source)
The full NYC TLC Yellow Taxi Trip Records dataset used in this project is publicly available from the official NYC Taxi and Limousine Commission open data portal:
Source: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
Files used: `yellow_tripdata_2023-01.parquet` through `yellow_tripdata_2024-12.parquet` (24 monthly files)
Property	Value
Raw records	79,479,946
Cleaned records	71,237,813
Retention rate	89.6%
Date range	January 2023 – December 2024
Format	Parquet (columnar)
Source	NYC TLC Open Data Portal
Licence	Public domain / open data
Sample Dataset (This Repository)
A representative 1% stratified random sample (~712,000 rows) of the cleaned dataset is provided in `data/sample/` for reproducibility verification without requiring full Azure infrastructure.
---
Azure Infrastructure
Service	Resource Name	Purpose
Resource Group	nyc-taxi-bigdata-rg	Container for all resources
ADLS Gen2	nyctaxidatalakesa	Raw and processed data storage
Azure Data Factory	nyc-taxi-pkg-adf	Pipeline orchestration and ingestion
Azure Databricks	nyc-taxi-databricks	Distributed Spark processing
Azure Key Vault	nyc-taxi-keyvault	Secrets management
Azure Monitor	nyc-taxi-monitor-alert	Performance alerting
Microsoft Defender	Defender CSPM	Security posture management
---
Notebook Overview
The main analysis notebook (`notebooks/NYC_Taxi_Analysis.ipynb`) contains 12 cells:
Cell	Purpose	Key Output
1	Storage configuration	Spark conf set — Ready!
2	Data loading	79,479,946 rows loaded
3	Data cleaning	71,237,813 rows retained (89.6%)
4	Schema validation	16-column cleaned schema
5	Temporal demand analysis	Hourly, daily, monthly patterns
6	Geographic zone analysis	Top 10 pickup and dropoff zones
7	Zone name enrichment	taxi_zone_lookup join
8	Year-over-year comparison	2023 vs 2024 metrics
9	Fare and distance distributions	Right-skewed histograms
10	Anomaly detection	3,005,492 anomalies (4.22%)
11	ML fare prediction	R²=0.8852, RMSE=6.11
12	Save processed data	71,237,813 rows → nyc-taxi-processed
---
Key Analytical Findings
Peak demand: Hour 18–19 (evening commute) — ~5.1M trips
Busiest day: Friday — 11,176,147 trips
Top pickup zone: JFK Airport Zone 132 — 3,747,865 trips
Top dropoff zone: Upper East Side North Zone 236 — 3,226,691 trips
YoY stability: 2023: 35.6M trips avg fare $19.73 | 2024: 35.6M trips avg fare $19.76
Anomaly rate: 4.22% (3,005,492 records flagged via 3-sigma threshold)
ML model: Linear Regression — R²=0.8852, RMSE=6.11
---
Running the Notebook
Prerequisites
Azure subscription (Azure for Students or equivalent)
Azure Databricks workspace (Runtime 14.3 LTS, Spark 3.5.0)
ADLS Gen2 storage account with hierarchical namespace enabled
24 monthly Parquet files uploaded to `nyc-taxi-raw` container
Configuration
In Cell 1, replace the placeholder values with your own credentials:
```python
storage_account_name = "YOUR_STORAGE_ACCOUNT_NAME"
storage_account_key  = "YOUR_STORAGE_ACCOUNT_KEY"
container_name       = "nyc-taxi-raw"
```
> **Security note:** Never commit real storage account keys to a public repository. Use Azure Key Vault to store credentials in production environments.
Cluster Specification
Setting	Value
Runtime	14.3 LTS (Apache Spark 3.5.0, Scala 2.12)
Node type	Standard_D4ds_v4
Memory	16 GB
Cores	4 vCPUs
DBU/hour	0.75
---
Requirements
```
pyspark>=3.5.0
pandas>=2.0.0
matplotlib>=3.7.0
```
---
References
NYC TLC (2024) TLC Trip Record Data. Available at: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
Microsoft (2024) Azure Data Lake Storage Gen2 documentation. Available at: https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction
Zaharia et al. (2016) 'Apache Spark: A unified engine for big data processing', Communications of the ACM, 59(11), pp. 56–65.
---
Academic Integrity
This repository is submitted as part of LDS7005M Component 1 at York St John University. All code and analysis is the original work of the submitting student. The NYC TLC dataset is publicly available open data published by the New York City Taxi and Limousine Commission.
