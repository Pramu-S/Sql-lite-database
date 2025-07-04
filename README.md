# Sql-lite-database
# 📊 Task 7 - Basic Sales Summary using SQLite and Python

This project is part of the Elevate Labs Data Analyst Internship under the Ministry of MSME, Govt. of India.

## 📝 Objective

Use SQL inside Python to pull basic sales information (like total quantity sold and total revenue) from a tiny SQLite database, then display the result using simple print statements and a basic bar chart.

## 🛠️ Tools & Libraries Used

- Python
- SQLite (built-in with Python)
- pandas
- matplotlib
- sqlite3 module

## 📁 Dataset

- A small SQLite database file `sales_data.db`
- Contains one table: `sales`

## 🔄 SQL Query Used

```sql
SELECT 
    product, 
    SUM(quantity) AS total_qty, 
    SUM(quantity * price) AS revenue 
FROM 
    sales 
GROUP BY 
    product;import sqlite3
import pandas as pd
import matplotlib.pyplot as plt

# Connect to SQLite DB
conn = sqlite3.connect("sales_data.db")

# SQL query
query = """
SELECT product, 
       SUM(quantity) AS total_qty, 
       SUM(quantity * price) AS revenue 
FROM sales 
GROUP BY product
"""

# Load to pandas
df = pd.read_sql_query(query, conn)

# Print results
print(df)

# Plot bar chart
df.plot(kind='bar', x='product', y='revenue')
plt.title("Revenue by Product")
plt.ylabel("Revenue")
plt.xlabel("Product")
plt.tight_layout()

# Save chart
plt.savefig("sales_chart.png")
plt.show()

# Close DB connection
conn.close()
