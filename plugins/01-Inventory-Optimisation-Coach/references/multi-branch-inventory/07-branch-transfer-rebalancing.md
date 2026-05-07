---
title: Branch Transfer Rebalancing
type: framework
category: multi-branch-inventory
confidence: High
source: Tenexity field experience; multi-branch HVAC and plumbing distribution
date_added: 2026-04-25
related: [03-abc-classification, 08-slow-mover-triage, 09-vendor-return-rga]
tags: [branch-transfer, rebalancing, multi-branch, working-capital-recovery]
---

# Branch Transfer Rebalancing

In a multi-branch distributor, the same SKU often shows up as overstocked at one branch and understocked or stocked-out at another at the same time. Rebalancing — moving inventory between branches before reordering or liquidating — typically recovers 5–12% of working capital on the rebalanced portion of the catalogue, and protects against the embarrassment of buying more of something the company already owns.

## When rebalancing is worth doing

Two preconditions:

1. **Multi-branch distributor with branch-level visibility into inventory.** If the ERP already shows "available across all branches" and the branches transfer freely, this isn't a rebalancing problem — it's already solved.

2. **Real friction between branches.** Most distributors have at least some friction: branch managers protect their stock, transfers are slow because nobody owns them, the freight cost between branches is treated as real even though it's between the same company. Rebalancing matters most where this friction has accumulated visible imbalance.

If neither precondition holds, point the user at dead-stock liquidation (entry 04) instead — single-branch distributors don't have a rebalancing lever.

## The rebalancing matrix

For each SKU above the working-capital threshold (typically $1,000+ on-hand value somewhere in the network), build a small matrix:

| Branch | On-hand | Trailing-12-mo demand | Months of supply |
|--------|---------|----------------------|------------------|
| Branch A | 240 units | 36 units | 80 months |
| Branch B | 0 units | 60 units | 0 months |
| Branch C | 12 units | 18 units | 8 months |

A SKU is a transfer candidate when one branch has more than 12 months of supply AND another branch has less than 2 months OR is currently stocked-out.

## How to size the transfer

Two principles:

1. **Don't move a branch from overstock to stockout.** Leave the source branch with at least 6 months of supply at its own demand rate. The goal is rebalancing, not creating a new problem at the source.

2. **Bring the destination branch to its own ROP, not to whatever the source branch had.** Each branch has its own demand pattern; the destination's ROP is the right target. (See entry 05 for ROP math.)

So in the example above, transfer from Branch A to Branch B: leave Branch A with 6 × 36/12 = 18 units (6 months at 3 units/month), transfer 60 × ~2 = 120 units to Branch B (enough for ~2 months at Branch B's rate plus safety stock), and the remaining 60 units stay at A as deeper buffer. That's one transfer instead of either an emergency vendor order or a full liquidation.

## What to watch for

Three patterns the specialist surfaces:

1. **The "owns the SKU" branch.** Many distributors have one branch that's the de facto stocking branch for slow movers — usually the largest branch or the one closest to the warehouse. Over time, that branch absorbs everyone's mistakes. The rebalancing recommendation often goes the other way — out of the de facto branch and back to where demand actually lives.

2. **Discontinued-at-vendor SKUs.** A SKU the vendor has discontinued or is end-of-life-ing should be aggressively rebalanced to wherever it's most likely to sell, not held at multiple branches "just in case." Confirm vendor status before recommending; if the user can't confirm, recommend they ask the vendor.

3. **Project-tail residuals.** A SKU brought in for one branch's contractor project, where the contractor took 80% and the residual is sitting at that branch with no remaining sell-through. Other branches may have actual demand; this is a high-yield rebalance.

## Output

A branch transfer recommendation list, sorted descending by working-capital release (units transferred × replacement cost). Each line shows:

- Part number, description
- Source branch + units to transfer
- Destination branch + units to receive
- Estimated freight cost (user's estimate; vary by branch distance)
- Net working-capital effect (= units × replacement cost at the source branch, less freight)

The specialist explicitly does not recommend transfers where the round-trip freight cost exceeds 30% of the working-capital release — at that point, the math has flipped and a different lever (liquidate, RGA, or hold) is better.

## Boundary

The specialist produces the recommendation. It does not initiate transfers, generate transfer paperwork, or commit dollars. Branch managers and the inventory ops team execute in the ERP. **Automated transfer recommendations and execution are part of the paid Tenexity Inventory Optimisation pilot.**
