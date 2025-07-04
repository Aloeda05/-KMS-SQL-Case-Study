# -KMS-SQL-Case-Study
This repository contains SQL-based analysis for a company, **KMS**, to explore customer segmentation, shipping cost optimization, and sales strategy.
## 📌 Project Overview

- **Dataset**: KMS Sales & Order Status CSVs
- **Tools**: SQL Server, Excel (for visuals), GitHub
- **Objective**: Answer key business questions using SQL queries
- **Data Source**: DSA Incubator Hub kms-sql-case-study/

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


## 🛠️ Methodology

- Used **GROUP BY**, **JOIN**, **ORDER BY**, **RANK()**, and **CASE** statements
- Performed aggregations on sales, shipping cost, and product categories
- Analyzed return behavior and profit contribution by segment


## 📂 Example SQL Snippets

```sql
Case Scenario I 
-----Which product category had the highest sales?------
SELECT [Product_Category], SUM(Sales) AS TotalSales
FROM [KMS Sql Case Study(2)]
GROUP BY [Product_Category]
ORDER BY TotalSales DESC
SELECT TOP 1
Case Scenario I 
1.	Which product category had the highest sales?
SELECT [Product_Category], SUM(Sales) AS TotalSales
FROM [KMS Sql Case Study(2)]
GROUP BY [Product_Category]
ORDER BY TotalSales DESC
SELECT TOP 1
Product_Category	TotalSales
Technology	5984248

-- Top 3 Regions by Total Sales
SELECT TOP 3 Region, SUM(Sales) AS TotalSales
FROM [KMS Sql Case Study(2)]
GROUP BY Region
ORDER BY TotalSales DESC;
Region	TotalSales	RankType
West  	3597549    	Top
Ontario	3063212	    Top
Prarie	2837305	    Top

-- Customers Who Returned Items and Their Segment
SELECT DISTINCT c.Customer_Name, c.Segment
FROM Orders o
JOIN Returns r ON o.Order_ID = r.Order_ID
JOIN Customers c ON o.Customer_ID = c.Customer_ID;


📊 Shipping Cost by Order Priority

  [Order_Priority], 
  [Ship_Mode], 
  COUNT([Order_ID]) AS NumberOfOrders,
  SUM([Shipping_Cost]) AS TotalShippingCost,
  AVG([Shipping_Cost]) AS AvgShippingCost
FROM [KMS Sql Case Study(2)]
GROUP BY [Order_Priority], [Ship_Mode]
ORDER BY [Order_Priority], [Ship_Mode];


📎 Resources
SQL Server Docs

👤 Author
Comfort Odutayo
GitHub: @aloeda05
