---
title: Slow-Mover Triage
type: framework
category: dead-stock-analysis
confidence: High
source: Tenexity field experience
date_added: 2026-04-25
related: [02-carrying-cost, 04-dead-stock-definition, 07-branch-transfer-rebalancing, 09-vendor-return-rga, 12-hvac-plumbing-seasonal-patterns]
tags: [slow-mover, triage, decision-tree, near-dead]
---

# Slow-Mover Triage

Slow-movers — SKUs that aren't fully dead but sell less than 2 units a month and have more than 12 months of supply on hand — are the largest hidden working-capital bucket in most distributors. They escape dead-stock filters because they show "some" sales, but the carrying cost of holding them through their long sales cycle usually exceeds the gross margin on what eventually moves.

## The triage decision tree

For each slow-mover, the specialist runs the same four-question filter and routes to one of four actions.

### Q1: Is the vendor accepting RGAs (returns) on this SKU?

- **Yes** — go to Q2.
- **No** — skip RGA, go to Q3.
- **Don't know** — flag the user to confirm with the vendor; in the meantime, treat as no.

### Q2: What's the RGA cost vs. liquidation cost?

Compute both:

- **RGA path:** typically 15–25% restocking fee + freight back to vendor. If on-hand is $10K replacement cost, RGA recovers $7,500–$8,500 in credit.
- **Liquidation path:** sell to a liquidator or surplus distributor at 30–60% of replacement. $10K becomes $3,000–$6,000 cash.

RGA almost always wins when the option exists. Recommend RGA. (See entry 09 for the RGA mechanics.)

### Q3: Can the SKU be transferred to a branch that's actively selling it?

(See entry 07 for branch-transfer math.) If yes, transfer rather than liquidate — the SKU still has economic life elsewhere in the network. If no transfer destination, go to Q4.

### Q4: What's the realistic liquidation value, and is the holding-cost arithmetic in favour of liquidating?

Compute:

- **Annual carrying cost** = on-hand value × 24% (entry 02)
- **Years until likely full sell-through** at current demand rate
- **Total carrying cost** = annual × years
- **Liquidation discount required** to make the math break even = carrying cost / on-hand value

If the required discount is less than 50%, liquidate. If the required discount is more than 50%, hold and review again in 6 months — the SKU might find demand, and a 60% discount is rarely worth the operational distraction unless the on-hand value is very large.

## Worked example

A SKU with $8K on-hand, 8 units in 12 months selling at $80 each (6.4% annual gross profit at 30% margin), 0.7 units/month demand rate. On-hand is 11 months of supply.

- Annual carrying cost = $8K × 24% = $1,920
- Years to sell-through at 0.7/month = 11.4 months ≈ 1 year
- Total carrying cost over the holding period = $1,920
- Required discount to break even = 24% on a $8K SKU = $1,920

A 25% liquidation discount makes the math indifferent. Below 25% required, liquidate. Above, hold. In this case the math is right at the threshold, so the call goes to other factors — is the SKU obsolete vs. the current product line? Is there a specific customer holding the residual? The specialist surfaces the math and lets the user make the call.

## When NOT to triage aggressively

Three exceptions:

1. **Strategic SKUs.** Some slow-movers are part of a complete product line the distributor must show to be credible to the trade — e.g., the large-diameter end of a pipe line where a contractor needs to know the distributor "carries the whole line." Pulling these is brand damage that the carrying cost doesn't capture. The specialist asks the user about strategic SKUs before listing them.

2. **Replacement parts for installed base.** A SKU that doesn't move much because the underlying product is rarely serviced, but is critical when it is — common in commercial HVAC and water heater repair. Don't liquidate without checking installed-base service implications.

3. **Allocation-time holds.** During an allocation cycle (vendor restricting shipments), a slow-mover today might be a hot SKU in 3 months. If the user is in a current allocation cycle, defer triage on the affected vendor's SKUs until the cycle ends.

## Output

A triaged slow-mover list. Each row shows the recommended action (RGA / transfer / liquidate / hold) plus the reasoning (the question that routed it). The user takes the list to their team — RGA paperwork, branch transfers, liquidator contacts, or a justified hold.
