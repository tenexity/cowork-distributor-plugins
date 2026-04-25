# Tenexity Setup Team — HVAC & Plumbing Distributor

**The multi-user setup plugin for [CoWork for Distributors](https://tenexity.ai/distributors).** Designed for HVAC and plumbing wholesale distributors deploying CoWork across a team of 5-50 employees. Install once per machine; the four bundled skills handle company-level setup, individual setup, ongoing reviews, and guided first-week onboarding.

For solo distributors and single-user installs, use the **Tenexity Setup — HVAC & Plumbing Distributor** plugin instead (one-skill setup, no company layer).

---

## What's inside

Four bundled skills, each handling a distinct part of the lifecycle:

### Setup Company (skill name: `setup-company`)

Run **once per company** by the GM, owner, or designated admin. ~15 minutes. Captures the business itself — ERP, branches, top vendors, customer mix, voice and writing rules, operational rhythm — into the four files in `ABOUT ME/COMPANY/`. Every employee at this company inherits this configuration when they run their individual setup.

**Trigger phrases:** "set up the company", "set up my company", "company setup", "configure the company layer", "I'm the GM doing the initial setup".

### Setup User (skill name: `setup-user`)

Run **once per individual employee**. ~5 minutes. Reads existing `ABOUT ME/COMPANY/` files (so it doesn't waste time re-asking about ERP, vendors, business context) and only captures individual info: name, role, branch, voice override (if any), priorities, pain points. Overwrites `first-run.md` with a SETUP COMPLETE marker when it finishes.

**Trigger phrases:** "set up my profile", "set up my user layer", "configure my profile", "set up my system", "help me get started", "onboard me".

### System Review (skill name: `system-review`)

Reads both COMPANY and USER layer files plus session memory and project work. Identifies patterns, catches setup drift, checks distributor-specific cadence signals (QBR cadence, rebate cycles, dead-stock reviews, AR triage), produces a System Health Report with proposed changes. Distinguishes COMPANY-level recommendations (admin approval) from USER-level recommendations (this user's call).

**Trigger phrases:** "review my system", "system health check", "monthly review", "audit my system".

### First Week Guide (skill name: `first-week-guide`)

Five days of guided wins: a vendor email, an AR-aging review, a customer quote, a slow-mover report, and a QBR prep — all in the user's voice with their company's context. Each day produces output the user keeps and uses.

**Trigger phrases:** "first week guide", "what should I do first", "show me what this can do", "day 1", "day 2", etc.

---

## Two-layer architecture

Setup happens in two stages because most distributor employees share the same business context (ERP, vendors, voice) but each has their own role, voice, and priorities.

```
ABOUT ME/
├── COMPANY/                          (admin-managed; identical across all 40 users)
│   ├── company-profile.md
│   ├── voice-and-writing-rules.md
│   ├── tools-and-context.md
│   └── specialist-routing.md
└── USER/                             (per-employee; their personal layer)
    ├── me.md
    ├── my-voice.md                   (overrides company default if present)
    ├── my-priorities.md
    └── my-memory.md
```

The first deployer at the company runs **Setup Company**. Each subsequent employee runs **Setup User**. Together they take ~15 minutes for the admin and ~5 minutes per employee — vs. ~20 minutes per employee in the single-user model.

For 40 employees: that's ~3 hours of total onboarding for the company instead of ~13 hours, and the company-level data is consistent across everyone instead of inconsistently re-typed by each user.

## Distribution — how the COMPANY/ layer reaches every employee

When the admin completes Setup Company, the four COMPANY/ files exist on their machine. To get those files onto every employee's machine, three options:

### Option 1 — Private GitHub repo (recommended for 5-50 users)

Admin creates a private GitHub repo (e.g., `acme-supply/cowork-config`) and pushes the COMPANY/ folder there. Each employee's first-run flow asks for the repo URL and clones it into their local scaffold. Updates ship via `git push` from admin and `git pull` from each user — or by re-running the bootstrap script.

The scaffold ships with a `bootstrap.sh` script that handles the clone for non-technical users.

### Option 2 — Cloud share (Google Drive, OneDrive)

Admin puts COMPANY/ in a shared cloud folder. Each employee copies the contents into their local `ABOUT ME/COMPANY/` before running Setup User. Manual but works for small teams that don't have a GitHub workflow.

### Option 3 — Tenexity-hosted private plugin (paid service)

Tenexity hosts a per-company private plugin in a dedicated marketplace. Each employee installs that plugin from a marketplace identifier, and CoWork's plugin install pipeline handles file delivery automatically — same flow as the public Tenexity Setup plugin, but with this specific company's COMPANY/ data baked in. Cleanest UX but Tenexity manages the per-company infrastructure. Available as part of paid pilots — contact `cowork@tenexity.ai`.

## Install (this plugin)

In CoWork (Claude desktop), with the CoWork for Distributors v2 scaffold selected as your workspace:

1. **Customise** (sliders icon) → **Plugins**
2. Click **+** next to *Personal plugins* → **Add marketplace**
3. Paste this marketplace identifier and click **Sync**:
   ```
   tenexity/cowork-distributor-plugins
   ```
4. Confirm the third-party safety notice (standard for non-Anthropic marketplaces)
5. Find **Tenexity Setup Team — HVAC & Plumbing Distributor** in the list and click **+** to install
6. Quit CoWork (Cmd+Q) and reopen if any of the four skills don't appear in `Customise → Personal Skills`
7. Back in chat, follow the first-run flow in `ABOUT ME/first-run.md`

---

## Support

- **This plugin:** [cowork@tenexity.ai](mailto:cowork@tenexity.ai)
- **The CoWork for Distributors scaffold:** [tenexity.ai/distributors](https://tenexity.ai/distributors)
- **Operational pilots and Tenexity-hosted private company plugins:** book 20 minutes — [https://calendly.com/graham-tenexity/quick-chat](https://calendly.com/graham-tenexity/quick-chat)

---

## Version

Tenexity Setup Team — HVAC & Plumbing Distributor v1.0.0 — April 2026
