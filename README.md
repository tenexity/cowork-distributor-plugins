# Tenexity Plugin Marketplace

**Plugins for HVAC and plumbing wholesale distributors using [CoWork for Distributors](https://tenexity.ai/distributors).**

This is the public Tenexity marketplace of CoWork OS plugins. Add it once to your CoWork desktop app and every Tenexity plugin — current and future — becomes installable in one click.

---

## How distributors install this marketplace

Inside CoWork, click **Customise** (sliders icon, bottom-left) → **Plugins** → click **+** next to "Personal plugins" → **Add marketplace**, then paste:

```
tenexity/cowork-distributor-plugins
```

Click **Sync**. CoWork shows a standard third-party safety notice (Anthropic shows this for every non-Anthropic plugin marketplace — it's not specific to Tenexity). Click **Sync** to confirm.

You'll see Tenexity's plugins listed under the **Personal** tab. Click **+** on each one you want to install.

---

## Available plugins

Plugins are added here as they ship. Run `cat .claude-plugin/marketplace.json` for the live list.

Shipping in v0.1:

- **Tenexity Setup — HVAC & Plumbing Distributor** — bundles the three skills required to personalise the CoWork for Distributors scaffold: Onboarding Coach, System Review, and First Week Guide. Install this first; everything else assumes you've completed onboarding.
- **Inventory Optimisation Coach** — coaches distributors through dead-stock analysis, reorder-point reviews, branch-level transfer rebalancing, vendor return programs, and working-capital snapshots. ERP-agnostic; you paste exports.
- **Rebate Reconciliation Specialist** — coaches distributors through vendor rebate program reconciliation, threshold tracking, claim drafting, and leakage identification. Vendor-agnostic; you paste program terms.

The **setup plugin** packages the three setup skills into a single one-click install — no file-permissions roulette, no marketplace fallback for skills.

The **two operational plugins** are scaffold-layer free coaches — they explain methodology, ask for ERP exports as pasted input, and produce one-shot analyses. They do not connect to ERPs, manufacturer portals, or run scheduled jobs. Ongoing automation, ERP integration, and persistent state are part of paid Tenexity pilots — see [tenexity.ai/distributors](https://tenexity.ai/distributors) for pilot details.

---

## Plugins planned for future versions

These will appear in the marketplace as they ship:

- Quote Desk Assistant (v0.2) — RFQ response coach with margin guardrails
- Vendor QBR Prep Specialist (v0.3) — quarterly business review prep coach
- Customer Account Health Monitor (v0.4)

Tracked in the parent CoWork-class repo at `tenexity-marketing/00-Marketing-Launch-Checklist.md`.

---

## How Tenexity adds new plugins to the marketplace

This marketplace repo is the published surface. The internal build process happens in the parent CoWork-class repo at `tenexity-plugins/`:

1. **Brief and curate.** Write the specialist brief and knowledge base entries in `tenexity-plugins/<NN>-<Specialist>/`.
2. **Run Better Creating's Specialist Sub-Agent Builder** in a CoWork session — it consumes the brief and KB, walks through the 8-step build, and outputs a `.plugin` file.
3. **Unpack the .plugin file** into `tenexity-plugins/marketplace/plugins/<plugin-name>/`. Each plugin's internal structure (`.claude-plugin/plugin.json`, `skills/`, `scripts/`, `README.md`) comes from the Builder.
4. **Update `.claude-plugin/marketplace.json`** in this folder — add an entry to the `plugins` array following BC's schema (name, source, description, version, author, category, tags).
5. **Push to the public marketplace repo** at `github.com/tenexity/cowork-distributor-plugins`. From that point distributors who have already added the marketplace see the new plugin appear automatically.

The full build workflow lives in `tenexity-plugins/README.md`.

---

## Schema reference

The `marketplace.json` schema follows the Anthropic plugin-marketplace standard, modeled directly on Better Creating's `bettercreating/cowork-os-plugins`. Top-level keys:

| Key | Required | Description |
|-----|----------|-------------|
| `name` | yes | Marketplace identifier (used in CoWork UI) |
| `owner` | yes | `{ name, email }` of the publisher |
| `metadata` | yes | `{ description, version }` for this marketplace |
| `plugins` | yes | Array of plugin entries |

Per-plugin entry keys:

| Key | Required | Description |
|-----|----------|-------------|
| `name` | yes | Plugin slug (kebab-case) |
| `source` | yes | Path within this repo (e.g. `./plugins/inventory-optimisation-coach`) |
| `description` | yes | One-paragraph description shown in the CoWork plugin browser |
| `version` | yes | Semver string |
| `author` | yes | `{ name }` |
| `category` | recommended | One of: `agent-building`, `productivity`, `inventory`, `finance`, `sales`, etc. |
| `tags` | recommended | Array of strings for search |

---

## License

Plugins published in this marketplace are under their individual licenses; see each plugin's own LICENSE file.

The marketplace metadata in this repo (this README, `.claude-plugin/marketplace.json`) is © Tenexity, MIT licensed.

---

## Support

- **Plugin questions:** [cowork@tenexity.ai](mailto:cowork@tenexity.ai)
- **Distributor scaffold questions:** see [tenexity.ai/distributors](https://tenexity.ai/distributors)
- **Pilot conversations:** book 20 minutes — see the link inside any installed plugin or email above

---

## Version

Tenexity Plugin Marketplace v0.1.0 — April 2026
Schema based on Better Creating's CoWork OS plugins marketplace.
