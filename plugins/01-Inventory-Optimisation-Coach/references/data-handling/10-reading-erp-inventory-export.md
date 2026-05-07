---
title: Reading an ERP Inventory Export
type: technique
category: data-handling
confidence: High
source: Tenexity field experience across P21, Eclipse, SX.e, Agility, DDI
date_added: 2026-04-25
related: [03-abc-classification, 04-dead-stock-definition, 05-reorder-point-calculation, 11-inventory-turnover]
tags: [erp-export, p21, eclipse, sx-e, data-handling, columns]
---

# Reading an ERP Inventory Export

When the user pastes an ERP inventory export, the specialist needs to identify the columns that matter, recognise the patterns of common ERPs, and ask only the questions that the export can't answer. Most distributor exports are messy — columns named idiosyncratically, mixed case, branch identifiers buried in suffixes — and the work happens at the column-mapping step before any analysis.

## The columns that always matter

Regardless of ERP, six columns are foundational. If any are missing, ask the user to re-export with them included rather than guessing:

1. **Part number / SKU identifier.** The unique key for each SKU. May be vendor part, distributor part, or a hybrid.
2. **Description.** Free text. Useful for spotting product family patterns and obvious obsolescence ("DISCONTINUED — see #####").
3. **Branch identifier.** Almost always present, even on single-branch exports.
4. **On-hand quantity.** Units physically present.
5. **On-hand value.** Replacement or weighted-average cost × on-hand quantity. Some exports show only one of cost or value; if value is missing, ask for unit cost so the math can be done.
6. **Trailing-period sales** (units, revenue, or both). The signal that determines dead vs. slow vs. moving. Trailing-12-month is ideal; trailing-90-day is acceptable for fast-moving categories but inadequate for full dead-stock work.

## Useful but not strictly required

Four more columns that improve the analysis when present:

7. **Last sale date.** Confirms recency separately from total movement.
8. **Last receipt date.** Helps identify aged-stock vs. recently-received-but-not-yet-moving.
9. **On-order quantity.** Open POs not yet received. Critical for ROP work — if the user is about to receive 200 units, that changes the recommendation.
10. **Vendor.** Matters for RGA work and vendor-program reconciliation.

## ERP-specific patterns to recognise

The specialist doesn't memorise schemas, but does recognise common naming patterns:

| ERP | Typical signature |
|-----|-------------------|
| **Epicor Eclipse** | Branch column often labeled `Branch ID` or branch number prefix; often exports as fixed-width or pipe-delimited; SKUs often have leading zeros |
| **Epicor Prophet 21 (P21)** | Columns often have spaces (`Part Number`, `Last Sold`); on-hand value often labeled `Extended Cost` |
| **Infor SX.e** | Branch numeric (e.g., `Whse 01`); cost methods labeled clearly (`Average Cost`, `Replacement Cost`) |
| **DDI Inform** | Tends to come as Excel workbooks with multiple tabs; one tab per branch is common |
| **DMSi Agility** | Strong on lumber/building-products fields; pack quantity columns more visible |
| **Custom / homegrown** | Anything goes. Always ask the user to walk through what each column means before analysis |

The specialist asks the user once: "Which ERP is this from?" and uses the answer to prime expectations, but does not assume the schema — the user always walks through the column meanings.

## The mapping conversation

Before any analysis, the specialist runs a short clarification:

> "Quick check on the columns before I start the analysis. I see [list the columns from the paste]. Walk me through which one is:
> - The on-hand quantity?
> - The on-hand cost (replacement or average)?
> - The trailing-12-month sales (or whatever sales window this is)?
> - Anything else I should know about — special branch codes, dummy SKUs you use for non-stock items, etc.?"

Then confirm the mapping back before computing anything.

## What to do when the export is partial

Three common gaps and the specialist's response:

1. **Trailing-12-month sales missing — only current month or YTD.** Insufficient for dead-stock work; ask for trailing-12-month or accept a tighter scope (e.g., "we can do reorder-point analysis on what you have, but dead-stock work needs the full 12-month view").

2. **Cost missing — only on-hand quantities.** Ask for unit cost. Without cost, no working-capital math, no carrying-cost framing, no liquidation analysis. Don't proceed.

3. **Multiple branches concatenated without branch identifier.** The same SKU appears multiple times. The specialist either asks for a re-export with branch codes or treats the data as a single combined inventory (and explains the limitation that branch transfer analysis can't be done).

## Output

After mapping, the specialist confirms the working interpretation in plain English — "I'm reading this as 1,247 SKUs across 3 branches, with $4.2M total on-hand value, trailing 12 months of sales data through March 2026. Does that match what you expected to see?" — and only proceeds when the user confirms.

This single confirmation step prevents the most common failure mode in distributor inventory work: building a 30-page analysis on a misread export.
