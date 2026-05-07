---
title: Reorder Point Calculation
type: framework
category: replenishment
confidence: High
source: Industry standard; Tenexity field-tuning for distributor lead-time variability
date_added: 2026-04-25
related: [03-abc-classification, 06-economic-order-quantity, 10-reading-erp-inventory-export, 12-hvac-plumbing-seasonal-patterns]
tags: [rop, reorder-point, replenishment, safety-stock, lead-time]
---

# Reorder Point Calculation

The reorder point (ROP) is the on-hand quantity at which a SKU should trigger replenishment. Calculated correctly, ROPs hold service levels at target while keeping working capital lean. Calculated lazily — the way most distributors do it — they create simultaneous overstocks on slow movers and stockouts on fast movers.

## The standard formula

```
ROP = (Average Daily Demand × Lead Time in Days) + Safety Stock
```

Three inputs:

1. **Average daily demand (ADD).** Units sold per day, computed over the relevant historical window. For most SKUs, use trailing 90 days; for highly seasonal SKUs, use trailing same-90-days last year.

2. **Lead time.** Calendar days between placing the PO and stock being available to sell. Includes vendor lead time + transit time + receiving time. Get this from the user — actual lead times in HVAC and plumbing wholesale vary wildly by vendor and by current allocation pressure.

3. **Safety stock.** A buffer to absorb demand spikes and lead-time variability. The crude version is "X days of demand"; the rigorous version uses the standard deviation of demand × a service-level Z-factor.

## The safety stock math (the part most distributors skip)

```
Safety Stock = Z × σ × √Lead Time
```

Where:
- **Z** = the service-level multiplier. Common targets:
  - 90% service level → Z = 1.28
  - 95% service level → Z = 1.65
  - 97.5% service level → Z = 1.96
  - 99% service level → Z = 2.33
- **σ** = standard deviation of daily demand (in units)
- **√Lead Time** = square root of the lead time in days

The square-root term is what most distributors miss. Doubling the lead time doesn't double the safety stock — it multiplies it by 1.41. This matters when comparing a domestic vendor (5-day lead time) to an overseas vendor (30-day lead time): the safety stock requirement is 2.4× higher, not 6× higher.

## Service level by ABC tier

Different SKU tiers warrant different service-level targets:

| Tier | Service level target | Z-factor |
|------|---------------------|----------|
| A | 97.5–99% | 1.96–2.33 |
| B | 95% | 1.65 |
| C | 90% | 1.28 |
| D | 50–80% (or no replenishment) | 0–0.84 |

Setting C-tier SKUs to 99% service level is the single most common reason distributors carry too much working capital in inventory. Each percentage point of service level above the right tier is roughly an extra 5–10% of inventory dollars on that SKU, with diminishing return.

## How the specialist applies this

Three workflows:

1. **ROP audit.** Pull current ROPs from the export, recalculate using the formula and the user's actual lead time + demand history, flag SKUs where current ROP is more than 20% off the calculated value (in either direction).

2. **Tier-based reset.** Reset all ROPs by ABC tier — A tier to 97.5%, B to 95%, C to 90%, D to no automatic replenishment. This typically releases 8–15% of inventory working capital on a $30M distributor, more on larger ones with looser historical discipline.

3. **Lead-time validation.** Ask the user when they last refreshed lead times in their ERP. If "more than a year ago," that alone is the most important fix — ROPs computed against stale lead times are wrong even when the formula is right.

## Boundary

The specialist explains the math, computes recommended ROPs, and produces a SKU-level worksheet the user takes to their ERP. **It does not push ROPs back to the ERP** — that's the paid Tenexity pilot.
