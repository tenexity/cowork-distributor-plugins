---
title: HVAC and Plumbing Seasonal Inventory Patterns
type: reference
category: seasonality
confidence: Medium
source: Tenexity field experience; HARDI seasonal sales reports
date_added: 2026-04-25
related: [04-dead-stock-definition, 05-reorder-point-calculation, 08-slow-mover-triage, 11-inventory-turnover]
tags: [seasonality, hvac-season, plumbing-season, peak-demand, allocation]
---

# HVAC and Plumbing Seasonal Inventory Patterns

Seasonality is the single biggest reason naive inventory math fails in HVAC and plumbing wholesale. A reorder-point computed against trailing-90-day demand in February will be catastrophically wrong by July for cooling product, and aggregate turns hide cooling/heating cross-cancellation that drowns out individual category signals. Every recommendation involving demand history should ask whether the SKU is seasonal and adjust accordingly.

## HVAC seasonal patterns

Roughly two seasons matter, with regional variation:

### Cooling season (residential)

- **Peak demand:** May–August in most of the continental US; April–September in the Southeast and Southwest; June–August in the upper Midwest and Northeast.
- **Pre-season build:** February–April. Distributors who don't pre-book allocations in this window face shortages when demand spikes.
- **Post-season slowdown:** September–October.
- **Off-season:** November–January, except for emergency/replacement.

Affected categories: condensing units, air handlers, package units, refrigerant, line sets, condenser pads, capacitors, contactors, blower motors.

### Heating season (residential and commercial)

- **Peak demand:** October–February in the upper US; November–January in the Southeast.
- **Pre-season build:** July–September.
- **Off-season:** April–June.

Affected categories: furnaces (gas and electric), heat pumps (overlaps with cooling), thermostats, ignition components, gas valves, heat exchangers.

### Allocation cycles

Vendors typically run allocation programs from **March through August** for cooling product and **August through January** for heating product. During allocation, vendor lead times stretch (sometimes from 2 weeks to 8+ weeks), and reorder points based on off-season lead times will run out. The specialist asks the user about current allocation status before recommending ROP changes during these windows.

## Plumbing seasonal patterns

Less peaky than HVAC but distinctly seasonal in two patterns:

### New construction cycle (residential)

- **Peak:** April–October in most regions.
- **Affected categories:** rough-in fittings, copper pipe, PEX, water heaters, fixtures, drain/waste/vent product.
- **Off-season demand:** primarily replacement and remodel — about 40–60% of peak.

### Frozen pipe / emergency cycle (cold regions)

- **Peak demand spike:** December–March, especially during cold snaps.
- **Affected categories:** insulation, heat tape, pipe-thaw equipment, water heater elements, emergency fittings.
- **Operational consideration:** demand spikes here are short and intense; safety stock for these categories should be sized for spike weeks, not annual averages.

## How to apply seasonality in the analysis

Three patterns the specialist watches for:

1. **Trailing 90-day demand in the wrong season.** If the user pastes a January export and asks for ROP review, trailing-90-day demand for cooling SKUs will be near zero and the formula will recommend zero stocking. Use trailing-12-month or — better — trailing-same-season-last-year for seasonal SKUs.

2. **Pre-season build vs. dead stock.** A SKU with no movement for 5 months might be dead, or might be cooling product sitting in pre-season inventory waiting for May. The dead-stock filters in entry 04 use trailing-12-month for exactly this reason — one full seasonal cycle is the minimum window for a credible dead-stock call.

3. **End-of-season residual.** Late September is the right time to look at cooling residuals; late February is the right time to look at heating residuals. These are also the highest-yield windows for vendor RGA on seasonal product — vendors often open special end-of-season RGA windows to clean their channel before next year's allocation.

## Regional adjustments

Seasonality is significantly regional. The specialist asks the user where their branches are concentrated before applying default seasonal patterns:

- **Northeast / Upper Midwest:** strong heating season, shorter cooling season, pronounced frozen-pipe spike.
- **Southeast:** longer cooling season, weaker heating season, year-round plumbing new construction.
- **Southwest:** very long cooling season (April–October), minimal heating, water heater and water treatment heavily seasonal in some sub-markets.
- **Northwest:** more even seasonality, less pronounced peaks, longer plumbing cycle.
- **Mountain / High-altitude:** heating season is dominant; cooling matters but in shorter windows.

If the user's branches span multiple regions, treat seasonal analysis at branch level, not aggregate.

## Confidence note

Confidence is **Medium** rather than High because the seasonal windows shift with weather (warmer or cooler than normal years), with construction cycles, and with broader economic conditions. Use these patterns as the default frame and ask the user to confirm the actual seasonal pattern of their business, especially during atypical years.
