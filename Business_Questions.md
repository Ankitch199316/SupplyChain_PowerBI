# 📄 Business_Questions.md

## Supply Chain Control Tower – Business Questions & How They Are Answered

This document outlines all business questions addressed in the dashboard and the DAX logic used to answer them.

---

# 1️⃣ Executive & Financial Strategy

### Q1: What is total revenue and profit?

**Measures Used:**

* `iTotal Revenue`
* `Total Profit`
* `Profit Margin %`

---

### Q2: Is revenue growing month-over-month or year-over-year?

**Measures Used:**

* `Revenue Growth MoM`
* `Revenue Growth YoY`
* `Revenue PM`
* `Revenue PY`

---

### Q3: What are the cumulative trends (MTD, QTD, YTD)?

**Measures Used:**

* `Revenue MTD`
* `Revenue QTD`
* `Revenue YTD`

---

### Q4: What is the rolling revenue trend?

**Measures Used:**

* `Revenue R3M`
* `Revenue R12M`

---

### Q5: Are supply chain costs impacting profitability?

**Measures Used:**

* `Total Procurement Cost`
* `Total Shipping Cost`
* `Supply Chain Cost Ratio %`

---

### Q6: Are discounts eroding margins?

**Measures Used:**

* `Total Discount Amount`
* `Discount Rate %`

---

# 2️⃣ Customer & Revenue Concentration

### Q7: Who are the top customers?

**Measures Used:**

* `Top Customer Name`
* `Top 3 Customer Revenue %`
* `Revenue Per Customer`
* `Number of Active Customers`

---

### Q8: Are we overly dependent on few customers?

**Measures Used:**

* `Top 3 Customer Revenue %`

---

### Q9: What is average order value?

**Measures Used:**

* `Average Customer Order Value`
* `Number of Transactions`

---

# 3️⃣ Product Performance

### Q10: Which products generate highest revenue?

**Measures Used:**

* `Product Sales Rank`
* `Rank_Badge`
* `Top Product Name`
* `Product Contribution %`

---

### Q11: What is average product price?

**Measures Used:**

* `Average Product Price`
* `Average Unit Price`

---

### Q12: How many products are active?

**Measures Used:**

* `Number of Products`

---

### Q13: How many units are sold per product?

**Measures Used:**

* `Units Sold Per Product`
* `Total Quantity Sold`

---

# 4️⃣ Production & Manufacturing

### Q14: What is total production volume?

**Measures Used:**

* `Total Units Produced`
* `Formatted_Total Units Produced`

---

### Q15: What is defect rate and quality yield?

**Measures Used:**

* `Total Defective Units`
* `Average Defect Rate %`
* `Quality Yield %`
* `Production Efficiency`

---

### Q16: What is OEE (Overall Equipment Effectiveness)?

**Measures Used:**

* `OEE %`

---

### Q17: What is production per facility?

**Measures Used:**

* `Production Per Facility`
* `Top Facility Name`
* `Number of Active Facilities`

---

### Q18: Is production growing month-over-month?

**Measures Used:**

* `Production Growth MoM`

---

### Q19: What is average batch size?

**Measures Used:**

* `Average Batch Size`
* `Number of Production Batches`

---

# 5️⃣ Procurement & Supplier Performance

### Q20: What is total procurement spend?

**Measures Used:**

* `Total Procurement Cost`

---

### Q21: Is procurement cost increasing MoM?

**Measures Used:**

* `Procurement Cost Growth MoM`

---

### Q22: What is average supplier lead time?

**Measures Used:**

* `Average Lead Time Days`

---

### Q23: What is average unit procurement cost?

**Measures Used:**

* `Average Unit Cost`
* `Total Order Quantity`

---

### Q24: What is average order value?

**Measures Used:**

* `Average Order Value`
* `Number of Orders`

---

### Q25: Are suppliers delivering within expected timelines?

**Measures Used:**

* `On-Time Delivery Rate %`
* `Number of Active Suppliers`

---

# 6️⃣ Inventory Optimization

### Q26: What is current stock level?

**Measures Used:**

* `Current Stock Level`

---

### Q27: What is inventory turnover?

**Measures Used:**

* `Inventory Turnover Ratio`

---

### Q28: How many days of inventory do we hold?

**Measures Used:**

* `Days of Inventory`
* `Stock Coverage Days`

---

### Q29: What is inventory value?

**Measures Used:**

* `Inventory Value`

---

### Q30: Are we overstocked?

**Measures Used:**

* `Overstock Items Count`

---

### Q31: Are we understocked?

**Measures Used:**

* `Understock Items Count`

---

### Q32: Is inventory within safety and reorder thresholds?

**Measures Used:**

* `Inventory Accuracy %`
* `Total Reorder Point`
* `Total Safety Stock`

---

# 7️⃣ Shipment & Logistics

### Q33: How many shipments are delivered, delayed, or in transit?

**Measures Used:**

* `Total Shipments`
* `Delivered_Shipment`
* `Delayed Shipments`
* `In Transit Shipments`

---

### Q34: What is total shipment volume?

**Measures Used:**

* `Total Quantity Shipped`
* `Delivered_Shipment_Quantity`

---

### Q35: What is on-time delivery rate?

**Measures Used:**

* `On-Time Delivery %`

---

### Q36: What is average transit time?

**Measures Used:**

* `Average Transit Time Days`

---

### Q37: What is shipping cost per unit?

**Measures Used:**

* `Cost Per Unit Shipped`
* `Average Shipping Cost`

---

### Q38: Is shipment volume growing MoM?

**Measures Used:**

* `Shipment Volume Growth MoM`

---

### Q39: What is delivery performance score?

**Measures Used:**

* `Delivery Performance Score`

---

### Q40: What is perfect order rate?

**Measures Used:**

* `Perfect Order Rate %`

---

# 8️⃣ Cross-Functional Supply Chain Metrics

### Q41: What is the order fulfillment cycle?

**Measures Used:**

* `Order Fulfillment Cycle Days`
* `Average Lead Time Days`
* `Average Transit Time Days`

---

### Q42: What is cash-to-cash cycle duration?

**Measures Used:**

* `Cash-to-Cash Cycle Days`

---

---

# 📌 Summary

This dashboard answers:

* 40+ strategic and operational business questions
* Across Finance, Sales, Production, Procurement, Inventory, and Logistics
* Using 81 DAX measures
* With advanced time intelligence and ranking logic

It is designed as a **Supply Chain Performance Intelligence System**, not a static dashboard.

---

