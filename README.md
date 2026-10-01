# Cortex Code Hands-On Lab — CGI Finland

## Building an AI Data Assistant for Grocery Retail

Welcome to the Cortex Code hands-on lab! In this session, we will build an AI-powered data assistant that lets business users ask questions about their grocery retail data in natural language — no SQL required.

## Overview

| Item | Detail |
|------|--------|
| **Duration** | ~1 hour |
| **Exercises** | 3 |
| **Audience** | CGI Finland consultants and data engineers |
| **Platform** | Cortex Code in Snowsight (browser) |
| **Language** | English |
| **Customer scenario** | Ruokavirta Oy — fictional Finnish grocery retail group |

## Your Customer

| Detail | Value |
|--------|-------|
| **Company** | Ruokavirta Oy |
| **Industry** | Grocery retail (supermarkets, neighbourhood stores, online) |
| **Headquarters** | Espoo, Finland |
| **Revenue** | ~EUR 1.8B |
| **Employees** | ~4,100 |
| **Stores** | 214 across Finland |
| **Current platform** | Snowflake (data warehouse), Power BI (reporting) |
| **Challenge** | Business users cannot query data without the data team — 47 open report requests, 8-14 day turnaround |
| **Goal** | AI data assistant that replaces the ad-hoc reporting bottleneck |

## What You'll Build Today

1. **Getting Started** — Generate a realistic grocery retail demo database with Finnish data
2. **Semantic View** — Build a semantic model that maps business vocabulary to SQL — the "brain" of the data assistant
3. **Cortex Agent** — Deploy an AI data assistant that business users can talk to in Snowflake Intelligence

## Lab Structure

| # | Exercise | Topic | Duration |
|---|----------|-------|----------|
| 1 | [Getting Started](exercises/exercise-1-getting-started.md) | Environment setup + demo data | ~20 min |
| 2 | [Semantic View](exercises/exercise-2-semantic-view.md) | Build the semantic model | ~20 min |
| 3 | [Cortex Agent](exercises/exercise-3-cortex-agent.md) | Deploy the AI data assistant | ~20 min |

## Getting Started

### Step 1: Open Snowsight

1. Log into your Snowflake account in your browser
2. Open the Snowsight UI

### Step 2: Upload Lab Files

1. Open **Projects** in the left sidebar
2. Create a new project or open an existing one
3. Upload this lab package's files to the project:
   - `assets/customer-brief.md`
   - `assets/discovery-notes.md`
   - All files from the `exercises/` folder

### Step 3: Open Cortex Code

1. Click the **Cortex Code** icon (CoCo) in the Snowsight sidebar
2. Verify CoCo is available and responds to questions
3. Confirm you have permissions to create databases and schemas

### Step 4: Begin Exercise 1

Open [Exercise 1: Getting Started](exercises/exercise-1-getting-started.md) and follow the instructions.

## Package Contents

```
cortex-code-enablement-cgi-finland-FI/
├── README.md                              ← This file — lab overview
├── presenter-guide.md                     ← Presenter instructions
├── presenter-guide.html                   ← Presenter guide in HTML (open in browser)
├── assets/
│   ├── customer-brief.md                  ← Fictional customer profile (CoCo reads this)
│   └── discovery-notes.md                 ← Stakeholder meeting notes (CoCo reads this)
├── exercises/
│   ├── exercise-1-getting-started.md      ← Environment setup and demo data
│   ├── exercise-2-semantic-view.md        ← Build the semantic model
│   └── exercise-3-cortex-agent.md         ← Deploy the AI data assistant
├── html/
│   ├── README.html                        ← HTML versions (open in browser)
│   ├── exercise-1-getting-started.html
│   ├── exercise-2-semantic-view.html
│   └── exercise-3-cortex-agent.html
└── _build/                                ← Build scripts (you can ignore this folder)
```

## How This Lab Works

This lab uses **copy-paste prompts**. Each exercise contains ready-made prompts that you paste directly into Cortex Code. CoCo then:

1. **Reads context** — the customer brief and stakeholder meeting notes
2. **Generates SQL** — creates databases, tables, semantic views, and agents
3. **Executes the code** — runs SQL in your Snowflake account
4. **Explains the results** — tells you what happened and why

You don't need to write SQL or code yourself — CoCo handles it for you!

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Cortex Code (CoCo)** | Snowflake's AI-powered coding assistant that understands your data catalog |
| **Semantic View** | A business-friendly data model that maps natural language terms to SQL. It defines dimensions, measures, and joins so an AI agent can translate questions into correct queries. |
| **Cortex Analyst** | The SQL engine behind the semantic view — it takes a natural language question and generates a SQL query using the semantic model |
| **Cortex Agent** | An AI assistant that combines Cortex Analyst with reasoning and conversation. Users ask questions, the agent queries the semantic view, and returns answers. |
| **Snowflake Intelligence** | A web portal where business users interact with Cortex Agents — no SQL tools required |

## Industry Context

| Context | Description |
|---------|-------------|
| Finnish grocery retail | Highly competitive, thin margins (2-5%), high volume |
| Key metrics | Gross margin %, like-for-like sales, waste %, stockout rate, basket size |
| Regulatory | EU GDPR, Finnish consumer protection, food safety regulations |
| Competitive pressure | K-Group (Kesko), S-Group, Lidl — constant price and assortment competition |

## After the Session

This lab is designed to be reusable. You can:

1. **Replace the customer context** — swap `customer-brief.md` and `discovery-notes.md` with real client details
2. **Customize prompts** — tailor exercise prompts to the client's specific data and metrics
3. **Extend the lab** — add exercises (e.g., data quality, governance, dashboards)
4. **Present to clients** — use the HTML versions for a professional presentation

---

*Happy building! If you encounter issues, ask Cortex Code for help — it can fix its own mistakes.*
