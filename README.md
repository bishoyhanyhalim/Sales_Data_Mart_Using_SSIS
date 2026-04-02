# Sales Data Mart: End-to-End ETL & BI Implementation
**Developer:** Bishoy Hany Halim 
**Specialization:** Database Engineering

---

##  Project Overview
This project demonstrates the design and implementation of a professional **Sales Data Mart** using **SQL Server Integration Services (SSIS)**. The goal was to transform raw transactional data from an OLTP source (AdventureWorks) into a structured Dimensional Model (Star Schema) optimized for analytical reporting and Business Intelligence.

The project covers the entire lifecycle: from **Source Profiling** and **Dimensional Modeling** to complex **ETL Pipeline Development** and **SCD (Slowly Changing Dimension)** management.

##  Key Features & Implementation Steps

### 1. Dimensional Modeling
* **Schema Design:** Implemented a **Star Schema** consisting of a Central Fact Table and multiple Dimension Tables (`Dim_Customer`, `Dim_Product`, `Dim_Date`).
* **Keys Management:** Utilized **Surrogate Keys** (e.g., `customer_key`, `product_key`) to decouple the Data Warehouse from source system changes and to support historical tracking.

### 2. Advanced ETL Workflows (SSIS)
The ETL logic was built using SQL Server Data Tools (SSDT) with a focus on data integrity and performance:

* **Data Cleansing:** Used **Derived Column** transformations to handle `NULL` values. For example, replacing nulls in `Color` or `Category` with "Unknown" to ensure report consistency.
* **Enrichment:** Implemented **Nested Lookups** to flatten normalized source tables (e.g., joining Products with Categories and Subcategories) into a single denormalized dimension.
* **Slowly Changing Dimensions (SCD):** * **Type 1:** Updated changing attributes (like `Phone` or `Address`) directly in existing records.
    * **Type 2:** Maintained full historical versions of data. When a critical attribute changes, the ETL expires the old record (`is_current = 0`) and inserts a new one (`is_current = 1`).

### 3. Data Validation & Quality Assurance
* **Audit Columns:** Every record includes `start_date`, `end_date`, and `is_current` flags to track the lineage of the data.
* **SQL Verification:** Rigorous testing was performed to ensure that the SCD logic correctly versions records. (e.g., verifying that a Customer ID with a changed address results in two distinct surrogate keys in the Data Mart).

## 🛠️ Tech Stack
* **ETL Engine:** SQL Server Integration Services (SSIS)
* **RDBMS:** SQL Server (SSMS)
* **Environment:** Windows 11 / Visual Studio 2022

---

##  Technical Deep Dive: The ETL Logic

### Dim_Customer Flow
The package utilizes a dedicated SCD component to split incoming data into three streams:
1.  **New Records:** Straight insertion into the destination.
2.  **Fixed/Changing Attributes:** OLE DB Command updates for Type 1 changes.
3.  **Historical Attributes:** Union All logic to expire old records and insert new versions for Type 2 changes.

### Dim_Product Flow
To maintain a high-performance star schema, the product flow performs multi-stage lookups:
* **Source:** Product Table
* **Lookup 1:** Model & Description
* **Lookup 2:** Category & Subcategory
* **Transformation:** Null replacement and Data Type casting.
* **Destination:** OLE DB Destination mapping to `Dim_Product`.

---

##  About the Author
I am a specialist in **Database Engineering**. My expertise includes:
* **Database Architecture:** SQL Server, Data Warehousing, and OLAP/OLTP optimization.
* **Development:** ETL Development (SSIS).

---

##  Let's Connect!
If you have questions about this project or want to discuss Data Engineering, feel free to reach out.

[[linkedin](https://www.linkedin.com/in/bishoyhanyhalim/)]
