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

![Sales Data](https://github.com/user-attachments/assets/3beeef12-9394-4975-9c4e-822afeed0516) 
###### *Image 1*

### Data Source

SalesData: The primary dataset used for this analysis is the "LITA Capstone Dataset.xlsx" file containing detailed information about each sale transaction made by the retail store during the period.

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
- What is the total revenue generated in each region?
- How much sales was made in each month?
- What is the average sales per product?
- Which products are top sellers by the total revenue generated?
- How many sales transactions were carried out in each region?
- What is the monthly sales trend for the current year?
- Who are the top 5 customers by total purchase amount spent?
- What percentage of total sales was contributed by each region?
- Were there any products with no sales in the last quarter?

### Data Analysis

#### - Using Pivot Tables in MS Excel:
Some analysis were performed using Pivot Tables to summarise data. Below is an image of the Pivot tables that were created.

![Pivot Table Image](https://github.com/user-attachments/assets/5bd67226-dde1-40af-b6c1-9d6edbb6c188)

###### *Image 2 shows the Total Sales made by the Retail Store in the period. It gives an insight into what portion of the Revenue was contributed by each product, each region, and each month.*

#### - Using Excel Function

Some of the formulas used includes:
```Excel
=SUMIF(Table1[[#All],[Region]], "East",Table1[[#All],[Revenue]])
=SUMIF(Table1[#All], "Gloves",Table1[[#All],[Quantity]])
=AVERAGEIF(Table1[#All], "Jacket",Table1[[#All],[Revenue]])
```


#### - Using SQL Server:
Majority of the analysis were carried out using SQL Server and some of the queries used includes:

**a. Total Sales for each Product Category:** The Retail store sells six (6) products, and each product with the revenue generated in the period are as follows, in descending order: Shoes (613380), Shirts (485600), Hats (316195), Gloves (296900), Jacket (208230), Socks(180785). **Majority of the revenue comes from selling Shoes**
```SQL
SELECT Product AS "PRODUCT CATEGORY", SUM (Revenue) AS "TOTAL SALES"
FROM [dbo].[SalesData]
GROUP BY Product
ORDER BY 2 desc
```
![SD_2c-Total Sales per Product Category](https://github.com/user-attachments/assets/88820410-fcd1-4595-b488-d4577980e6f2)
###### *Image 3*


**b. Number of Sales transaction in each Region:** In descending order, the East region carried out 2483 sales transactions, North - 2481, South - 2480, West - 2477. Such close margin!
```SQL
SELECT Region AS "REGION", COUNT(Region) AS "SALES TRANSACTION"
FROM [dbo].[SalesData]
GROUP BY Region
ORDER BY 2 desc
```
![SD_2b-Sales Transaction in each Region](https://github.com/user-attachments/assets/c72c35ca-63bc-486a-8390-1c9966596bfa)
###### *Image 4*


**c. Highest-selling product by Total Sales value:** Like mentioned above and as seen in [Image 3](#image-3), majority of the revenue comes from selling Shoes.
```SQL
SELECT Product AS "PRODUCT CATEGORY", SUM (Revenue) AS "TOTAL SALES"
FROM [dbo].[SalesData]
GROUP BY Product
ORDER BY 2 desc
```


**d. Total Revenue per product:** refer to [Image 3](#image-3) above.
```SQL
SELECT Product AS "PRODUCT", SUM (Revenue) AS "REVENUE"
FROM [dbo].[SalesData]
GROUP BY Product
```


**e. Monthly Sales Total for the Current Year**
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
![SD_2e-Monthly Sales for the Current Year](https://github.com/user-attachments/assets/5167b4ad-1ef6-41d4-a47f-4b415539ba78)
###### *Image 5*

**f. Top 5 Customers by Total Purchase Amount:** About     customers has same purchase amount of 4235, so there is no way to choose the Top 5
```SQL
SELECT TOP 5 (CustomerId),
SUM(Revenue) AS 'TOTAL PURCHASE AMOUNT'
FROM [dbo].[SalesData]
GROUP BY CustomerId
ORDER BY 'TOTAL PURCHASE AMOUNT' DESC
```
![SD_2f-Top Five Customers by Purchase Amount](https://github.com/user-attachments/assets/8d576941-ad8a-41a6-a08b-ea2ada8ed7fa)
###### *Image 6*

**g. Percentage of Total Sales contributed by each Region:** In descending order, South (44%), East (23%), North (19%), West (14%)
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
![SD_2g-Percentage of Total Sales by Region](https://github.com/user-attachments/assets/8842033b-dfa7-4c7b-b3fc-1ddd40e2ffc6)
###### *Image 7*

**h. Products with no sales in the last quarter:** There were not sales for Gloves, Jackets, Socks, and Shirts. Only Shoes and Hats were sold in the last quarter (Quarter 3, 2024).
```SQL
SELECT Product, OrderDate,
	   DATEPART(QUARTER, OrderDate) AS 'QUARTER',
	   SUM(Quantity) AS 'SALES'
FROM [dbo].[SalesData]
WHERE DATEPART(YEAR, OrderDate) = 2024 
AND   DATEPART(QUARTER, OrderDate) = 3
GROUP BY Product, OrderDate
```
![SD_2h-Products with no Sales in last Quarter](https://github.com/user-attachments/assets/ba012ba1-ca6c-4173-bb74-4ba538463b15)
###### *Image 8*

### Data Visualisation

Using Power BI, I was able to create an interactive dashboard showing the insights and findings from my analysis using MS Excel and SQL Server. Please refer to [Image 1](#image-1) above.


### Results and Findings
After critical analysis of the given data, the following were discovered:
1. There were no sales of Hats, Jackets, and Shirts in the South.
2. There were no sales of Gloves and Socks in the East.
3. There were no sales of Gloves, Shoes, and Socks in the North
4. There were no sales of Jackets and Shirts in the West.
5. The revenue generated from the sales of Shoes in the South is 11 times more that the revenue generated from the sale of the same product in both the East and West combined.
6. The sales of Socks generated the least revenue.

### Recommendations
I have the following recommendations:
1. The retail store should put in marketing efforts into penetrating the East region for the sales of Shoes. First, doing a market test, then adopt strategies such as Personal Selling and Promotions.
2. It appears that the retail store has its largest customer base in the South, but they do not sell Hats, Jackets, and Shirts to their customers. It would be good to begin to introduce these three products to their customers in the South.


### References

1. Meta AI, WhatsApp
2. Video Tutorials from [The Incubator Hub](https://www.youtube.com/@theincubatornniggeria) YouTube Channel 
