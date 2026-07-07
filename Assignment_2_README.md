# E-Commerce Sales Performance & Target Tracking Dashboard

An interactive Power BI dashboard designed to analyze e-commerce sales, monitor profit margins, track regional performance, and evaluate actual performance against predefined corporate sales targets. 

This repository contains the complete data model, DAX calculations, and reports developed to turn raw transactional logs into actionable executive insights.

---

## 📊 Project Overview & Architecture

This project maps operational sales datasets across three distinct dimensions to uncover product margin trends, geographic performance bottlenecks, and target achievement strategies.

### Datasets Used
* **List of Orders:** Transactional data containing unique Order IDs, Order Dates, Customer Names, and geographic details (City, State).
* **Order Details:** Granular line-item details per order, including Category, Sub-Category, Quantity, Amount, and Profit.
* **Sales Target:** Corporate targets established across operational Categories on a monthly time frame.

### Data Model Structure
* **List of Orders** `(1)` to `(*)` **Order Details** connected via `[Order ID]`
* **Sales Target** `(*)` to `(*)` **Order Details** connected via `[Category]` *(Note: Optimization using a unified Category Dimension table is recommended to eliminate many-to-many complexities).*

---

## ⚡ DAX Implementations

The business logic of this dashboard is powered by custom DAX formulas split between calculated rows for categorical sorting and dynamic measures for evaluation.

### Calculated Columns (Order Details Table)

* **Category Type:** Consolidates product groupings into a single unique label.
    ```dax
    Category Type = 'Order Details'[Category] & " - " & 'Order Details'[Sub-Category]
    ```
* **Revenue per Order:** Evaluates gross revenue per line item before deductions.
    ```dax
    Revenue per Order = 'Order Details'[Amount] * 'Order Details'[Quantity]
    ```
* **Sales Category:** Flags performance tiers by evaluating individual order amounts against the absolute historical average.
    ```dax
    Sales Category = 
    IF(
        'Order Details'[Amount] >= CALCULATE(AVERAGE('Order Details'[Amount]), ALL('Order Details')), 
        "Above Average", 
        "Below Average"
    )
    ```

### Calculated Measures

* **Order Count:** Captures the unique volume of processed transactions.
    ```dax
    Order Count = DISTINCTCOUNT('Order Details'[Order ID])
    ```
* **Average Profit in Delhi:** Filters structural profitability strictly within the Delhi region.
    ```dax
    Average Profit in Delhi = 
    CALCULATE(
        AVERAGE('Order Details'[Profit]), 
        'List of orders'[City] = "Delhi"
    )
    ```
* **Year-to-Date (YTD) Sales:** Dynamically aggregates cumulative sales from the first day of the calendar year relative to the active filter timeline.
    ```dax
    YTD Sales = TOTALYTD(SUM('Order Details'[Amount]), 'List of orders'[Order Date])
    ```

---
