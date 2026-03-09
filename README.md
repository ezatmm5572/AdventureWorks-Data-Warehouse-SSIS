# AdventureWorks Data Warehouse – SSIS

Overview

This project implements a Data Warehouse solution using SQL Server and SQL Server Integration Services (SSIS) based on the AdventureWorksLT2017 database.

The ETL pipeline extracts transactional data, transforms it, and loads it into a Galaxy Schema (Fact Constellation) designed for analytical workloads.

---

Data Warehouse Architecture

The solution follows a typical three-layer architecture:

1. Source Layer
   
   - AdventureWorksLT2017 transactional database.

2. Staging Layer
   
   - Raw data is extracted from the source system and loaded into staging tables.

3. Data Warehouse Layer
   
   - Dimension tables
   - Multiple fact tables

---

Schema Design

The Data Warehouse is modeled using a Galaxy Schema where multiple fact tables share the same dimensions.

Dimension Tables

- DimCustomer (SCD Type 2)
- DimProduct (SCD Type 2)
- DimDate

The dimensions implement Slowly Changing Dimension Type 2 (SCD Type 2) to track historical changes using columns such as:

- StartDate
- EndDate
- IsCurrent

---

Fact Tables

FactSalesOrder

Stores high-level information about sales orders.

Example attributes:

- CustomerKey
- OrderDateKey
- DueDateKey
- ShipDateKey
- SubTotal
- TaxAmt
- Freight
- TotalDue

FactSalesOrderLine

Stores detailed order transactions.

Example attributes:

- ProductKey
- CustomerKey
- OrderDateKey
- OrderQty
- UnitPrice
- LineTotal

---

ETL Process (SSIS)

The ETL pipeline is implemented using SSIS packages.

Execution Order

1. Load Staging Tables
2. Load Dimension Tables (SCD Type 2)
3. Load FactSalesOrder
4. Load FactSalesOrderLine

Transformations Used

- Lookup Transformation
- Data Conversion
- Slowly Changing Dimension (Type 2)
- Surrogate Key Mapping

Lookups are used to retrieve dimension surrogate keys before loading the fact tables.

---

Tools & Technologies

- SQL Server
- SQL Server Integration Services (SSIS)
- AdventureWorksLT2017
- Visual Studio / SSDT

---

Dataset

This project uses the AdventureWorksLT2017 sample database provided by Microsoft.
Microsoft provides installation and configuration instructions for the dataset here:

https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver17&tabs=ssms

---

Architecture Diagram

<img width="2560" height="1440" alt="Galaxy Schema" src="https://github.com/user-attachments/assets/57a0096c-222f-4a38-a6b6-d83b551e039b" />


---

SSIS Control Flow

<img width="2560" height="1440" alt="STG_ControlFlow" src="https://github.com/user-attachments/assets/12da9c05-afde-4712-bb5b-200685b72f2c" />
<img width="2560" height="1440" alt="DIM_ControlFlow" src="https://github.com/user-attachments/assets/85a243bb-28e6-4551-903e-921c44261659" />
<img width="2560" height="1440" alt="FACT_ControlFlow" src="https://github.com/user-attachments/assets/2b2ecb9a-4375-4fe3-a696-1baf405c14b1" />

---

SSIS Data Flow

<img width="2560" height="1440" alt="STG_DataFlow" src="https://github.com/user-attachments/assets/fc872aff-695f-4dca-b864-886394370f9f" />
<img width="2560" height="1440" alt="DIM_DataFlow" src="https://github.com/user-attachments/assets/e600b470-c99a-4632-b23d-9c9b690f3d45" />
<img width="2560" height="1440" alt="Fact_DataFlow" src="https://github.com/user-attachments/assets/f63fc569-093a-4194-8fda-45c0a833ac33" />

---

Author

Ezat Mohamed
