# NeoBank_Data_Engineering_Project

## 📌 Overview

This project implements a **modern end-to-end data engineering pipeline** using **Azure Databricks**.
It ingests data from multiple sources, processes it through layered architecture (**Bronze → Silver → Gold**), and exposes business-ready insights through dashboards.

---

## 🧱 Architecture

The pipeline follows a **Medallion Architecture**:


Sources → Bronze → Silver → Gold → Dashboards → Notifications


### 🔹 Data Sources

* SQL Server (transactional banking data)
* Blob Storage (external files like credit reports & logs)

### 🔹 Layers

#### 🥉 Bronze Layer

* Raw ingestion (no transformations)
* Stores data as-is from sources

#### 🥈 Silver Layer

* Cleaned & structured data
* Handles:

  * Deduplication
  * Incremental loads (watermarks)
  * Merge / Append logic

#### 🥇 Gold Layer

* Business-level aggregations
* Optimized for analytics & dashboards

---

## ⚙️ Key Features

### ✅ Metadata-Driven Pipeline

All processing is controlled via metadata tables:

* `metadata.tables` → which tables to process
* `metadata.table_parameters` → how to process
* `metadata.table_watermarks` → incremental tracking
* `metadata.pipeline_runs` → audit logs

---

### 🔁 Incremental Processing

* Uses **watermark columns** (e.g. `updated_at`)
* Only new/updated data is processed
* Improves performance and scalability

---

### 🔄 Orchestration (Databricks Jobs)

Pipeline is split into modular tasks:


1. source_to_silver_sqlserver
2. source_to_silver_blob
3. silver_to_gold
4. notification (email)


* SQL Server and Blob ingestion run in parallel ⚡
* Gold layer depends on both
* Fully automated execution

---

### 📊 Gold Layer Transformations

Key business tables:

* `customer_360` → unified customer view
* `branch_performance` → branch KPIs
* `daily_bank_kpi` → daily metrics
* `risk_customer_summary` → risk segmentation
* `transaction_channel_summary` → channel analytics

---

## 📈 Dashboards

Built directly on Gold tables.

### 🔢 KPIs

* Total Customers
* Total Deposits
* Total Transactions
* High Risk Customers

### 📊 Distributions

* Customer Segment Distribution
* Credit Risk Distribution

### 🏆 Rankings

* Top Customers
* Branch Performance

### 💳 Transaction Insights

* Gateway performance (success vs failure)
* Device usage (mobile/web/etc.)

---

## 🔐 Secrets Management

Sensitive data is stored securely using **Databricks Secret Scopes**:

* SQL Server connection config
* Email API keys

---

## 📧 Notifications

* Email alerts sent after pipeline execution
* Includes:

  * execution status (SUCCESS / FAILED)
  * processed tables
  * record counts

---

## 🧠 Key Concepts Demonstrated

* Medallion Architecture
* Metadata-driven pipelines
* Incremental data processing (watermarks)
* ETL/ELT design patterns
* Parallel job orchestration
* Data quality & audit tracking

---

## 🚀 How to Run

1. Configure metadata tables
2. Set up secret scope
3. Create Databricks jobs
4. Run master pipeline

---

## 📌 Tech Stack

* Azure Databricks
* PySpark
* Delta Lake
* SQL
* Azure Blob Storage
* SQL Server

---

## 💡 Future Improvements

* Add streaming ingestion (real-time)
* Integrate with Power BI
* Add data quality checks
* Use Azure Key Vault for secrets
* Add CI/CD pipeline

---

## 👩‍💻 Author

Nadine Hadjaissa
Data Engineering Enthusiast 🚀
