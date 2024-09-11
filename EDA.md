### Question 1: Find the total number of products in each product category
````sql
SELECT
	PC.ProductCategoryKey,
	COUNT(*) AS TotalProducts
FROM DimProduct P
	JOIN DimProductSubcategory PS
		ON P.ProductSubcategoryKey= PS.ProductSubcategoryKey
	JOIN DimProductCategory PC
		ON PC.ProductCategoryKey =PS. ProductCategoryKey
GROUP BY PC.ProductCategoryKey;
````

![image](https://github.com/user-attachments/assets/9be23daa-365c-45c1-8f3f-b7f8086a7fb6)


### Question 2: Find the top 10 customers with the highest total purchase amount
````sql

SELECT TOP 10 
  CONCAT(C.FirstName, ' ', C.LastName) FullName,
  SUM(S.SalesAmount) AS TotalPurchase
FROM FactInternetSales S
	JOIN DimCustomer C
		ON S.CustomerKey = C.CustomerKey
GROUP BY
    CONCAT(C.FirstName, ' ', C.LastName) 
ORDER BY TotalPurchase DESC;
````

![image](https://github.com/user-attachments/assets/e5ba76ed-9c20-45aa-98cb-328bd46071a0)

### Question 3: Find the average purchase for each customer
````sql

SELECT 
  CONCAT(C.FirstName, ' ', C.LastName) FullName,
  AVG(S.SalesAmount) AS AVGPurchase
FROM FactInternetSales S
	JOIN DimCustomer C
		ON S.CustomerKey = C.CustomerKey
GROUP BY CONCAT(C.FirstName, ' ', C.LastName);
````

![image](https://github.com/user-attachments/assets/51cecc12-c052-45fc-bdd9-d8a523a2fdff)


### Question 4: Find the total quantity sold for each product
````sql

SELECT
	DP.ProductKey,
	SUM(FS.OrderQuantity) TotalQuantity
FROM FactInternetSales FS 
	JOIN DimProduct DP
		ON DP.ProductKey = FS.ProductKey
GROUP BY DP.ProductKey;
````
![image](https://github.com/user-attachments/assets/de2befb9-8871-4924-bcc8-2830899d3bde)


### Question 5: Find the total sales amount for each territory
````sql

SELECT
	SalesTerritoryKey,
	SUM(SalesAmount) AS Totalsales
FROM [dbo].[FactInternetSales]
GROUP BY SalesTerritoryKey;
````

![image](https://github.com/user-attachments/assets/a3a30125-dc59-48e9-999f-6d41649e8f4e)


### Question 6: Find the total number of orders placed in each year
````sql

SELECT
	YEAR(OrderDate) AS OrderYear,
	COUNT(*) AS TotalOrders
FROM FactInternetSales 
GROUP BY YEAR(OrderDate)
````
![image](https://github.com/user-attachments/assets/26661d12-00a8-4277-999f-da978d3634f4)


### Question 7: Find the average sales amount for each year.
````sql

SELECT
	YEAR(OrderDate) AS OrderYear,
	AVG(SalesAmount) AS AverageSalesAmount
FROM [dbo].[FactInternetSales]
GROUP BY YEAR(OrderDate);
````
![image](https://github.com/user-attachments/assets/1830e4a6-673c-498a-85f8-1b0f4fd89f5e)



### Question 8: Find the top 5 products with the highest total sales amount
````sql

SELECT TOP 5
	DP.EnglishProductName,
	SUM(SF.SalesAmount) AS TotalSalesAmount
FROM  FactInternetSales SF
	JOIN DimProduct DP 
		ON DP.ProductKey = SF.ProductKey
GROUP BY DP.EnglishProductName
ORDER BY TotalSalesAmount DESC;
````
![image](https://github.com/user-attachments/assets/f036f5ba-0ac7-4129-b6ef-1aae06f8e775)

### Question 9: Find the total number of employees in each job title
````sql

SELECT
	Title,
	COUNT(*) AS TotalEmployees
FROM [dbo].[DimEmployee]
GROUP BY Title;
````

![image](https://github.com/user-attachments/assets/db722788-8d0d-41bd-aea7-ba2570fa4bf9)

### Question 10: Find the total number of products in each colour.
````sql

SELECT
	Color,
	COUNT(*) AS Totalnumber
FROM [dbo].[DimProduct]
GROUP BY Color;
````
![image](https://github.com/user-attachments/assets/d0dbf3dd-46b1-474f-a086-aa46b3d96700)

### Question 11: Find the top 10 Customers with the highest number of orders
````sql

SELECT TOP 10
	CONCAT(C.FirstName, ' ', C.LastName) FullName,
	COUNT(*) AS TotalOrders
FROM FactInternetSales SF
	JOIN DimCustomer C
		ON C.CustomerKey = SF.CustomerKey
GROUP BY CONCAT(C.FirstName, ' ', C.LastName)
ORDER BY TotalOrders DESC;
````

![image](https://github.com/user-attachments/assets/30b49b59-7dcd-44c3-9aff-ea2e0ca0f090)

### Question 12: Find the total number of products in each subcategory
````sql

SELECT
	P.ProductSubcategoryKey,
	COUNT(P.ProductKey) AS ProductCount
FROM DimProduct P
	JOIN DimProductSubcategory SB
		ON SB.ProductSubcategoryKey = P.ProductSubcategoryKey
GROUP BY P. ProductSubcategoryKey
ORDER BY 2 DESC;
````

![image](https://github.com/user-attachments/assets/ceb88ce0-0af5-4d9b-8a7c-6e107d322973)

### Question 13: Find the top 5 products with the highest profit margin
````sql

SELECT DISTINCT TOP 5
	P.EnglishProductName,
	SalesAmount,
	TotalProductCost,
	SalesAmount - TotalProductCost AS Profit,
	(SalesAmount - TotalProductCost)/ TotalProductCost * 100 AS ProfitMargin
FROM FactInternetSales SF
	JOIN DimProduct P
		ON SF.ProductKey=P.ProductKey
ORDER BY ProfitMargin DESC;
````

![image](https://github.com/user-attachments/assets/5c39bb0e-e1c4-4395-8108-7e292d663562)

