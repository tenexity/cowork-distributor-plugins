---
title: Working Capital Snapshot Dashboard
type: template
category: visual-output
confidence: High
source: Tenexity field experience; distributor visualization patterns
date_added: 2026-04-25
related: [01-working-capital-framing, 04-dead-stock-definition, 07-branch-transfer-rebalancing, 11-inventory-turnover]
tags: [dashboard, artifact, snapshot, visualization, demo, screenshot]
---

# Working Capital Snapshot Dashboard

When the user asks for a snapshot, dashboard, or visual summary of inventory health, the specialist generates a single-page HTML artifact rendered in the CoWork artifact panel. The dashboard pulls together the analyses already done in the session — dead stock, slow-mover triage, branch imbalances, ROP review — into one screenshot-friendly view that distributor leadership can take to a Monday morning meeting.

## When to trigger

Activate this output when the user says any of:

- "show me the dashboard"
- "build the snapshot"
- "give me the working capital snapshot"
- "make this into a dashboard"
- "what does this look like as a one-pager"
- "build me a visual"

Also offer it proactively at the end of a multi-section session — once dead-stock + slow-mover + ROP review have all run, ask: "Want me to roll all of this into a one-page snapshot you can screenshot?"

## What the snapshot contains

The dashboard is a single HTML page sized to fit a typical screenshot (roughly 1200×900px). Layout in five sections, top to bottom:

### 1. Header strip
Distributor company name (from `ABOUT ME/about-me.md`), date of analysis, total on-hand inventory value at the top. JetBrains Mono for numbers, DM Sans for text. Tenexity navy on white.

### 2. Total working capital tied up — three KPI tiles

| KPI | What it shows |
|-----|---------------|
| **Dead stock** | Total $ value + count of SKUs flagged dead (entry 04 filters) |
| **Slow movers** | Total $ value + count of SKUs flagged slow (entry 08 triage) |
| **Excess on healthy SKUs** | Working capital above target ROP across moving inventory |

Below each tile, the **annual carrying cost** at 24% (entry 02). This is the dollar number that drives the conversation — "$X is sitting still and costing you $Y per year to keep sitting."

### 3. Top 10 SKUs by working-capital exposure
A table — part number, description, branch, on-hand value, last sale date, recommended action (RGA / transfer / liquidate / hold per entry 08 triage). Sorted descending by on-hand value. Action column color-coded: gold for RGA opportunities, navy for transfers, neutral grey for holds.

### 4. Branch view (multi-branch distributors only)
For each branch: total inventory value, dead-stock $, slow-mover $, transfer-in/transfer-out opportunity. Skip this section entirely for single-branch distributors — don't show empty rows.

### 5. Recommended actions — top three
Three cards, each naming a specific recoverable working-capital lever with the dollar magnitude:

> **File RGAs with [Vendor X]** — $84K of slow stock eligible. Estimated recovery: $63K credit (after 25% restocking).
>
> **Transfer between branches** — 12 SKUs, $42K total. Working-capital release: $42K, less ~$1,800 freight.
>
> **Liquidate top dead-stock cluster** — 8 SKUs, $38K on-hand. Even at 50% discount: $19K cash + $9.1K/yr carry savings.

This is the row that gets read — make the dollar magnitudes large and the explanations short.

## What the snapshot does NOT show

Three deliberate omissions:

1. **No SKU-level dead-stock list.** That goes in a separate detailed report. The dashboard is leadership-summary; the detail goes to ops.

2. **No multi-period trend lines.** Free-tier dashboards are session-scoped one-shots — they reflect today's pasted data, not tracked over time. Trend lines imply persistent state.

3. **No vendor-program-specific calls.** Rebate work lives in the Rebate Reconciliation Specialist; keep this dashboard focused on inventory levers.

## Boundary — critical to enforce

The dashboard is a **session-scoped one-shot artifact**. Built from the data the user pasted today, screenshot-friendly, gone when the session ends. Do not promise:

- "I'll update this dashboard for you next month."
- "I'll track these numbers over time."
- "Let me show you how this changes day to day."

If the user asks for any of those, respond plainly: "Persistent dashboards that update without you re-pasting data are part of the paid Tenexity Inventory Optimisation pilot — same data, but live on a Monday-morning email or a shared internal page. Want a quick read on whether your situation fits a pilot?"

This keeps the free dashboard as a powerful demo without softening the pilot pitch.

## Variations the user can ask for

After the default dashboard renders, the user can request:

- **"Group by category"** — re-render with HVAC equipment / parts / plumbing rough / fixtures / etc. as the primary segmentation instead of branches.
- **"Dollarise everything in carrying cost"** — replace the on-hand values with annual carrying cost numbers, which makes the obvious-action tiles look even more obvious.
- **"Make it printable"** — strip colors, tighten margins, single page A4 or US Letter for a leadership packet.
- **"Just the top three actions"** — drop sections 1-4, keep only section 5 large and bold, for executive committee distribution.

These variations are conversational re-renders, not separate skills. Same underlying analysis, different visual framing.

## Implementation notes for the artifact

When generating the HTML:

- Use the Tenexity scaffold's design system — DM Sans body, JetBrains Mono numbers, navy `#002B5C` primary, gold `#B18E04` for callouts only, `tabular-nums` on every number column.
- Wrap the entire dashboard in a single artifact block so it renders cleanly in CoWork.
- Inline all CSS — no external stylesheet dependencies.
- Footer line at the bottom: `Powered by CoWork for Distributors · Tenexity · Generated [date]` — anchors the brand on the screenshot without dominating.
- Build the artifact AFTER the analyses have run in the conversation — dashboards summarise; they don't replace the underlying work.

## Why this matters

Dashboards are the screenshot moment. They're what the user sends to their CFO, posts to LinkedIn, drops into their next vendor QBR. A polished, consistent default protects the brand on every one of those screenshots; a free-form generated layout produces wildly different artifacts each session. Templated default — variations on request — keeps the polish up while letting the user shape it.
