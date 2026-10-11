# SupplyGuard: Procurement, Supplier & Inventory Analytics Platform

## Executive Summary

SupplyGuard is an end-to-end data analytics project designed to help procurement teams monitor supplier performance, improve profitability, optimize inventory investments, and reduce operational risks.

Using procurement, vendor, sales, freight, and inventory data, the project answers critical business questions through descriptive and diagnostic analytics, enabling stakeholders to make data-driven procurement decisions.



# Business Problem

Procurement teams often struggle to identify:

* Supplier concentration risks
* Unprofitable vendor relationships
* Inventory overstocking
* Slow-moving inventory
* Freight cost inefficiencies
* Procurement decisions that negatively impact profitability

Without a centralized analytics solution, these issues can lead to reduced margins, excess working capital, and increased operational risk.



# Business Questions

1. Which vendors account for most procurement spend?
2. Which vendors generate the highest gross profit?
3. Which vendors earn below the portfolio margin, and is any vendor actually losing money?
4. Which vendors demonstrate the most efficient inventory turnover?
5. Which products tie up the most inventory capital?
6. Which cities hold the most stock?
7. Are procurement volumes aligned with vendor profitability?
8. Are freight costs proportionate to procurement activity?



# Dataset Overview

The analysis was performed using procurement, supplier, inventory, and sales datasets containing:

* Vendor Information
* Purchase Transactions
* Sales Transactions
* Freight Costs
* Inventory Records
* Product Information
* Store Information



# Methodology

### Data Preparation

* Data ingestion using Microsoft Fabric Dataflows Gen2
* Data cleaning and transformation using PySpark
* Gold-layer analytical tables created for reporting

### Data Analysis

* Procurement Spend Analysis
* Vendor Profitability Analysis
* Inventory Analysis
* Inventory Turnover Analysis
* Freight Cost Analysis
* Supplier Risk Analysis

### Reporting

* Interactive 4-page Power BI dashboard on a Fabric semantic model
* DAX measures and KPIs
* Bookmarks, drill-through and a last-refreshed stamp
* Automated refresh pipelines



# Solution Architecture

```text
Source Data
    │
    ▼
Dataflows Gen2
    │
    ▼
Lakehouse (Silver Layer)
    │
    ▼
PySpark Transformations
    │
    ▼
Gold Analytical Tables
    │
    ▼
Semantic Model
    │
    ▼
Power BI Dashboard
    │
    ▼
Business Insights & Decisions
```



# Key Findings & Recommendations

## Q1. Which Vendors Account for Most Procurement Spend?

### Observation

Top 3 vendors—DIAGEO ($51M), MARTIGNETTI ($28M), and JIM BEAM ($24M)—account for 32.01% of the total procurement spend.

### Root Cause

Procurement activity is concentrated among a small group of strategic suppliers.

### Recommendation

Diversify supplier allocation and gradually reduce dependency on top vendors.

### Expected Business Impact

Reduce supplier concentration risk and improve supply continuity.



## Q2. Which Vendors Generate the Highest Gross Profit?

### Observation

DIAGEO, MARTIGNETTI, CONSTELLATION, and PERNOD RICARD contribute approximately 37% of total gross profit.

### Root Cause

Strong sales demand combined with efficient procurement relationships.

### Recommendation

Prioritize these vendors during procurement planning and contract negotiations.

### Expected Business Impact

Protect a significant portion of portfolio profitability.



## Q3. Which Vendors Earn Below the Portfolio Margin, and Is Any Vendor Actually Losing Money?

### Observation

Only 13 small vendors lose money, about $33K combined (0.03% of gross profit). The real margin gap is in 12 large vendors (at least 1% of spend each) that earn below the 28.7% portfolio margin, including Diageo (25.9%), Jim Beam (24.1%) and Pernod Ricard (25.3%).

### Root Cause

High purchase costs on high-volume vendors. Margin is measured as weighted margin (gross profit / sales), not an average of product margins, which exaggerated tiny vendors.

### Recommendation

Renegotiate cost prices and terms with the below-average vendors, starting with Diageo, Jim Beam and Pernod Ricard.

### Expected Business Impact

Up to $7.4M of additional gross profit if these vendors reached the portfolio average (an upper bound, not a forecast).



## Q4. Which Vendors Demonstrate the Most Efficient Inventory Turnover?

### Observation

Portfolio turnover is 6.1x (about 60 days of stock), measured as COGS / average inventory at cost. Among large vendors, Bacardi (8.3x) and Brown-Forman (8.1x) lead; Ultra Beverage (4.0x) and Martignetti (5.1x) lag.

### Root Cause

Faster sell-through and replenishment for the leaders, slower sell-through for the laggards.

### Recommendation

Reduce reorder quantities for slow-turning vendors and keep the ordering cadence for fast ones.

### Expected Business Impact

Frees working capital and lowers holding costs.


## Q5. Which Products Tie Up the Most Inventory Capital?

### Observation

$10.6M (19% of the $55.4M closing stock at cost) has 180+ days of supply, including about $0.4M in brands with no sales. The largest single products (Jack Daniels, Jameson, Grey Goose, Ketel One) hold only about $2.8M at retail, so there is no single-product dependence.

### Root Cause

A long tail of brands whose stock is high relative to sales; reorder points are not tied to sales velocity.

### Recommendation

Lower reorder points on 180+ day items and mark down or return no-sales stock.

### Expected Business Impact

Up to $10.6M of working capital is tied up (not all of it releasable).



## Q6. Which Cities Hold the Most Stock?

### Observation

Inventory is well spread: Mountmend holds 12.2%, Eanverness 8.5% and Doncaster 7.8%. The top 3 cities hold 28.5% across 67 cities.

### Root Cause

Stock follows the store network; there is no concentration problem.

### Recommendation

No rebalancing needed. Monitor quarterly and focus on slow-moving stock instead.

### Expected Business Impact

Low risk.



## Q7. Are Procurement Volumes Aligned with Vendor Profitability?

### Observation

Certain vendors receive high procurement volumes despite weak profitability.

### Root Cause

Procurement decisions focus on volume rather than margin performance.

### Recommendation

Introduce Profit Margin and Gross Profit per Unit as procurement KPIs.

### Expected Business Impact

Improve procurement effectiveness and portfolio profitability.



## Q8. Are Freight Costs Proportionate to Procurement Activity?

### Observation

Freight is a flat 0.51% of spend for every vendor (range about 0.46% to 0.54%), $1.64M in total.

### Root Cause

Freight is charged in proportion to purchases, so no vendor stands out.

### Recommendation

No vendor-specific action; review freight terms only at contract renewal.

### Expected Business Impact

No material savings available from freight; effort is better spent on margin and slow stock.


# Dashboard Pages

### Page 1 - Overview

KPIs (spend, gross profit, weighted margin, inventory, turnover, freight), spend treemap, gross profit by vendor, inventory by city, turnover by vendor, and an attention panel.

### Page 2 - Supplier Risk

Spend-vs-margin quadrant, spend concentration (Pareto), renegotiation shortlist, and a loss-making vendor check.

### Page 3 - Inventory & Procurement

Stock by product and city, stock health by days of supply, units purchased, freight as % of spend, and procurement actions.

### Page 4 - Insights & Actions

Eight business questions with findings, recommended actions and expected impact. A hidden Vendor Detail page supports drill-through. Every page has reset-filter bookmarks and a last-refreshed stamp.



# Technology Stack

### Analytics

* Power BI
* DAX
* SQL
* PySpark

### Data Engineering

* Microsoft Fabric
* Dataflows Gen2
* Lakehouse
* Fabric Pipelines

### Governance

* Semantic Model
* Row-Level Security (RLS)



# Business Impact

* Identified supplier concentration risk: the top 3 vendors account for 32% of procurement spend.
* Showed that only 13 small vendors lose money ($33K), while up to $7.4M of margin upside sits with 12 large vendors earning below the 28.7% portfolio margin.
* Found $10.6M (19%) of inventory with 180+ days of supply, including $0.4M with no sales.
* Showed that inventory is well spread across 67 cities and that freight is a flat 0.51% of spend, so neither needs action.



# Dashboard Preview


### Business Performance Overview

<img width="1157" height="664" alt="image" src="https://github.com/user-attachments/assets/cf0f4087-d203-443f-8b04-b9e5089920d7" />


### Supplier Risk and vendor performance

<img width="1132" height="635" alt="image" src="https://github.com/user-attachments/assets/529204d5-b2f6-41b5-b0f9-6dc16c5417f4" />



### Inventory & Procurement Optimization

<img width="1118" height="626" alt="image" src="https://github.com/user-attachments/assets/4d3cc9b1-f6a2-4fcf-b54b-6425088aaedf" />



### Business Insights Dashboard

<img width="1104" height="622" alt="image" src="https://github.com/user-attachments/assets/5e9c5d64-a182-45fd-8336-e042ecc34926" />


### Fabric Pipeline

[<img width="1477" height="732" alt="Master Pipeline" src="https://github.com/user-attachments/assets/0a350d72-2833-4440-9b2a-09ac4bd474f1" />

### Semantic Model
<img width="1536" height="742" alt="Semantic Model" src="https://github.com/user-attachments/assets/8eb06998-eddd-4e01-96b6-d3d4d1fd8a13" />



# Future Enhancements

* Predictive Supplier Risk Scoring
* Vendor Performance Forecasting
* Inventory Demand Forecasting
* AI-Powered Procurement Assistant
* Automated Executive Summary Generation using Azure OpenAI
