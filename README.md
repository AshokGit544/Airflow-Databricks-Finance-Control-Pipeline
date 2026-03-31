# Airflow Databricks Finance Control Pipeline

## Overview
This project demonstrates an enterprise-style data engineering workflow where Apache Airflow triggers a Databricks job to run PySpark-based finance data processing.

The pipeline reads finance-related source data such as invoices, payments, vendors, GL accounts, and cost centers, then performs:
- data integration
- standardization
- common business key creation
- data quality validation
- payment reconciliation
- retrieval-ready output generation

This project is designed to showcase the manager requirement:
**Airflow to Databricks job triggering**

---

## Project Goal
The goal of this project is to separate:
- **orchestration layer** using Airflow
- **processing layer** using Databricks and PySpark

Airflow controls the workflow and triggers the Databricks job.
Databricks performs the heavy data transformation and validation logic.

---

## Architecture
Source Data  
→ Airflow DAG  
→ Databricks Job Trigger  
→ PySpark Processing  
→ Output Files

---

## Source Datasets
The pipeline uses the following input datasets:
- vendors.csv
- gl_accounts.csv
- cost_centers.csv
- invoices.csv
- payments.csv

---

## Processing Logic
The Databricks-style PySpark notebook performs the following steps:
1. Reads all input source files
2. Standardizes text fields
3. Creates a common business key using vendor, cost center, and GL account
4. Joins all finance datasets into one integrated view
5. Applies data quality checks
6. Calculates payment reconciliation gaps
7. Generates retrieval-ready text output for downstream AI/search use cases

---

## Output Files
The pipeline generates:
- **integrated_finance_view.csv** → full joined business dataset
- **data_quality_issues.csv** → records with missing or invalid values
- **exception_summary.csv** → grouped summary for finance controls
- **payment_reconciliation.csv** → invoice vs paid amount comparison
- **retrieval_ready_output.csv** → AI/search-ready business text output

---

## Airflow to Databricks Trigger Flow
This project includes an Airflow DAG that:
1. Starts the workflow
2. Creates or updates a Databricks job
3. Triggers the Databricks job
4. Ends the workflow

Main Airflow operators used:
- `DatabricksCreateJobsOperator`
- `DatabricksRunNowOperator`

This shows how Airflow can act as the orchestration layer while Databricks acts as the execution layer.
