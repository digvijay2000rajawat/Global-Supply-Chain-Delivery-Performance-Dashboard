# Global Supply Chain & Delivery Performance Dashboard

## Note

This repository contains the Power BI report and project documentation.

If the dataset is not available locally, Power BI may display a refresh warning. To use the report with live data, download the original dataset, update the data source path in Power BI, and refresh the report.

## Project Overview

This Power BI project analyses global supply chain, sales, profitability, order volume, and delivery performance using a supply chain order dataset.

The main business problem identified in this project is that the business generates strong revenue and profit, but delivery performance is a major operational concern because a large share of orders are delivered late.

The dashboard helps business users monitor key supply chain KPIs, identify late delivery patterns, compare market performance, and understand which products and categories contribute most to revenue and profitability.

---

## Business Objective

The goal of this project is to answer the following business questions:

* How much revenue and profit is the business generating?
* What is the overall order volume?
* What percentage of orders are delivered late?
* Which shipping modes have the highest late delivery rate?
* Which markets are most affected by delivery delays?
* Which product categories and products drive the most revenue?
* Are high-revenue markets also performing well operationally?

---

## Dashboard Pages

### 1. Executive Overview

This page provides a high-level summary of business and delivery performance.

Key metrics shown:

* Total Revenue
* Total Profit
* Total Orders
* Late Order Rate
* Average Order Value
* Monthly Revenue Trend
* Orders by Delivery Status
* Revenue and Profit by Market
* Late Order Rate by Market

![Executive Overview](executive-overview.png)

---

### 2. Delivery Performance Analysis

This page focuses on delivery delays and fulfilment performance.

Key metrics shown:

* Late Orders
* Late Order Rate
* On-Time Order Rate
* Average Shipping Delay Days
* Cancelled Orders
* Late Order Rate by Shipping Mode
* Average Shipping Delay by Shipping Mode
* Late Order Rate Trend
* Delivery Status by Shipping Mode

![Delivery Performance](delivery-performance.png)

---

### 3. Market & Product Performance

This page connects commercial performance with supply chain performance.

Key metrics shown:

* Revenue by Product Category
* Profit Margin by Category
* Top 5 Products by Revenue
* Market Performance Summary
* Revenue
* Profit
* Profit Margin
* Quantity Sold
* Late Order Rate

![Market & Product Performance](market-product-performance.png)

---

## Dataset

The dashboard was built using the public DataCo Supply Chain Dataset.

The original dataset is not included in this repository because of GitHub file size limitations and customer-related fields contained in the source data.

You can download the dataset from its original public source and refresh the Power BI report if required.

---

## Data Cleaning and Transformation

Data cleaning was performed in Power Query.

Main cleaning steps included:

* Removed unnecessary personal information such as customer email, password, name, and street address
* Removed empty or low-value columns
* Removed duplicate information columns
* Renamed columns for better business readability
* Changed data types for dates, currency, percentages, IDs, and text fields
* Cleaned and trimmed text values
* Standardised delivery status labels
* Created a Shipping Delay Days column
* Created a Destination Key for the destination dimension

---

## Data Model

A star schema was created to make the model clean and easy to understand.

### Fact Table

* FactOrderItems

### Dimension Tables

* DimDate
* DimOrder
* DimProduct
* DimCustomer
* DimOrderDestination

The fact table stores transactional order-item values such as revenue, profit, quantity, and discount.

The dimension tables store descriptive fields such as product, customer, order, date, and destination information.

---

## Key DAX Measures

The project includes essential DAX measures such as:

* Total Revenue
* Gross Sales
* Total Discount
* Total Profit
* Profit Margin %
* Total Quantity
* Total Orders
* Average Order Value
* Late Orders
* On-Time Orders
* Late Order Rate %
* On-Time Order Rate %
* Average Shipping Delay Days
* Cancelled Orders

---

## Key Insights

* The business generates strong global revenue and profit.
* Delivery performance is a major concern because a large share of orders are late.
* Late delivery rate should be analysed by shipping mode, market, and time period.
* High-revenue markets should not be judged only by sales; profit margin and delivery performance should also be considered.
* Product categories and top products can help identify where the business should focus inventory, fulfilment, and delivery improvements.

---

## Tools Used

* Power BI Desktop
* Power Query
* DAX
* Data Modelling
* Star Schema
* Data Visualization

---

## Skills Demonstrated

* Data cleaning and transformation
* Data modelling using star schema
* DAX measure creation
* KPI design
* Business analysis
* Supply chain performance analysis
* Dashboard storytelling
* Interactive report design
* Executive-level dashboard layout

---

## Project Outcome

This dashboard provides a clean and professional supply chain performance analysis that can help business users monitor financial performance, identify delivery issues, and evaluate market and product performance.

The project demonstrates the ability to build a practical Power BI dashboard from raw data and convert it into useful business insights.
