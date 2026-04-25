# Pattern recognition examples for distributors

These examples help the System Review identify real patterns in memory entries. Use them as reference — not a checklist. Real memory files will be messier and more varied than these examples.

## Recurring corrections

These are entries where the distributor corrected Claude's behaviour. When the same correction appears multiple times, it should become a permanent rule.

**Example memory entries that reveal corrections:**

> "Claude drafted the Carrier email in corporate-speak again — told it to sound like a text to a rep I've known 10 years, not a legal letter."

> "Had to remind Claude that our branch codes are ALB/SYR/ROC/BUF, not 'Albany Branch 1' etc."

> "Told Claude to stop using 'partner' as a verb. Fourth time this quarter."

> "Claude assumed we could see the Carrier rebate portal. We can't — need to paste screenshots."

> "Claude invented a margin percentage in the vendor email. Caught it before sending. No invented numbers, ever."

**What to do:**

1. Check if the correction is already captured in writing-rules.md, about-me.md, or CLAUDE.md. If yes, note the rule exists but isn't being followed (the rule might be buried or the file too long).
2. If the correction isn't captured, draft the specific text to add to the right file.
3. If the same correction appears 3+ times and a rule already exists, consider whether the rule needs to be more prominent (moved higher in the file, made more explicit, or added to CLAUDE.md as well).

## Common task types

Look for patterns in what the distributor actually does. Memory entries often describe completed work.

**Indicators of distributor task types:**

- "Drafted three vendor pushback emails this week" → Vendor negotiation is a primary task
- "Ran the Q1 dead-stock analysis for Albany branch" → Dead-stock review is active cadence
- "Prepped QBR for Acme Plumbing" → Key-account QBR work is recurring
- "Finished the Carrier rebate reconciliation for Q1" → Rebate tracking is a quarterly beat
- "Drafted 12 collection notices this week" → AR collection is a regular need
- "Wrote the May contractor newsletter" → Customer communication is recurring

**What to do:**

1. List the top 3-5 task types by frequency.
2. For each, check whether the system is well-configured:
   - Does a matching template exist in RESOURCES/TEMPLATES/?
   - Does the writing rules cover this type of content?
   - Is the relevant work area being used (not defaulting to Admin-PA)?
3. If a common task type has no template or specific guidance, suggest creating one.
4. If a task type is done repeatedly by hand when a Tenexity pilot could automate it, flag as Tenexity-match (see Phase 3 cadence checks in the main SKILL.md).

## Missing context

These are moments where Claude needed information it didn't have.

**Indicators of missing context for distributors:**

- "Had to explain our commission structure to Claude again — should be in About Me"
- "Claude asked which ERP we run — should be in the context map"
- "Drafted a vendor email but used the wrong primary contact — we changed reps in January"
- "Claude didn't know we're AD (Affiliated Distributors) — this matters for rebate programs"
- "Had to clarify that our warranty desk is different from our AR desk — Claude tried to route a customer refund wrong"
- "Claude didn't know our key competitor in the Albany market is Wholesale Supply — should be in context"

**What to do:**

1. Identify which file the missing information belongs in:
   - about-me.md — business facts, team structure, key vendors
   - my-context-map.md — tool locations, ERP details, portal URLs
   - writing-rules.md — communication preferences
   - specialist-routing.md — domain pain points
2. Draft the specific line to add.
3. If the information doesn't fit any existing file, note this — it might suggest a need for a new section or file.

## Cross-project insights

These are lessons from one project that apply broadly.

**What to look for across project memory files:**

- A workflow that worked well and could be reused (→ suggest a template or skill)
- A vendor-specific tactic discovered in one QBR that applies to similar vendors (→ add to universal memory)
- A mistake that cost money, to avoid in future projects (→ add as a "Lessons Learned" entry)
- A decision framework that proved useful (→ suggest adding to CLAUDE.md or creating a skill)
- Communication patterns that worked with specific customer segments (→ add to writing rules)

**Example cross-project insight for distributors:**

Project A memory: "Carrier Q1 QBR — added fill-rate trend as a required metric after getting caught off guard by a 5-point drop."
Project B memory: "Trane Q1 QBR — also caught a fill-rate drop we didn't see coming. Should have had trend data in hand."

→ This is a cross-project pattern. Propose: "Update the vendor-scorecard-template to require fill-rate trend (last 4 weeks) as a mandatory field, not optional. All vendor QBRs going forward use the trend version."

## Stale content

Things that may have been true once but aren't now.

**What to look for in distributor context:**

- Tools in the context map not mentioned in recent memory entries (stopped using? Or just didn't come up?)
- Vendors listed in About Me that don't appear in any Procurement-Vendors project in the last 6 months (relationship dormant? Dropped carry?)
- Pain points flagged as priority in specialist-routing that haven't generated any projects (fixed? Wrong priority?)
- Writing rules consistently overridden in memory corrections (rule is wrong)
- Projects in WORK AREAS/ with no memory updates in 60+ days (completed? Abandoned?)
- Branch details in About Me that memory contradicts (consolidation happened? New branch opened without updating file?)

**What to do:**

Don't assume things are stale — flag them as questions. "Your About Me lists Wolseley as a top vendor, but I haven't seen Wolseley come up in any project memory for 4 months. Still a top vendor, or should we update?" The user decides.

## Distributor-specific pattern to watch for

**The "one rep doing it all" signal** — if memory entries overwhelmingly mention one rep's name (Sarah/Tom/Mike), that rep might be overloaded. Flag: "Sarah's name appears in 40% of your project memory in the last 60 days. Either she's your best rep or your highest-risk attrition candidate. Worth a check-in."

**The "one account dominates" signal** — if one customer name dominates Customer-Accounts memory, the concentration is real. Flag the concentration % and ask whether mitigation projects should be spun up.

**The "same vendor problem repeats" signal** — if the same vendor (e.g., "Navien") shows up in negative memory entries multiple times (allocation issue, back-order, rebate dispute), surface the pattern. "Navien has appeared in 6 Procurement-Vendors memory entries in 90 days, all negative. Is this relationship at risk?"
