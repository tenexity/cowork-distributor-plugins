# Task Extraction Rules — Distributor Edition

## Purpose

When processing captain's log entries or conversational input, automatically identify action items and create tasks in `WORK AREAS/Admin-PA/tasks.md`. The user should never have to say "create a task" — the system spots obligations and tracks them.

This file lists the signal phrases that trigger task creation, with distributor-specific patterns layered on top of generic productivity patterns.

## Generic signal phrases

These are common across any kind of work:

**Direct obligation:** "need to", "have to", "must", "should", "going to"
- "I need to send her the YTD purchase data" → Task: Send YTD purchase data to [person]

**Future intent:** "will", "planning to", "want to", "going to"
- "I'm going to push back on the Carrier allocation this week" → Task: Push back on Carrier allocation (due: this week)

**Reminders:** "remind me", "don't forget", "remember to", "follow up"
- "Remind me to follow up with Pat at Smith Plumbing on Friday" → Task: Follow up with Pat at Smith Plumbing (due: Friday)

**Commitments to others:** "I told them I'd", "I promised", "I said I'd", "I'll send"
- "I told Mike at Carrier I'd have the YTD data over by Friday" → Task: Send YTD data to Mike at Carrier (due: Friday) [vendor: Carrier]

**Waiting signals:** "waiting on", "they're going to", "expecting", "should hear back"
- "Bradford White is going to send the credit memo" → Task: Waiting — Bradford White credit memo (status: Waiting) [vendor: Bradford White]

## Distributor-specific signal phrases

These trigger task creation AND apply distributor-specific tags / due-date defaults.

### Vendor signals

| Phrase pattern | Task type | Default due |
|---|---|---|
| "RGA back to [vendor]" / "send back to [vendor]" | Vendor return | 5 business days |
| "Allocation came in short" / "allocation cut" | Vendor escalation | Tomorrow |
| "Push back on [vendor]" / "negotiate [vendor]" | Vendor negotiation | This week (Friday) |
| "QBR with [vendor] in [N] weeks" | QBR prep | QBR date - 21 days |
| "Rebate [accepted / disputed / claim]" | Rebate task | 14 days |
| "Need to update [vendor] tracker" | Tracker update | This week |
| "Vendor visit / rep visit" | Visit prep | Visit date - 2 days |
| "Price file from [vendor]" | Price file processing | 7 days |

### Customer signals

| Phrase pattern | Task type | Default due |
|---|---|---|
| "[Customer] on credit hold" / "credit hold pending [amount]" | AR follow-up | Tomorrow |
| "Aged over 60/90 days" | AR collection | Tomorrow |
| "Lost [customer] to [competitor]" | Post-loss debrief | 2 weeks |
| "Quote went out for [$X+]" | Quote follow-up | 7 days from quote date |
| "Contractor wants delivered tomorrow" | Operational urgent | Tomorrow morning |
| "QBR with [customer] in [N] weeks" | Customer QBR prep | QBR date - 14 days |
| "[Customer] complaint" / "[Customer] unhappy" | Service recovery | Tomorrow |

### Inventory signals

| Phrase pattern | Task type | Default due |
|---|---|---|
| "Pulled the dead-stock report" | Dead-stock review | This week |
| "Need to RGA [SKU/quantity]" | Vendor return | 5 business days |
| "Transfer from [branch A] to [branch B]" | Inventory transfer | 3 business days |
| "Killing the line on [SKU]" / "Drop the [SKU] line" | Discontinuation paperwork | This week (also log to preferences.md) |
| "Cycle count [date]" | Cycle count prep | Date - 1 |

### AR / credit signals

| Phrase pattern | Task type | Default due |
|---|---|---|
| "Wrote off [amount]" | Decision logging (preferences.md) | Done — log only |
| "Payment plan with [customer]" | Payment plan documentation | This week |
| "New credit line for [customer]" | Credit decision | This week |

### Internal team signals

| Phrase pattern | Task type | Default due |
|---|---|---|
| "Onboard [new hire]" | Onboarding plan | Hire date - 7 days |
| "Performance review for [person]" | HR task | Review date - 14 days, [private] |
| "Hire for [role]" | Hiring task | Open-ended |

## What's NOT a task

Not everything that sounds like an action is worth tracking:

- **Completed actions:** "I sent the email to Mike" → not a task, it's done (but log it)
- **Hypothetical/exploratory:** "maybe I should look at switching ERPs" / "wondering if Trane would..." → not a task unless the user confirms intent
- **Observations:** "The Bradford White line is shrinking" → not a task unless paired with intent to act
- **Routine ops:** "Counter was busy this morning" → log it but no task

If you're genuinely unsure, lean toward capturing it. A task the user marks "not needed" is less costly than a forgotten commitment with a vendor or customer.

## Task format in tasks.md

Every task should be linked to a work area and tagged appropriately. This creates a web of connections — when someone asks "what's happening with vendors?", vendor-tagged tasks surface alongside vendor-related project work.

```markdown
## Open

- [ ] **[Task description]** — Due: [date or "no date"] | Source: [date, log entry reference] | Area: [work area name] | Project: [project name, if applicable] | Tags: [vendor:name / customer:name / AR / inventory / internal / private]
```

### How to determine the area/project link

1. **Explicit mention:** "I need to finish the QBR for Acme Plumbing" → Area: Customer-Accounts, Project: acme-plumbing-qbr-project (create if doesn't exist)
2. **Vendor mention:** "Send YTD data to Mike at Carrier" → Area: Procurement-Vendors, Project: carrier-correspondence-project
3. **Customer mention:** "Call Pat at Smith Plumbing about credit hold" → Area: Finance, Project: smith-plumbing-collection-project
4. **Context clues:** "Pull the dead-stock report" → Area: Inventory-Ops
5. **Default:** Admin-PA. Everything has a home — nothing floats unlinked.

### Example

```markdown
## Open

- [ ] **Send YTD purchase data to Mike at Carrier** — Due: Friday 11 Apr | Source: 9 Apr, 09:15 log | Area: Procurement-Vendors | Project: carrier-correspondence-project | Tags: vendor:Carrier
- [ ] **Call Pat at Smith Plumbing re credit hold** — Due: Tue 10 Apr | Source: 9 Apr, 10:30 log | Area: Finance | Project: smith-plumbing-collection-project | Tags: customer:Smith Plumbing, AR
- [ ] **Schedule dead-stock review with Eric and Tony** — Due: Mon 14 Apr | Source: 9 Apr, 15:00 log | Area: Inventory-Ops | Project: q2-dead-stock-review-project | Tags: inventory, internal
```

## Smart due-date defaults

If the user doesn't specify a due date, use these defaults:

- AR / credit hold: tomorrow
- Vendor escalations (allocation, dispute): tomorrow
- Vendor negotiations (general pushback): this Friday
- QBR prep: 21 days before QBR date if vendor, 14 days before if customer
- Quote follow-up: 7 days from quote send
- Dead-stock review: this week
- General "follow up": Friday of this week

If the user phrases it with "this week" → use Friday of the current week. "Next week" → Friday of next week. "Soon" → Friday of next week. "ASAP" → tomorrow.
