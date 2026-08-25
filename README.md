# Data Technician Bootcamp: Databases & SQL Project

## 📌 Project Overview

This repository contains the database design notes, conceptual research, schema architecture, and SQL query scripts completed during Week 3 of the **Data Technician Bootcamp**. The project focuses on relational database management systems (RDBMS), database normalization, relational schema design, and hands-on PostgreSQL querying using Supabase.

The project covers two core operational areas:

* **Retail & Sales Database Engineering ("Smart Corner")**: Designing and implementing a multi-table relational schema for a convenience store to manage inventory, sales transactions, supplier relations, customer profiles, and loyalty programs.


* **PostgreSQL Data Analysis (`world_combined_30`)**: Executing data retrieval, filtering, aggregation, pattern matching, and subqueries on global demographic and linguistic data.



---

## 🛠️ Core Skills & SQL Techniques Demonstrated

### 1. Database Concepts & Data Modeling

* **Primary & Foreign Keys**: Used unique identifiers (PKs) and relational links (FKs) to enforce entity integrity and referential integrity across related tables.


* **Cardinality & Relationships**: Modeled One-to-One (1:1), One-to-Many (1:N), and Many-to-Many (N:M) relationships. Resolved N:M relationships between sales transactions and product SKUs using associative bridge tables (`Sale_Items`).


* **Relational vs. Non-Relational Architectures**: Evaluated structured SQL databases for strict data accuracy against flexible NoSQL databases suited for high-velocity, unstructured data such as real-time fraud detection.



### 2. Table JOIN Operations

Researched, classified, and applied SQL `JOIN` types to combine multi-table datasets:

* **`INNER JOIN`**: Extracted matching records across tables (e.g., mapping enrolled students to course modules).


* **`LEFT JOIN` & `RIGHT JOIN**`: Maintained all records from a primary table while populating unmapped outer fields with `NULL` (e.g., identifying courses without enrolled students).


* **`FULL OUTER JOIN`**: Identified data gaps, discrepancies, and overlaps across distinct datasets.


* **`CROSS JOIN`**: Produced Cartesian products for complete combination matrices (e.g., generating all product size and color variations).


* **`SELF JOIN`**: Evaluated intra-table comparative relationships (e.g., comparing employee training progress).



### 3. PostgreSQL Querying & Data Extraction Techniques

* **Data Selection & Filtering (`SELECT`, `WHERE`, `DISTINCT`)**: Filtered records using exact values, boolean flags (`is_official = FALSE`), range conditions (`BETWEEN`), and string matching (`LIKE '%la%'`).


* **Data Sorting (`ORDER BY`)**: Sorted numerical metrics and text columns in ascending or descending (`DESC`) order.


* **Data Aggregation (`GROUP BY`, `HAVING`, Aggregate Functions)**: Aggregated data using `COUNT()`, `MAX()`, and `SUM()`, using `HAVING` clauses to filter grouped results.


* **Correlated Subqueries**: Built nested subqueries to identify complex conditions (e.g., finding countries where the most spoken language is non-official).



---

## 🏪 Case Study: Retail & Sales Database ("Smart Corner")

A multi-table relational schema was created for **Smart Corner**, a retail convenience store modeled after Co-op operational structures. The database tracks inventory, multi-item customer sales transactions, supplier details, and loyalty membership details.

### Relational Schema Architecture

| Table Name | Primary Key (PK) | Foreign Keys (FK) | Core Fields & Purpose |
| --- | --- | --- | --- |
| **`Inventory`** | `SKU`<br> | `Supplier_ID` → `Suppliers(Supplier_ID)`<br> | Product Name, Category, Price, StockCount

 |
| **`Suppliers`** | `Supplier_ID`<br> | None

 | Supplier Name, Contact Details

 |
| **`Customers`** | `Customer_ID`<br> | None

 | Customer Name, Address, Phone, Email, Membership Details

 |
| **`Sales`** | `Transaction_ID`<br> | `Customer_ID` → `Customers(Customer_ID)`<br> | Transaction Date, Customer Link

 |
| **`Sale_Items`** | `Sale_Item_ID`<br> | `Transaction_ID` → `Sales(Transaction_ID)`, `SKU` → `Inventory(SKU)`<br> | Quantity (Bridge table for Sales ↔ Products N:M relationship)

 |

### DDL & DML SQL Implementation Examples

```sql
-- 1. Database & Table Creation[cite: 1]
CREATE DATABASE smart_corner;

CREATE TABLE Products (
    SKU VARCHAR(20) PRIMARY KEY,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10, 2),
    StockCount INT,
    Supplier_ID INT
);

-- 2. Establishing Foreign Key Constraints[cite: 1]
ALTER TABLE Products
ADD FOREIGN KEY (Supplier_ID) 
REFERENCES Suppliers(Supplier_ID);

-- 3. Inserting Initial Inventory Data[cite: 1]
INSERT INTO Products (SKU, ProductName, Category, Price, StockCount, Supplier_ID)
VALUES ('A123', 'Basmati Rice', 'Cupboard', 2.30, 18, 3);

```

### Data Governance, Security & Maintenance

* **Stock Accuracy**: Enforced stock level updates upon sales or deliveries alongside regular physical inventory audits.


* **Validation Rules**: Implemented database validation constraints to prevent incorrect entry insertion.


* **Security & Compliance**: Implemented regular backups and restricted customer sensitive data access to authorized management only.



---

## 📊 PostgreSQL Data Analysis Examples (`world_combined_30`)

```sql
-- 1. Language breakdown for Angola ordered by percentage share[cite: 1]
SELECT language, language_percentage
FROM world_combined_30
WHERE country_name = 'Angola'
ORDER BY language_percentage DESC;

-- 2. Filtering countries by population range[cite: 1]
SELECT DISTINCT country_name, country_population
FROM world_combined_30
WHERE country_population BETWEEN 100000 AND 3000000
ORDER BY country_population;

-- 3. Identifying countries with multiple official languages[cite: 1]
SELECT country_name, COUNT(*) AS official_language_count
FROM world_combined_30
WHERE is_official = TRUE
GROUP BY country_name
HAVING COUNT(*) > 1
ORDER BY official_language_count DESC;

-- 4. Finding countries where the most spoken language is NOT official[cite: 1]
SELECT country_name
FROM world_combined_30
WHERE language_percentage = (
    SELECT MAX(w2.language_percentage)
    FROM world_combined_30 AS w2
    WHERE w2.country_name = world_combined_30.country_name
)
AND is_official = FALSE;

```
