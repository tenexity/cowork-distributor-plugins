---
name: vendor-pulse
description: >
  Weekly summary of vendor activity drawn from the captain's log. Triggers when the
  user says "vendor pulse", "vendor activity this week", "what's happening with my
  vendors", "weekly vendor summary", "which vendors am I overdue with", or when
  the scheduled vendor-pulse task fires. Reads the past 7 days of captain's log
  entries, counts and categorises vendor mentions, surfaces vendors going quiet,
  and proposes follow-up actions. Designed specifically for HVAC and plumbing
  wholesale distributors managing relationships with manufacturer reps and buying
  group contacts.
version: 1.0.0
---

# Vendor Pulse — Weekly Activity Summary

This skill reads the past 7 days of the user's captain's log entries and produces a vendor-focused activity summary. The point: **catch vendor signals before they become problems.** Allocation issues, rebate disputes, QBR prep windows, and going-quiet patterns all show up in conversation; this skill aggregates them so they're not lost in the noise.

## When this fires

- User asks for vendor pulse / vendor summary / "what's happening with vendors"
- Scheduled task runs weekly (typical: Friday 4 PM, configurable)
- User asks "which vendors am I overdue with" or "any vendors gone quiet"

## Sources

1. **Captain's log** — past 7 days of entries from the current month's log file (and the previous month's file if today is in the first 7 days of the month). Path: `WORK AREAS/Admin-PA/captains-log/YYYY-MM-captains-log.md`.
2. **Top vendors list** — read from `ABOUT ME/COMPANY/company-profile.md` (v2 multi-user) or `ABOUT ME/about-me.md` (v1 solo). This gives the canonical list of vendors that matter.
3. **Tasks** — `WORK AREAS/Admin-PA/tasks.md` for any vendor-tagged tasks open, completed this week, or overdue.
4. **Inventory action log** — `WORK AREAS/Admin-PA/inventory-action-log.md` for any vendor-related decisions captured this week.

## What to look for in captain's log entries

Vendor mentions are tagged or implied. Recognise these patterns:

- Direct vendor name (from the top vendors list)
- "Carrier rep called", "talked to [name] at Bradford White", "Trane visit"
- Vendor program references: "Bradford White rebate", "Carrier allocation", "Kohler co-op"
- Buying group contacts: "Affiliated", "IMARK", "Wolseley", "AD"

For each entry mentioning a vendor, classify the mention:

| Tone | Examples |
|------|----------|
| Positive | "rebate accepted", "allocation came in", "credit memo issued", "QBR went well" |
| Neutral | "rep visit scheduled", "QBR on calendar", "general check-in", "price file received" |
| Concerning | "allocation cut", "rebate disputed", "price increase", "back-order", "RGA refused", "rep changed" |

Track count per vendor + tone breakdown for the week.

## Output format

Produce a clear, scannable summary. Save to `WORK AREAS/Admin-PA/vendor-pulse-reports/Vendor-Pulse_[YYYY-MM-DD].md` (create the folder if it doesn't exist) AND surface it in chat.

```markdown
## Vendor Pulse — Week of [Monday date] to [Sunday date]

### Active this week ([N] vendors)

For each vendor with mentions this week, in descending mention count order:

- **[Vendor name]** ([N] mentions: [breakdown by tone])
  - [Brief summary of activity — pull the most important entries]
  - [Open task or follow-up if any]

### Going quiet ([N] vendors)

Vendors from your top list that haven't appeared in conversation in:

- **30+ days:** [vendor names]
- **60+ days:** [vendor names]
- **90+ days:** [vendor names — flag these as worth a check-in]

### Open vendor tasks ([N])

[List of vendor-tagged tasks from tasks.md — open or due this week]

### Concerning signals this week

[Anything in the "concerning" tone bucket — allocation cuts, disputed rebates, price increases, etc. Brief recap with proposed actions.]

### Action items

Based on what's above, propose 2-4 specific actions for next week:

1. [Action — e.g., "Schedule check-in call with Trane (90+ days quiet)"]
2. [Action]
3. [Action]
```

## Going-quiet logic

A vendor "going quiet" is a real signal — could mean the relationship is healthy and steady (good), or could mean drift before something breaks (bad). Either way, surface it.

**Threshold defaults:**
- 30+ days no mentions: list as a soft heads-up
- 60+ days no mentions: prompt a check-in
- 90+ days no mentions: flag as **worth a real call** — relationships erode this fast

If a vendor's gone quiet AND they have an upcoming QBR (check calendar or COMPANY's operational rhythm), surface that combination as the highest priority — going into a QBR cold is bad.

If a vendor's gone quiet AND they haven't shipped recently (check inventory action log or the user's recent comments about back-orders / fill rate), that's a different signal — could mean the line is dying.

## Concerning-signal handling

When you find a concerning signal in the week's mentions:

- Surface in the "concerning signals" section
- Cross-check against tasks.md — is there an open task addressing this? If yes, note the task. If no, propose creating one.
- For allocation issues: propose pulling YTD purchase volume so the user can negotiate from data
- For rebate disputes: propose putting a real claim package together (referenced against `tools-and-context.md` rebate programs)
- For price increases: check `RESOURCES/TEMPLATES/price-increase-letter-template.md` exists; offer to draft a customer letter

## Voice

Use the user's voice profile and writing rules. The vendor pulse should sound like a colleague who's been around the trade — not a marketing summary, not a SaaS dashboard.

When proposing actions, be specific. "Schedule a check-in call with Trane" is better than "engage with Trane." Use the trade's language: RGA, allocation, fill rate, QBR.
