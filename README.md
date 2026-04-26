# AWS Big Data Pipeline for Rental Vehicles Analytics

## Project Overview

This project demonstrates an end-to-end **AWS Big Data Processing Pipeline** for rental vehicle datasets using:

- Amazon S3
- Amazon EMR
- PySpark
- AWS Glue Crawler
- AWS Glue Data Catalog
- Amazon Athena
- AWS Step Functions

The system processes raw rental vehicle data stored in Amazon S3, transforms it using PySpark jobs running on EMR, catalogs the processed data with Glue, and enables SQL analytics through Athena.

---

# Architecture Diagram

```text
Raw CSV Files (S3)
      |
      v
AWS Step Functions
      |
      v
Create EMR Cluster
      |
      v
Run Spark Job 1
      |
      v
Run Spark Job 2
      |
      v
Store Output in S3 (Parquet)
      |
      v
Run Glue Crawler
      |
      v
Glue Data Catalog
      |
      v
Amazon Athena Queries
      |
      v
Terminate EMR Cluster

Workflow: DATALAKE

Step 1: Upload Raw Data to S3

Step 2: AWS Step Functions Starts Workflow
Create EMR Cluster
Submit Spark Job 1
Submit Spark Job 2
Run Glue Crawler
Terminate EMR Cluster

Step 3: Spark Job 1 (Cleaning Layer)
Tasks:

Remove null values
Fix date formats
Standardize text columns
Remove duplicates

Step 4: Spark Job 2 (Analytics Layer)
Tasks:
Join transactions + vehicles + users + locations
Revenue calculation
Vehicle utilization metrics
Partition by year/month

Step 5: AWS Glue Crawler

Step 6: Query with Athena
