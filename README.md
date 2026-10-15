# -Predictive-Ecommerce-Logistics-SQL-Audit.
# Predictive E-Commerce Delivery Risk & Logistics SLA Matrix (SQL) 🚚💨

## 📌 Project Overview
In global e-commerce supply chains, meeting the **SLA (Service Level Agreement)** is critical for customer retention. This project transitions away from basic spreadsheet filtering to build a multi-table relational database architecture using advanced **Cloud SQL (PostgreSQL/MySQL)**. The objective is to track shipment delays, grade courier performance, and calculate the exact financial value at risk during fulfillment operational failure.

## 🛠️ Tech Stack & Database Architecture
* **Database Engine:** PostgreSQL / MySQL 8.0
* **Data Modeling Framework:** Relational Schema Mapping (Products, Couriers, Shipments)
* **AI Debugging Partner:** ChatGPT (Leveraged for dynamic date-interval syntax validation)

### Core Schema Definition:
1. `products`: Tracks inventory item metadata, unit costs, and security tiering.
2. `couriers`: Manages logistics carrier profiles and SLA delivery window promises.
3. `shipments`: Logs real-time quantity dispatches, tracking shipping dates vs physical delivery dates.

## 🔍 Advanced Production Queries & Business Logic

### 1. The Operational SLA Breach Monitor
To isolate specific operational failures, I engineered an explicit `JOIN` query tracking date deltas. This query filters out successful deliveries and isolates only the orders that breached delivery timelines, displaying the exact revenue sitting at risk:

```sql
SELECT 
    s.shipment_id,
    p.description AS product_name,
    c.courier_name,
    s.country,
    (s.delivery_date - s.ship_date) AS actual_delivery_days,
    c.promised_days AS sla_promised_days,
    (s.quantity * p.unit_price) AS financial_value_at_risk
FROM shipments s
JOIN products p ON s.product_id = p.product_id
JOIN couriers c ON s.courier_id = c.courier_id
WHERE (s.delivery_date - s.ship_date) > c.promised_days;
```

## 📊 Business Operations Strategy & Impact
* **Courier Accountability:** By auditing delivery day metrics against carrier promises, procurement teams can dynamically penalize consistently delayed couriers.
* **Risk Asset Mitigation:** Isolating the `financial_value_at_risk` helps warehouse managers allocate premium tracking resources to high-value items during delayed transport routes.

---
*This advanced database query matrix forms part of my operational data engine portfolio as I actively pursue a 2-month paid Data Analyst / Data Science internship globally.*
