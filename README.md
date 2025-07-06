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

|Product_Category|	TotalSales |
|:---------------|:------------|
|Technology      |5984248      |

-- Top 3 Regions by Total Sales
SELECT TOP 3 Region, SUM(Sales) AS TotalSales
FROM [KMS Sql Case Study(2)]
GROUP BY Region
ORDER BY TotalSales DESC;
|Region  |	TotalSales|	RankType  |
|:-----  |:-----------|:----------|
|West 	 |3597549    	|Top        |
|Ontario |3063212	    |Top        |
|Prarie  |2837305	    |Top        |

-- Customers Who Returned Items and Their Segment
SELECT DISTINCT c.Customer_Name, c.Segment
FROM Orders o
JOIN Returns r ON o.Order_ID = r.Order_ID
JOIN Customers c ON o.Customer_ID = c.Customer_ID;


----Shipping Cost by Order Priority

  [Order_Priority], 
  [Ship_Mode], 
  COUNT([Order_ID]) AS NumberOfOrders,
  SUM([Shipping_Cost]) AS TotalShippingCost,
  AVG([Shipping_Cost]) AS AvgShippingCost
FROM [KMS Sql Case Study(2)]
GROUP BY [Order_Priority], [Ship_Mode]
ORDER BY [Order_Priority], [Ship_Mode];

-----What were the total sales of appliances in Ontario?
|Total_Sales|
|202346.8396|

  SELECT SUM ([Sales]) AS [Total_Sales]
FROM [KMS Sql Case Study(2)]
WHERE [Region] = 'Ontario'
AND [Product_Sub_Category] = 'Appliances'

----Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
Identify Bottom 10 Customers (SQL)
SELECT TOP 10 [Customer_Name], SUM(Sales) AS TotalSales
FROM KMS data
GROUP BY [Customer_Name]
ORDER BY TotalSales ASC;
Analyze Their Behavior
•	What products do they typically buy?
•	How often do they place orders?
SELECT [customer_name], [Product_Category], COUNT(*) AS OrderCount, SUM(Sales) AS TotalSpent
FROM [KMS Sql Case Study(2)]
WHERE [Customer_Name] IN (
    SELECT TOP 10 [Customer_Name]
    FROM [KMS Sql Case Study(2)]
    GROUP BY [Customer_Name]
    ORDER BY SUM(Sales) ASC
)
GROUP BY [Customer_Name], [Product_Category];

 KMS should:
- Engage Them with Personalized Promotions
--Offer discounts or bundled offers based on what they already buy.
- Upsell or Cross-Sell Products
--If they only buy low-cost items (e.g., accessories), suggest related high-value items (e.g., appliances or electronics).
- Loyalty Rewards Offer
--	Give incentives for ordering frequently (e.g., free shipping after X orders).
- Survey or Contact Them for Feedback
--	Ask why they don’t buy more. Feedback can reveal hidden barriers (e.g., website experience, delivery issues, unclear product specs).


Case Scenario II
---- Who are the most valuable customers, and what products or services do they typically purchase?
SELECT [Customer_Name], [Product_Category], SUM(Sales) AS CategorySales
FROM [KMS Sql Case Study(2)]
WHERE [Customer_Name] IN (
    SELECT TOP 3 [Customer_Name]
    FROM [KMS Sql Case Study(2)]
    GROUP BY [Customer_Name]
    ORDER BY SUM(Sales) DESC
)
GROUP BY [Customer_Name], [Product_Category]
ORDER BY [Customer_Name], CategorySales DESC;
|Customer_Name	|Product_Category	|CategorySales|
|:--------------|:----------------|:------------|
|Deborah Brumfield|	Technology|	76795.79|
|Deborah Brumfield|	Furniture|	12809.62|
|Deborah Brumfield|	Office Supplies|	7827.72|
|Emily Phan|	Technology|	110481.97|
|Emily Phan|	Furniture|	4011.65|
|Emily Phan|	Office Supplies|	2630.82|
|Roy Skaria|	Furniture|	50177.24|
|Roy Skaria|	Technology|	30349.39|
|Roy Skaria|	Office Supplies|	12015.52|

-----	Which small business customer had the highest sales?
SELECT TOP 1 [Customer_Name], SUM(Sales) AS TotalSales
FROM [KMS Sql Case Study(2)]
WHERE [Customer_Segment] = 'Small Business'
GROUP BY [Customer_Name]
ORDER BY TotalSales DESC;
|Customer_Name|	TotalSales|
|Dennis Kane|	75968

-------If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer
SELECT 
  [Order_Priority], 
  [Ship_Mode], 
  COUNT([Order_ID]) AS NumberOfOrders,
  SUM([Shipping_Cost]) AS TotalShippingCost,
  AVG([Shipping_Cost]) AS AvgShippingCost
FROM [KMS Sql Case Study(2)]
GROUP BY [Order_Priority], [Ship_Mode]
ORDER BY [Order_Priority], [Ship_Mode];

Critical and High Priority Orders:
•	Expected Shipping Method: Express Air (fastest)
•	Observation: Most Critical and High orders were shipped with Delivery Truck and Regular Air, which are slower. Misalignment between urgency and shipping method.
low and Not Specified Priority Orders:
•	Expected Shipping Method: Delivery Truck (slow and cheap)
•	Observation: Many Low and Not Specified orders used Express Air or Regular Air, which are more expensive. Overuse of expensive shipping on non-urgent orders.
The company did not always spend shipping costs appropriately based on order priority.

	


📎 Resources
SQL Server Docs

👤 Author
Comfort Odutayo
http://www.linkedin.com/in/adeolacomfort05
GitHub: @aloeda05
