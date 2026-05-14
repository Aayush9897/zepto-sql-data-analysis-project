
#  🛒 Zepto E-commerce SQL Data Analyst Portfolio Project

A real-world data analytics portfolio project using scraped Zepto e-commerce inventory data to demonstrate end-to-end analyst workflows, from raw data cleaning and exploration to actionable business insights._

---

## 📌 Table of Contents
- <a href="#overview">Overview</a>
- <a href="#dataset">Dataset</a>
- <a href="#tools--technologies">Tools & Technologies</a>
- <a href="#project-workflow">Project Workflow</a>
- <a href="#how-to-run-this-project">How To Run This Project</a>
- <a href="#author--contact">Author & Contact</a>

---
<h2><a class="anchor" id="overview"></a>Overview</h2>

The goal is to simulate how actual data analysts in the e-commerce or retail industries work behind the scenes to use SQL to:

- Set up a messy, real-world e-commerce inventory database

- Perform Exploratory Data Analysis (EDA) to explore product categories, availability, and pricing inconsistencies

- Implement Data Cleaning to handle null values, remove invalid entries, and convert pricing from paise to rupees

- Write business-driven SQL queries to derive insights around pricing, inventory, stock availability, revenue and more

---
<h2><a class="anchor" id="dataset"></a>Dataset</h2>

The dataset was sourced from Kaggle and was originally scraped from Zepto’s official product listings. It mimics what you’d typically encounter in a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility – exactly how real catalog data looks.

 **Columns:**

- sku_id: Unique identifier for each product entry (Synthetic Primary Key)

- name: Product name as it appears on the app

- category: Product category like Fruits, Snacks, Beverages, etc.

- mrp: Maximum Retail Price (originally in paise, converted to ₹)

- discountPercent: Discount applied on MRP

- discountedSellingPrice: Final price after discount (also converted to ₹)

- availableQuantity: Units available in inventory

- weightInGms: Product weight in grams

- outOfStock: Boolean flag indicating stock availability

- quantity: Number of units per package (mixed with grams for loose produce)

---

<h2><a class="anchor" id="tools--technologies"></a>Tools & Technologies</h2>

- SQL (Common Table Expressions, Joins, Filtering)
- GitHub

---
<h2><a class="anchor" id="project-workflow"></a>Project Workflow</h2>

Here’s a step-by-step breakdown of what we do in this project:

### 1. Database & Table Creation
We start by creating a SQL table with appropriate data types:

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
```

### 2. Data Import
- Loaded CSV using pgAdmin's import feature.

 - If you're not able to use the import feature, write this code instead:
```sql
   \copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
  FROM 'data/zepto_v2.csv' WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');
```
- Faced encoding issues (UTF-8 error), which were fixed by saving the CSV file using CSV UTF-8 format.

### 3. Data Exploration
- Counted the total number of records in the dataset

- Viewed a sample of the dataset to understand structure and content

- Checked for null values across all columns

- Identified distinct product categories available in the dataset

- Compared in-stock vs out-of-stock product counts

- Detected products present multiple times, representing different SKUs

### 4. Data Cleaning
- Identified and removed rows where MRP or discounted selling price was zero

- Converted mrp and discountedSellingPrice from paise to rupees for consistency and readability
  
### 5. Business Insights
- Found top 10 best-value products based on discount percentage

- Identified high-MRP products that are currently out of stock

- Estimated potential revenue for each product category

- Filtered expensive products (MRP > ₹500) with minimal discount

- Ranked top 5 categories offering highest average discounts

- Calculated price per gram to identify value-for-money products

- Grouped products based on weight into Low, Medium, and Bulk categories

- Measured total inventory weight per product category

---

<h2><a class="anchor" id="how-to-run-this-project"></a>How To Run This Project</h2>

1. Clone the repository:
```bash
git clone https://github.com/Aayush9897/zepto-sql-data-analysis-project.git
```
2. Open zepto_SQL_data_analysis.sql

    This file contains:

      - Table creation

      - Data exploration

      - Data cleaning

      - SQL Business analysis
3. Load the dataset into pgAdmin or any other PostgreSQL client

      - Create a database and run the SQL file

      - Import the dataset (convert to UTF-8 if necessary)

---
<h2><a class="anchor" id="author--contact"></a>Author & Contact</h2>

**Aayush Kumar Singh**  
 
📧 Email: aayushmaanthakur30@gmail.com  

