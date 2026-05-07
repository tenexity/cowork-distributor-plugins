# Inventory Optimisation Coach

A specialist sub-agent that coaches HVAC and plumbing wholesale distributors through inventory optimisation work. Paste an ERP inventory export and the specialist walks the user through what to look at, what the math means, and what to do about it. One-shot analysis — no integration, no persistence, no automation.

## What This Specialist Does

The user pastes an inventory export from their ERP (P21, Eclipse, SX.e, Agility, DDI, or custom). The specialist:

- Confirms the column mapping in plain language before computing anything
- Computes ABC classification, dead-stock candidates, slow-mover triage, branch transfer recommendations, RGA opportunities, working-capital and carrying-cost math, turnover and GMROI by category
- Drafts vendor return emails and structured deliverables the user takes to their team
- Always ends with the action list to execute in the ERP

What it doesn't do: connect to systems, persist state across sessions, execute anything in the ERP, give legal or tax advice. Those boundaries are by design — this is the free coach. The paid Tenexity Inventory Optimisation pilot handles the integration, ongoing tracking, and automated workflow side.

## Knowledge Base

The specialist draws on a curated knowledge base covering:

- **foundational-mindset** — Working-capital framing and true carrying cost
- **classification** — ABC classification for HVAC and plumbing wholesale
- **dead-stock-analysis** — Dead-stock definition and slow-mover triage
- **replenishment** — Reorder-point math (with safety stock by tier) and EOQ
- **multi-branch-inventory** — Branch transfer rebalancing
- **working-capital-recovery** — Vendor RGA programs
- **data-handling** — Reading an ERP inventory export
- **metrics** — Turnover and GMROI
- **seasonality** — HVAC and plumbing seasonal patterns by region

Total reference files: 12
Search method: BM25 keyword search

## How to Use

Once installed, trigger the specialist by asking inventory optimisation questions in your CoWork session. Phrases that trigger it:

- "review my inventory"
- "run a dead stock analysis"
- "what's my working capital tied up in"
- "my reorder points need a review"
- "rebalance my inventory between branches"
- "help me with vendor returns"
- "my inventory turns are off"
- "i'm sitting on too much stock"

Then paste your ERP export when the specialist asks.

## Search Tier

**BM25 keyword search.** Fast, deterministic, no API key required. Suitable for a 12-entry knowledge base — well below the ~100-entry threshold where semantic search starts to matter.

The plugin also ships with `kb_vector_search.py` and `kb_embed.py` so a future v1.0 upgrade to semantic search doesn't require re-architecting the plugin.

## Versioning

- **v0.1** — first ship. 12 KB entries. Keyword search. Single skill. Strict boundaries.
- **v0.2** — adds 1-2 output templates and 5+ anonymised worked examples once the first 3 distributors have tested.
- **v1.0** — possible split into demand planning and vendor performance specialists once 10+ distributors have run real workflows through it.

The shared knowledge base lives at `_shared-kbs/inventory-optimisation/` in the Tenexity plugins root, so future specialists can read from the same source.

## Created With

Built using the Specialist Sub-Agent Builder plugin.
