# Captain's Log — Format Specification

## Purpose

The captain's log is the single input stream for the Personal Assistant. Everything the user tells you in conversational mode gets captured here. Vendor calls, customer escalations, AR firefights, counter-rush observations, internal team notes, quick thoughts — all in one place, in the order they happened.

The user doesn't think about where things go. They talk. You log. The structuring (task extraction, contact updates, vendor tagging, customer tagging, preference capture) happens downstream automatically.

## File location and rotation

- **Path:** `WORK AREAS/Admin-PA/captains-log/YYYY-MM-captains-log.md`
- **Rotation:** monthly. Start a new file on the 1st of each month.
- **Naming:** `2026-04-captains-log.md`, `2026-05-captains-log.md`, etc.

Monthly rotation keeps files manageable. After a few months of daily distributor use (which is high-volume — many short entries), a single file would be unmanageable. Monthly files stay readable.

## Entry format

```markdown
## [Day of week], [Date]

### [HH:MM]
[Entry content — natural language, as close to what the user said as possible]

### [HH:MM]
[Next entry]
```

## Distributor example

```markdown
## Wednesday, 9 April 2026

### 07:45
Counter rush starting early — three contractors waiting at 7:30. Will-call on the Carrier rooftop got delayed because the LP cylinders we ordered didn't ship.

### 09:15
Talked to Mike at Carrier about the Q2 allocation. He's saying 12% reduction across the board — pushing back. Need to send YTD purchase data by Friday so we can negotiate from real numbers.

### 10:30
Smith Plumbing went on credit hold this morning. $34K aged over 90, no contact in 30 days. Need to call Pat directly tomorrow before this becomes a write-off conversation.

### 11:30
Bradford White rebate dispute came back — they're agreeing to the $18K we claimed. Took 6 weeks but worth it. Need to update the Bradford White rebate tracker and remind the team this works when we push.

### 13:15
Lost the Garcia Mechanical bid — went to Wolseley on price (they were 7% under us on the Trane bundle). Worth a debrief: was it actually competitive pricing or did they just buy the deal? Worth talking to Garcia about future jobs.

### 15:00
Pulled the dead-stock report for branches. ALB has $185K in dead stock, mostly Bradford White water heaters from the 2024 buy-in. Need to schedule the review with Eric (purchasing) and Tony (ALB branch manager) for early next week.

### 17:30 — Reflection
**What went well:** The Bradford White rebate win. We pushed and they came back. Good template for future disputes.
**What felt harder than it should:** Carrier allocation came at us with no warning. Should be tracking allocation signals quarterly, not reacting in the moment.
**Remember:** Schedule allocation review as a quarterly scheduled task. Track YTD purchase data per vendor on a running basis.
```

## What gets logged

Everything conversational that isn't part of a specific deliverable. Distributor rules of thumb:

- "Had a call with Mike at Carrier about allocation" → log it
- "Draft a vendor email to Mike at Carrier pushing back on allocation" → this is project work, not a log entry (though the email's existence might be noted in `output-log.md`)
- "Counter was insane this morning, shipped 47 will-call before noon" → log it (operational signal)
- "Smith Plumbing on credit hold pending payment" → log it AND create AR follow-up task
- "Lost Garcia Mechanical bid to Wolseley on price" → log it AND consider a follow-up task to debrief
- "Decided to drop the Liberty pump line" → log it AND add to `preferences.md` (this is a company memory event)
- "Eric is unhappy with the new ERP module rollout" → log it [private] (sensitive personnel — see private tagging below)

## Tagging conventions

You don't ask the user to tag anything. You auto-tag during the log capture by recognising patterns. Tags help downstream skills (vendor-pulse, account-drift, system-review) find what they need.

### Vendor tag
When a vendor name from the user's top vendors list (in `COMPANY/company-profile.md` or `about-me.md`) is mentioned, tag the entry. Format: append `[vendor: name]` at the end of the entry text, OR maintain a separate `vendor-mentions.json` index — whichever is cleaner. For natural-language consumption, the inline tag is simpler.

### Customer tag
Same pattern for customer accounts. `[customer: name]`.

### Sensitivity tag
For sensitive entries — performance discussions, salary, escalations involving named individuals — append `[private]`. The System Review skill skips `[private]` entries when generating reports the company admin sees. Examples:
- "Talked to Eric about his counter performance" → tag `[private]`
- "Considering letting [person] go" → tag `[private]`
- "Salary review for [person]" → tag `[private]`

The user can mark entries `[private]` themselves by typing it; the agent should also auto-detect sensitive content.

## Reflection block format

End-of-day reflection (from the `daily-briefing` skill's EOD flow) appends a `### HH:MM — Reflection` block:

```markdown
### 17:30 — Reflection
**What went well:** [User's answer]
**What felt harder than it should:** [User's answer]
**Remember:** [User's answer]
```

These reflections are gold for the System Review — patterns of recurring frustrations become candidates for new scheduled tasks, additional automation, or paid-pilot conversations with Tenexity.

## What about vendor or customer specifics?

If the user references confidential customer pricing, contract terms, or sensitive vendor agreements in conversation, log them — the captain's log is private to the user's workspace. But never paste these into customer-facing or vendor-facing communications without explicit approval. The PA's behavior already follows this rule, but it's worth noting here too.
