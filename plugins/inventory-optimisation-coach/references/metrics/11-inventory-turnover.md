---
title: Inventory Turnover Calculation and Interpretation
type: technique
category: metrics
confidence: High
source: Industry standard; Tenexity benchmarks for HVAC and plumbing wholesale
date_added: 2026-04-25
related: [01-working-capital-framing, 02-carrying-cost, 03-abc-classification, 10-reading-erp-inventory-export, 12-hvac-plumbing-seasonal-patterns]
tags: [turns, turnover, days-on-hand, gmroi, metrics]
---

# Inventory Turnover Calculation and Interpretation

Inventory turnover (turns) is the ratio of annual cost of goods sold (COGS) to average inventory value. It's the cleanest one-number summary of how productively a distributor is converting inventory dollars into sales. The trap is interpreting turns without context — a high turn rate isn't always good, and a low turn rate isn't always bad.

## The formula

```
Turns = Annual COGS / Average Inventory at Cost
```

Where:
- **Annual COGS** = trailing 12 months of cost-of-goods-sold (sales × (1 − gross margin), or pulled directly from the P&L).
- **Average inventory at cost** = (beginning inventory + ending inventory) / 2 at replacement or weighted-average cost. Monthly averages are better than two-point averages if the data is available.

Inverse: **Days on hand (DOH) = 365 / Turns.** If turns = 6, DOH = 60 days. Distributors often think in days more naturally than in turns; switch back and forth as the conversation needs.

## Healthy ranges by category in HVAC and plumbing wholesale

Turns vary significantly by product category. Aggregate turns are useful as a top-line trend but mislead if compared to "industry average" without category mix awareness.

| Category | Healthy turns | Healthy DOH |
|----------|---------------|-------------|
| HVAC equipment (condensers, air handlers, package units) | 4–6 | 60–90 days |
| HVAC parts and components | 3–5 | 75–120 days |
| Plumbing — copper, PEX, PVC pipe and fittings | 6–10 | 36–60 days |
| Plumbing — fixtures and faucets | 3–5 | 75–120 days |
| Water heaters | 5–8 | 45–75 days |
| Tools and small accessories | 4–6 | 60–90 days |

**Aggregate distributor average:** 4–6 turns is healthy. Above 8 is unusually high (and often signals frequent stockouts, not great efficiency). Below 3 is a working-capital problem worth investigating.

## When high turns are a problem, not a win

Three scenarios where high turns hide damage:

1. **Stockout-driven.** Turns are high because the distributor is running out of stock and customers are buying elsewhere. Sales suffer; turns look great. Cross-check against fill-rate metrics — if fill rate is below 95% on A-tier SKUs, the turns aren't a sign of efficiency.

2. **Mix shift toward commodities.** A shift away from specialty product (high margin, slower turns) toward commodity product (low margin, fast turns) raises aggregate turns but compresses gross profit dollars. Check whether GMROI is moving in the same direction.

3. **A-tier focus, C-tier neglect.** Distributors who ruthlessly trim C-tier inventory boost turns but lose breadth-of-line — and breadth-of-line is what differentiates a distributor from a big-box reseller. Trim with intent, not by formula.

## GMROI: the better single metric

For the sharpest single-number view, use **Gross Margin Return on Inventory Investment**:

```
GMROI = Gross Margin % × Turns
```

A category with 25% gross margin × 5 turns = 1.25 (interpreted as $1.25 of gross profit for every $1 of average inventory investment). Healthy GMROI for distributor categories sits in 1.0–2.5 range; below 0.8 is a category bleeding capital, above 3.0 is exceptional.

GMROI captures both efficiency (turns) and profitability (margin) in one number, which is why it's the better metric for category-level decisions. The specialist defaults to GMROI when comparing categories or product lines.

## The conversation pattern

When the user mentions turns or asks about turnover health:

1. Ask whether they have category-level turns or only aggregate. If only aggregate, suggest computing category-level — aggregate turns hide the actual problem categories.

2. Compare category turns to the healthy range above. Flag categories that are below range (working capital tied up) or unusually above range (possible stockouts).

3. Compute GMROI alongside turns where margin data is available. GMROI flips the diagnosis on at least one or two categories in most distributor reviews.

4. Avoid comparing to "industry average" without naming the source — HARDI, NAW, ASA each publish different numbers, and category mix differences make benchmark comparisons coarse. Use the ranges above as broad guides, not strict targets.

## Boundary

The specialist computes turns and GMROI from data the user pastes. It does not pull from the ERP, persist month-over-month tracking, or build a turns dashboard. Ongoing turns and GMROI dashboards are part of the paid Tenexity Inventory Optimisation pilot.
