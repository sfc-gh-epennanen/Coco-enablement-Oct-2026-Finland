# Exercise 3: Cortex Agent — Deploy the AI Data Assistant

> **Duration:** ~20 min | **Tasks:** 4

## Objective

Build and deploy a **Cortex Agent** — an AI-powered data assistant that business users at Ruokavirta can talk to in natural language. The agent uses the semantic view from Exercise 2 as its data tool, and is deployed to **Snowflake Intelligence** where non-technical users can access it from a simple web portal.

By the end of this exercise, you will have a working AI data assistant that can answer grocery retail business questions — the kind that currently take Ruokavirta's data team 8-14 days to handle.

---

## Task 1: Create the Cortex Agent

Build the agent and connect it to your semantic view. Copy and paste:

```
Create a Snowflake Cortex Agent called RUOKAVIRTA_DEMO.ANALYTICS.RETAIL_DATA_ASSISTANT.

System prompt for the agent:
"You are the Ruokavirta Data Assistant — an AI analyst for Ruokavirta Oy, a Finnish grocery retail group with 214 stores, EUR 1.8B revenue, and 32,000 SKUs.

Your role: answer business questions about sales, margins, waste, inventory, and suppliers using live Snowflake data.

You have access to the Cortex Analyst tool connected to RUOKAVIRTA_DEMO.ANALYTICS.RETAIL_SEMANTIC_VIEW.

When answering:
- Always cite specific numbers from the data (EUR values, percentages, counts)
- Use grocery retail context: margins are thin (2-6%), waste is critical (especially fresh), seasonal patterns matter
- Currency is EUR, Finnish city names, Finnish business conventions
- If asked about a trend, show at least 3 months of data
- If a question is ambiguous, ask for clarification before querying
- For executive questions, include a 1-sentence business recommendation
- Format numbers clearly: EUR with 2 decimals, percentages with 1 decimal

Do not make up data. If the data is not available, say so clearly."

Connect the semantic view RUOKAVIRTA_DEMO.ANALYTICS.RETAIL_SEMANTIC_VIEW as the agent's primary data tool via Cortex Analyst.
```

**Expected outcome:** CoCo creates the Cortex Agent with the specified system prompt and connects it to the semantic view.

---

## Task 2: Test the Agent with Business Questions

Test the agent with progressively complex questions — the kind that Ruokavirta's business users would actually ask. Copy and paste:

```
Test the RETAIL_DATA_ASSISTANT agent with the following 5 questions. For each question, show the agent's full response:

1. "What were our total sales last month?"
   (Jari Hämäläinen — store operations — morning check)

2. "Which stores have the worst gross margin this quarter? What is dragging them down?"
   (Laura Niemi — CFO — performance review)

3. "Show me waste by product category for the last 3 months. Is Fresh Produce getting better or worse?"
   (Tiina Mäkelä — category director — waste reduction initiative)

4. "Which suppliers have the highest revenue but lowest quality rating? Should we be concerned?"
   (Petri Virtanen — supply chain — supplier review)

5. "Give me a summary I can present to the board: total revenue, margin trend, top issue, and one recommendation."
   (Markku Lahtinen — CDO — board preparation)
```

**Expected outcome:** The agent answers all 5 questions with specific numbers from the data. The board summary (question 5) should be concise and executive-ready.

---

## Task 3: Deploy to Snowflake Intelligence

Make the agent accessible to business users through Snowflake Intelligence — a clean web interface where users can ask questions without any SQL tools.

Copy and paste:

```
Show me how to make the RETAIL_DATA_ASSISTANT agent available in Snowflake Intelligence so that Ruokavirta's business users can access it.

Walk me through:
1. How to publish the agent to Snowflake Intelligence
2. How to set up the agent's display name and description for end users
3. How business users would access it (URL, login, interface)
4. How role-based access works — ensuring store managers see only their data

If Snowflake Intelligence is available in this account, set it up. If not, explain the steps and show what the end-user experience looks like.
```

**Expected outcome:** CoCo either configures Snowflake Intelligence (if available) or provides a clear walkthrough of the setup steps. You understand how business users will interact with the agent.

---

## Task 4: The CGI Value Proposition

Finally, frame this as a deliverable that CGI can offer to customers. Copy and paste:

```
Based on what we built today — the demo database, semantic view, and Cortex Agent — create a summary that answers these questions for a CGI sales meeting:

1. WHAT WE BUILT: Describe the three components and how they work together
2. BUSINESS VALUE: Calculate the potential value for Ruokavirta:
   - If the data team's time costs EUR 80/hour, and each ad-hoc report takes ~4 hours, and we can eliminate 60% of the 47 open requests...
   - If faster waste detection saves even 10% of the estimated EUR 2-3M annual waste...
   - Time to first answer: from 8-14 days to < 30 seconds
3. REUSABILITY: How can CGI reuse this approach with other customers?
   - What stays the same? (Architecture, approach, Cortex Agent pattern)
   - What changes per customer? (Data, semantic view definitions, system prompt)
4. NEXT STEPS: What would a production deployment look like?
   - Role-based access setup
   - Metric validation with the customer's data team
   - User acceptance testing with 5-10 pilot users
   - Rollout to all 290 Power BI users

Format this as a 1-page executive summary suitable for a CGI internal opportunity review.
```

**Expected outcome:** A concise executive summary that CGI consultants can use to pitch the AI data assistant solution to other customers.

---

## Summary

After completing this exercise you should have:

- [x] Created a Cortex Agent with a grocery retail system prompt
- [x] Tested 5 real-world business questions with accurate answers
- [x] Understood how to deploy to Snowflake Intelligence
- [x] Built a CGI-ready value proposition and reusability framework

## What We Built Today — End to End

```
Business User (Snowflake Intelligence)
     ↓
"What is our waste % for Fresh Produce?"
     ↓
Cortex Agent (RETAIL_DATA_ASSISTANT)
     ↓
Cortex Analyst + Semantic View (RETAIL_SEMANTIC_VIEW)
     ↓
SQL: SELECT ... FROM WASTE_RECORDS JOIN PRODUCTS ... WHERE category = 'Fresh Produce'
     ↓
RUOKAVIRTA_DEMO (Snowflake)
     ↓
"Fresh Produce waste is 4.2% this month, up from 3.8% last month.
 The increase is driven by berries (6.1%) and salads (5.3%).
 Recommendation: Review berry suppliers with quality rating < 4."
```

This is the architecture that replaces 47 open report requests and 8-14 day turnaround with a 30-second answer.

---

Return to the lab overview: [../README.md](../README.md)
