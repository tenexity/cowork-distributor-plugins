---
title: Dead Stock — Definition and Identification
type: framework
category: dead-stock-analysis
confidence: High
source: Tenexity field experience; HARDI dead-stock benchmarks
date_added: 2026-04-25
related: [03-abc-classification, 08-slow-mover-triage, 09-vendor-return-rga, 10-reading-erp-inventory-export, 12-hvac-plumbing-seasonal-patterns]
tags: [dead-stock, slow-mover, obsolescence, working-capital-recovery]
---

# Dead Stock — Definition and Identification

Dead stock is inventory that has lost its economic right to a slot on the shelf. There's no single industry-standard definition, but the working definition that holds up across HVAC and plumbing wholesale distribution is: **a SKU with zero sales in the last 12 months and on-hand quantity greater than zero.**

That's the strict definition. There's also a softer category — **near-dead** or **deeply-slow** — for SKUs with one or two sales in 12 months, where the carrying cost of remaining stock will eat the margin on any future sale.

## Three filters that work in practice

Apply all three; the SKU is dead when at least two are true:

1. **Movement filter.** Zero sales in the trailing 12 months, OR units-sold-per-month is less than 1/24th of on-hand quantity (i.e., more than 24 months of supply at current movement).

2. **Recency filter.** Last sale date is more than 12 months ago, OR last receipt date is more than 24 months ago and units have not turned over in that time.

3. **Working-capital filter.** On-hand value (units × replacement cost) exceeds a threshold that warrants action — typically $500 per SKU for a $30M distributor, $1,500+ per SKU for a $100M+ distributor. Below the threshold, the labour to research and dispose isn't worth it; bundle low-value dead stock for liquidation pallet sales.

## Why these filters and not "didn't sell this month"

Distributors get this wrong by being too aggressive (calling a seasonal SKU dead in February when its season is July) or too lenient (waiting three years to admit a SKU is gone). Twelve months captures one full seasonal cycle plus one buffer cycle — long enough to filter out seasonality but short enough to act before more carrying cost is bled.

## What's NOT dead stock

Three categories that look dead but aren't:

1. **Project stock.** A SKU brought in for a specific contractor project that's still active. Last sale was 14 months ago, but the contractor placed the project order then and will take residuals next quarter. Tag it; don't liquidate.

2. **Newly added SKUs.** A SKU added in the last 6 months that hasn't moved yet might just need time to find its market. Don't call it dead until it's had at least 9 months on the shelf.

3. **Counterpart pairs.** Some SKUs sell as pairs or sets (e.g., flange + gasket combinations). One half might show no movement because it's only sold attached to the other; pulling it kills both.

The specialist asks the user about these three categories before finalising a dead-stock list — it's the difference between a credible report and a list that gets one item liquidated and then ignored.

## Output

A dead-stock report from this framework lists, for each candidate SKU:

- Part number, description, branch
- On-hand quantity, on-hand value (replacement cost)
- Last sale date, last receipt date
- Trailing-12-month sales (usually zero)
- Carrying cost per year (24% × on-hand value, see entry 02)
- Recommended action (return to vendor, transfer to other branch, liquidate, hold with reason)

Sort the list descending by on-hand value. The top 20 SKUs typically account for 60–80% of total dead-stock dollar exposure — focus there first.

## Typical findings

For a $30M HVAC/plumbing distributor: $250K–$750K of dead stock is normal. Above $1M is a flag that the buying discipline has eroded. For $100M+ distributors: $1M–$3M is normal; $5M+ is a working-capital crisis worth a controller-level conversation.
