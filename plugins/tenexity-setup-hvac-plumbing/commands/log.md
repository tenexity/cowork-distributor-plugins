---
name: log
description: Quick captain's log entry — capture what's happening right now
---

# /log — Quick Captain's Log Entry

The user wants to make a quick log entry. Don't ask clarifying questions — just log what they say.

1. Read the current month's captain's log file from `WORK AREAS/Admin-PA/captains-log/YYYY-MM-captains-log.md`. If it doesn't exist for this month, create it from the template in `${CLAUDE_PLUGIN_ROOT}/reference/captains-log-format.md`.
2. Append a new timestamped entry with the current time. Format: `### HH:MM` followed by the user's content.
3. Scan the entry for distributor-relevant signals using `${CLAUDE_PLUGIN_ROOT}/reference/task-extraction-rules.md`. If found:
   - Add tasks to `WORK AREAS/Admin-PA/tasks.md`
   - Update `WORK AREAS/Admin-PA/contacts.md` if vendors, customers, or internal team members are mentioned with context
   - Log preferences and decisions to `WORK AREAS/Admin-PA/preferences.md`
   - Tag vendor mentions for vendor-pulse aggregation
   - Tag customer mentions for account-drift-detector
4. Confirm in one line: "Logged. [What was captured, e.g. 'Task added: push back on Carrier allocation by Friday. Contact added: Mike at Carrier — first mention.']"

Keep confirmation to one line. The user chose `/log` for speed, not conversation.

If the user typed `/log` with no message after it, use AskUserQuestion to ask: "What's happening?" with a freeform text input.
