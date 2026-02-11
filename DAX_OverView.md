### Supply Chain Control Tower – Measure Documentation

This document outlines all DAX measures used in the Supply Chain Analytics Power BI model.
Measures are grouped by domain and categorized into:

* Base Measures (Raw Aggregations)
* Derived KPIs
* Time Intelligence
* Ranking & Advanced Logic
* Operational Efficiency Metrics

---

# 1️⃣ Core Financial Measures

## Base Revenue & Cost Measures

```DAX
iTotal Revenue = SUM('fact_sales'[revenue])
Total Profit = SUM('fact_sales'[profit])
Total Cost = SUM('fact_sales'[cost])
Total Discount Amount = SUM('fact_sales'[discount_amount])
Total Procurement Cost = SUM('fact_procurement'[total_cost])
Total Shipping Cost = SUM('fact_shipment'[shipping_cost])
```

---

## Margin & Contribution

```DAX
Profit Margin % =
DIVIDE([Total Profit], [iTotal Revenue])

Discount Rate % =
DIVIDE([Total Discount Amount], [iTotal Revenue] + [Total Discount Amount])

Product Contribution % =
DIVIDE(
    [iTotal Revenue],
    CALCULATE([iTotal Revenue], ALL('dim_product')),
    0
) * 100
```

---

# 2️⃣ Sales & Customer Analytics

```DAX
Number of Transactions = DISTINCTCOUNT('fact_sales'[sales_id])
Number of Active Customers = DISTINCTCOUNT('fact_sales'[customer_id])

Average Customer Order Value =
DIVIDE([iTotal Revenue], [Number of Transactions], 0)

Revenue Per Customer =
DIVIDE([iTotal Revenue], DISTINCTCOUNT('fact_sales'[customer_id]), 0)

Units Sold Per Product =
DIVIDE([Total Quantity Sold], DISTINCTCOUNT('fact_sales'[product_id]), 0)
```

---

## Customer Concentration

```DAX
Top 3 Customer Revenue % =
VAR Top3Revenue =
    CALCULATE(
        [iTotal Revenue],
        TOPN(3, ALL('dim_customer'), [iTotal Revenue], DESC)
    )
VAR TotalRevenue = CALCULATE([iTotal Revenue], ALL('dim_customer'))
RETURN DIVIDE(Top3Revenue, TotalRevenue, 0) * 100
```

---

# 3️⃣ Production & Manufacturing KPIs

```DAX
Total Units Produced = SUM('fact_production'[quantity_produced])
Total Defective Units = SUM('fact_production'[defective_units])

Quality Yield % =
(1 - DIVIDE([Total Defective Units], [Total Units Produced], 0)) * 100

Production Efficiency =
VAR GoodUnits = [Total Units Produced] - [Total Defective Units]
RETURN DIVIDE(GoodUnits, [Total Units Produced], 0) * 100

Average Batch Size =
DIVIDE([Total Units Produced], [Number of Production Batches], 0)
```

---

## OEE & Facility Metrics

```DAX
OEE % = [Quality Yield %] * 0.85 * 0.90

Facility Utilization Score =
([Total Units Produced] / 1000000) * [Quality Yield %]
```

---

# 4️⃣ Procurement & Supplier Analytics

```DAX
Average Lead Time Days =
AVERAGE('fact_procurement'[lead_time_days])

Average Order Value =
DIVIDE([Total Procurement Cost], [Number of Orders], 0)

Average Unit Cost =
DIVIDE([Total Procurement Cost], [Total Order Quantity], 0)

On-Time Delivery Rate % =
VAR OnTimeOrders =
    CALCULATE(
        [Number of Orders],
        'fact_procurement'[lead_time_days] <= 30
    )
RETURN DIVIDE(OnTimeOrders, [Number of Orders], 0)
```

---

# 5️⃣ Inventory Optimization Metrics

```DAX
Current Stock Level = SUM('fact_inventory'[stock_level])

Inventory Turnover Ratio =
DIVIDE([Total Quantity Sold], [Current Stock Level], 0)

Days of Inventory =
DIVIDE(365, [Inventory Turnover Ratio], 0)

Stock Coverage Days =
VAR DailySales = DIVIDE([Total Quantity Sold], 365, 0)
RETURN DIVIDE([Current Stock Level], DailySales, 0)
```

---

## Stock Health

```DAX
Overstock Items Count =
COUNTROWS(
    FILTER(
        'fact_inventory',
        'fact_inventory'[stock_level] > 'fact_inventory'[reorder_point] * 2
    )
)

Understock Items Count =
COUNTROWS(
    FILTER(
        'fact_inventory',
        'fact_inventory'[stock_level] < 'fact_inventory'[safety_stock_level]
    )
)
```

---

# 6️⃣ Shipment & Logistics Performance

```DAX
Total Shipments = DISTINCTCOUNT('fact_shipment'[shipment_id])
Total Quantity Shipped = SUM('fact_shipment'[quantity])

On-Time Delivery % =
VAR OnTimeShipments = [Delivered_Shipment]
RETURN DIVIDE(OnTimeShipments, [Total Shipments], 0)

Average Transit Time Days =
AVERAGEX(
    'fact_shipment',
    'fact_shipment'[delivery_date_key] - 'fact_shipment'[ship_date_key]
)

Cost Per Unit Shipped =
DIVIDE([Total Shipping Cost], [Total Quantity Shipped], 0)
```

---

# 7️⃣ Time Intelligence Measures

```DAX
Revenue YTD = TOTALYTD([iTotal Revenue], 'dim_date'[date])
Revenue QTD = TOTALQTD([iTotal Revenue], 'dim_date'[date])
Revenue MTD = TOTALMTD([iTotal Revenue], 'dim_date'[date])

Revenue Growth MoM =
VAR CurrentRevenue = [iTotal Revenue]
VAR PreviousRevenue =
    CALCULATE(
        [iTotal Revenue],
        DATEADD('dim_date'[date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue, 0) * 100
```

Includes:

* Revenue YoY
* Rolling 3M
* Rolling 12M
* Procurement Growth MoM
* Production Growth MoM
* Shipment Volume Growth MoM

---

# 8️⃣ Ranking & Visual Enhancement

```DAX
Product Sales Rank =
RANKX(ALL('dim_product'), [iTotal Revenue], , DESC, DENSE)
```

Custom SVG Rank Badge implemented for dynamic medal styling.

---

# 9️⃣ Composite KPIs

```DAX
Supply Chain Cost Ratio % =
DIVIDE(
    [Total Procurement Cost] + [Total Shipping Cost],
    [iTotal Revenue],
    0
) * 100

Cash-to-Cash Cycle Days =
[Days of Inventory] + [Average Lead Time Days] - 30
```

---

This model contains:

* 81 total measures
* 30+ base aggregations
* 25+ derived KPIs
* 10+ time intelligence calculations
* Advanced ranking & SVG logic
* Multi-domain performance scoring

---
