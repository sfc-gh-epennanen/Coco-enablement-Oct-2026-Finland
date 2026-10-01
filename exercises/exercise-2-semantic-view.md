# Exercise 2: Semantic View — The Brain of the Data Assistant

> **Duration:** ~20 min | **Tasks:** 4

## Objective

Build a **semantic view** over the Ruokavirta demo data. A semantic view is a business-friendly layer that maps natural language terms to SQL — so when a user asks "What is our gross margin this month?", the system knows exactly which columns to query and how to calculate the answer.

By the end of this exercise you will have a working semantic view that Cortex Analyst can use to answer grocery retail business questions.

---

## Task 1: Understand What a Semantic View Does

Before creating one, understand why it matters. Copy and paste:

```
Explain what a Snowflake Semantic View is and why it is important for building an AI data assistant. Use the Ruokavirta Oy scenario as an example:
- Ruokavirta's CFO says "gross margin" — how does the system know that means (revenue - cost) / revenue * 100?
- A store manager says "waste" — how does it know to query WASTE_RECORDS?
- A category manager asks about "like-for-like sales" — how does the system filter to stores open > 12 months?

Explain how a semantic view solves these mapping problems.
```

**Expected outcome:** CoCo explains that a semantic view defines dimensions, measures, and their SQL expressions — creating a bridge between business vocabulary and database schema.

---

## Task 2: Create the Semantic View

Now build the semantic view. This is the core deliverable — the "brain" that powers the data assistant.

Copy and paste:

```
Read the customer-brief.md to understand Ruokavirta's business metrics. Then create a Snowflake Semantic View called RUOKAVIRTA_DEMO.ANALYTICS.RETAIL_SEMANTIC_VIEW over the tables in RUOKAVIRTA_DEMO.RAW.

The semantic view should include:

ENTITIES (base tables):
- STORES: the store dimension (store_id, name, city, region, format)
- PRODUCTS: the product dimension (product_id, name, category, subcategory, supplier)
- DAILY_SALES: the core fact table for sales transactions
- WASTE_RECORDS: waste/spoilage fact table
- INVENTORY_SNAPSHOTS: inventory levels fact table
- SUPPLIERS: supplier dimension

DIMENSIONS:
- store_name, store_city, store_region, store_format (from STORES)
- product_name, product_category, product_subcategory, supplier_name (from PRODUCTS)
- sale_date (from DAILY_SALES — for time-based queries)
- waste_date, waste_reason (from WASTE_RECORDS)

MEASURES:
- total_revenue: SUM(DAILY_SALES.revenue_eur)
- total_cost: SUM(DAILY_SALES.cost_eur)
- gross_margin_pct: (SUM(revenue_eur) - SUM(cost_eur)) / NULLIF(SUM(revenue_eur), 0) * 100
- total_quantity_sold: SUM(DAILY_SALES.quantity)
- waste_cost: SUM(WASTE_RECORDS.cost_eur)
- waste_quantity: SUM(WASTE_RECORDS.qty_wasted)
- waste_pct: SUM(WASTE_RECORDS.cost_eur) / NULLIF(SUM(DAILY_SALES.cost_eur), 0) * 100
- avg_stock_qty: AVG(INVENTORY_SNAPSHOTS.stock_qty)
- stockout_days: COUNT of days where INVENTORY_SNAPSHOTS.stock_qty = 0

RELATIONSHIPS (joins):
- DAILY_SALES.store_id = STORES.store_id
- DAILY_SALES.product_id = PRODUCTS.product_id
- WASTE_RECORDS.store_id = STORES.store_id
- WASTE_RECORDS.product_id = PRODUCTS.product_id
- INVENTORY_SNAPSHOTS.store_id = STORES.store_id
- INVENTORY_SNAPSHOTS.product_id = PRODUCTS.product_id
- PRODUCTS.supplier = SUPPLIERS.name

SYNONYMS (business vocabulary):
- "margin" = gross_margin_pct
- "waste" = waste_cost or waste_pct (depending on context)
- "stockout" = stockout_days
- "sales" = total_revenue
- "basket" = relates to LOYALTY_TRANSACTIONS
- "fresh" = product_category = 'Fresh Produce'
- "spoilage" = waste_cost

Include clear descriptions for each measure in plain English that a non-technical grocery retail user would understand.
```

**Expected outcome:** CoCo creates the semantic view DDL and executes it. The semantic view defines all entities, dimensions, measures, relationships, and synonyms.

---

## Task 3: Test the Semantic View with Cortex Analyst

Now test whether the semantic view works by asking business questions through Cortex Analyst.

Copy and paste:

```
Test the semantic view RUOKAVIRTA_DEMO.ANALYTICS.RETAIL_SEMANTIC_VIEW by asking these 5 questions via Cortex Analyst. For each question, show me:
- The natural language question
- The SQL that Cortex Analyst generates
- The result

Questions:
1. "What was our total revenue last month?"
2. "Which store has the highest gross margin this quarter?"
3. "What is the waste percentage for Fresh Produce compared to other categories?"
4. "Show me the top 5 suppliers by total revenue"
5. "Which stores had stockouts on dairy products in the last 30 days?"
```

**Expected outcome:** Cortex Analyst generates correct SQL for all 5 questions and returns sensible results. If any question fails or returns wrong data, CoCo can debug and fix the semantic view.

---

## Task 4: Refine and Improve

Real semantic views need iteration. Test an edge case and improve the model.

Copy and paste:

```
Now ask Cortex Analyst a harder question via the semantic view:

"Compare our gross margin trend month-over-month for the last 6 months, broken down by store format. Which format is improving and which is declining?"

If Cortex Analyst gets this wrong or cannot answer it, diagnose the issue and update the semantic view to handle it. Common fixes:
- Adding a time grain dimension (month, quarter)
- Adding a derived measure for month-over-month comparison
- Improving join definitions

After fixing, re-test the question to confirm it works.
```

**Expected outcome:** Either Cortex Analyst answers correctly (great!) or CoCo identifies a gap in the semantic view, fixes it, and the re-test succeeds.

---

## Summary

After completing this exercise you should have:

- [x] Understood what a semantic view does and why it matters
- [x] Created `RETAIL_SEMANTIC_VIEW` with dimensions, measures, and relationships
- [x] Tested 5 business questions via Cortex Analyst
- [x] Refined the semantic view to handle complex queries

The semantic view is the foundation. In Exercise 3, you will wrap it in a Cortex Agent and deploy it to Snowflake Intelligence — where business users can interact with it directly.

---

**Next:** [Exercise 3 — Cortex Agent](exercise-3-cortex-agent.md)
