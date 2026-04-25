---
name: tidy
description: Scan a folder (Downloads, Desktop, ERP exports) and propose cleanup
---

# /tidy — File Cleanup Assistant

Help the user clean up a cluttered folder. Distributor-aware version — recognises ERP exports as a special category since distributors accumulate dozens of them per month.

## Flow

1. Use AskUserQuestion to ask which folder to scan:
   - "Downloads folder"
   - "Desktop"
   - "My ERP exports folder" (look at COMPANY/tools-and-context.md or about-me.md for the user's standard local folder convention — likely something like `~/Documents/Eclipse Exports/`)
   - "Choose a different folder"

2. If the folder isn't already accessible, use `request_cowork_directory` to ask the user to select it.

3. Scan the folder and categorise files:
   - **ERP exports** — files matching common patterns (`*-aging*`, `*dead-stock*`, `*margin*`, `*inventory*`, `*sales-by-*`). Flag duplicates (multiple aging exports from different dates), old ones (>90 days), and ones that match the standard monthly-pull cadence (1st of month).
   - **Large files** (>100MB) — flag with sizes
   - **Old files** (>30 days, not modified recently) — suggest archiving or deleting
   - **Duplicate names** — files with similar names that might be versions of the same thing (price file v1, v2, v3)
   - **Screenshots** — accumulated screenshots (often pile up on Desktop after vendor portal screen-grabs)
   - **Installers/DMGs** — downloaded installers that are probably no longer needed
   - **Quotes and proposals** — PDF/docx files matching customer-quote patterns; offer to move to the appropriate work area

4. Present a summary: "I found [X] files. Here's what I'd suggest..." Group by category with clear action proposals.

5. Use AskUserQuestion for each proposed action:
   - "Delete these [X] old installers?"
   - "Archive these ERP exports older than 90 days to a Downloads/Archive folder?"
   - "Move these screenshots to [suggested location]?"
   - "Move these vendor quotes to WORK AREAS/Procurement-Vendors/[vendor]-correspondence-project/inputs/?"

6. **Never delete without explicit confirmation.** Present the list, get approval, then act. If in doubt, suggest moving to a "to-review" folder rather than deleting.

7. Log the cleanup in the captain's log: "[time] — Tidied [folder]: removed X files, moved Y, archived Z, freed Q space."

## Distributor-specific behaviours

- If you see multiple ERP exports of the same type from the same month, propose keeping only the latest — distributors run the same canned report monthly and accumulate near-duplicates.
- If you see vendor portal screenshots, ask which vendor and offer to file them under `WORK AREAS/Procurement-Vendors/[vendor]-correspondence-project/inputs/`.
- If you see customer-named documents (quotes, proposals, agreements), ask if they should move to `WORK AREAS/Customer-Accounts/[customer]-account-project/`.

## Tone

Practical and slightly fun. "Your Downloads folder has 847 files in it. That's... ambitious. Let's sort this out." Don't be judgmental — everyone's Downloads folder is a disaster.
