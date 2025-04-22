# 🧾 Sales Orders Data Pipeline using Cloud Composer & Looker Studio (GCP)

This project demonstrates a fully automated **ELT pipeline** that ingests, processes, and visualizes sales order data. The solution uses **Apache Airflow (Cloud Composer)**, **Google Cloud Storage**, **BigQuery**, and **Looker Studio**, with data generation powered by **Python (Faker)**.

---

## 📌 Project Overview

**Objective:** Generate mock sales data, categorize orders by amount, transform and extract large orders, and visualize overall insights in a business dashboard.

**Technologies Used:**
- 🐍 Python (Fake Sales Data Generation)
- ☁️ Cloud Composer (ELT Workflow Automation)
- 🗃 Google Cloud Storage (Raw File Storage)
- 🔎 BigQuery (SQL-based Data Warehousing)
- 📈 Looker Studio (Sales Insights Dashboard)

---

## 🧱 Architecture

![Architecture](https://github.com/jubairt/sales-order-etl-gcp-pipeline/blob/main/architecture.png)

---

## 🌀 Airflow DAG Pipeline

The pipeline is managed by **Cloud Composer**, which runs a DAG to automate all tasks—from data creation to transformation and loading into BigQuery.

![DAG Pipeline](https://github.com/jubairt/sales-order-etl-gcp-pipeline/blob/main/Airflow_dagflow.png)

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

![Dashboard](https://github.com/jubairt/sales-order-etl-gcp-pipeline/blob/main/Lookerstudio_Dashboard.png)

---

## 📂 Repository Contents

| File / Folder | Description |
|---------------|-------------|
| `dag.py` | Airflow DAG that triggers data generation and transformation |
| `architecture.png` | Architecture diagram showcasing the full pipeline |
| `Airflow_dagflow.png` | Visual representation of the Airflow DAG in Composer |
| `Lookerstudio_Dashboard.png` | Screenshot of the final dashboard in Looker Studio |
| `desktop.ini` | System-generated file (can be ignored or deleted) |
| `Tables/` | Folder containing table structure visuals used in the ETL process |
| └── `sales_orders_table.png` | Raw sales orders table structure |
| └── `transformed_sales_orders_table.png` | Table after transformation (with categorized amounts) |
| └── `large_orders_table.png` | Filtered table showing large orders (amount ≥ 500) |

---

## ✅ Conclusion

This pipeline showcases how to implement an end-to-end **ELT workflow** using **Google Cloud services**. It simulates real-world sales data, categorizes it efficiently, and presents insights in a business-ready dashboard.

Whether you’re experimenting with cloud ELT tools or building production-grade analytics systems, this project highlights **best practices in data engineering** using GCP.
