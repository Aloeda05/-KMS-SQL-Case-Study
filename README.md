# -KMS-SQL-Case-Study
This repository contains SQL-based analysis for a fictional company, **KMS**, to explore customer segmentation, shipping cost optimization, and sales strategy.
## 📌 Project Overview

- **Dataset**: KMS Sales & Order Status CSVs
- **Tools**: SQL Server, Excel (for visuals), GitHub
- **Objective**: Answer key business questions using SQL queries

---

## 📂 Repository Structure

kms-sql-case-study/
├── data/ # Source data files
├── queries/ # SQL scripts answering each business question
├── visuals/ # Charts/images from SQL or Excel
├── docs/ # Supporting files, question list, notes
└── README.md # Project documentation

pgsql
Copy
Edit

---

## 📊 Business Questions Answered

1. **Top-selling Product Category**
2. **Top 3 & Bottom 3 Regions by Sales**
3. **Total Sales of Appliances in Ontario**
4. **How to Improve Revenue from Bottom 10 Customers**
5. **Shipping Method with Highest Cost**
6. **Most Valuable Customers & Their Products**
7. **Top Small Business by Sales**
8. **Corporate Customer with Most Orders (2009–2012)**
9. **Most Profitable Consumer Customer**
10. **Customers Who Returned Items & Their Segment**
11. **Did Shipping Method Align with Order Priority?**

---

## 🛠️ Methodology

- Used **GROUP BY**, **JOIN**, **ORDER BY**, **RANK()**, and **CASE** statements
- Performed aggregations on sales, shipping cost, and product categories
- Analyzed return behavior and profit contribution by segment

---

## 📂 Example SQL Snippets

```sql
-- Top 3 Regions by Total Sales
SELECT TOP 3 Region, SUM(Sales) AS TotalSales
FROM KMS_Sales
GROUP BY Region
ORDER BY TotalSales DESC;
sql
Copy
Edit
-- Customers Who Returned Items and Their Segment
SELECT DISTINCT c.Customer_Name, c.Segment
FROM Orders o
JOIN Returns r ON o.Order_ID = r.Order_ID
JOIN Customers c ON o.Customer_ID = c.Customer_ID;
📈 Sample Visuals
See /visuals/ for:

📊 Shipping Cost by Order Priority

📉 Bottom 10 Customers by Revenue

📎 Resources
SQL Server Docs

W3Schools SQL Reference

Kaggle Case Studies

👤 Author
Comfort Adelegan
GitHub: @yourusername
