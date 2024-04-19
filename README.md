# Project_PowerBI
There are provided three tables: Products, Sales, and Customers. These tables integrate into a SQL Server environment, perform data transformations, optimize the database, and generate a BI report.

# Table Schema

### Customers Table
        CREATE TABLE `customers` (
        `CustomerID` int(11) NOT NULL,
        `CustomerName` varchar(255) DEFAULT NULL,
        `ContactNumber` varchar(255) DEFAULT NULL
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

### Products Table
        CREATE TABLE `products` (
        `ProductID` int(11) NOT NULL,
        `ProductName` varchar(255) DEFAULT NULL,
        `Price` decimal(10,2) DEFAULT NULL
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

### Sales Table
        CREATE TABLE `sales` (
        `SaleID` int(11) NOT NULL,
        `ProductID` int(11) DEFAULT NULL,
        `CustomerID` int(11) DEFAULT NULL,
        `Quantity` int(11) DEFAULT NULL,
        `SaleDate` date DEFAULT NULL
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

<p>
  <img src="https://github.com/Saruj-chy/Project_PowerBI/blob/main/Image/database_ss.PNG"   width="600" title="Database Schema">
  </p>

# ETL Process
Load data from excel files on Microsoft Power BI platform and generate the dashboard report of whole sales.

# Query Optimization
### Write an SQL query to find the total revenue per product for the last quarter
SELECT p.ProductID, p.ProductName, SUM(p.Price*s.Quantity) AS TotalRevenue
FROM products AS p INNER JOIN sales AS s
ON p.ProductID = s.ProductID
WHERE QUARTER(s.SaleDate) = QUARTER(CURDATE()) - 1
GROUP BY p.ProductID
ORDER BY p.ProductID

# Business Intelligence Reporting

### Total sales by product category
        SELECT p.ProductID, p.ProductName, p.Price, SUM(s.Quantity) AS Sales
        FROM products AS p INNER JOIN sales AS s
        ON p.ProductID = s.ProductID
        GROUP BY p.ProductName
        ORDER BY p.ProductID
        

### Trends of sales over the last year
        SELECT 
            YEAR(s.SaleDate) AS Year,
            MONTH(s.SaleDate) AS Month,
            SUM(s.Quantity*p.Price) AS TotalRevenue
        FROM products AS p 
        INNER JOIN sales AS s
        ON p.ProductID = s.ProductID
        WHERE 
            s.SaleDate >= DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
        GROUP BY 
            YEAR(s.SaleDate), MONTH(s.SaleDate)
        ORDER BY 
            YEAR(s.SaleDate), MONTH(s.SaleDate);

### Top 10 customers by sales volume
        SELECT 
            c.CustomerName,
            SUM(s.Quantity) AS TotalSales
        FROM 
            sales s
        JOIN 
            customers c ON s.CustomerID = c.CustomerID
        GROUP BY 
            s.CustomerID, c.CustomerName
        ORDER BY 
            TotalSales DESC
        LIMIT 10;
<h1> Download <a href ="https://github.com/Saruj-chy/Project_PowerBI/blob/main/Excel%20Files/sales_table.xlsx" >Excel Files </a> </h1>

## Using a Microsoft PowerBI tool, create a dashboard that displays:
<p>
  <img src="https://github.com/Saruj-chy/Project_PowerBI/blob/main/Image/Dashboard_Report_Created_by_PowerBI.PNG"   width="600" title="Dashboard_Report_Created_by_PowerBI ">
  </p>







