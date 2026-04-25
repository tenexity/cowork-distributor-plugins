---
name: account-drift-detector
description: >
  Flags customer accounts that have gone quiet in conversation. Triggers when the
  user says "account drift", "any accounts gone quiet", "customers I haven't talked
  to", "drift check", "show me drifting accounts", or when the scheduled
  account-drift task fires (typically monthly). Reads recent captain's log entries,
  cross-references against the user's customer list and top-25 tracker if it
  exists, and surfaces accounts that haven't appeared in conversation for 30+
  days. Designed for HVAC and plumbing wholesale distributors managing key
  contractor accounts where silence often precedes loss.
version: 1.0.0
---

# Account Drift Detector

In wholesale distribution, the contractor or customer who stops calling first stops buying second. Loss usually shows up in the captain's log as silence — they haven't been mentioned in 30, 45, 60 days. By the time the ERP shows the revenue drop, the relationship is already cold.

This skill surfaces drifting accounts before that point.

## When this fires

- User says "account drift" / "any accounts gone quiet" / "customers I haven't talked to"
- Scheduled task runs monthly (typical: first Monday of the month)
- User triggers from a relevant context — e.g., during a slow Friday afternoon

## Sources

1. **Captain's log** — past 60 days of entries from `WORK AREAS/Admin-PA/captains-log/`. Read multiple monthly files if needed.
2. **Top-25 account tracker** (if it exists) — `WORK AREAS/Customer-Accounts/top-25-tracker-project/outputs/Top-25-Account-Tracker_v1.md`. This is the canonical "who matters" list. If the user built this artifact during setup or after, it's the highest-quality source.
3. **Contacts.md** — `WORK AREAS/Admin-PA/contacts.md`. Customer-type contacts (filter by type field — see `reference/contact-structure.md`).
4. **Tasks.md** — any open or recent customer-tagged tasks.

## Drift detection logic

For each customer account in the user's tracker (or contacts list if no tracker exists):

1. Search the past 60 days of captain's log for any mention of that customer (name, contact name, or known aliases).
2. Find the most recent mention. Compute days-since.
3. Bucket the account:

| Days since last mention | Bucket | Action |
|---|---|---|
| 0-14 days | Active | No action — they're top of mind |
| 15-29 days | Steady | No action — normal cadence for most accounts |
| 30-44 days | **Quiet** | Surface — may be fine, may be drifting |
| 45-59 days | **Drifting** | Surface with stronger signal — probably worth a check-in |
| 60+ days | **At risk** | Surface as priority — relationship is cold |

**Special considerations:**

- If the account is in the top-25 tracker AND status is "drifting" or "at risk" already, escalate the bucket by one level (their own assessment is concerning + your detector agrees = critical signal).
- If the account is a service-rich type (lots of will-call, frequent counter visits) the drift threshold should be tighter (15-29 days = drifting). Read the user's customer mix from `COMPANY/company-profile.md` or `about-me.md` to calibrate.
- If the account is a project-business type (one big job per quarter) the drift threshold should be looser (60-89 days might be normal). Same source.

## Output format

Save to `WORK AREAS/Admin-PA/drift-reports/Account-Drift_[YYYY-MM-DD].md` (create folder if needed) AND surface in chat.

```markdown
## Account Drift Check — [Date]

### At risk (60+ days no mention) — [N] accounts

For each, list:
- **[Account name]** — last mentioned [date], [N] days ago
  - Last context: [pull the most recent mention from log]
  - Recent revenue trend (if known from tracker): [up / steady / down / unknown]
  - **Suggested action:** [Specific call to make, conversation to have]

### Drifting (45-59 days no mention) — [N] accounts

[Same format, less urgent]

### Quiet (30-44 days no mention) — [N] accounts

Brief list. May be fine. Worth knowing.

### Healthy (0-29 days, top 5 by recent activity)

[Quick positive note — these are humming. List the top 5 most-mentioned for context.]

### Patterns

[Any patterns worth flagging:
- Multiple accounts at the same buying group going quiet — competitor activity?
- Multiple accounts in the same trade segment going quiet — segment shift?
- One sales rep's accounts disproportionately drifting — rep coverage issue?]

### Action items

Based on the above, propose 3-5 specific actions:

1. [Action — most urgent]
2. [Action]
3. [Action]
```

## Distributor-tuned considerations

**Service techs and will-call customers** are mentioned constantly (every counter visit), so silence is unusual and very meaningful. Use tighter thresholds for these.

**Project contractors** (residential builders, multi-family GCs) work in multi-month cycles — a contractor running a large job won't mention you for 6 weeks because they're working through their original PO. Use looser thresholds.

**MRO and facilities accounts** are typically email-driven and slow-cadence — quarterly conversations are normal. Use loosest thresholds.

If the user hasn't characterised their customer mix in the COMPANY profile or About Me, default to mid-range thresholds (30/45/60 days).

## What this skill does NOT do

- Does not contact customers directly
- Does not write outreach emails (offers to do so as a follow-on action)
- Does not pull ERP revenue data — works only from captain's log + tracker. If the user wants revenue-validated drift detection, that's a paid Tenexity pilot conversation (Customer Account Health Monitor).

## Voice

Use the user's voice profile. Direct, trade-fluent, no corporate-speak. Surface the data, propose actions, leave the calls to the user.
