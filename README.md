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
<img width="1007" height="565" alt="Screenshot 2026-02-11 at 10 45 25 AM" src="https://github.com/user-attachments/assets/719bebb0-448b-4f46-a285-de4372a118ed" />

2. Sales
<img width="1012" height="570" alt="Screenshot 2026-02-11 at 10 46 32 AM" src="https://github.com/user-attachments/assets/c03997b6-fd2d-41c4-ba06-75aa9b81e6f5" />

3. Production Performance
<img width="1008" height="567" alt="Screenshot 2026-02-11 at 10 46 00 AM" src="https://github.com/user-attachments/assets/25d804ed-864e-4fdd-9284-75150f74f444" />

4. Procurement & Supplier Efficiency
<img width="1007" height="565" alt="Screenshot 2026-02-11 at 10 45 40 AM" src="https://github.com/user-attachments/assets/f32cdece-5d92-4ed8-9590-3d626d024174" />

5. Inventory Optimization
<img width="1011" height="569" alt="Screenshot 2026-02-11 at 10 46 09 AM" src="https://github.com/user-attachments/assets/9365d4ce-1eee-419f-ae40-7d1d5cb3aa92" />

6. Shipment & Logistics Monitoring
<img width="1005" height="568" alt="Screenshot 2026-02-11 at 10 46 23 AM" src="https://github.com/user-attachments/assets/399f7c19-eb51-426d-8d2f-1a53e9eb3dcf" />

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
├── SupplyChain_dashboard.pdf
├── DAX_Overview.md
├── Samsung.pbix
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
