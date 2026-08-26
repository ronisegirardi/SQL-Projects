# 🗄️ SQL Retail & Sales Data Analysis

## 📊 Project Overview

This project was completed as part of my **Level 3 Data Technician bootcamp** and focused on using **SQL to query and analyse relational retail and sales data**.

The project provided practical experience working with data relating to **products, suppliers, customers and sales**. SQL queries were used to retrieve, filter, organise and combine data to explore the information within the dataset.

## 🧩 SQL Skills Practised

- 🔎 **`SELECT`** – retrieving information from database tables
- 🔍 **`WHERE`** – filtering records based on specific conditions
- ↕️ **`ORDER BY`** – sorting query results
- 📊 **`GROUP BY`** – grouping records for analysis
- 🔗 **`JOIN`** – combining information from related tables
- 🔑 Working with **primary and foreign keys**
- 🗃️ Understanding **relational database structures**

## 🛒 Retail & Sales Analysis

The SQL exercises focused on exploring retail and sales data and understanding the relationships between different areas of the database.

Queries were used to investigate:

- Products and suppliers
- Customers and sales
- Sales transactions and sale items
- Products and quantities sold

Using `WHERE`, `ORDER BY` and `GROUP BY` helped filter, organise and analyse the data, while `JOIN` queries made it possible to combine information from multiple related tables.

## 🔗 Working with Table JOINs

A key part of the project was understanding how information in a relational database is connected.

For example, sales can be linked to customers, while individual sale items can be linked to both sales transactions and products.

This provided practical experience in using **table JOINs to bring related information together** and create a more complete view of the data.

## 📊 PostgreSQL Data Analysis Examples (`world_combined_30`)

```sql
-- 1. Language breakdown for Angola ordered by percentage share
SELECT language, language_percentage
FROM world_combined_30
WHERE country_name = 'Angola'
ORDER BY language_percentage DESC;

-- 2. Filtering countries by population range
SELECT DISTINCT country_name, country_population
FROM world_combined_30
WHERE country_population BETWEEN 100000 AND 3000000
ORDER BY country_population;

-- 3. Identifying countries with multiple official languages
SELECT country_name, COUNT(*) AS official_language_count
FROM world_combined_30
WHERE is_official = TRUE
GROUP BY country_name
HAVING COUNT(*) > 1
ORDER BY official_language_count DESC;

-- 4. Finding countries where the most spoken language is NOT official
SELECT country_name
FROM world_combined_30
WHERE language_percentage = (
    SELECT MAX(w2.language_percentage)
    FROM world_combined_30 AS w2
    WHERE w2.country_name = world_combined_30.country_name
)
AND is_official = FALSE;

```


## 💡 Extracting Insights

The project demonstrated how SQL can be used to move from raw database records towards answering practical business questions, such as:

- Which products are available or being sold?
- Which customers are associated with particular sales?
- How are products connected to suppliers?
- How can sales information be grouped and compared?
- How can information from multiple tables be combined for analysis?

The focus was not only on writing SQL syntax, but also on understanding **what the data shows and how queries can be used to investigate business-related questions**.

## 🎯 Learning Outcome

This project helped me build a foundation in **SQL and relational database analysis**. It provided practical experience with querying, filtering, sorting, grouping and joining data, while demonstrating how SQL can be used to explore retail and sales information.

I'm continuing to practise and consolidate these skills as I develop my wider data analysis toolkit.

---

### 🛠️ Tools & Technologies

**SQL** · **Supabase** · **PostgreSQL** · **Relational Databases**
