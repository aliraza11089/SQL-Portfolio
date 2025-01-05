# SQL Portfolio

## Overview
This repository contains SQL queries for customer and invoice analysis. These queries showcase my ability to analyze data from real-world business scenarios, focusing on customer locations, invoice statistics, and employee roles. The repository includes various SQL queries that answer important business questions related to customer demographics, billing, and sales support.

## Projects

### 1. Customer and Invoice Analysis
This project includes SQL queries to answer business questions using customer and invoice data. The queries include:

1. **Which customers are located outside the USA?**  
   ```sql
   SELECT FirstName, LastName, CustomerId, Country 
   FROM customers 
   WHERE Country != "USA";

2. Which customers are located in Brazil?
 ```sql 
SELECT * 
FROM customers 
WHERE Country = "Brazil";

3. Which customers from Brazil made purchases, and what are the details of their invoices, including invoice ID, billing country, and invoice date?
 ```sql
SELECT cust.FirstName, cust.LastName, inv.InvoiceId, inv.BillingCountry, inv.InvoiceDate
FROM invoices AS inv
LEFT JOIN customers AS cust
ON inv.CustomerId = cust.CustomerId
WHERE inv.BillingCountry = "Brazil";




