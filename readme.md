Online Retail Database Project
Table: online_retail

This project sets up a sample table online_retail to simulate an e-commerce retail dataset, typically used for data analysis, visualization, and database practice.

Table Schema

CREATE TABLE online_retail (
    InvoiceNo VARCHAR(20),
    StockCode VARCHAR(20),
    Description TEXT,
    Quantity INT,
    InvoiceDate DATETIME,
    UnitPrice DECIMAL(10, 2),
    CustomerID INT,
    Country VARCHAR(100)
);
Column Descriptions

Column Name	Data Type	Description

InvoiceNo	VARCHAR(20)	Unique identifier for each transaction
StockCode	VARCHAR(20)	Product/item code
Description	TEXT	Description of the product
Quantity	INT	Number of units sold
InvoiceDate	DATETIME	Date and time of the invoice
UnitPrice	DECIMAL(10,2)	Price per unit of product
CustomerID	INT	ID of the customer
Country	VARCHAR(100)	Country where the invoice was issued

Common Errors and Fixes

Error Code	Problem	Solution

1050	Table already exists	Use DROP TABLE IF EXISTS before creating the table
1054	Unknown column in field list	Check spelling; e.g., use InvoiceDate, not order_date

Tips

Always verify column names before using them in INSERT, SELECT, or UPDATE statements.

Use IF NOT EXISTS or DROP TABLE IF EXISTS to avoid duplication errors.

Example Use Case

INSERT INTO online_retail (
    InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country
) VALUES
('536365', '85123A', 'WHITE HANGING HEART T-LIGHT HOLDER', 6, '2010-12-01 08:26:00', 2.55, 17850, 'United Kingdom'),
('536365', '71053', 'WHITE METAL LANTERN', 6, '2010-12-01 08:26:00', 3.39, 17850, 'United Kingdom'),
('536365', '84406B', 'CREAM CUPID HEARTS COAT HANGER', 8, '2010-12-01 08:26:00', 2.75, 17850, 'United Kingdom'),
('536365', '84029G', 'KNITTED UNION FLAG HOT WATER BOTTLE', 6, '2010-12-01 08:26:00', 3.39, 17850, 'United Kingdom'),
('536365', '84029E', 'RED WOOLLY HOTTIE WHITE HEART.', 6, '2010-12-01 08:26:00', 3.39, 17850, 'United Kingdom');
Query 1: Monthly Sales Revenue & Order Volume

```sql
SELECT
    EXTRACT(YEAR FROM InvoiceDate) AS year,
    EXTRACT(MONTH FROM InvoiceDate) AS month,
    SUM(Quantity * UnitPrice) AS total_revenue,
    COUNT(DISTINCT InvoiceNo) AS order_volume
FROM online_retail
GROUP BY year, month
ORDER BY year, month;
 Query 2: Top 10 Selling Products by Quantity

SELECT
    Description,
    SUM(Quantity) AS total_quantity_sold
FROM online_retail
GROUP BY Description
ORDER BY total_quantity_sold DESC
LIMIT 10;
Ouery 3 :Top 10 Products by Revenue

SELECT
    Description,
    SUM(Quantity * UnitPrice) AS total_revenue
FROM online_retail
GROUP BY Description
ORDER BY total_revenue DESC
LIMIT 10;

Query 4 :Total Revenue by Country

SELECT
    Country,
    SUM(Quantity * UnitPrice) AS total_revenue
FROM online_retail
GROUP BY Country
ORDER BY total_revenue DESC;
Query 5 :Customer Lifetime Value

SELECT
    CustomerID,
    SUM(Quantity * UnitPrice) AS lifetime_value
FROM online_retail
WHERE CustomerID IS NOT NULL
GROUP BY CustomerID
ORDER BY lifetime_value DESC;

Query 6 : Daily Sales Trends

SELECT
    DATE(InvoiceDate) AS sale_date,
    SUM(Quantity * UnitPrice) AS daily_revenue
FROM online_retail
GROUP BY sale_date
ORDER BY sale_date;
Notes

Dates should be in the format: YYYY-MM-DD HH:MM:SS
Ensure that NULL values in CustomerID, Quantity, UnitPrice, and InvoiceDate are handled appropriately.
 Use Cases

Analyze customer value and purchase behavior.
Track trends in sales over time (monthly/daily).
Identify top products and regions contributing to revenue.
