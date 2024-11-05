# SALES DATA

## Table of Content
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Data Preparation and Data Summarization](#data-preparation-and-data-summarization)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Data Visualisation](#data-visualisation)
- [Results and Findings](#results-and-findings)
- [Recommendations](#recommendations)
- [References](#references)

### Project Overview

This data analysis project aims to analyze the sales performance of a retail store from January 2023 - August 2024. By analysing various aspects of the Sales data, I see to identify trends and uncover key insights such as top-selling products, regional performance, and monthly sales trends. The ultimate goal is to produce an interactive Power BI dashboard that highlights these findings.



### Data Source

SalesData: The primary dataset used for this analysis is the "LITA Capstone Dataset.xlsx" file containing detailed information about each sale transaction made by the retail store during the period

### Tools Used

- Microsoft Excel -for Data Cleaning and Data Summarization [Download here](https://microsoft.com)
- SQL Server -for Data Analysis [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- Power BI -for Data Visualization [Download here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

### Data Preparation and Data Summarization

In the initial data preparation phase, the following tasks were performed:
1. Data loading and Inspection.
2. Search for missing values and blank spaces using the COUNTBLANK function.
3. Removing duplicates.
4. Data cleaning and formatting.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions such as:
- What is the total sales on each product?
- What is the total revenues generated in each region?
- How much sales was made in each month?
- What is the average sales per product?
- Which products are top sellers by the total revenue generated?
- How many sales transactions were carried out in each region?
- What is the monthly sales trend for the current year?
- Who are the top 5 customers by total purchase amount spent?
- What percentage of total sales was contributed by each region?
- Were there any products with no sales in the last quarter?

### Data Analysis

#### Using Pivot Tables in MS Excel:
Some analysis were performed using Pivot Tables to summarise data. Below is an image of the Pivot tables that were created.

![Pivot Table Image](https://github.com/user-attachments/assets/5bd67226-dde1-40af-b6c1-9d6edbb6c188)


#### Using Excel Function
![Excel Formula Image](https://github.com/user-attachments/assets/30596391-cc53-4692-9869-08ffd8a28839)


#### Using SQL Server:
Majority of the analysis were carried out using SQL Server and some of the queries used includes:

a. Total Sales for each Product Category
```SQL
SELECT Product AS "PRODUCT CATEGORY", SUM (Revenue) AS "TOTAL SALES"
FROM [dbo].[SalesData]
GROUP BY Product
ORDER BY 2 desc
```

b. Number of Sales transaction in each Region
```SQL
SELECT Region AS "REGION", COUNT(Region) AS "SALES TRANSACTION"
FROM [dbo].[SalesData]
GROUP BY Region
ORDER BY 2 desc
```

c. Highest-selling product by Total Sales value
```SQL
SELECT Product AS "PRODUCT CATEGORY", SUM (Revenue) AS "TOTAL SALES"
FROM [dbo].[SalesData]
GROUP BY Product
ORDER BY 2 desc
```

d. Total Revenue per product
```SQL
SELECT Product AS "PRODUCT", SUM (Revenue) AS "REVENUE"
FROM [dbo].[SalesData]
GROUP BY Product
```

e. Monthly Sales Total for the Current Year
```SQL
SELECT * FROM [dbo].[SalesData]
WHERE OrderDate BETWEEN '2024-01-01' AND '2024-09-30'
```
```SQL
Monthly Sales Total for the Current Year
SELECT OrderDate,
	   DATEPART(YEAR, OrderDate) AS 'Current Year',
	   DATENAME(MONTH, OrderDate) AS 'MONTH',
	   SUM(Revenue) AS 'MONTHLY SALES'
FROM [dbo].[SalesData]
WHERE DATEPART(YEAR, OrderDate) = 2024
GROUP BY OrderDate
ORDER BY 1 asc
```

f. Top 5 Customers by Total Purchase Amount
```SQL
SELECT TOP 5 (CustomerId),
SUM(Revenue) AS 'TOTAL PURCHASE AMOUNT'
FROM [dbo].[SalesData]
GROUP BY CustomerId
ORDER BY 'TOTAL PURCHASE AMOUNT' DESC
```

g. Percentage of Total Sales contributed by each Region
```SQL
SELECT SUM(Revenue) FROM [dbo].[SalesData]
```
```SQL
SELECT Region,
	   SUM(Revenue) AS 'TOTAL SALES', ROUND ((SUM(Revenue)/2101090)*100, 2) AS 'PERCENTAGE'
FROM [dbo].[SalesData]
GROUP BY Region
ORDER BY 3 DESC
```

h. Products with no sales in the last quarter
```SQL
SELECT Product, OrderDate,
	   DATEPART(QUARTER, OrderDate) AS 'QUARTER',
	   SUM(Quantity) AS 'SALES'
FROM [dbo].[SalesData]
WHERE DATEPART(YEAR, OrderDate) = 2024 
AND   DATEPART(QUARTER, OrderDate) = 3
GROUP BY Product, OrderDate
```

### Data Visualisation

Using Power BI, I was able to create an interactive dashboard showing the insights and findings from my analysis using MS Excel and SQL Server.



### Results and Findings

### Recommendations



### References

1. Meta AI, WhatsApp
2. Video Tutorials from [The Incubator Hub](https://www.youtube.com/@theincubatornniggeria) YouTube Channel 
