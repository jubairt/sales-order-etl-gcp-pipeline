# 🧾 Sales Orders Data Pipeline using Cloud Composer & Looker Studio (GCP)

This project demonstrates a fully automated **ETL pipeline** that ingests, processes, and visualizes sales order data. The solution uses **Apache Airflow (Cloud Composer)**, **Google Cloud Storage**, **BigQuery**, and **Looker Studio**, with data generation powered by **Python (Faker)**.

---

## 📌 Project Overview

**Objective:** Generate mock sales data, categorize orders by amount, transform and extract large orders, and visualize overall insights in a business dashboard.

**Technologies Used:**
- 🐍 Python (Fake Sales Data Generation)
- ☁️ Cloud Composer (ETL Workflow Automation)
- 🗃 Google Cloud Storage (Raw File Storage)
- 🔎 BigQuery (SQL-based Data Warehousing)
- 📈 Looker Studio (Sales Insights Dashboard)

---

## 🧱 Architecture

![Architecture](Architecture.png)

---

## 🌀 Airflow DAG Pipeline

The pipeline is managed by **Cloud Composer**, which runs a DAG to automate all tasks—from data creation to transformation and loading into BigQuery.

![DAG Pipeline](Dag_pipeline.png)

---

## 🔄 Pipeline Steps

### 1. **Generate & Upload Sales Data**
- Script: `generate_sales_data.py`
- Uses `Faker` to simulate 500 random sales orders
- Fields: `order_id`, `customer_name`, `product`, `order_date`, `order_amount`
- CSV is uploaded to a GCS bucket

### 2. **Cloud Composer DAG**
- File: `sales_orders_to_bigquery_with_transformation.py`
- DAG Tasks:
  - Generate sales data using Python
  - Upload CSV to GCS
  - Load data into BigQuery table `raw_sales_data`
  - Perform transformation: categorize orders as **Small**, **Medium**, or **Large**
  - Extract only **Large Orders** into a separate table `large_sales_orders`

### 3. **BigQuery Transformation Logic**
- Categorization by `order_amount`:
  - Small: `< 200`
  - Medium: `200 - 499.99`
  - Large: `>= 500`
- Final tables: `sales_dataset.raw_sales_data`, `sales_dataset.transformed_sales`, `sales_dataset.large_sales_orders`

### 4. **Visualization with Looker Studio**
- Sales trends, top products/customers, and categorized orders are visualized through Looker Studio.
- Data source: BigQuery

![Dashboard](Looker_studio.png)

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `generate_sales_data.py` | Python script to create and upload sales data |
| `sales_orders_to_bigquery_with_transformation.py` | Cloud Composer DAG script |
| `Dag_pipeline.png` | DAG visual representation |
| `Architecture.png` | Architecture diagram |
| `Looker_studio.png` | Final dashboard screenshot |
| `sales_data.csv` | Sample sales data |
| `desktop.ini` | System file (can be ignored or removed) |

---

## ✅ Conclusion

This pipeline showcases how to implement an end-to-end **ETL workflow** using **Google Cloud services**. It simulates real-world sales data, categorizes it efficiently, and presents insights in a business-ready dashboard.

Whether you’re experimenting with cloud ETL tools or building production-grade analytics systems, this project highlights **best practices in data engineering** using GCP.
