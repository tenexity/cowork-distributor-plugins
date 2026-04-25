---
name: tasks
description: Show current open tasks grouped by urgency
---

# /tasks — Show Open Tasks

Read `WORK AREAS/Admin-PA/tasks.md` and present the current task list in a clear, scannable format.

Group by urgency:

1. **Overdue** — past due date, still open. Flag clearly.
2. **Due today** — due today.
3. **Due this week** — due in the next 7 days.
4. **Waiting on others** — tasks where you're waiting on someone else.
5. **No date** — open tasks with no due date, listed briefly.

For each task show: description, due date (if any), source (one-line reference), and tag (vendor / customer / AR / inventory / internal / other).

Distributor-aware highlighting:
- **Bold** vendor-tagged tasks where the vendor has a QBR coming up in the next 21 days (cross-check against COMPANY's operational rhythm or tasks.md QBR entries)
- **Bold** AR-tagged tasks where the customer is on credit hold or crossing 60+ days
- **Italic** any task created from a captain's log entry more than 7 days ago that hasn't been touched (potential drift)

If there are no tasks, say: "No open tasks right now. That's either very good or very suspicious."

After showing the list, offer: "Want to mark anything as done, add a new task, or change a due date?" Accept the response naturally.
