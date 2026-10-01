# Exercise 1: Getting Started — Environment Setup and Demo Data

> **Duration:** ~20 min | **Tasks:** 4

## Objective

Set up your lab environment, verify Cortex Code is working, read the customer context for Ruokavirta Oy (a Finnish grocery retail group), and generate a realistic demo database with sales, inventory, waste, and loyalty data.

By the end of this exercise you will have a `RUOKAVIRTA_DEMO` database with seven populated tables that the remaining exercises build on.

---

## Task 1: Upload Files and Explore the Environment

Upload the lab materials into Snowsight and open Cortex Code for the first time.

**Steps:**

1. In Snowsight, go to **Projects** and open a Cortex Code session.
2. Upload the `assets/` and `exercises/` directories from the lab package.
3. Verify the environment — paste this prompt into Cortex Code:

```
What Snowflake role and warehouse am I currently using? List my available databases.
```

**Expected outcome:** CoCo responds with your active role, warehouse, and database list.

---

## Task 2: Read Customer Context

Before building anything, understand the customer. The `assets/` folder contains two files about Ruokavirta Oy — a fictional Finnish grocery retail company struggling with data accessibility.

Copy and paste:

```
Read the files assets/customer-brief.md and assets/discovery-notes.md. Summarize:
1. What does Ruokavirta Oy do?
2. What is their main data problem?
3. What do the business users want?
4. What data is already available in Snowflake?
```

**Expected outcome:** CoCo produces a summary covering the grocery retail business, the report request bottleneck (47 open requests, 8-14 day turnaround), business users wanting self-service analytics, and the available data tables.

---

## Task 3: Generate Demo Database

Create a realistic grocery retail demo database. This single prompt generates all tables with Finnish data.

Copy and paste:

```
Create a demo database called RUOKAVIRTA_DEMO in Snowflake with three schemas: RAW, ANALYTICS, and GOVERNANCE.

In the RAW schema, generate the following tables with realistic Finnish grocery retail data:

- STORES (store_id, name, city, region, format, sqm, opened_date) — 50 stores across Finland. Formats: 'Suuret' (supermarket), 'Lähikauppa' (neighbourhood), 'Verkkokauppa' (online hub). Cities: Helsinki, Espoo, Vantaa, Tampere, Turku, Oulu, Kuopio, Jyväskylä, Lahti, Rovaniemi.

- PRODUCTS (product_id, name, category, subcategory, supplier, unit_cost_eur, unit_price_eur) — 500 products. Categories: Fresh Produce, Dairy, Meat & Fish, Bakery, Beverages, Frozen, Household, Snacks. Finnish product names.

- DAILY_SALES (sale_id, date, store_id, product_id, quantity, revenue_eur, cost_eur) — 100,000 rows over 12 months. Revenue and cost should show realistic grocery margins (2-6% net, higher for private label).

- INVENTORY_SNAPSHOTS (snapshot_id, date, store_id, product_id, stock_qty, stock_value_eur) — 50,000 rows. Include some stockout situations (stock_qty = 0).

- WASTE_RECORDS (waste_id, date, store_id, product_id, qty_wasted, waste_reason, cost_eur) — 10,000 rows. Waste reasons: 'Expired', 'Damaged', 'Quality issue', 'Overstock'. Fresh produce should have highest waste.

- LOYALTY_TRANSACTIONS (transaction_id, date, store_id, member_id, basket_value_eur, items_count, points_earned) — 80,000 rows. 5,000 unique loyalty members.

- SUPPLIERS (supplier_id, name, country, category, lead_time_days, quality_rating) — 100 suppliers. Mix of Finnish, European, and global suppliers.

Use Finnish city names, realistic EUR prices (milk ~1.50, bread ~2.50, chicken ~8/kg), and seasonal patterns (higher sales before Christmas, Juhannus, Easter).
```

**Expected outcome:** CoCo generates and runs all CREATE TABLE and INSERT statements. Verify:

```
Show me the row counts for all tables in RUOKAVIRTA_DEMO.RAW.
```

You should see counts close to the targets above.

---

## Task 4: Explore the Data

Use Cortex Code to run some exploratory queries to understand the data.

**Prompt 1 — Sales overview:**

```
What are total sales (EUR) by store format (Suuret, Lähikauppa, Verkkokauppa) for the last 3 months? Which format has the highest margin?
```

**Prompt 2 — Waste analysis:**

```
Which product categories have the highest waste percentage (waste cost / total cost)? Show the top 5 categories by waste rate.
```

**Prompt 3 — The question Tiina Mäkelä would ask:**

```
Show me waste by supplier for Fresh Produce products this month compared to the same month last year. Are any suppliers getting worse?
```

These queries confirm the data is realistic and interlinked. You are now ready to build the semantic model.

---

## Summary

After completing this exercise you should have:

- [x] Uploaded lab files and opened Cortex Code
- [x] Read and understood the Ruokavirta customer context
- [x] Created `RUOKAVIRTA_DEMO` with seven populated tables
- [x] Explored sales, waste, and supplier data with natural language queries

---

**Next:** [Exercise 2 — Semantic View](exercise-2-semantic-view.md)
