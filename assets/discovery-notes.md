# Discovery Workshop — Meeting Minutes

**Customer:** Ruokavirta Oy
**Date:** September 18, 2026
**Location:** Ruokavirta HQ, Keilaniementie 4, Espoo
**Duration:** 09:00–11:30 (2.5 hours)
**Facilitator:** CGI Finland Oy — Data & Analytics Practice

## Attendees

| # | Name | Title |
|---|------|-------|
| 1 | Markku Lahtinen | Chief Digital Officer |
| 2 | Elina Koskinen | Head of Data & Analytics |
| 3 | Jari Hämäläinen | VP Retail Operations |
| 4 | Tiina Mäkelä | Category Director — Fresh |
| 5 | Petri Virtanen | Director of Supply Chain |
| 6 | Laura Niemi | CFO |

**From CGI:** Mika Rantanen (Lead Consultant), Hanna Lehtonen (Data Engineer)

---

## 1. Opening — The Data Access Problem

Markku Lahtinen opened the session by framing the challenge. Ruokavirta has invested significantly in data infrastructure over the past two years — migrating to Snowflake, building a modern data warehouse, hiring a dedicated analytics team. The data is there. The problem is getting it to the people who need it.

> **Markku Lahtinen (CDO):** "We spent two years building a world-class data platform. Our Snowflake environment is solid, our data is clean, our pipelines work. But our business users still cannot get answers without filing a Jira ticket and waiting two weeks. That is not acceptable. The board wants us to democratize data access — they want every store manager, every category manager, every executive to be able to ask a question and get an answer immediately. Not next week. Now."

---

## 2. Business User Frustrations

### 2.1 Store Operations

Jari Hämäläinen described the daily reality for store managers. Each morning, 214 store managers need to understand yesterday's performance — sales, margins, waste, inventory gaps — to make decisions about staffing, ordering, and promotions for the day ahead.

> **Jari Hämäläinen (VP Retail):** "My store managers open Power BI every morning and look at the same five reports. But the moment they have a question that is not on the dashboard — 'Why did my fresh produce margin drop last Tuesday?' or 'Which products should I promote this weekend based on current stock levels?' — they are stuck. They either call the data team, who take two weeks to respond, or they export to Excel and make up their own numbers. I have 214 stores and each one invents its own version of the truth."

### 2.2 Category Management

Tiina Mäkelä runs the fresh produce category — the highest-margin but also highest-waste segment. She described how slow data access directly costs money.

> **Tiina Mäkelä (Category Director — Fresh):** "Fresh is where we make and lose money. Every day we do not catch a waste problem, we lose thousands of euros. Last month I suspected our berry supplier was sending us short-dated stock, but it took the data team 11 days to pull the data I needed to confirm it. By then we had already wasted EUR 40,000 worth of strawberries. If I could have asked a question and gotten an answer the same day, we would have switched suppliers immediately. I need an assistant I can just ask: 'Show me waste by supplier for berries this month compared to last year.'"

### 2.3 Supply Chain

Petri Virtanen highlighted the inventory visibility gap. The supply chain team manages replenishment across 214 stores and 4 distribution centres, but their view of what is happening is always at least one day behind.

> **Petri Virtanen (Supply Chain):** "I want to ask: 'Which stores are about to run out of milk tomorrow based on current sales velocity?' Right now I cannot answer that question without running a custom SQL query, and I do not know SQL. My team builds Excel models. We have smart people building dumb spreadsheets because they cannot talk to the data warehouse."

### 2.4 Finance

Laura Niemi raised the consistency problem. Different teams calculate the same metrics differently, leading to conflicting numbers in board presentations.

> **Laura Niemi (CFO):** "Last quarter, the retail team reported 3.2% like-for-like sales growth. My finance team calculated 2.8%. The board asked why the numbers were different. The answer? Two different Power BI reports using two different definitions of 'like-for-like.' We need one place where the metric is defined once and everyone gets the same answer. I do not care what tool they use — I care that the number is right."

---

## 3. Data Team Perspective

Elina Koskinen described the situation from the analytics team's side. Her 4-person team is overwhelmed by ad-hoc requests and cannot invest in strategic work.

> **Elina Koskinen (Head of Data):** "My team is talented. They can build amazing things. But they spend 70% of their time answering questions like 'What were sales in Oulu last week?' That is not a hard question — it is a SELECT SUM query. But our business users cannot run that query themselves, so they submit a ticket and my analyst writes the SQL and emails back an Excel file. We do this 12 times a week. If we could redirect even half of those requests to a self-service AI assistant, my team could finally work on the projects that actually move the business forward — demand forecasting, customer segmentation, supplier analytics."

---

## 4. Pain Points Summary

| # | Category | Description | Impact |
|---|----------|-------------|--------|
| 1 | Slow time-to-insight | 8-14 day average for ad-hoc report requests | Delayed decisions, missed opportunities |
| 2 | Metric inconsistency | Same KPI calculated differently across teams | Conflicting board reports, eroded trust |
| 3 | Data team bottleneck | 47 open requests, 4-person team at capacity | Burnout, no strategic work capacity |
| 4 | Shadow IT | Business users build Excel workarounds | Errors, inconsistency, duplication of effort |
| 5 | No self-service | Business users cannot query Snowflake directly | Complete dependency on data team for every question |
| 6 | Waste visibility | Fresh category waste problems detected too late | Estimated EUR 2-3M/year in preventable waste |

---

## 5. Requirements (Prioritized)

| Priority | Requirement | Business Driver |
|----------|-------------|-----------------|
| P0 | AI data assistant that answers business questions from Snowflake data | Eliminate report request bottleneck |
| P0 | Standardized metric definitions in a semantic model | One version of the truth for all users |
| P0 | Natural language interface — no SQL required | Accessible to all 290 Power BI users |
| P1 | Available in Snowflake Intelligence portal | Simple, clean interface for business users |
| P1 | Understands grocery retail vocabulary (margin, waste, stockout, LFL, basket size) | Domain-specific accuracy |
| P2 | Role-based data access (store-level, category-level, executive) | Security and compliance |

---

## 6. Urgency Driver

Markku Lahtinen confirmed that the Ruokavirta board of directors has included "AI-powered data democratization" as a strategic initiative for 2026. The **annual board strategy review is scheduled for November 15, 2026** (7 weeks away). The board expects to see:

1. A working proof-of-concept of an AI data assistant
2. A plan for rolling it out to the 290 business intelligence users
3. Cost/benefit analysis

> **Markku Lahtinen (CDO):** "The board approved the Snowflake investment. Now they want to see the return. An AI assistant that lets 290 people ask questions without bothering the data team — that is the ROI story. If we cannot demonstrate this works by November, the board will question whether the Snowflake investment was worth it."

---

## 7. Next Steps

| # | Action | Owner | Deadline |
|---|--------|-------|----------|
| 1 | Provide Snowflake account access and data catalog | Elina Koskinen | September 25, 2026 |
| 2 | Document the 10 most common report request types | Elina Koskinen | September 25, 2026 |
| 3 | Define official metric definitions (margin, LFL, waste, stockout) | Laura Niemi + Elina | October 1, 2026 |
| 4 | Build semantic view POC with Cortex Code | CGI (Mika Rantanen) | October 8, 2026 |
| 5 | Deploy Cortex Agent and test with 5 business users | CGI (Hanna Lehtonen) | October 15, 2026 |
| 6 | Prepare board presentation | Markku Lahtinen + CGI | November 1, 2026 |
| 7 | Board strategy review | Ruokavirta Board | November 15, 2026 |

---

*Minutes recorded by Mika Rantanen, CGI Finland Oy. Distributed to all attendees on September 19, 2026.*
