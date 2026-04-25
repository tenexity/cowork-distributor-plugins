# About Me file scoring guide

Use this to consistently score each About Me file during the health check. The goal is to distinguish between files actually helping Claude understand the distributor versus files that exist but aren't doing much.

## about-me.md

| Score | What it looks like |
|-------|-------------------|
| Empty | File missing or blank |
| Template | Contains bracketed placeholders like `[Replace with...]` or "Default profile (delete once replaced)" blocks still present |
| Shallow | Has a company name and a role but no specifics — no branches named, no ERP named, no top vendors, no customer mix. Example: "I work at a plumbing distributor. We use ERP software." |
| Good | Has specific details: company name, branch count or locations, named ERP, revenue range, product mix, customer mix, key vendors at least in the Key Terms section. You could write a relevant vendor email for this distributor. |
| Strong | Deeply specific. Includes rep team structure, key-account segmentation, branch codes, buying-group affiliation, industry association membership, specific tool-specific workflows. You could generate content that sounds like this specific company without additional context. |

## voice-profile.md

| Score | What it looks like |
|-------|-------------------|
| Empty | File missing or blank |
| Template | Still has the pre-filled defaults with no customisation — no contrarian beliefs edited, no natural phrases changed from defaults |
| Shallow | Has 1-2 brief answers. No clear perspective or distributor-specific personality comes through. |
| Good | Has answers in at least 3 sections. A clear perspective emerges — you can tell this is a contractor-side-of-the-counter person, or a vendor-side, or a margin-obsessed CFO, or a service-obsessed owner. Audience-specific communication patterns described. |
| Strong | Deeply filled in. Beliefs about distribution, audience-specific voice (customer vs vendor vs team), hard boundaries, and natural speech patterns are all specific and personal. The voice profile alone could guide a full vendor QBR prep. |

## writing-rules.md

| Score | What it looks like |
|-------|-------------------|
| Empty | File missing or blank |
| Template | Has the universal anti-AI and anti-SaaS-jargon sections (which ship pre-filled) but the "Your voice" section is empty or has only template prompts |
| Shallow | Has 1-2 personal preferences added but generic ("Be friendly"). The universal sections are doing all the work. |
| Good | Has specific personal rules — tone in 3-5 words, spelling (American/British), at least 2-3 always-do rules that are clearly this distributor's, at least 2-3 never-do rules, some natural phrases. The universal sections + personal rules together create a distinctive style. |
| Strong | Personal voice section is detailed with industry-specific examples, natural phrases (specific distributor-trade language), format preferences, audience-aware rules (customer tone differs from vendor tone differs from team tone). Writing produced with this file sounds noticeably different from default AI output and noticeably different from other distributors' output. |

## my-context-map.md

| Score | What it looks like |
|-------|-------------------|
| Empty | File missing or blank |
| Template | Has the pre-filled tool tables but no ERP specified (still listed as "Eclipse / P21 / SX.e / other"), no vendors named, no actual tools filled in |
| Shallow | Lists 2-3 tools with minimal description. Example: "Eclipse — ERP. Gmail — email." |
| Good | Lists main tools with what they're used for. ERP is named specifically. Top vendors listed. Claude could route requests to the right tool. Example: "Epicor Eclipse 9.0.2 — ERP, pull monthly dead-stock, AR aging, margin by vendor. Bradford White portal — water heater pricing and warranty. Trade Service — competitive pricing checks." |
| Strong | Comprehensive tool map: ERP specified with version, specific reports named, top 10-20 vendors listed with portal URLs or notes, buying-group affiliation noted, local folder paths if applicable, manufacturer portals categorised. Claude could find a specific file or know exactly which portal to reference without asking. |

## specialist-routing.md

| Score | What it looks like |
|-------|-------------------|
| Empty | File missing or blank |
| Template | Has the 10 pre-seeded domains but no prioritisation, no installed plugins registered |
| Shallow | Domains reordered once but vaguely. No named pain points. |
| Good | Installed plugins (if any) are correctly listed. Top 3 priority domains are clearly flagged with specific distributor pain points (e.g., "Pricing and rebate management — priority because we've missed two Carrier Q4 claims in the last 18 months"). |
| Strong | Installed plugins match RESOURCES/PLUGINS/ folder. Top 3 priority domains each have a specific business-impact statement. Tenexity pilots listed in the routing file match the distributor's actual pain points. Clear map of what's covered, what's wishlist, what's a Tenexity candidate. |

## memory.md

Memory is scored on health, not depth:

| Score | What it looks like |
|-------|-------------------|
| Empty | No entries beyond the install entry |
| Sparse | Fewer than 5 entries, or no entries in the last 30 days |
| Active | Regular entries following the expected format, recent activity within the last 2 weeks |

## Scoring notes

- **Don't penalise files for being brief** if the distributor's situation is simple. A one-branch 3-person distributor doesn't need a 500-word context map.
- **Do penalise files for being generic.** "We sell plumbing stuff" is shallow regardless of word count. The whole point is distributor-specific detail.
- **Default-archetype content counts as Template, not Good.** The pre-filled "HVAC and plumbing wholesale distributor" defaults in the files are templates until customised. A file that still has "[Replace with your name...]" prompts or "Default profile (delete once replaced)" blocks is Template, not Shallow.
- **A file can be Good even if not every section is filled in.** The question is: does this file meaningfully help Claude do better work for this specific distributor? Branches can be listed elsewhere if the company is single-branch.
- **Template placeholders are always a critical flag** — they mean onboarding wasn't completed. Flag for return to the Onboarding Coach.
