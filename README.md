# 📊 Supply Chain Control Tower Dashboard – Power BI

## 📌 Project Overview

This project presents an end-to-end **Supply Chain Performance Intelligence Dashboard** built in Power BI.

It integrates procurement, production, inventory, shipment, and sales data into a unified **star schema semantic model** (5 fact tables + 5 dimension tables) to enable cross-functional decision-making.

The dashboard functions as a centralized Supply Chain Control Tower for monitoring operational efficiency, cost optimization, and revenue performance.

---

## 🎯 Business Objectives

The dashboard answers critical operational and financial questions:

* Is revenue growing MoM and YoY?
* Are margins being eroded by discounts or supply chain costs?
* Which products and customers drive profitability?
* Are suppliers meeting lead time expectations?
* Is inventory optimized or at risk of over/understock?
* Are shipments delivered on time?
* What is the overall supply chain cost ratio?

Detailed breakdown available in:
➡ `Business_Questions.md`

---

## 🏗 Data Model Architecture

**Star Schema Design**

**Fact Tables**

* fact_sales
* fact_procurement
* fact_production
* fact_inventory
* fact_shipment

**Dimension Tables**

* dim_customer
* dim_product
* dim_supplier
* dim_facility
* dim_date

All fact tables connect through a centralized `dim_date` table to enable advanced time intelligence (MoM, YoY, R12M, etc.).

Model documentation available in:
➡ `Data_Model.md`

---

## 📈 Key KPIs Implemented

### Financial & Sales

* Total Revenue
* Profit Margin %
* Discount Rate %
* Revenue Growth MoM / YoY
* Revenue R3M / R12M
* Top 3 Customer Revenue %

### Production

* Total Units Produced
* Quality Yield %
* Production Efficiency
* OEE %
* Facility Utilization Score

### Procurement

* Average Lead Time
* Procurement Cost Growth MoM
* Average Unit Cost
* On-Time Procurement Rate %

### Inventory

* Inventory Turnover Ratio
* Days of Inventory
* Stock Coverage Days
* Overstock / Understock Count
* Inventory Accuracy %

### Logistics

* On-Time Delivery %
* Shipment Volume Growth MoM
* Average Transit Time
* Perfect Order Rate %
* Supply Chain Cost Ratio %

---

## 🧠 Advanced DAX Features

This model contains **81 DAX measures**, including:

* Base aggregations
* Time intelligence (MTD, QTD, YTD, YoY, Rolling 12M)
* Ranking logic (RANKX)
* Top-N contribution analysis
* Supply chain composite metrics
* Custom SVG rank badge for product performance visualization
* Multi-domain KPI calculations

Full measure documentation:
➡ `DAX_Notes.md`

---

## 📊 Dashboard Pages

The report is structured across multiple analytical domains:

1. Executive Overview
2. Sales & Customer Analytics
3. Production Performance
4. Procurement & Supplier Efficiency
5. Inventory Optimization
6. Shipment & Logistics Monitoring

Each page focuses on actionable metrics rather than descriptive reporting.

---

## 🛠 Tools & Techniques Used

* Power BI Desktop
* DAX (81 Measures)
* Star Schema Data Modeling
* Time Intelligence Functions
* Advanced Filter Context Manipulation
* SVG-based dynamic KPI indicators
* Cross-functional KPI design

---

## 📁 Repository Structure

```
Supply-Chain-Control-Tower/
│
├── README.md
├── DAX_Notes.md
├── Business_Questions.md
├── Data_Model.md
├── Screenshots/
├── Data/
```

---

## 🚀 Project Positioning

This project demonstrates:

* Multi-fact modeling capability
* Advanced DAX proficiency
* Cross-functional supply chain analytics
* KPI framework design
* Executive dashboard structuring
* Business-to-technical translation skills

It is designed to showcase expertise in:

* Power BI Report Development
* Data Modeling & Semantic Layer Design
* Business Intelligence Strategy
* End-to-End Operational Analytics

---
