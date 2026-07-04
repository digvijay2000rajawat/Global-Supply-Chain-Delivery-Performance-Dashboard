# Global Supply Chain & Delivery Performance Dashboard

## Project Documentation

## 1. Project Title

**Global Supply Chain & Delivery Performance Dashboard**

---

## 2. Project Objective

The objective of this project is to analyse global supply chain performance using Power BI.

The dashboard helps business users understand sales performance, profitability, order volume, product performance, market performance, and delivery efficiency.

The main business problem identified in the dataset is that the business has strong revenue and profit, but delivery delays are a major operational concern.

---

## 3. Business Questions

This project answers the following business questions:

1. What is the total revenue, profit, and order volume?
2. What percentage of orders are delivered late?
3. Which shipping modes have the highest late delivery rate?
4. Which markets have the highest delivery risk?
5. Which product categories generate the most revenue?
6. Which products are the top revenue contributors?
7. Are high-revenue markets also performing well in terms of delivery?
8. How does delivery performance change over time?

---

## 4. Dataset Overview

The dataset contains supply chain order data including customer, product, sales, profit, shipping, delivery, and geographic information.

The dataset is at **order-item level**. This means each row represents one product line inside an order.

Because one order can contain multiple products, order-level metrics were calculated using distinct count of Order ID.

Example:

```DAX
Total Orders =
DISTINCTCOUNT(FactOrderItems[Order Id])
```

This prevents double-counting orders.

---

## 5. Data Cleaning in Power Query

The following data cleaning steps were performed in Power Query:

### Removed unnecessary columns

Columns with personal, empty, duplicate, or low-value information were removed.

Examples:

* Customer Email
* Customer Password
* Customer Name fields
* Customer Street
* Product Description
* Product Image
* Product Status
* Duplicate sales and product ID fields

### Renamed columns

Several columns were renamed to make them easier to understand.

Examples:

* `Sales` → `Gross Sales`
* `Order Item Total` → `Net Sales`
* `Order Profit Per Order` → `Profit`
* `Days for shipping (real)` → `Actual Shipping Days`
* `Days for shipment (scheduled)` → `Scheduled Shipping Days`
* `Late_delivery_risk` → `Late Delivery Risk`

### Changed data types

Correct data types were applied:

* Dates as Date
* Financial columns as Fixed Decimal Number
* IDs as Whole Number
* Percentage columns as Decimal Number
* Text columns as Text
* Latitude and Longitude as Decimal Number

### Cleaned text values

Text columns were trimmed and cleaned to remove unnecessary spaces and hidden characters.

Order status and delivery status values were standardised for better readability.

### Created calculated column

A new Power Query column was created:

```powerquery
Shipping Delay Days = [Actual Shipping Days] - [Scheduled Shipping Days]
```

This column helps compare actual shipping time against scheduled shipping time.

---

## 6. Data Model

A star schema was created to keep the model clean and beginner-friendly.

### Fact Table

**FactOrderItems**

This table contains transaction-level numerical values such as:

* Gross Sales
* Net Sales
* Discount Amount
* Profit
* Quantity
* Product Price

### Dimension Tables

**DimDate**

Used for time-based analysis.

**DimOrder**

Stores order-level and delivery-related fields such as:

* Order Date
* Shipping Date
* Delivery Status
* Shipping Mode
* Order Status
* Late Delivery Risk
* Shipping Delay Days

**DimProduct**

Stores product-related information such as:

* Product Name
* Category Name
* Department Name
* Product Price

**DimCustomer**

Stores customer segment and customer location fields.

**DimOrderDestination**

Stores delivery destination geography such as:

* Market
* Region
* Country
* State
* City

---

## 7. Relationships

The model uses one-to-many relationships from dimensions to the fact table.

Main relationships:

* `DimProduct[Product Id]` → `FactOrderItems[Product Id]`
* `DimCustomer[Customer Id]` → `FactOrderItems[Customer Id]`
* `DimOrderDestination[Destination Key]` → `FactOrderItems[Destination Key]`
* `DimOrder[Order Id]` → `FactOrderItems[Order Id]`
* `DimDate[Date]` → `DimOrder[Order Date]`

All relationships use single-direction filtering to keep the model simple and reliable.

---

## 8. DAX Measures

The dashboard uses essential DAX measures only.

### Sales and Profit Measures

```DAX
Total Revenue =
SUM(FactOrderItems[Net Sales])
```

```DAX
Gross Sales =
SUM(FactOrderItems[Gross Sales])
```

```DAX
Total Discount =
SUM(FactOrderItems[Discount Amount])
```

```DAX
Total Profit =
SUM(FactOrderItems[Profit])
```

```DAX
Profit Margin % =
DIVIDE(
    [Total Profit],
    [Total Revenue]
)
```

```DAX
Total Quantity =
SUM(FactOrderItems[Quantity])
```

```DAX
Average Order Value =
DIVIDE(
    [Total Revenue],
    [Total Orders]
)
```

### Order and Delivery Measures

```DAX
Total Orders =
DISTINCTCOUNT(FactOrderItems[Order Id])
```

```DAX
Late Orders =
CALCULATE(
    DISTINCTCOUNT(FactOrderItems[Order Id]),
    DimOrder[Late Delivery Risk] = 1
)
```

```DAX
On-Time Orders =
CALCULATE(
    DISTINCTCOUNT(FactOrderItems[Order Id]),
    DimOrder[Late Delivery Risk] = 0
)
```

```DAX
Late Order Rate % =
DIVIDE(
    [Late Orders],
    [Total Orders]
)
```

```DAX
On-Time Order Rate % =
DIVIDE(
    [On-Time Orders],
    [Total Orders]
)
```

```DAX
Average Shipping Delay Days =
AVERAGE(FactOrderItems[Shipping Delay Days])
```

```DAX
Cancelled Orders =
CALCULATE(
    DISTINCTCOUNT(FactOrderItems[Order Id]),
    DimOrder[Delivery Status] = "Cancelled"
)
```

---

## 9. Dashboard Pages

### Page 1: Executive Overview

This page provides a high-level summary of overall business performance.

Main visuals:

* KPI cards for revenue, profit, orders, late order rate, and average order value
* Monthly revenue trend
* Orders by delivery status
* Revenue and profit by market
* Late order rate by market

Business purpose:

This page helps executives quickly understand overall financial performance and delivery risk.

---

### Page 2: Delivery Performance Analysis

This page focuses on late deliveries and shipping performance.

Main visuals:

* Late orders KPI
* Late order rate KPI
* On-time order rate KPI
* Average shipping delay days
* Cancelled orders
* Late order rate by shipping mode
* Average shipping delay by shipping mode
* Late Order Rate Trend
* Delivery status by shipping mode

Business purpose:

This page helps identify whether delivery issues are caused by shipping mode, market, time period, or broader operational problems.

---

### Page 3: Market & Product Performance

This page connects revenue, profitability, product performance, and delivery risk.

Main visuals:

* Revenue by product category
* Profit margin by category
* Top 10 products by revenue
* Market performance summary table

Business purpose:

This page helps business users understand which markets and products drive performance, while also checking whether high revenue is supported by healthy profit and delivery performance.

---

## 10. Interactivity

The report includes simple interactive features:

* Slicers for Year, Market, Shipping Mode, and Customer Segment
* Synced slicers across pages
* Tooltip fields for additional context

These features improve usability without making the project too advanced.

---

## 11. Key Insights

1. The business generates strong global revenue and profit.
2. Delivery performance is a major concern because many orders are late.
3. Shipping mode should be investigated as a possible cause of late deliveries.
4. Market-level analysis helps identify regions with higher delivery risk.
5. Product and category performance should be evaluated using revenue, profit margin, and delivery performance together.
6. High revenue does not always mean strong business performance if late delivery rate is also high.

---

## 12. Skills Demonstrated

This project demonstrates the following skills:

* Power Query data cleaning
* Data type correction
* Column renaming and transformation
* Star schema modelling
* Fact and dimension table design
* DAX measure creation
* KPI design
* Business analysis
* Supply chain performance analysis
* Dashboard storytelling
* Interactive report design
* Professional Power BI layout design

---

## 13. Final Outcome

The final dashboard provides a clean and professional Power BI report for analysing global supply chain and delivery performance.

It is suitable for a data analyst or Power BI portfolio because it demonstrates data cleaning, modelling, DAX, visualization, business thinking, and storytelling using a real-world style dataset.