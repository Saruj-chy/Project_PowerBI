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
