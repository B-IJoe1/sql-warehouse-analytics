# sql-datawarehouse-project
Building a modest data warehouse with SQL Server, including ETL processes, data modelling &amp; analytics.

# Naming Conventions

This document defines naming standards for tables, columns, and stored procedures in the data warehouse. These conventions ensure consistency across layers and make the system easier to understand and maintain.

## Why This Matters

Clear and consistent naming improves readability, reduces onboarding time for new contributors, and prevents ambiguity when working across multiple data layers and source systems. Following these rules also makes debugging, lineage tracking, and long-term maintenance significantly easier.

---

## General Rules

- Use **snake_case** with lowercase letters.
- Use **English** for all object names.
- Avoid **SQL reserved keywords**.
- Names should be descriptive and concise.

---

## Table Naming

### Bronze and Silver Layers

- Table names must retain their original source table names.
- Each table must be prefixed with the source system name to preserve lineage.

**Format**


- `sourcesystem`: Origin system (e.g., `crm`, `erp`)
- `entity`: Original table name from the source

**Example**
- `crm_customer_info`

---

### Gold Layer

- Table names should reflect business concepts rather than source structures.
- Use prefixes to indicate the analytical role of the table.

**Format**


- `category`: Table type (`dim`, `fact`, `agg`)
- `entity`: Business-aligned name

**Examples**
- `dim_customers`
- `fact_sales`
- `agg_sales_monthly`

**Category Prefixes**

| Prefix | Purpose            | Example              |
|------|--------------------|----------------------|
| dim_ | Dimension tables   | dim_product          |
| fact_| Fact tables        | fact_orders          |
| agg_ | Aggregated tables  | agg_revenue_daily    |

---

## Column Naming

### Surrogate Keys

- Dimension tables must use surrogate primary keys.
- Surrogate keys must end with `_key`.

**Example**
- `customer_key`

---

## Data Architecture 
Displays the ETL process from Bronze to Gold into the consumer layer

![Data Architecture](docs/data_architecture.png)

## Data Integration
How the tables connect with each other from the different source tables (CRM & ERP)

![Data Integration](docs/data_integration.png)

## Data Flow
The source data that flows from the Silver layer into the Gold layer

![Data Flow](docs/data_flow.png)



### Technical Columns

- System-generated metadata columns must start with `dwh_`.

**Example**
- `dwh_load_date`

---

## Stored Procedure Naming

- Stored procedures responsible for loading data must indicate the target layer.

**Format**


- `layer`: `bronze`, `silver`, or `gold`

**Examples**
- `load_bronze`
- `load_silver`
- `load_gold`
