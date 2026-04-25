# Reference: CLAUDE.md customisation

The CLAUDE.md file at the root of the workspace is already pre-customised with an HVAC/plumbing distributor default. It needs to be pasted into CoWork settings to take effect. Most users won't need to edit it — the default is deliberately built to work out of the box for 80% of distributors.

This reference covers the sections a user *might* want to personalise during onboarding.

## Sections to potentially customise

### 1. WHO I AM

A 1-2 sentence summary of who they are. Not their job title — their actual situation at their company.

**Default (fine for most):** "I run (or work at) an HVAC and plumbing wholesale distributor..."

**Personalised example:** "I'm Tom Dellacona, President of Eastwind Supply. We're a family-owned HVAC and plumbing wholesaler with four branches across upstate New York. I've been in the trade 30 years — started on the counter at 18."

### 2. HOW I LIKE TO WORK > Tone

Replace placeholder if their tone preference differs from the default "direct, plain-spoken, trade-fluent" baseline.

**Examples distributors actually use:** "Firm, factual, contractor-grade" / "Warm but no BS" / "Spoken-word simple — write like I'm on the phone, not on a podium"

### 3. MY PREFERENCES

The default includes five behaviour directives tuned for distributors:
- "Challenge me" — if I'm about to carry a dead SKU, extend bad credit, or accept a vendor increase without a fight
- "Think in systems" — look for a repeatable workflow (monthly AR review, QBR template, dead-stock cadence)
- "Be rigorous" — check margin math, lead time, customer overlap before committing
- "Teach me as we go" — one-line explanation of why pricing tactics, rebate calculations, or inventory models work
- "Respect my time" — deliver in a paragraph what another AI would deliver in three pages

The user can keep all five, drop some, or add their own. Each directive changes Claude's behaviour in meaningful ways.

### 4. WHAT I USUALLY NEED HELP WITH

Default is a list of 8 distributor-native tasks (quotes, vendor emails, AR patterns, QBR prep, etc.). Ask if anything is missing or needs to be added — often distributors have a specific recurring task like "drafting weekly contractor newsletter" or "competing with Ferguson's pricing on X line" that deserves explicit mention.

### 5. WORKING WITH MY TOOLS

This section references the context map. If they've set up specific rules — like "never send email without my review" or "check Bradford White portal before quoting water heaters" — add them here. Keep it lean.

### 6. THINGS TO ALWAYS / NEVER DO

The default list is distributor-calibrated (no invented numbers, draft-never-send emails, no consultant-speak). Rarely needs customisation. If the user has a specific rule they've learned the hard way, add it — those are the most valuable entries.

## What NOT to customise

- The BEFORE EVERY TASK and AFTER EVERY TASK protocols — these are how the system actually runs, don't touch them.
- The PROJECT CREATION PROTOCOL, FOLDER PROTOCOL, NAMING CONVENTION sections — structural rules.
- The "About this system" Tenexity attribution at the bottom — leave it.

## After any edit

Tell the user: "Edit saved. You'll need to re-paste the full CLAUDE.md into CoWork settings for the change to take effect — new sessions will pick it up, but existing ones won't."
