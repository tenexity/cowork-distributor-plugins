# Contact Structure — Distributor Edition

## Purpose

When people are mentioned in conversation with context, the PA logs them in `WORK AREAS/Admin-PA/contacts.md`. Over time this becomes a living register of every relationship that touches the user's work — vendors, customers, internal team, buying group contacts.

This file specifies the format and the distributor-specific contact types.

## File path

`WORK AREAS/Admin-PA/contacts.md`

## Contact types (distributor-specific)

Every contact gets a type. Defaults:

| Type | Examples |
|---|---|
| **Vendor** | Manufacturer reps, principals, regional managers, factory contacts |
| **Customer** | Plumbing/HVAC contractors, service techs, builders, MRO accounts, key-account decision-makers |
| **Internal** | Branch managers, counter sales, outside sales, inside sales, purchasing, AR, warehouse |
| **Buying group** | Affiliated, IMARK, Wolseley, AD, NETWORK contacts |
| **Trade association** | HARDI, ASA, PHCC, ACCA, ASHRAE contacts |
| **Service provider** | Accountant, lawyer, IT vendor, freight provider, consulting |
| **Other** | Anything that doesn't fit above |

## Entry format

```markdown
## [Name]

- **Type:** [Vendor / Customer / Internal / Buying group / Trade association / Service provider / Other]
- **Company / Account:** [Their company / for customers, the contractor or shop name]
- **Role:** [Title / function]
- **Last mentioned:** [date]
- **Mention count (last 90 days):** [N]
- **Context:** [How the user knows them, what they're known for, distinctive attributes]
- **Notes:** [Key facts from conversations — preferences, history, deals in flight]
- **Follow-ups:** [Pending actions involving them — links to task IDs or descriptions]
- **Preferred contact mode:** [Phone / email / text / in-person / unspecified]
```

## Distributor-specific fields

Beyond the basics, capture these when they come up naturally:

### For Vendors

- **Region:** Their territory (Northeast, Southeast, etc.)
- **Programs:** Which programs they manage for the user (allocation, rebate, MDF, co-op)
- **Decision authority:** Are they the rep with rope to negotiate, or the conduit to the principal?
- **Last QBR:** Date of last QBR meeting
- **Next QBR:** Scheduled date

### For Customers

- **Trade type:** Plumbing contractor / HVAC contractor / mechanical contractor / service tech / builder / MRO / other
- **Account size tier:** Top 25 / top 100 / general account
- **Decision-maker:** Yes / no — are they the one making purchase decisions, or are they a buyer relaying decisions from someone else?
- **Cadence:** Daily / weekly / monthly / project-based — how often you'd expect to interact
- **Pricing tier:** Standard / contract / matrix tier (if you use tiered pricing)
- **Credit status:** Good / watch / hold

### For Internal team

- **Branch:** Which branch they're based at (use the branch list from COMPANY/company-profile.md or about-me.md)
- **Reporting line:** Who they report to / who reports to them
- **Specialisms:** What categories or accounts they own

## Auto-update rules

The PA updates contact entries automatically when new information appears in conversation:

- **First mention** — create the entry with whatever info is in that mention
- **Subsequent mentions** — increment mention count, update "last mentioned" date, append to notes if there's new context
- **Type inference** — if not explicit, infer from context:
  - "Mike at Carrier" → Vendor
  - "Pat at Smith Plumbing" → Customer
  - "Eric in purchasing" or "Eric (purchasing)" → Internal
  - "Tom from Affiliated" → Buying group
  - "the rep from Bradford White" → Vendor
- **Role inference** — pick up titles from conversational mentions ("their VP of operations", "the regional manager")

If type is genuinely ambiguous (just a name, no context), default to "Other" and ask the user once: "I added [name] but wasn't sure if they're a vendor, customer, or internal — quick clarification?"

## Example entries

```markdown
## Mike Reynolds

- **Type:** Vendor
- **Company / Account:** Carrier
- **Role:** Regional Sales Manager — Northeast
- **Last mentioned:** 2026-04-09
- **Mention count (last 90 days):** 7
- **Context:** Carrier rep covering our four-branch territory. Took over from Bob in January 2026. Works on commission-plus-allocation programmes; has rope to negotiate but tougher than Bob was.
- **Notes:** Allocation discussions in March '26 went better than expected. Rebate Q1 came in at plan. Fluent in our YTD purchase numbers — assume he prepares with our data.
- **Follow-ups:** Send Q2 YTD purchase data by Friday 11 Apr (re Q2 allocation pushback)
- **Preferred contact mode:** Phone — does not respond well to email-only
- **Region:** Northeast
- **Programs:** Allocation, MDF, growth rebate
- **Decision authority:** Has rope to negotiate up to a point; goes to principal for major exceptions
- **Last QBR:** 2026-01-15
- **Next QBR:** 2026-04-22

## Pat O'Brien

- **Type:** Customer
- **Company / Account:** Smith Plumbing
- **Role:** Owner / decision-maker
- **Last mentioned:** 2026-04-09
- **Mention count (last 90 days):** 3
- **Context:** Pat owns Smith Plumbing — 8 plumbers in residential and light commercial. Been a customer 12 years. Strong relationship until Q1 when his AR started slipping.
- **Notes:** $34K aged over 90 days as of 9 Apr. Went on credit hold this morning. Pat has not been answering emails — phone-only contact mode confirmed.
- **Follow-ups:** Call Pat tomorrow re credit hold
- **Preferred contact mode:** Phone
- **Trade type:** Plumbing contractor
- **Account size tier:** Top 25
- **Decision-maker:** Yes
- **Cadence:** Was weekly; recently quiet
- **Credit status:** Hold
```

## Privacy considerations

For internal team entries, mark anything sensitive (performance, salary, HR escalations) with `[private]` after the relevant field. The System Review skips `[private]` fields when generating reports the company admin sees.
