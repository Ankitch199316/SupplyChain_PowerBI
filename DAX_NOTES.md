# DAX Notes — Supply Chain Control Tower (81 Measures)

This file documents all measures used in the Power BI model, grouped by domain.

---

## Sales / Revenue

iTotal Revenue =
SUM('fact_sales'[revenue])

Total Cost =
SUM('fact_sales'[cost])

Total Profit =
SUM('fact_sales'[profit])

Total Discount Amount =
SUM('fact_sales'[discount_amount])

Total Quantity Sold =
SUM('fact_sales'[quantity_sold])

Average Unit Price =
AVERAGE('fact_sales'[unit_price])

Number of Transactions =
DISTINCTCOUNT('fact_sales'[sales_id])

Number of Active Customers =
DISTINCTCOUNT('fact_sales'[customer_id])

Average Customer Order Value =
DIVIDE([iTotal Revenue], [Number of Transactions], 0)

Revenue Per Customer =
DIVIDE([iTotal Revenue], DISTINCTCOUNT('fact_sales'[customer_id]), 0)

Revenue Per Product =
DIVIDE([iTotal Revenue], DISTINCTCOUNT('fact_sales'[product_id]), 0)

Units Sold Per Product =
DIVIDE([Total Quantity Sold], DISTINCTCOUNT('fact_sales'[product_id]), 0)

Profit Margin % =
DIVIDE([Total Profit], [iTotal Revenue])

Discount Rate % =
DIVIDE([Total Discount Amount], [iTotal Revenue] + [Total Discount Amount])

Top 3 Customer Revenue % =
VAR Top3Revenue =
    CALCULATE(
        [iTotal Revenue],
        TOPN(3, ALL('dim_customer'), [iTotal Revenue], DESC)
    )
VAR TotalRevenue = CALCULATE([iTotal Revenue], ALL('dim_customer'))
RETURN DIVIDE(Top3Revenue, TotalRevenue, 0) * 100

Top Customer Name =
CALCULATE(
    SELECTEDVALUE('dim_customer'[customer_name]),
    TOPN(1, ALL('dim_customer'), [iTotal Revenue], DESC)
)

Top Product Name =
CALCULATE(
    SELECTEDVALUE('dim_product'[product_name]),
    TOPN(1, ALL('dim_product'), [iTotal Revenue], DESC)
)

Product Contribution % =
DIVIDE(
    [iTotal Revenue],
    CALCULATE([iTotal Revenue], ALL('dim_product')),
    0
) * 100

Product Sales Rank =
RANKX(ALL('dim_product'), [iTotal Revenue], , DESC, DENSE)

Rank_Badge =
VAR r = [Product Sales Rank]

VAR bg =
    SWITCH(
        TRUE(),
        r = 1, "%23FFD700",   -- Gold
        r = 2, "%23C0C0C0",   -- Silver
        r = 3, "%23CD7F32",   -- Bronze
        "%23F2F4F7"           -- Default light gray
    )

VAR txt =
    SWITCH(
        TRUE(),
        r IN {1,2,3}, "%23000000",  -- black text for top ranks
        "%23111A2C"                -- dark text
    )

VAR border =
    SWITCH(
        TRUE(),
        r IN {1,2,3}, bg,
        bg
    )

RETURN
IF(
    ISBLANK(r),
    BLANK(),
    "data:image/svg+xml;utf8," &
    "<svg xmlns='http://www.w3.org/2000/svg' width='30' height='50' viewBox='0 0 42 28'>
        <rect x='1' y='1' rx='8' ry='8' width='40' height='30'
              fill='" & bg & "' stroke='" & border & "' stroke-width='1.5'/>
        <text x='21' y='19' text-anchor='middle'
              font-family='Segoe UI' font-size='14' font-weight='700'
              fill='" & txt & "'>" & r & "</text>
    </svg>"
)

---

## Time Intelligence — Revenue

Revenue YTD =
TOTALYTD([iTotal Revenue], 'dim_date'[date])

Revenue QTD =
TOTALQTD([iTotal Revenue], 'dim_date'[date])

Revenue MTD =
TOTALMTD([iTotal Revenue], 'dim_date'[date])

Revenue PM =
CALCULATE([iTotal Revenue], DATEADD('dim_date'[date], -1, MONTH))

Revenue PY =
CALCULATE([iTotal Revenue], SAMEPERIODLASTYEAR('dim_date'[date]))

Revenue R3M =
CALCULATE(
    [iTotal Revenue],
    DATESINPERIOD('dim_date'[date], LASTDATE('dim_date'[date]), -3, MONTH)
)

Revenue R12M =
CALCULATE(
    [iTotal Revenue],
    DATESINPERIOD('dim_date'[date], LASTDATE('dim_date'[date]), -12, MONTH)
)

Revenue Growth MoM =
VAR CurrentRevenue = [iTotal Revenue]
VAR PreviousRevenue =
    CALCULATE(
        [iTotal Revenue],
        DATEADD('dim_date'[date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue, 0) * 100

Revenue Growth YoY =
VAR CurrentRevenue = [iTotal Revenue]
VAR PreviousRevenue =
    CALCULATE(
        [iTotal Revenue],
        SAMEPERIODLASTYEAR('dim_date'[date])
    )
RETURN
    DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue, 0) * 100

---

## Products / Master Data

Number of Products =
DISTINCTCOUNT('dim_product'[product_id])

Average Product Price =
AVERAGE('dim_product'[unit_price])

---

## Procurement / Suppliers

Total Procurement Cost =
SUM('fact_procurement'[total_cost])

Total Order Quantity =
SUM('fact_procurement'[order_quantity])

Number of Orders =
DISTINCTCOUNT('fact_procurement'[procurement_id])

Number of Active Suppliers =
DISTINCTCOUNT('fact_procurement'[supplier_id])

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

Procurement Cost Growth MoM =
VAR CurrentCost = [Total Procurement Cost]
VAR PreviousCost =
    CALCULATE(
        [Total Procurement Cost],
        DATEADD('dim_date'[date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentCost - PreviousCost, PreviousCost)

---

## Production / Facilities

Total Units Produced =
SUM('fact_production'[quantity_produced])

Total Defective Units =
SUM('fact_production'[defective_units])

Number of Production Batches =
DISTINCTCOUNT('fact_production'[production_id])

Number of Active Facilities =
DISTINCTCOUNT('fact_production'[facility_id])

Average Batch Size =
DIVIDE([Total Units Produced], [Number of Production Batches], 0)

Average Defect Rate % =
DIVIDE([Total Defective Units], [Total Units Produced])

Quality Yield % =
(1 - DIVIDE([Total Defective Units], [Total Units Produced], 0)) * 100

Production Efficiency =
VAR GoodUnits = [Total Units Produced] - [Total Defective Units]
RETURN DIVIDE(GoodUnits, [Total Units Produced], 0) * 100

Production Per Facility =
DIVIDE([Total Units Produced], DISTINCTCOUNT('fact_production'[facility_id]), 0)

OEE % =
[Quality Yield %] * 0.85 * 0.90

Facility Utilization Score =
([Total Units Produced] / 1000000) * [Quality Yield %]

Production Growth MoM =
VAR CurrentProduction = [Total Units Produced]
VAR PreviousProduction =
    CALCULATE(
        [Total Units Produced],
        DATEADD('dim_date'[date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentProduction - PreviousProduction, PreviousProduction)

Top Facility Name =
CALCULATE(
    SELECTEDVALUE('dim_facility'[facility_name]),
    TOPN(1, ALL('dim_facility'), [Total Units Produced], DESC)
)

Formatted_Total Units Produced =
VAR val = SUM('fact_production'[quantity_produced])
RETURN
SWITCH(
    TRUE(),
    val >= 1000000000, FORMAT(val / 1000000000, "0.0") & "B",
    val >= 1000000,    FORMAT(val / 1000000,    "0.0") & "M",
    val >= 1000,       FORMAT(val / 1000,       "0.0") & "K",
    FORMAT(val, "#,0")
)

---

## Inventory

Current Stock Level =
SUM('fact_inventory'[stock_level])

Total Reorder Point =
SUM('fact_inventory'[reorder_point])

Total Safety Stock =
SUM('fact_inventory'[safety_stock_level])

Inventory Turnover Ratio =
DIVIDE([Total Quantity Sold], [Current Stock Level], 0)

Days of Inventory =
DIVIDE(365, [Inventory Turnover Ratio], 0)

Stock Coverage Days =
VAR DailySales = DIVIDE([Total Quantity Sold], 365, 0)
RETURN DIVIDE([Current Stock Level], DailySales, 0)

Inventory Value =
SUMX(
    'fact_inventory',
    'fact_inventory'[stock_level] *
    RELATED('dim_product'[unit_price]) * 0.75
)

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

Inventory Accuracy % =
VAR StockWithinRange =
    COUNTROWS(
        FILTER(
            'fact_inventory',
            'fact_inventory'[stock_level] >= 'fact_inventory'[safety_stock_level] &&
            'fact_inventory'[stock_level] <= 'fact_inventory'[reorder_point] * 1.5
        )
    )
VAR TotalRecords = COUNTROWS('fact_inventory')
RETURN DIVIDE(StockWithinRange, TotalRecords, 0) * 100

---

## Shipment / Logistics

Total Shipments =
DISTINCTCOUNT('fact_shipment'[shipment_id])

Total Quantity Shipped =
SUM('fact_shipment'[quantity])

Total Shipping Cost =
SUM('fact_shipment'[shipping_cost])

Average Shipping Cost =
DIVIDE([Total Shipping Cost], [Total Shipments], 0)

Cost Per Unit Shipped =
DIVIDE([Total Shipping Cost], [Total Quantity Shipped], 0)

Delivered_Shipment =
CALCULATE(
    [Total Shipments],
    'fact_shipment'[status] = "Delivered"
)

Delivered_Shipment_Quantity =
CALCULATE(
    [Total Quantity Shipped],
    'fact_shipment'[status] = "Delivered"
)

Delayed Shipments =
CALCULATE(
    [Total Shipments],
    'fact_shipment'[status] = "Delayed"
)

In Transit Shipments =
CALCULATE(
    [Total Shipments],
    'fact_shipment'[status] = "In Transit"
)

On-Time Delivery % =
VAR OnTimeShipments =
    [Delivered_Shipment]
RETURN DIVIDE(OnTimeShipments, [Total Shipments], 0)

Average Transit Time Days =
AVERAGEX(
    'fact_shipment',
    'fact_shipment'[delivery_date_key] - 'fact_shipment'[ship_date_key]
)

Shipment Volume Growth MoM =
VAR CurrentVolume = [Total Quantity Shipped]
VAR PreviousVolume =
    CALCULATE(
        [Total Quantity Shipped],
        DATEADD('dim_date'[date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentVolume - PreviousVolume, PreviousVolume, 0) * 100

Delivery Performance Score =
([On-Time Delivery %] + (100 - ([Average Transit Time Days] / 30 * 100))) / 2

Perfect Order Rate % =
VAR PerfectOrders =
    CALCULATE(
        [Total Shipments],
        'fact_shipment'[status] = "Delivered",
        'fact_production'[defect_rate_pct] < 1
    )
RETURN DIVIDE(PerfectOrders, [Total Shipments], 0) * 100

---

## Cross-Domain / Supply Chain Metrics

Average Unit Cost =
DIVIDE([Total Procurement Cost], [Total Order Quantity], 0)

Order Fulfillment Cycle Days =
[Average Lead Time Days] + [Average Transit Time Days]

Cash-to-Cash Cycle Days =
[Days of Inventory] + [Average Lead Time Days] - 30

Supply Chain Cost Ratio % =
DIVIDE(
    [Total Procurement Cost] + [Total Shipping Cost],
    [iTotal Revenue],
    0
) * 100
