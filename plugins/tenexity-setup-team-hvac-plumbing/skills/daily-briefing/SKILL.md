---
name: daily-briefing
description: >
  Generates the daily morning briefing or end-of-day summary for distributor work.
  Triggers when the user asks "what's on my plate today", "give me my briefing",
  "morning briefing", "end of day", "what did I do today", "daily summary", "EOD
  summary", "what's hot today", or when a scheduled task runs the daily briefing
  or end-of-day prompt. Also triggers on /briefing and /eod commands. Reads the
  captain's log, tasks, calendar, and AR/vendor signals to produce a clear,
  scannable briefing in distributor language.
version: 1.0.0
---

# Daily Briefing & End-of-Day Summary — Distributor Edition

This skill generates two types of briefing from the user's PA data, both tuned to how a distributor's day actually works.

## Morning briefing

Read these sources and synthesise into a clear, scannable briefing:

1. **Calendar** — If Google Calendar is connected, read today's events. List with times. Skip if not connected.
2. **Overdue tasks** — Read `WORK AREAS/Admin-PA/tasks.md`. Any open tasks past their due date. **Most important section — flag clearly.**
3. **Due today** — Tasks due today.
4. **AR watch** — From recent captain's log entries or tasks tagged with credit-hold/aged-AR signals: customers currently on credit hold, customers crossing 60/90 day thresholds. Surface with the dollar amount if known.
5. **Vendor watch** — Vendors with active issues from the past 7 days of log entries: open allocation pushbacks, pending rebate disputes, scheduled QBR prep windows.
6. **Follow-up reminders** — Tasks in "Waiting" status where the follow-up date is today or past.
7. **Yesterday's highlights** — Read yesterday's entries from the current month's captain's log. Pull the 3-5 most significant items — vendor calls, customer outcomes, completed tasks, notable conversations.
8. **Coming up (next 3 days)** — Tasks due within 72 hours. Heads-up only.

### Briefing format

Keep it tight. Distributor mornings are short. No walls of text.

```
## Morning Briefing — [Day, Date]

### Overdue (needs attention)
[Items, or "Nothing overdue — you're clear."]

### Today
[Calendar events + tasks due today, merged into a timeline if possible]

### AR watch
[Customers on credit hold or crossing aging thresholds, or "AR clean — nothing crossing thresholds today."]

### Vendor watch
[Open vendor issues, or "No active vendor escalations."]

### Waiting on others
[Follow-ups due, or "Nothing pending."]

### Yesterday's highlights
[3-5 bullet points from the captain's log]

### Coming up (next 3 days)
[Brief list, or "Nothing scheduled."]
```

If a section is empty, include it with a positive note ("AR clean," "No active vendor escalations") rather than omitting it. The user should see the full picture every morning.

## End-of-day summary

Read these sources and produce the summary:

1. **Today's captain's log** — Everything logged today. Primary source.
2. **Task changes** — What moved to "Done" today? What new tasks were created? What's still open?
3. **Output log** — Read `WORK AREAS/Admin-PA/output-log.md` for files created today.
4. **Inventory action log** — If anything was added today (a dead-stock pull, an RGA, a transfer decision), summarise.
5. **Tomorrow preview** — Tasks due tomorrow + calendar events.

### EOD format

```
## End of Day — [Day, Date]

### What got done
[Completed tasks + key activities from the log]

### What you created
[Files from output log, or "No files created today."]

### Decisions made today
[Major decisions captured in preferences.md or inventory-action-log.md, or omit if none]

### Still open
[Remaining open tasks, briefly]

### Tomorrow
[Preview of tomorrow's commitments, or "Nothing scheduled yet."]
```

### Reflection prompt

After presenting the EOD summary, offer a reflection:

> "Want to take a minute to reflect on the day?"

If yes, ask these three questions one at a time using AskUserQuestion (with a freeform text option):

1. "What went well today?"
2. "What felt harder than it should have?"
3. "Anything you'd do differently or want to remember?"

Log the reflection in today's captain's log under a `### Reflection` heading with the timestamp. These reflections feed into the System Review — patterns of recurring frustrations become candidates for new scheduled tasks or workflow changes.

If the user declines, move on without comment.

## Distributor-specific surfacing rules

When generating either briefing, prioritise distributor-relevant signals over generic productivity:

- **Credit hold pending payment by [date]** — surface in AR watch every morning until resolved
- **Vendor allocation pushback awaiting response** — surface in vendor watch until it lands or resolves
- **QBR prep windows** — if a QBR is in 21 days or less and prep hasn't started, surface in "today" or "coming up"
- **Dead-stock review overdue** — if the cadence in `COMPANY/tools-and-context.md` says monthly and the last `inventory-action-log.md` entry is over 30 days old, surface as a one-line nudge in "today"
- **Rebate program deadline within 14 days** — if `COMPANY/tools-and-context.md` lists rebate programs with claim deadlines, check the calendar; surface anything within 14 days

These take precedence over non-distributor reminders. A vendor allocation pushback is more urgent than "remind me to back up my phone."

## Handling missing data

If the PA was just set up and there's no data yet, don't produce an empty briefing. Say something like: "Your PA is fresh — there's nothing to brief on yet. Start logging throughout the day and tomorrow's briefing will have something to work with. In the meantime: [show calendar events for today if Calendar is connected, or just acknowledge it's day one]."

If only some sections have data, populate what's available and use empty-state notes for the rest.

## Voice

Use the user's voice profile and writing rules. If they've banned "circle back," your briefing doesn't say "let's circle back tomorrow." If their tone is direct, your briefing is direct. The PA's voice is the user's voice.

The briefing is for an experienced distributor — assume trade fluency. "AR over 60" doesn't need explanation. "RGA" doesn't need explanation. "QBR with Carrier" doesn't need explanation.
