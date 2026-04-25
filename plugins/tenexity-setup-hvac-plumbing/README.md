# Tenexity Setup — HVAC & Plumbing Distributor

**The setup plugin for [CoWork for Distributors](https://tenexity.ai/distributors).** Install this once and the three skills required to use the scaffold are available in every CoWork session.

This plugin is the install path for setup. It is not an operational tool — once setup is complete, you'll rarely interact with it directly. The skills inside trigger on natural-language phrases like "set up my system" or "first week guide."

---

## What's inside

Three bundled skills, one per phase of getting started:

### Onboarding Coach (skill name: `setup-guide`)

A 20-minute guided session that customises the pre-filled `ABOUT ME/` files in the scaffold to your specific business — your company name, ERP, branch footprint, top vendors, customer mix, voice, and current operational pain. Replaces the HVAC/plumbing distributor archetype with your real details. After it runs, every future CoWork session knows your business without you re-explaining.

**Trigger phrases:** "set up my system," "help me get started," "configure my workspace," "personalise Claude," "onboard me," "walk me through setup."

### System Review (skill name: `system-review`)

Reads your memory files and About Me content, identifies patterns in how you've been using the system, catches setup problems, checks distributor-specific cadence signals (QBR cadence, rebate cycles, dead-stock reviews, AR triage), extracts cross-project lessons, and produces a System Health Report with proposed changes you approve or reject one at a time. Run it on demand or as a monthly scheduled task. The Onboarding Coach offers to set up the monthly cadence at the end of setup.

**Trigger phrases:** "review my system," "system health check," "what should I improve," "monthly review," "audit my system."

### First Week Guide (skill name: `first-week-guide`)

Five days of guided wins: a vendor email, an AR-aging review, a customer quote, a slow-mover report, and a QBR prep — all in your voice, all using your real business context. Each day produces output you keep and use. Teaches prompting principles by doing the work, not lecturing.

**Trigger phrases:** "first week guide," "what should I do first," "show me what this can do," "day 1," "day 2," etc.

---

## How this plugin differs from operational Tenexity plugins

This is a **setup** plugin — it bundles the three skills required to personalise the CoWork for Distributors scaffold to your business. It's the foundation for everything else.

The other plugins in the [Tenexity marketplace](https://github.com/tenexity/cowork-distributor-plugins) — Inventory Optimisation Coach, Rebate Reconciliation Specialist, future Quote Desk Assistant and Vendor QBR Prep Specialist — are **operational** plugins. They're deeper, domain-specific specialist agents you install when you're ready to tackle a specific operational problem (dead stock, rebate leakage, RFQ response, vendor QBR prep). They're optional. They don't depend on the setup plugin, but they assume you've completed onboarding so they know your business context.

**Setup is a one-time event. Operational plugins ship with their own ongoing cadence.**

---

## Why we ship setup as a plugin (not as a skill bundle in the scaffold)

The CoWork for Distributors scaffold also ships the same three `.skill` files inside `RESOURCES/MY-SKILLS-INSTALL/` for offline installs. The plugin path is the recommended install method because:

1. **No filesystem permission issues.** The plugin install pipeline pulls skills directly into Claude's managed skill area. The user's local file permissions, sandboxed app perms, and macOS TCC restrictions are all bypassed.
2. **Updates ship via `git push`.** When we revise a skill, distributors who installed via the marketplace get the update on their next CoWork open. No need to re-download the scaffold.
3. **One install, three skills.** Marketplace install loads all three skills in a single click. The loose-`.skill` path requires either three separate clicks or a working `present_files` flow, both of which are fragile across user environments.

The loose `.skill` files in the scaffold remain available as a documented offline fallback for users who can't connect to the marketplace (corporate firewalls, offline machines, audit requirements).

---

## Install

In CoWork (the Claude desktop app), with the CoWork for Distributors scaffold selected as your workspace:

1. Click **Customise** (sliders icon, bottom of the sidebar)
2. Go to **Plugins**
3. Click the **+** button next to *Personal plugins* and select **Add marketplace**
4. Paste this marketplace identifier and click **Sync**:
   ```
   tenexity/cowork-distributor-plugins
   ```
5. Once the marketplace loads, find **Tenexity Setup — HVAC & Plumbing Distributor** and click the **+** to install
6. The three skills auto-load. Restart CoWork if any of them don't appear immediately.
7. Back in chat, say **"set up my system"** — the Onboarding Coach takes it from there.

---

## Support

- **This plugin:** [cowork@tenexity.ai](mailto:cowork@tenexity.ai)
- **The CoWork for Distributors scaffold:** [tenexity.ai/distributors](https://tenexity.ai/distributors)
- **Operational pilots:** book 20 minutes — [https://calendly.com/graham-tenexity/quick-chat](https://calendly.com/graham-tenexity/quick-chat)

---

## Version

Tenexity Setup — HVAC & Plumbing Distributor v1.0.0 — April 2026
