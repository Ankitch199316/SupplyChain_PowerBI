# 📄 Data_Model.md

## Supply Chain Control Tower – Data Model Architecture

---

# 1️⃣ Model Overview

This Power BI report is built using a **multi-fact star schema model** designed to integrate end-to-end supply chain operations across:

* Sales
* Procurement
* Production
* Inventory
* Shipment

The model contains:

* **5 Fact Tables**
* **5 Dimension Tables**
* **81 DAX Measures**
* Centralized Time Intelligence via `dim_date`

The design enables cross-functional analytics across financial, operational, and logistics domains.

---

# 2️⃣ Fact Tables (Transactional Layer)

These tables contain quantitative business events.

---

## 🟦 fact_sales

Captures all sales transactions.

**Key Columns**

* sales_id
* customer_id
* product_id
* date_key
* revenue
* cost
* profit
* quantity_sold
* discount_amount
* unit_price

**Purpose**
Drives revenue, profitability, customer, and product performance analytics.

---

## 🟦 fact_procurement

Captures supplier purchase orders.

**Key Columns**

* procurement_id
* supplier_id
* product_id
* date_key
* order_quantity
* total_cost
* lead_time_days

**Purpose**
Enables procurement cost analysis and supplier performance tracking.

---

## 🟦 fact_production

Captures manufacturing output.

**Key Columns**

* production_id
* facility_id
* product_id
* date_key
* quantity_produced
* defective_units

**Purpose**
Drives production volume, defect rate, and quality yield metrics.

---

## 🟦 fact_inventory

Captures stock levels and reorder thresholds.

**Key Columns**

* product_id
* date_key
* stock_level
* reorder_point
* safety_stock_level

**Purpose**
Supports inventory turnover, stock health, and optimization metrics.

---

## 🟦 fact_shipment

Captures logistics and delivery activity.

**Key Columns**

* shipment_id
* customer_id
* product_id
* date_key
* quantity
* shipping_cost
* ship_date_key
* delivery_date_key
* status (Delivered, Delayed, In Transit)

**Purpose**
Enables delivery performance, transit time, and logistics cost analysis.

---

# 3️⃣ Dimension Tables (Descriptive Layer)

These tables provide filtering, slicing, and grouping capability.

---

## 🟩 dim_customer

* customer_id
* customer_name
* region (if available)

Used for customer segmentation and revenue concentration analysis.

---

## 🟩 dim_product

* product_id
* product_name
* unit_price

Used for product ranking and contribution analysis.

---

## 🟩 dim_supplier

* supplier_id
* supplier_name

Used for procurement efficiency metrics.

---

## 🟩 dim_facility

* facility_id
* facility_name

Used for production performance comparison.

---

## 🟩 dim_date

* date
* year
* quarter
* month
* date_key

Central time intelligence table used across all fact tables.

Enables:

* MoM calculations
* YoY calculations
* Rolling 3M / 12M
* YTD / QTD / MTD

---

# 4️⃣ Relationships

All fact tables connect to their relevant dimension tables via surrogate keys.

### Relationship Structure

* fact_sales → dim_customer

* fact_sales → dim_product

* fact_sales → dim_date

* fact_procurement → dim_supplier

* fact_procurement → dim_product

* fact_procurement → dim_date

* fact_production → dim_facility

* fact_production → dim_product

* fact_production → dim_date

* fact_inventory → dim_product

* fact_inventory → dim_date

* fact_shipment → dim_customer

* fact_shipment → dim_product

* fact_shipment → dim_date

All relationships are:

* One-to-Many (Dimension → Fact)
* Single Direction Filter (Dimension → Fact)
* No bi-directional ambiguity

---

# 5️⃣ Modeling Principles Applied

### ✔ Star Schema Design

Avoided snowflake complexity to maintain clarity and performance.

### ✔ Centralized Time Dimension

Ensures consistent time intelligence across domains.

### ✔ Measure-Based Calculations

All KPIs implemented as DAX measures (no heavy calculated columns).

### ✔ Cross-Fact Intelligence

Enabled multi-domain KPIs such as:

* Supply Chain Cost Ratio
* Cash-to-Cash Cycle
* Order Fulfillment Cycle

### ✔ Avoided Circular Dependencies

Each fact table remains domain-specific and connects only via dimensions.

---

# 6️⃣ Model Complexity Summary

* 10 Tables
* 81 Measures
* 40+ Business Questions Answered
* Multi-domain cross-functional analytics

This design reflects:

* Enterprise-grade BI modeling
* Semantic layer engineering
* Operational intelligence structuring
* Scalable architecture approach

---

# 7️⃣ Model Strengths

✔ Supports financial + operational analytics
✔ Enables cross-functional KPI layering
✔ Designed for scalability
✔ Clean relationship structure
✔ Strong separation of concerns (facts vs dimensions)

---

This is not a flat report model.

It is a **multi-domain supply chain semantic model** built to simulate enterprise BI architecture.

---


