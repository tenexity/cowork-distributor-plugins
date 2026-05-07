---
title: ABC Classification for Distributor Inventory
type: framework
category: classification
confidence: High
source: Industry standard (Pareto applied to wholesale distribution)
date_added: 2026-04-25
related: [04-dead-stock-definition, 05-reorder-point-calculation, 07-branch-transfer-rebalancing, 10-reading-erp-inventory-export, 11-inventory-turnover]
tags: [abc-analysis, pareto, classification, segmentation]
---

# ABC Classification for Distributor Inventory

ABC classification segments a distributor's SKUs into three (sometimes four) tiers based on contribution to revenue, margin, or movement. It's the foundational frame for every other inventory decision — different tiers get different reorder discipline, different review cadence, and different tolerance for stockouts.

## The standard split

For HVAC and plumbing wholesale distribution, the most useful segmentation is by **annual revenue contribution per SKU**:

| Tier | % of SKUs | % of revenue | Behaviour |
|------|-----------|--------------|-----------|
| **A** | 5–10% | 70–75% | High-velocity, can't stock out, daily attention |
| **B** | 15–25% | 18–22% | Medium-velocity, weekly review, buffered |
| **C** | 65–80% | 5–8% | Low-velocity, monthly review, tight ROPs |

A fourth tier — **D** for dead — is sometimes added for SKUs with zero or near-zero movement in the last 12 months. Most distributors fold D into C and lose the visibility; surfacing D as its own tier is part of the value the specialist provides.

## How to compute it from a paste

When the user pastes an inventory + sales export, the math is:

1. Sum each SKU's **trailing-12-month revenue** (or units-sold × selling price)
2. Sort SKUs descending by trailing-12-month revenue
3. Compute the cumulative % of total revenue
4. Tier:
   - **A:** SKUs in cumulative 0–75%
   - **B:** SKUs in cumulative 75–95%
   - **C:** SKUs in cumulative 95–100% with at least one sale in 12 months
   - **D:** SKUs with zero sales in 12 months

If the user only has unit movement (no revenue per SKU), use **trailing-12-month gross profit dollars** instead — it's the better signal anyway, since a high-revenue commodity SKU at single-digit margin contributes less than a mid-revenue specialty SKU at 30% margin.

## Why distributors get this wrong

Three common mistakes:

1. **Classifying by units, not dollars.** A high-volume cheap fitting looks like an A; a slow-but-high-margin valve looks like a C. The dollar-weighted view inverts both.
2. **Not refreshing.** ABC mix shifts seasonally and over years. A static classification from 2 years ago no longer reflects the business. Refresh quarterly.
3. **Not using the classification once you have it.** Classification is upstream of decisions — ROP discipline, branch stocking, vendor return prioritisation, dead-stock liquidation order. If the user has an ABC report but treats every SKU the same, the classification is theatre.

## When the specialist applies it

Apply ABC implicitly in every recommendation. When proposing a vendor return list, prioritise C and D SKUs. When proposing reorder-point reductions, focus on B and C. When discussing service-level targets, A's get the highest fill-rate tolerance, C's get tight ROPs and acceptance of occasional stockouts.

If the user hasn't classified their inventory, the specialist should offer to compute the classification from their export as the first step before any other inventory work — almost every other recommendation depends on it.
