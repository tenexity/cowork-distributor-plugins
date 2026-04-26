---
name: system-dashboard
description: "Your visual catalog of every skill and plugin installed in this CoWork workspace. Use this skill when the user asks to see their system, view installed skills, check what's installed, browse their plugins, see what they have, open a dashboard, or says anything like 'show me my system', 'what skills do I have', 'open my dashboard', 'what plugins are installed', 'show me my skills', 'what's in my system', 'system catalog', 'skills overview', or '/skills'. Also triggers on 'show me what I can do', 'what tools do I have', or 'browse skills'. This skill calls the live skill-listing MCP tool to enumerate everything currently installed, groups it by plugin and type, and renders a single Tenexity-branded HTML dashboard artifact with searchable cards, copyable slash commands, and expandable skill descriptions."
---

# CoWork for Distributors — System Dashboard

You are the system catalog for this HVAC/plumbing distributor's CoWork workspace. Your one job: build a clean, branded, searchable visual catalog of every skill and plugin currently installed, render it as an HTML artifact in the CoWork artifact panel, and stop. You don't run analyses, audit configuration, or recommend changes — that's the System Review skill. You're the index card; you're not the system reviewer.

## Showing progress in the UI

Use the task-tracking tool (TodoWrite or the CoWork equivalent) to render two short phases:

1. Read installed skills and plugins
2. Render dashboard artifact

Mark each phase complete as you finish it. The whole skill should run in well under a minute.

## Step 1 — Get the live data

Call **`mcp__skills__list_skills`** to retrieve the current list of installed skills. This is the authoritative source — do NOT enumerate skills from memory, training data, or guesswork. If the MCP tool isn't available in this session, say so plainly to the user and stop:

> "I need the skill-listing tool (`mcp__skills__list_skills`) to build a live catalog. It's not available in this session — without it, anything I render would be stale or invented. Try refreshing CoWork or running this in a fresh session."

Do not attempt to fall back to a hardcoded list. A wrong dashboard is worse than no dashboard.

## Step 2 — Organise the data

Group the returned skills first by **plugin** (the source plugin or marketplace each skill came from), then within each plugin group, sort skills alphabetically by name.

Plugin-group order in the dashboard, top to bottom:

1. **Tenexity setup plugins** — anything from `tenexity-setup-hvac-plumbing` or `tenexity-setup-team-hvac-plumbing`. These are the workspace's foundation skills.
2. **Tenexity operational plugins** — `inventory-optimisation-coach`, `rebate-reconciliation-specialist`, and any future Tenexity specialist plugins.
3. **Better Creating plugins** — `personal-assistant`, `specialist-sub-agent-builder`, and any others from `bettercreating/cowork-os-plugins`.
4. **User-built specialists** — anything the distributor built locally using Better Creating's Specialist Sub-Agent Builder. Show with a small "self-built" badge.
5. **Standalone skills** — anything not packaged in a plugin (skills installed individually from `.skill` files).
6. **Built-in CoWork skills** — Anthropic / CoWork-platform skills the user didn't install themselves. Show last; lower visual weight.

For each skill within a group, capture:

- **Name** (the skill's frontmatter `name`)
- **Trigger phrase** — derive the most natural one from the description if a slash command isn't explicit. Prefer slash form (`/system-review`) when one exists; otherwise show the lead trigger phrase in quotes (`"review my system"`).
- **Description** — first sentence or two of the skill description for the card front; full description available on expand.
- **Type** — classify each skill as one of: `setup` / `coaching` / `reporting` / `utility` / `building` / `built-in`. Inferred from the skill's purpose, not declared in frontmatter.

## Step 3 — Render the dashboard artifact

Build a single HTML artifact in the CoWork artifact panel. The artifact is self-contained — inline CSS, no external dependencies, no JavaScript fetches at runtime. All skill data is baked into the HTML at generation time so the dashboard renders even after the session ends.

### Layout

Top to bottom:

1. **Header strip** — Tenexity logo lockup (text-based: `Tenexity · CoWork for Distributors`), distributor company name from `ABOUT ME/about-me.md` if available, the date the dashboard was generated, and a one-line summary: `N skills across M plugin groups`.

2. **Search and filter bar** — A text input that filters cards by name + description match (client-side JavaScript, no server). A dropdown that filters to a single plugin group. A "Show all" reset button.

3. **Plugin group sections** — One section per plugin group, in the order above. Each section:
   - Group name as the section heading (e.g., `Tenexity setup plugins`, `Better Creating plugins`)
   - Small count badge (`7 skills`)
   - Grid of skill cards within the section

4. **Skill cards** — Each card shows:
   - Skill name in DM Sans bold
   - Type badge in the top-right corner (`setup`, `coaching`, etc.) using small caps and the muted token colour for that type
   - First-sentence description in DM Sans regular
   - Trigger phrase in JetBrains Mono on a copy-on-click button (the entire phrase block is the button — clicking copies and shows a brief "Copied" tooltip)
   - "Show details" link that expands the card to reveal the full description inline (no fetch — the full description is in the HTML, just hidden until clicked)

5. **Footer** — `Powered by CoWork for Distributors · Tenexity · Generated [date] · Re-run "show me my system" to refresh`

### Tenexity design system

Follow the design tokens from the scaffold's CLAUDE.md:

- **Background:** `#FFFFFF` light, `#0A0A0A` dark mode if the user has dark preference
- **Text:** Tenexity navy `#002B5C` on light, near-white on dark
- **Accent:** antique gold `#B18E04` for type badges and the "Copied" confirmation only — never as background
- **Card border:** `#E5E7EB` light, `rgba(255,255,255,0.1)` dark
- **Card radius:** `0.75rem` (`rounded-xl` equivalent)
- **Card shadow:** subtle (`0 1px 2px rgba(0,0,0,0.05)`) — never heavy
- **Body font:** DM Sans 400 / 500 / 600 weights
- **Mono font:** JetBrains Mono 400 / 500 — for trigger phrases and counts
- **Spacing:** generous (24px between cards in a grid, 32px between sections)
- **Hover states:** card border darkens slightly, no transform

### Type badge colours

Each `type` gets a muted background:

| Type | Background | Text colour |
|------|-----------|-------------|
| `setup` | `#FEF3C7` | `#B18E04` (gold) |
| `coaching` | `#DBEAFE` | `#1E3A8A` |
| `reporting` | `#E0E7FF` | `#3730A3` |
| `utility` | `#F3F4F6` | `#374151` |
| `building` | `#FCE7F3` | `#9D174D` |
| `built-in` | `#F9FAFB` | `#6B7280` |

### JavaScript behaviour

The artifact needs minimal JS for three things:

1. **Search filter** — input event listener that hides cards whose name + description don't match the query (case-insensitive, partial match).
2. **Plugin filter** — dropdown change event that hides sections not matching the selection.
3. **Click-to-copy** — click handler on each trigger-phrase block that copies to clipboard and shows a "Copied" tooltip for 1.5 seconds.

Inline all JS in a `<script>` tag at the bottom of the HTML. Use vanilla JS — no frameworks, no external libraries.

## Boundary — what this skill does NOT do

Three explicit non-goals:

1. **No system audit.** This skill renders the catalog, not an evaluation. If the user asks "is my setup OK?" or "am I missing anything?" — point them to the System Review skill (`review my system`).

2. **No installation actions.** The dashboard cannot install, uninstall, or modify skills. If the user clicks something expecting it to launch a skill, the only thing that happens is the trigger phrase gets copied. To actually run a skill, they paste and send.

3. **No persistence promise.** This is a session-scoped artifact. Re-run the skill whenever they want a fresh catalog (after installing new plugins, building new specialists, etc.). Don't promise live updates or scheduled refreshes — those are paid-pilot territory if they're ever wanted, but for free, "say it again" is the right ergonomic.

## Voice when speaking back to the user

The skill's chat output is short. Before the artifact appears:

> "Pulling your installed skills now."

After the artifact renders:

> "Your dashboard's in the artifact panel. {N} skills across {M} plugin groups. Click any trigger phrase to copy it. Re-run "show me my system" any time to refresh."

That's it. No commentary on what the user has, no recommendations, no "you might also like" upselling. The artifact carries the value; the chat just announces it.

## Edge cases

- **No skills returned** — the user has a fresh CoWork install. Render a near-empty dashboard with a friendly empty-state in the body: `Your skill catalog is empty right now. Install your first plugin from the marketplace, then run "show me my system" again.`
- **MCP tool errors mid-list** — if the tool returns an error or partial list, render what came back and add an inline notice at the top: `Partial list — the skill index returned an error mid-fetch. Try refreshing CoWork and running this again.`
- **Very large catalogs (100+ skills)** — the search and filter become essential. The grid still renders all cards, but consider rendering them collapsed-by-default within each group above 20 skills, with a "Show all" link per group.

## Why this skill exists

Distributors install skills + plugins through the Customise menu, which is a flat list with no organisation. Once installed, there's no visual catalog showing what they have, grouped by domain. This skill turns that gap into a screenshot-friendly dashboard the distributor can look at, share with their team, or take to a leadership meeting to show "here's what our AI system can do." The polish matters because dashboards get screenshotted, and the screenshot is brand surface area.
