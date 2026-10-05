# CareSync Health Network: Metadata-Driven Data Platform on Azure

A guided project that I built and extended, based on the CareSync course by Narender Kumar (DataBeli).

## Problem
Hospitals keep patient and hospital data in internal systems and receive lab results and insurance files from partners. Combining them by hand is slow and error-prone, and adding a new source is hard.

## Solution
- One reusable Azure Data Factory pipeline, driven by a SQL control table, ingests PostgreSQL and CSV sources (full and incremental loads).
- Databricks transforms the data through Bronze, Silver and Gold layers (Delta Lake, Unity Catalog).
- Every run is logged in an audit table, and a status email is sent through Logic Apps.
- A Databricks dashboard and Genie sit on the Gold tables.

## Architecture
```mermaid
flowchart LR
  A[PostgreSQL] --> C[ADF metadata-driven pipeline]
  B[CSV in ADLS] --> C
  C --> D[Bronze]
  D --> E[Silver]
  E --> F[Gold]
  F --> G[Dashboard and Genie]
  H[(SQL control and audit tables)] --- C
  C --> I[Logic App status email]
```

## Tech stack
Azure Data Factory, ADLS Gen2, Azure SQL, Key Vault, Logic Apps, Databricks, PySpark, Delta Lake, Unity Catalog, GitHub

## What I added
- Null handling for config-driven notebook parameters
- A path-exists check, so the notebook exits cleanly when no new files arrive
- Gold notebooks and dashboard



## Pipelines
![Master pipeline](master-pipeline.png)
![Ingestion pipeline](ingestion-pipeline.png)
![Gold pipeline](gold-pipeline.png)

## Dashboard
![Hospital overview](dashboard-overview.png)
![Lab trends](dashboard-lab-trends.png)
![Patients](dashboard-patients.png)

## Repositories
- ADF pipelines: https://github.com/Vega343/caresync-adf
- Databricks notebooks: https://github.com/Vega343/caresync-databricks

## Credit
Original project and course by Narender Kumar: https://github.com/databeli/caresync_azure_project
