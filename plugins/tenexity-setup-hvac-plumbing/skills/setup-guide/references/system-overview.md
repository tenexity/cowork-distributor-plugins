# CoWork for Distributors — system overview

This is the detailed explanation of how CoWork for Distributors works. The setup guide reads this when a user wants more detail before starting.

---

## What is CoWork for Distributors?

A system that turns Claude into a personalised AI assistant tuned for HVAC and plumbing wholesale distribution. Instead of starting every conversation from scratch, Claude reads files about your company, your ERP, your vendors, your customers, and how you work. Claude remembers your preferences, follows your rules, and builds context over time — so over six months of use, Claude knows which vendors give you trouble, which contractors pay on time, which SKUs should be killed, and which reps need coaching.

Built on three top-level folders and one settings file. Each has a specific job.

## The three folders

**ABOUT ME/** contains six files that define your identity to Claude:

- `about-me.md` — who you are, your company (branches, revenue, product mix), your ERP, your customers, your role. Pre-filled with an HVAC/plumbing distributor archetype — customise during onboarding.
- `voice-profile.md` — how you communicate with contractors, vendors, and your team. Your beliefs about distribution, your instincts, your hard boundaries.
- `writing-rules.md` — how you want things written. Anti-AI patterns, anti-SaaS-jargon rules, no-invented-numbers rule, your personal tone, your banned words.
- `my-context-map.md` — where your information lives. Your ERP, manufacturer portals, price tools, rebate systems, trade associations.
- `specialist-routing.md` — which parts of distribution have specialist plugins and which are on your wishlist.
- `memory.md` — a running log of decisions, preferences, and context. Claude writes to this automatically.

**WORK AREAS/** is where all your active work lives. Six areas tuned for distributors:

- **Admin-PA** — quick tasks, system reviews, general admin (required, can't be deleted)
- **Sales-Ops** — quote desk, RFQ response, rep territory, lost-sales follow-up
- **Customer-Accounts** — key-account QBRs, contractor relationships, newsletters
- **Procurement-Vendors** — vendor QBRs, rebate programs, price negotiations, carry-line reviews
- **Inventory-Ops** — dead stock, reorder points, ABC analysis, branch transfers, seasonal stock builds
- **Finance** — AR aging, credit decisions, collections, cash flow, branch P&L

Inside each area, projects live as subfolders (always ending with `-project`). Each project has a brief, memory log, and outputs/ folder.

**RESOURCES/** contains reference material and tools:
- `MY SKILLS/` — the Onboarding Coach, System Review, and First Week Guide
- `PLUGINS/` — the Specialist Sub-Agent Builder and Personal Assistant
- `TEMPLATES/` — quote templates, vendor scorecards, QBR one-pagers, SKU rationalisation, price-increase letters, weekly reviews, decision docs, emails, invoices
- `GUIDES/` — the Prompting Cookbook, CASA Framework Guide, Good Practice Guide

## Skills vs plugins

**Skills** handle specific tasks (running a dead-stock analysis, generating a QBR one-pager, drafting an email). Built-in CoWork skills trigger automatically. Custom skills live in `RESOURCES/MY SKILLS/`.

**Plugins** are specialist agents with deep domain knowledge. A rebate specialist doesn't just track numbers — it knows the SPA/POA structure of each manufacturer, the typical threshold gotchas, and your buying-group program. A quote desk assistant doesn't just respond — it knows your margin guardrails, your substitution rules, and your customer's carry list.

Think of it this way: skills are tools (a calculator, a drafting template). Plugins are specialists who bring their own tools and domain expertise (a buyer, an AR manager).

You can build your own plugins using the Specialist Sub-Agent Builder included. You can also run Tenexity's pre-built pilots (Inventory Optimisation Coach, Rebate Reconciliation Specialist, Quote Desk Assistant, Vendor QBR Prep Specialist) if you want something ERP-connected and running automatically.

## The settings file — CLAUDE.md

CLAUDE.md lives in CoWork's settings, not in the folder structure. It contains the global rules: how Claude uses folders, how to name files, how to behave, and a quick-reference of who you are and what you need. Think of it as the OS configuration file.

Claude reads CLAUDE.md at the start of every session, before anything else. It then follows those instructions to read your ABOUT ME files, check for active projects, and prepare for whatever you need.

CLAUDE.md is pre-customised for HVAC/plumbing distributors — most users won't need to edit it beyond a quick sanity check during onboarding.

## How it all connects

**Session starts** → Claude reads CLAUDE.md → Claude reads all ABOUT ME files → Claude knows your company, your rules, your tools, your history.

**You ask for something** → Claude checks if it matches a plugin domain → If yes, plugin activates. If no, general distributor knowledge. Either way, your ABOUT ME context is always present.

**You start a new project** (a carry-line review, a QBR cycle, a dead-stock cleanup) → Claude creates a project folder (with `-project` suffix) inside the right work area, with brief, memory log, and outputs/ → Next time you work on it, Claude reads the folder first.

**Session ends** → Claude logs anything important to the relevant memory file → Next session picks up where this one left off.

## The memory system

Memory is what makes the system get better over time. Two types:

**Universal memory** (`ABOUT ME/memory.md`) captures decisions, preferences, and context that apply across all your work. Examples:
- "Switched primary condenser line from Brand A to Brand B effective April 2026"
- "Our #1 rep preference — Tom gets the key account calls, Sarah handles new-construction bids"
- "Decided not to carry commercial refrigeration — margins are thin and we don't have the expertise"

**Project memory** (`WORK AREAS/[area]/[project-name]/memory.md`) captures progress, decisions, blockers for specific work. Examples:
- "Acme Plumbing QBR — fill-rate drop spotted, reduced min/max on Rheem XE50"
- "Carrier Q2 rebate claim — corrected their $18,400 calc to $23,200 after PO audit"

Claude writes to both automatically. You glance occasionally to make sure they're accurate. If something's wrong, edit the files directly.

## Why this works for distributors specifically

Most AI tools are generic. You spend half the conversation explaining your business before you can get to the real work. This system front-loads that: your ERP, your vendors, your pain points, your voice are already in Claude's context at session start.

After a month of use, Claude knows things like:
- Your top 25 customers by name
- Your top 20 vendors and their QBR cadence
- Which SKUs are your margin-makers and which are dead weight
- How your voice shifts between writing to a contractor vs. a manufacturer VP
- What decisions you've already made and what trade-offs you've rejected

That's the compounding effect — and it's why this system was built on CoWork rather than from scratch. CoWork handles the session state, file persistence, and connector ecosystem. Tenexity built the distributor layer on top.
