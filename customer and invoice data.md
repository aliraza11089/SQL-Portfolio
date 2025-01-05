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


2. **Which customers are located in Brazil?**  
   ```sql 
   SELECT * 
   FROM customers 
   WHERE Country = "Brazil";

3. **Which customers from Brazil made purchases, and what are the details of their invoices, including invoice ID, billing country, and invoice date?**

   ```sql
   SELECT cust.FirstName, cust.LastName, inv.InvoiceId, inv.BillingCountry, inv.InvoiceDate
   FROM invoices AS inv
   LEFT JOIN customers AS cust
   ON inv.CustomerId = cust.CustomerId
   WHERE inv.BillingCountry = "Brazil";

4. **Which employees have the title of 'Sales Support Agent'?**
   ```sql
   SELECT * 
   FROM Employees
   WHERE Title = "Sales Support Agent";

5. **Which distinct billing countries are listed in the invoices?**
   ```sql
   SELECT DISTINCT BillingCountry 
   FROM Invoices;

6. **What is the number of invoices grouped by billing country, sorted in descending order?**
   ```sql
   SELECT BillingCountry, COUNT(*) 
   FROM Invoices
   GROUP BY BillingCountry
   ORDER BY COUNT(*) DESC;

7. **How many invoices were issued between January 1, 2009, and December 31, 2009?**
    ```sql
    SELECT COUNT(*) 
    FROM Invoices
    WHERE InvoiceDate BETWEEN '2009-01-01' AND '2009-12-31';

8. **How many invoices were issued in the USA?**
   ```sql
   SELECT COUNT(*) 
   FROM Invoices
   WHERE BillingCountry = "USA";




