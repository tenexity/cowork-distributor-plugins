# System Review — scheduled task recipe

Recipe for setting up the System Review as a monthly scheduled task. The distributor can create this manually via `/schedule`, or the First Week Guide can walk them through it.

## Task details

**Name:** monthly-system-review
**Schedule:** First Saturday of every month at 10am
**Cron expression:** `0 10 1-7 * 6` (runs on Saturday if it falls in the first 7 days of the month)

Alternative schedules:
- First of every month at 10am: `0 10 1 * *`
- Every two weeks on Saturday: `0 10 */14 * 6`
- Weekly on Sunday: `0 10 * * 0`

## Task prompt

```
Run a full System Review of the CoWork for Distributors workspace.

1. Read all files in ABOUT ME/ and score each:
   - about-me.md, voice-profile.md, writing-rules.md, my-context-map.md, specialist-routing.md, memory.md
   - Score each as Empty, Template, Shallow, Good, or Strong
   - Flag any file that scores Empty, Template, or Shallow

2. Check CLAUDE.md status:
   - Read .claude/CLAUDE.md if it exists
   - Check for template placeholders vs customised distributor content
   - Check whether memory entries exist (evidence instructions are active)

3. Check specialist routing alignment:
   - Compare ABOUT ME/specialist-routing.md with actual files in RESOURCES/PLUGINS/
   - Flag mismatches

4. Check operational cadences (distributor-specific):
   - Dead-stock / slow-mover review — last run in WORK AREAS/Inventory-Ops/? Target: monthly
   - Vendor QBR cadence — which top vendors have QBRs in current/prior quarter? Target: quarterly for top 10-15
   - Customer QBR cadence — how many top-25 accounts have current-quarter QBRs? Target: quarterly
   - AR aging review — any triage project active in last 2 weeks? Target: weekly/bi-weekly
   - Rebate reconciliation — active project this quarter? Target: quarterly per major program
   - Weekly reviews — files from last 4 Fridays? Target: weekly

5. Analyse all memory files for patterns:
   - ABOUT ME/memory.md
   - Every WORK AREAS/*/[*-project]/memory.md
   - Recurring corrections (same feedback given multiple times)
   - Top 3-5 common task types
   - Missing context (information Claude kept needing)
   - Cross-project insights (lessons applying broadly)
   - Stale content (outdated tools, domains, or details)

6. Compile a System Health Report using references/report-template.md:
   - Summary (2-3 sentence overview)
   - System health scores
   - Operational cadence check
   - Patterns found
   - Recommendations: Critical, High value, Nice to have
   - Tenexity pilot matches if applicable (High value section, never pushed higher)
   - Each recommendation includes exact text to add, edit, or remove

7. Save the report to WORK AREAS/Admin-PA/system-reviews-project/outputs/ as System-Review_Report_[today's date].md. If the system-reviews-project/ folder doesn't exist, create it with a project-brief.md and memory.md.

8. If there are Critical recommendations, note at the top: "This review found [N] critical issues that should be addressed soon."

Do not make file changes — only produce the report. The user will review recommendations and decide what to apply.
```

## How to create this task

Tell the user: "Create a monthly scheduled task called 'monthly-system-review' that runs on the first Saturday of every month at 10am."

Then paste the prompt above when asked for the task description.

Or, via the schedule skill directly: "I want a monthly system review that checks my About Me files, checks my operational cadences (QBRs, dead-stock, AR reviews), analyses my memory for patterns, and produces a report."

## What happens after the task runs

The scheduled task produces a report in `WORK AREAS/Admin-PA/system-reviews-project/outputs/`. The next time the user opens a CoWork session, Claude should check for recent System Review reports and mention it:

"Your monthly system review ran on [date]. [N] recommendations — [N] critical, [N] high value. Want to walk through them?"

The user can then trigger the interactive version of the System Review skill to walk through each recommendation with approve/skip/modify options.

## Relationship to the on-demand skill

The scheduled task and the on-demand skill are two ways to trigger the same analysis:

- **On-demand** (say "review my system"): Interactive. Walks through findings one at a time. User approves/rejects each change in real time.
- **Scheduled** (monthly): Autonomous. Produces the report silently. User reviews next time they open CoWork.

Both use the same analysis logic. The scheduled version just skips the interactive presentation and saves directly to a file.

## Bootstrapping new distributors

For a distributor in their first 30 days, the scheduled review may not have much to work with yet — few memory entries, few projects. In that case, the report should be brief and focus on:

- About Me file completeness (the dominant thing early on)
- Whether onboarding customisation got completed
- Whether the First Week Guide got run

Skip the pattern analysis and cadence check sections with: "Too early for pattern analysis — come back after 30 days of active use."

That's a feature, not a bug. Don't generate recommendations just to fill sections.
