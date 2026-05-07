---
title: Economic Order Quantity (EOQ)
type: framework
category: replenishment
confidence: Medium
source: Industry standard; Tenexity caveats for distributor real-world friction
date_added: 2026-04-25
related: [02-carrying-cost, 05-reorder-point-calculation]
tags: [eoq, order-quantity, replenishment, vendor-minimums]
---

# Economic Order Quantity (EOQ)

EOQ is the order quantity that minimises the total cost of ordering plus carrying inventory. It's the textbook answer to "how much should we order each time?" The textbook formula is useful — but the textbook answer is rarely directly applicable in HVAC and plumbing wholesale, because vendor minimums, pack quantities, freight tiers, and rebate thresholds usually override the math.

## The textbook formula

```
EOQ = √((2 × D × S) / H)
```

Where:
- **D** = annual demand in units
- **S** = cost per order placed (administrative cost — typically $20–$60 per PO line in distributor reality)
- **H** = annual carrying cost per unit (replacement cost × carrying cost rate; see entry 02)

Example: a SKU with annual demand of 1,200 units, $40 ordering cost, $5 unit cost, 24% carrying cost. EOQ = √((2 × 1,200 × 40) / (5 × 0.24)) = √(80,000) = **283 units per order**.

That math says order ~280 units roughly four times per year.

## Why textbook EOQ usually doesn't survive contact with reality

Five real-world overrides:

1. **Vendor pack quantities.** The vendor only ships in cases of 50 or pallets of 144. Round to the nearest pack.

2. **Freight tier breaks.** Vendors typically have free-freight thresholds (often $2,500 or $5,000). If EOQ falls just below that threshold, increasing the order to hit the threshold often saves more in freight than it costs in extra carrying.

3. **Vendor minimum order quantity (MOQ).** Many vendors require minimum POs ($1,500, $5,000, etc.). If EOQ × replacement cost falls below the MOQ, the actual order has to be larger.

4. **Rebate thresholds.** Volume rebates often kick in at quarterly or annual purchase thresholds. Pulling demand forward to hit a rebate tier can be worth more than the carrying cost of a few extra weeks of stock. (See the Rebate Reconciliation Specialist for the rebate side of this math.)

5. **Allocation conditions.** When a vendor is on allocation (common in HVAC during peak season), order quantities are dictated by vendor allocation, not EOQ.

The specialist computes the textbook EOQ as a **starting point**, then asks the user about each of these five constraints before proposing a final reorder quantity.

## When EOQ is genuinely useful

Two situations where the math holds well:

1. **Mid-velocity SKUs from in-stock vendors with low MOQ.** B-tier SKUs that aren't on allocation, where the vendor has flexible pack sizes — EOQ math gives a cleaner answer than gut.

2. **Auditing whether current order quantities are dramatically off.** A SKU where current standing-order quantity is 5× or 1/5× the EOQ is worth a closer look, even if neither extreme is the right answer.

## When EOQ is misleading

Two situations where it's actively harmful:

1. **Highly seasonal SKUs.** Annual demand averaged over 12 months hides the fact that 80% of demand falls in 3 months. Use seasonal logic instead — pre-season build-up, in-season maintenance orders.

2. **A-tier SKUs with frequent in-and-out movement.** For these, fill rate matters far more than ordering cost — order more frequently than EOQ suggests, just to keep the safety stock low and the turns high.

## How the specialist applies this

Used as one input among several in a reorder-quantity recommendation, never as the only input. The output should always show:

- Textbook EOQ
- The constraints that override it (pack quantity, MOQ, freight tier, rebate threshold)
- The proposed order quantity after applying constraints
- The user's call on whether to deviate

Confidence on this entry is **Medium** because the formula is well-established but its applicability to distributor reality is partial. Use the math, but use it carefully.
