# Personal Assistant — Quick Reference

The PA is always on once it's been activated. You don't need to "tell it to track" — it does that automatically as you talk.

---

## Just talk to it

The fastest way to use the PA is to talk about what's happening. The PA captures it.

| You say | The PA does |
|---|---|
| "Had a call with Mike at Carrier — allocation is short" | Logs the entry, adds Mike to contacts (vendor type), tags Carrier for vendor-pulse |
| "Smith Plumbing on credit hold pending payment" | Logs entry, creates AR follow-up task for tomorrow, surfaces in tomorrow's morning briefing |
| "Need to send YTD purchase data by Friday" | Creates a task with Friday due date |
| "Decided to drop the Liberty pump line" | Logs entry, adds to preferences.md (company-level decision) |
| "Lost Garcia Mechanical to Wolseley on price" | Logs entry, creates post-loss debrief task |
| "Pulled the dead-stock report — ALB has $185K dead" | Logs entry, adds to inventory-action-log.md |

---

## Slash commands

| Command | What it does |
|---|---|
| `/log [message]` | Quick log entry. If no message, asks you "what's happening?" |
| `/tasks` | Shows current open tasks grouped by urgency, with vendor/customer/AR tags |
| `/briefing` | On-demand morning briefing — same as the scheduled one |
| `/eod` | End-of-day summary with optional reflection (3 questions) |
| `/tidy` | Folder cleanup — Downloads, Desktop, ERP exports |

---

## Skills you can trigger by name

These run automatically on a schedule but can also be triggered on demand.

| Trigger phrase | What runs |
|---|---|
| "vendor pulse" / "vendor activity this week" | Weekly vendor-pulse summary |
| "account drift" / "any accounts gone quiet" | Customer drift detector |
| "review my system" | Monthly System Review |
| "first week guide" | First Week guided tasks (5 days, role-based selection) |

---

## What lives where

All PA data lives in `WORK AREAS/Admin-PA/`:

| File | What's in it |
|---|---|
| `captains-log/YYYY-MM-captains-log.md` | Daily running log of everything you've talked about |
| `tasks.md` | Open / waiting / done tasks, tagged by area and source |
| `contacts.md` | Vendors, customers, internal team, buying group contacts |
| `preferences.md` | Decisions and preferences you've stated |
| `output-log.md` | Every file the system has created for you, with timestamps |
| `inventory-action-log.md` | Inventory decisions over time (RGAs, transfers, line drops, dead-stock pulls) |
| `vendor-pulse-reports/` | Weekly vendor activity summaries |
| `drift-reports/` | Monthly account drift checks |
| `system-reviews-project/outputs/` | Monthly System Review reports |

---

## Scheduled tasks

Set up during PA activation. Default cadences:

| Task | When |
|---|---|
| Morning briefing | Weekdays, 8:00 AM (configurable) |
| End-of-day summary | Weekdays, 6:00 PM (configurable) |
| Weekly vendor pulse | Fridays, 4:00 PM |
| Monthly account drift check | First Monday, 9:00 AM |
| Monthly System Review | First Tuesday, 8:00 AM |

Plus role-based options offered during setup (AR triage, dead-stock review, vendor QBR prep reminder, Friday weekly review, daily counter pulse).

You can edit, pause, or delete any of these in CoWork's scheduled tasks panel.

---

## When the PA pulls back

The PA stays quieter when you're working on a specific deliverable (drafting an email, building a report). It logs outputs but doesn't interrupt the work with logging confirmations. It comes back to full mode when you're chatting conversationally about your day.

---

## Privacy

Anything you tag `[private]` (or the PA auto-tags as private — performance discussions, salary, HR matters) stays out of:

- Vendor-pulse summaries
- Account-drift reports
- Company-level System Review reports (the admin's view in multi-user deployments)

Your personal System Review still sees everything. Your CoWork data stays on your machine — the PA does not transmit anything to Tenexity or any third party.

---

## What if I don't want some of this?

- Don't want morning briefings? Pause that scheduled task.
- Don't want auto task extraction? Tell the PA: "stop auto-creating tasks." It'll only create tasks when you explicitly say so.
- Don't want certain contacts auto-tracked? Tell the PA: "don't track contacts." It'll log conversations without updating contacts.md.
- Want to reset everything? Say "reset my PA." The PA will ask which files to clear (it never deletes without explicit confirmation).

The PA's defaults match what most distributors want. Override anything that doesn't fit.
