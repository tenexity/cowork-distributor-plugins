# Scheduled Task Recipes — Distributor Edition

## About scheduled tasks in CoWork

Scheduled tasks are automated prompts that fire on a schedule. CoWork's native scheduled-tasks UI handles the timing; the agent runs the prompt at the scheduled moment.

The PA plugin creates two scheduled tasks during setup (morning briefing, EOD summary). The setup-user / setup-guide skill's "scheduled tasks" step offers role-based options on top. Vendor-pulse and account-drift-detector each have their own recommended scheduled task.

## PA-default scheduled tasks (created during PA activation)

These two are pre-checked when the user activates the PA. They run every weekday by default; weekend behaviour is the user's call.

### Morning briefing

**Name:** PA — Morning Briefing
**Default schedule:** Weekdays, 8:00 AM (ask user for preferred time during setup)
**Prompt:**

```
Run my morning briefing using the daily-briefing skill. Read these sources:

1. Today's calendar events (if Google Calendar is connected)
2. WORK AREAS/Admin-PA/tasks.md — overdue tasks and tasks due today
3. Yesterday's captain's log entries
4. WORK AREAS/Admin-PA/inventory-action-log.md — any open inventory decisions
5. Vendor watch — open allocation pushbacks, pending rebate disputes, scheduled QBR prep windows from the past 7 days of log
6. AR watch — customers on credit hold or crossing 60+ day thresholds

Produce a clear morning briefing in the format the daily-briefing skill specifies. Keep it scannable — I want to know what needs my attention in under 30 seconds of reading.
```

### End-of-day summary

**Name:** PA — End-of-Day Summary
**Default schedule:** Weekdays, 6:00 PM (ask user for preferred time during setup)
**Prompt:**

```
Run my end-of-day summary using the daily-briefing skill. Read these sources:

1. Today's captain's log entries
2. WORK AREAS/Admin-PA/tasks.md — what was completed today, what's still open
3. WORK AREAS/Admin-PA/output-log.md — files created today
4. WORK AREAS/Admin-PA/inventory-action-log.md — any decisions captured today
5. Tomorrow's calendar events and tasks due tomorrow

Produce the EOD summary, then offer the reflection prompt. If I want to reflect, walk me through the three questions and log my answers in today's captain's log under a Reflection heading.
```

## Distributor-specific recurring tasks (offered as options during setup)

These ship as part of the setup-user / setup-guide "scheduled tasks" step. The user multi-selects which they want; the agent generates the exact prompt + schedule for each selected task.

### Weekly vendor pulse

**Name:** PA — Weekly Vendor Pulse
**Default schedule:** Fridays, 4:00 PM
**When to suggest:** Always — universally useful for distributor work
**Prompt:**

```
Run the vendor-pulse skill. Read the past 7 days of captain's log entries and produce the weekly vendor activity summary. Save the report to WORK AREAS/Admin-PA/vendor-pulse-reports/Vendor-Pulse_[YYYY-MM-DD].md and surface the key findings in chat — active vendors this week, vendors going quiet, concerning signals, and proposed actions for next week.
```

### Monthly account drift check

**Name:** PA — Monthly Account Drift Check
**Default schedule:** First Monday of each month, 9:00 AM
**When to suggest:** Always — universally useful
**Prompt:**

```
Run the account-drift-detector skill. Read the past 60 days of captain's log entries, cross-reference against my customer contacts and top-25 tracker (if it exists), and surface customer accounts that have gone quiet. Save the report to WORK AREAS/Admin-PA/drift-reports/Account-Drift_[YYYY-MM-DD].md and walk me through the top items in chat.
```

### Monthly System Review

**Name:** Monthly System Review
**Default schedule:** First Tuesday of each month, 8:00 AM
**When to suggest:** Always (pre-checked) — System Review is the highest-value loop in the whole system
**Prompt:**

```
Run the system-review skill. Read all ABOUT ME files (including COMPANY/ and USER/ if multi-user), recent captain's log entries, recent project memory updates, and the past month's PA data (tasks, contacts, preferences, output log, vendor-pulse reports, account-drift reports). Identify patterns, catch setup drift, check distributor cadence signals, extract cross-project lessons, and produce a System Health Report saved to WORK AREAS/Admin-PA/system-reviews-project/outputs/System-Review_Report_[YYYY-MM-DD].md. Walk me through the recommendations one at a time.
```

### Weekly AR aging triage

**Name:** AR Weekly Triage
**Default schedule:** Mondays, 9:00 AM
**When to suggest:** GM, Branch Manager, Finance, AR, Credit roles
**Prompt:**

```
Run my weekly AR aging triage. Ask me to paste the latest aging export from the ERP. Once I do, populate or update WORK AREAS/Finance/ar-collection-priorities-project/outputs/AR-Collection-Matrix_v1.md (the AR collection prioritisation artifact). Highlight new top-right quadrant items (Hard / High Impact), draft collection emails for those that are ready, and surface customers crossing 60- or 90-day thresholds since last week.
```

### Monthly dead-stock review

**Name:** Monthly Dead-Stock Review
**Default schedule:** First Tuesday of each month, 10:00 AM
**When to suggest:** Purchasing, GM roles
**Prompt:**

```
Run my monthly dead-stock review. Ask me to paste the dead-stock export from the ERP. Once I do, walk me through the SKU-rationalisation framework (use the template at RESOURCES/TEMPLATES/sku-rationalisation-template.md). Identify the top RGA candidates by dollar value, the top transfer candidates between branches, and any vendor return programmes worth activating. Save the report to WORK AREAS/Inventory-Ops/monthly-dead-stock-project/outputs/Dead-Stock_[Month-Year]_v1.md and log the decisions to inventory-action-log.md.
```

### Quarterly vendor QBR prep reminder

**Name:** Vendor QBR Prep Reminder
**Default schedule:** Custom — fires 21 days before each scheduled vendor QBR (set per vendor or as a generic quarterly)
**When to suggest:** Purchasing, Outside Sales, GM roles
**Prompt:**

```
QBR with [vendor name] is in about 3 weeks. Walk me through QBR prep using the vendor-scorecard template (RESOURCES/TEMPLATES/vendor-scorecard-template.md). Pull the scorecard from the last QBR if it exists, ask me for the current YTD purchase numbers and rebate progress, and produce a draft scorecard plus 3-5 negotiation talking points. Save to WORK AREAS/Procurement-Vendors/[vendor-slug]-correspondence-project/outputs/[Vendor]_QBR-Prep_[Date]_v1.md.
```

### Friday weekly review

**Name:** Friday Weekly Review
**Default schedule:** Fridays, 3:00 PM
**When to suggest:** GM, Branch Manager, VP roles
**Prompt:**

```
Walk me through my Friday weekly review using the weekly-review-template (RESOURCES/TEMPLATES/weekly-review-template.md). Read this week's captain's log, this week's completed tasks, this week's vendor-pulse report (if it ran today), and any drift reports from this month. Help me synthesise: what worked, what slipped, what's queued for next week. Save the result to WORK AREAS/Admin-PA/weekly-review-project/outputs/Weekly-Review_[Week-Of-Date]_v1.md.
```

### Daily counter rush check (Branch Manager only)

**Name:** Daily Counter Pulse
**Default schedule:** Weekdays, 11:00 AM (after the morning rush)
**When to suggest:** Branch Manager role only
**Prompt:**

```
Quick counter pulse. Ask me: how was the morning rush? Any unusual issues — backorders, will-call delays, customer complaints, staffing gaps? Capture my answer in today's captain's log under a [counter-pulse] tag. If issues are recurring (same kind of complaint or same product line short multiple days in a row), surface that pattern.
```

## Recommending new scheduled tasks

Part of the PA's value is spotting patterns that could become automated. When reviewing captain's log entries or during System Review, look for:

- **Repeated manual checks:** "I checked AR aging again" appearing weekly → user already has this scheduled, may want a more aggressive cadence
- **Regular reports the user produces manually:** "Pulled the dead-stock report by hand again" → push toward the scheduled monthly dead-stock review
- **Recurring reminders:** User keeps logging "need to remember to follow up with [vendor]" for the same vendor → propose a scheduled vendor follow-up specifically for that relationship

When you spot a candidate, propose it to the user during the next System Review or briefing, not interrupting active work.

## Custom scheduled tasks

If the user describes a recurring task in plain English ("I'd like a reminder every other Tuesday to check rebate program progress"), generate the prompt and schedule for them in the same Task / Schedule / Prompt format used above. Then tell them to paste it into CoWork's scheduled-tasks UI.
