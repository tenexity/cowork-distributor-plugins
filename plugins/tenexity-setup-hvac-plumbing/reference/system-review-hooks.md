# System Review Hooks — How System Review reads PA data

## Purpose

The System Review skill reads everything in the user's workspace to produce monthly health reports. The PA generates substantial new data — captain's log entries, tasks, contacts, preferences, output log, vendor-pulse reports, account-drift reports, inventory action log. This file specifies what System Review pulls from each source and how.

## Sources System Review reads (PA-related)

### Captain's log

**Path:** `WORK AREAS/Admin-PA/captains-log/YYYY-MM-captains-log.md` (current month + previous month if review covers a 30-60 day window)

**What System Review extracts:**

- **Recurring corrections** — phrases the user has used to correct Claude's output multiple times. If the same correction appears 2+ times and isn't already in the writing rules or voice profile, propose adding it.
- **Recurring frustrations** — patterns in reflection blocks ("filing system needs work," "couldn't find the receipts," "vendor came at us with no warning"). These often signal automation opportunities.
- **Decision log** — entries that announced a real decision ("decided to drop the Liberty pump line," "switching to monthly rebate accruals"). Cross-check against `preferences.md` — if they're not captured there, propose adding.
- **Vendor / customer mentions** — used by vendor-pulse and account-drift but also surfaced in System Review as part of "is your attention going to the right places?"

### Tasks

**Path:** `WORK AREAS/Admin-PA/tasks.md`

**What System Review extracts:**

- **Aging open tasks** — open tasks with due dates more than 30 days in the past. These are signals that something is wrong: either the task should be re-prioritised, dropped, or escalated.
- **Distribution by tag** — what % of tasks are vendor / customer / AR / inventory / internal. Drift from the user's own stated priorities is worth surfacing.
- **Done velocity** — count of completed tasks per week over the review period. Trending down is a signal.
- **Same-vendor or same-customer task piles** — if a single account has 5+ open tasks, that's likely a relationship that needs deeper attention than ad-hoc task work can provide.

### Contacts

**Path:** `WORK AREAS/Admin-PA/contacts.md`

**What System Review extracts:**

- **Mention count distribution** — top mentioned contacts (good signal for who's getting attention) and bottom (stale relationships)
- **New contacts this period** — anyone mentioned for the first time in the review window
- **Contact type balance** — too vendor-heavy / too customer-heavy / not enough internal team mentions can each be a signal
- **Drift candidates** — already covered by account-drift-detector, but System Review surfaces a summary

### Preferences

**Path:** `WORK AREAS/Admin-PA/preferences.md`

**What System Review extracts:**

- **Promotable preferences** — anything in preferences.md that should arguably be promoted to the user's About Me files (voice profile, writing rules, my-priorities). Examples: "I prefer direct phone for top accounts" → could go in voice profile. "We dropped the Liberty pump line" → company-level decision, should be in company-profile.md.
- **Conflicting preferences** — if the user logged a preference that contradicts what's in their About Me, surface it.

### Output log

**Path:** `WORK AREAS/Admin-PA/output-log.md`

**What System Review extracts:**

- **Top output types** — what kinds of files is the user creating most? Vendor emails / customer quotes / QBR prep / reports / dead-stock analyses. Compare to the user's stated priorities — alignment or drift?
- **Output cadence** — produced steadily, or in clumps? Clumps often indicate firefighting; steady production indicates a healthy rhythm.

### Vendor-pulse reports

**Path:** `WORK AREAS/Admin-PA/vendor-pulse-reports/`

**What System Review extracts:**

- Concerning signals across multiple weeks (the same vendor showing up in concerning bucket repeatedly = systemic issue)
- Going-quiet patterns (vendors that have stayed quiet across multiple pulse reports = relationship that needs revival or won't recover)
- Vendor mention-count trends (dropping = drift; spiking = active negotiation or escalation)

### Account-drift reports

**Path:** `WORK AREAS/Admin-PA/drift-reports/`

**What System Review extracts:**

- Accounts that have been in drifting/at-risk buckets for 2+ consecutive monthly reports — these are getting worse, not better
- Patterns: same buying group, same trade segment, same sales rep — clusters of drift often have structural causes

### Inventory action log

**Path:** `WORK AREAS/Admin-PA/inventory-action-log.md`

**What System Review extracts:**

- Decisions made in the period (RGAs, transfers, line drops, write-offs)
- Cumulative dollar impact of inventory actions over the period
- Cross-reference to vendor-pulse — did dead-stock decisions improve relationships with the relevant vendors?

## How System Review presents PA findings

System Review's report has standard phases (system health, pattern analysis, distributor cadence, compile and present). PA data feeds into:

- **System health phase** — checks PA file completeness (has the captain's log been used? are tasks being captured?). Reports if PA is configured but unused.
- **Pattern analysis phase** — the bulk of PA-derived insights surface here. Recurring corrections, frustrations, drift, vendor patterns.
- **Distributor cadence phase** — vendor-pulse and account-drift reports inform whether the user is keeping cadence with their commitments.
- **Compile and present phase** — recommendations get tagged with their PA source so the user can drill in.

## Privacy: skip [private] entries

Anything in the captain's log, tasks.md, or contacts.md tagged `[private]` is excluded from System Review reports that the company admin will see (in v2 multi-user deployments). Personal review reports for the user themselves include everything.

The rule: in v2, System Review produces two reports — the user's personal review (full data) and the admin's company-level review (private entries omitted). In v1 solo, there's just one report and `[private]` tagging is mostly used to keep certain entries out of vendor-pulse / account-drift summaries.

## What System Review does NOT do

- Does not modify PA files automatically. Recommendations propose changes; the user approves before anything is written.
- Does not delete captain's log entries, tasks, or contacts. These are the user's history; System Review surfaces patterns but never edits the source.
- Does not contact vendors or customers based on PA findings. Suggests outreach as actions; the user decides and acts.
