# Data Warehouse and Analytics Project

This repository contains my **Data Warehouse and Analytics project** built using **SQL Server**.

The goal of this project is to take raw data from different systems, clean and transform it, and build a **data warehouse that can be used for analytics and reporting**.

Through this project, I practiced concepts like **ETL pipelines, data modeling, and data warehouse architecture**.

---

# Data Architecture

The project follows the **Medallion Architecture**, which consists of three layers:

## Bronze Layer
- Stores **raw data exactly as it comes from the source systems**
- Data is loaded from **CSV files into SQL Server tables**
- No transformations are applied in this layer

## Silver Layer
- This layer contains **cleaned and standardized data**
- Main tasks performed:
  - Removing duplicates
  - Handling missing values
  - Fixing data formats
  - Standardizing inconsistent values

## Gold Layer
- Contains **business-ready data**
- Data is structured using a **Star Schema**
- Used for **analytics, reporting, and dashboards**

---

# Project Overview

In this project I worked on the following steps:

## 1. Data Architecture
Designed a **data warehouse using Bronze, Silver, and Gold layers**.

## 2. ETL Pipelines
Built **ETL pipelines using SQL stored procedures** to move data from **Bronze → Silver → Gold**.

## 3. Data Modeling
Created **fact and dimension tables** using a **Star Schema** for analytical queries.

## 4. Analytics & Reporting
Wrote SQL queries to analyze:
- Customer behavior
- Product performance
- Sales trends

---

# Skills Demonstrated

Through this project I practiced:

- SQL Development  
- Data Warehousing Concepts  
- ETL Pipeline Development  
- Data Cleaning and Transformation  
- Star Schema Data Modeling  
- Analytical SQL Queries  

---

# Tools Used

The following tools were used in this project:

- **SQL Server Express** – used for creating the data warehouse
- **SQL Server Management Studio (SSMS)** – used to run SQL queries and manage the database
- **Git & GitHub** – for version control and project sharing
- **Draw.io** – for creating architecture and data flow diagrams

---

# Dataset

The dataset used in this project comes from two source systems:

- **CRM System**
- **ERP System**

Both datasets are provided as **CSV files** and can be found in the `datasets/` folder.

---

# Project Requirements

## Data Engineering

The objective was to build a **data warehouse that integrates data from CRM and ERP systems**.

Steps included:

- Importing data from CSV files
- Cleaning and transforming the data
- Integrating multiple data sources
- Creating a structured data model for analytics

---

## Analytics

After building the warehouse, SQL queries were used to analyze:

- Customer information
- Product categories
- Sales performance
- Revenue trends

---

# Repository Structure

```
data-warehouse-project/
│
├── datasets/               # Raw CRM and ERP datasets (CSV files)
│
├── scripts/                # SQL scripts for ETL and transformations
│   ├── bronze/             # Scripts for loading raw data
│   ├── silver/             # Data cleaning and transformation
│   ├── gold/               # Analytical models and views
│
├── tests/                  # Data validation and testing scripts
│
├── README.md               # Project documentation
├── LICENSE
├── .gitignore
├── requirements.txt
```

---

# What I Learned

This project helped me understand:

- How **real-world data warehouses are structured**
- How **ETL pipelines work**
- How to clean and standardize messy data
- How to design **fact and dimension tables**
- How to write SQL queries for business insights

---

# License

This project is licensed under the **MIT License**.
