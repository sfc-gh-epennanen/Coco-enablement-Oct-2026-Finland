# Customer Brief: Ruokavirta Oy

> **Engagement:** AI-Powered Data Assistant for Self-Service Analytics
> **Partner:** CGI Finland Oy
> **Classification:** Confidential — Lab Exercise Material
> **Date:** 2026-10-01

---

## 1. Company Overview

**Ruokavirta Oy** is a Finnish grocery retail group operating a chain of supermarkets, neighbourhood stores, and an online grocery platform across Finland. Founded in 1978 as a regional cooperative in Tampere, Ruokavirta has grown through acquisitions into one of Finland's mid-sized grocery retailers.

| Attribute | Detail |
|---|---|
| **Legal name** | Ruokavirta Oy |
| **Trade name** | Ruokavirta |
| **Business ID (Y-tunnus)** | 2345678-9 |
| **Headquarters** | Keilaniementie 4, 02150 Espoo |
| **Regional offices** | Tampere, Oulu, Turku |
| **Employees** | ~4,100 (3,200 stores, 400 warehouse/logistics, 500 HQ) |
| **Annual revenue** | EUR 1.8B (FY 2025) |
| **Ownership** | Private — founding family (55%), institutional investors (45%) |

### Revenue Breakdown

| Division | Revenue | EBITDA Margin | Trend |
|---|---|---|---|
| **Supermarkets (Ruokavirta Suuret)** | EUR 1.1B | 3.8% | Stable, organic growth +2% |
| **Neighbourhood stores (Ruokavirta Lähikaupat)** | EUR 420M | 2.9% | Declining footfall -3% YoY |
| **Online grocery (Ruokavirta Verkkokauppa)** | EUR 180M | 1.2% | Fast growth +24% YoY |
| **Wholesale / B2B (Ruokavirta Tukku)** | EUR 100M | 5.1% | Stable |
| **Group total** | EUR 1.8B | 3.5% | — |

---

## 2. Business Operations

### 2.1 Store Network

Ruokavirta operates **214 stores** across Finland in three formats:

- **Ruokavirta Suuret** (68 supermarkets): 1,500-4,000 sqm, full assortment, fresh departments
- **Ruokavirta Lähikaupat** (138 neighbourhood stores): 200-600 sqm, convenience, limited range
- **Ruokavirta Verkkokauppa** (8 fulfilment hubs): Online grocery picking and delivery in Helsinki, Tampere, Oulu, Turku, Kuopio, Jyväskylä, Lahti, Espoo metro areas

Key operational data:

- **POS transactions:** ~1.8M per day across all stores
- **Active SKUs:** ~32,000 (supermarkets) / ~6,000 (neighbourhood stores)
- **Loyalty program (Virta Bonus):** 1.9M active members, personalized offers
- **Supply chain:** 4 distribution centres (Vantaa, Tampere, Oulu, Turku), 580 active suppliers
- **Private label:** "Virta" brand covers ~2,200 SKUs across groceries, household, and personal care

### 2.2 Data Landscape

Ruokavirta's data infrastructure evolved organically over 15 years and now spans multiple systems:

| System | Purpose | Data Volume |
|---|---|---|
| SAP Retail (on-prem) | ERP — procurement, inventory, finance | ~500 GB |
| Oracle RMS | Merchandise management, pricing | ~200 GB |
| NCR Aloha POS | Point-of-sale transactions | ~2.5 TB (3 years) |
| Salesforce Marketing Cloud | Loyalty, campaigns, CRM | ~80 GB |
| Microsoft Power BI (Premium P2) | Reporting — 420 reports, 290 active users | N/A |
| Azure SQL Database | Data warehouse (staging + marts) | ~1.8 TB |
| Snowflake | New analytics platform (adopted Q1 2025) | ~900 GB and growing |

---

## 3. The Problem: Self-Service Reporting Gap

Ruokavirta's biggest data challenge is not data availability — it is **data accessibility**. The data team has done an excellent job loading data into Snowflake, but business users still cannot get answers without submitting a report request.

### Current Report Request Process

1. Business user identifies a question (e.g., "Which stores are losing margin on fresh produce?")
2. User submits a request to the data team via Jira (average 12 new requests per week)
3. Data analyst interprets the question, writes SQL, validates results
4. Analyst builds a Power BI report or exports to Excel
5. Report is delivered to the requester

**Average turnaround:** 8-14 business days
**Current backlog:** 47 open requests (oldest: 6 weeks)

### Why This Matters

| Impact Area | Description |
|---|---|
| **Decision speed** | Store managers cannot react to margin erosion, stock issues, or local trends in time |
| **Data team burnout** | 4-person analytics team spends 70% of time on ad-hoc report requests instead of strategic work |
| **Missed opportunities** | Category managers estimate EUR 3-5M/year in missed margin optimization due to slow insights |
| **Shadow IT** | Business users export data to Excel and build their own calculations — inconsistent, error-prone |
| **Executive frustration** | CEO and CFO want "one version of the truth" but get different numbers from different teams |

---

## 4. Key Stakeholders

| # | Name | Title | Primary Concern |
|---|---|---|---|
| 1 | **Markku Lahtinen** | Chief Digital Officer | AI strategy, board mandate to "democratize data access" by end of 2026 |
| 2 | **Elina Koskinen** | Head of Data & Analytics | Reduce report backlog, free the team for strategic work, prove AI value |
| 3 | **Jari Hämäläinen** | VP Retail Operations | Real-time store performance visibility, daily sales and margin insights |
| 4 | **Tiina Mäkelä** | Category Director — Fresh | Product-level margin analysis, waste reduction, supplier performance |
| 5 | **Petri Virtanen** | Director of Supply Chain | Inventory optimization, stockout prediction, distribution efficiency |
| 6 | **Laura Niemi** | CFO | Cost control, consistent financial metrics, board-level reporting |
| 7 | **Tommi Korhonen** | IT Security & Compliance Manager | GDPR compliance, data access governance, role-based access |

---

## 5. What They Want: An AI Data Assistant

Ruokavirta wants to replace the manual report request process with an **AI-powered data assistant** that business users can ask questions in natural language and get accurate answers from their Snowflake data — without writing SQL or waiting for the data team.

### Requirements

| # | Requirement | Priority |
|---|---|---|
| 1 | Natural language query interface — users ask questions in plain Finnish or English, get answers from live data | P0 |
| 2 | Accurate SQL generation — the assistant must produce correct SQL, not hallucinate columns or join paths | P0 |
| 3 | Business-level vocabulary — users say "margin", "waste", "stockout" and the system maps these to the correct calculations | P0 |
| 4 | Role-based access — store managers see only their store(s), category managers see their categories, executives see everything | P1 |
| 5 | Consistent metrics — every user gets the same definition of "gross margin", "like-for-like sales", "waste percentage" | P1 |
| 6 | Available in Snowflake Intelligence — business users access the assistant from a simple web portal, no SQL tools required | P1 |
| 7 | Extensible — CGI should be able to add new data sources and metrics as the business evolves | P2 |

---

## 6. Available Data in Snowflake

The data team has already loaded the following into Snowflake:

### Database: `RUOKAVIRTA_DW`

| Schema | Table | Description | Rows (approx.) |
|---|---|---|---|
| `RAW` | `STORES` | Store master data — 214 stores, format, city, region, sqm | 214 |
| `RAW` | `PRODUCTS` | Product catalog — SKU, name, category, subcategory, supplier, unit cost | 32,000 |
| `RAW` | `DAILY_SALES` | Daily store-product sales aggregates — date, store, product, qty, revenue, cost | ~18M (2 years) |
| `RAW` | `INVENTORY_SNAPSHOTS` | Daily inventory levels per store-product — date, store, product, stock_qty, stock_value | ~12M |
| `RAW` | `WASTE_RECORDS` | Waste/spoilage — date, store, product, qty_wasted, waste_reason, cost_eur | ~800K |
| `RAW` | `LOYALTY_TRANSACTIONS` | Virta Bonus loyalty — member_id, store, basket_items, basket_value, points_earned | ~25M |
| `RAW` | `SUPPLIERS` | Supplier master — supplier_id, name, country, category, lead_time_days, rating | 580 |
| `ANALYTICS` | (empty) | Target schema for semantic views and curated data | — |
| `GOVERNANCE` | (empty) | Target schema for data quality and access policies | — |

### Key Business Metrics (Currently Defined Only in Power BI)

| Metric | Definition | Used By |
|---|---|---|
| **Gross Margin %** | (Revenue - COGS) / Revenue * 100 | Everyone |
| **Like-for-Like Sales** | Sales growth comparing same stores open > 12 months, same period YoY | CFO, CEO |
| **Waste %** | Waste cost / Total COGS * 100, by category | Category managers, store managers |
| **Stockout Rate** | Days with zero stock / Total days in period, by store-product | Supply chain, store managers |
| **Basket Size** | Average basket value (EUR) per transaction | Marketing, loyalty team |
| **Customer Frequency** | Average visits per loyalty member per month | Marketing |

The problem: these metrics are defined in Power BI DAX formulas. Different reports sometimes use slightly different versions. Moving them into a **semantic view** in Snowflake would create a single source of truth.

---

## 7. Lab Exercise Mapping

| Exercise | Title | Business Scenario |
|---|---|---|
| **Exercise 1** | Getting Started | Generate realistic grocery retail demo data in Snowflake |
| **Exercise 2** | Semantic View | Build a semantic model that maps business terms to SQL — the "brain" of the data assistant |
| **Exercise 3** | Cortex Agent | Deploy an AI data assistant that business users can talk to in Snowflake Intelligence |

---

## 8. Success Criteria

| # | Criterion | Target |
|---|---|---|
| 1 | Natural language questions answered correctly | 8 out of 10 test questions return accurate results |
| 2 | Business vocabulary understood | "margin", "waste", "stockout", "like-for-like" all resolve correctly |
| 3 | Consistent answers | Same question asked twice returns the same number |
| 4 | Accessible to non-technical users | Business user can get an answer in < 30 seconds from Snowflake Intelligence |
| 5 | Report backlog impact | Estimated 60-70% of ad-hoc requests could be self-served through the assistant |

---

## 9. Contacts

| Role | Name | Email | Phone |
|---|---|---|---|
| CDO (sponsor) | Markku Lahtinen | markku.lahtinen@ruokavirta.fi | +358 40 555 0301 |
| Head of Data | Elina Koskinen | elina.koskinen@ruokavirta.fi | +358 40 555 0302 |
| CGI Lead Consultant | Mika Rantanen | mika.rantanen@cgi.com | +358 40 555 0400 |
| CGI Data Engineer | Hanna Lehtonen | hanna.lehtonen@cgi.com | +358 40 555 0401 |

---

*This document is fictional training material created for the CGI Finland Snowflake Enablement Lab. Any resemblance to real companies or persons is coincidental.*
