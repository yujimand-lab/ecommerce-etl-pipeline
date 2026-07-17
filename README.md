# ecommerce-etl-pipeline
Portfolio project demonstrating ETL pipeline development, data validation, reporting, and Apache Airflow orchestration.

An end-to-end ETL (Extract, Transform, Load) pipeline built with **Python**, **Pandas**, **Docker**, and **Apache Airflow** to process e-commerce transaction data into analytics-ready datasets.

---

## 📖 Project Overview

This project demonstrates a complete ETL workflow for processing e-commerce order data. The pipeline extracts raw data, cleans and validates it, transforms it into a structured format, and generates reports for analysis.

The workflow is orchestrated using **Apache Airflow**, making it suitable for automation and production-like environments.

---

## 🚀 Tech Stack

- Python
- Pandas
- NumPy
- Apache Airflow
- Docker
- VS Code

---

## ⚙️ ETL Workflow

```text
Extract
   ↓
Transform
   ↓
Validate
   ↓
Load
   ↓
Generate Report
   ↓
Notification
```

---

## ✨ Features

- Extract raw order and product datasets
- Clean duplicate and missing values
- Validate data quality
- Generate analytics-ready datasets
- Produce summary reports
- Logging and monitoring
- Airflow DAG orchestration

---

## 📂 Project Structure

```text
project/
│
├── dags/
│   └── etl_ecommerce_dag.py
│
├── etl_pipeline.py
├── orchestrator.py
├── orders_clean.csv
├── summary_report.csv
├── pipeline_log.txt
├── requirements.txt
└── README.md
```

---

## 🛠 Installation

Clone this repository:

```bash
git clone https://github.com/yourusername/ecommerce-etl-pipeline.git
cd ecommerce-etl-pipeline
```

Install dependencies:

```bash
pip install pandas numpy
```

Or using:

```bash
pip install -r requirements.txt
```

---

## ▶️ Run the Project

Run the ETL pipeline:

```bash
python orchestrator.py
```

If using Apache Airflow:

```bash
airflow scheduler
airflow webserver
```

---

## 📊 Output

The pipeline generates:

- Cleaned datasets
- Summary reports
- Pipeline logs
- Analytics-ready data

Example output files:

```text
orders_clean.csv
summary_report.csv
pipeline_log.txt
```

---

## 📚 Learning Outcomes

This project demonstrates experience with:

- ETL Pipeline Design
- Data Cleaning
- Data Validation
- Data Transformation
- Apache Airflow
- Logging & Monitoring
- Data Engineering Workflow

---

## 🔮 Future Improvements

- Database integration (PostgreSQL/MySQL)
- Cloud storage support (AWS S3)
- Data quality testing
- CI/CD deployment
- Dashboard integration (Power BI/Tableau)
- Email notification after pipeline execution

---

## 👤 Author

**Andi Siti Fatimah Alwi**

💊 Pharmacist  
📊 Aspiring Data Engineer & Bioinformatics Enthusiast

---

## ⭐ If you find this project useful, feel free to give it a star!
