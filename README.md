# Josiah's Life Skills

A small collection of personal [Claude Agent Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) — reusable, structured workflows that make Claude tackle a task the same careful way every time.

Each skill is a folder with a `SKILL.md` (the instructions Claude follows) plus any supporting files. They work in **Claude Code**, and — because they use the open Agent Skills format — also in **Claude on the desktop / web (including Cowork)**. Install instructions for both are below.

## Skills in this repo

### 🛒 product-scout

Finds the best product to buy in a category and hands you a formatted HTML buying report.

You ask something like *"what's the best e-ink phone I can use in Australia?"* and it:

1. **Scopes** the category with a few quick searches — the features that matter, the price bands, the dedicated subreddit.
2. **Grills** you, one question at a time, into a sharp brief: what it's for and *why*, your non-negotiables vs nice-to-haves, budget, country, how you'll buy it, and how long you'll wait.
3. **Researches** the market — current, upcoming, and adjacent products — weighing manufacturer specs against real **owner reports** from Reddit and forums, and checks it can actually be bought and supported where you live.
4. **Writes** a single self-contained HTML report: a clear verdict, comparison table, pros/cons grounded in owner reports, device photos, a trustworthy video review per top pick, and local pricing.
5. **Fact-checks** it with a fresh, independent reviewer before you ever see it, so the headline claims are verified — not just asserted.

Best results need the **Exa** and **Firecrawl** tools (see [Requirements](#requirements)); without them it still runs, just shallower, and says so.

### 🥾 Hike Route Skill

*(work in progress)*

## Requirements

`product-scout` is designed around two web-research tools and is much better with them:

- **[Exa](https://exa.ai)** — semantic, meaning-based web search.
- **[Firecrawl](https://firecrawl.dev)** — full-page scraping of sites that block simple fetches (retailer pricing, Reddit, JS-heavy pages).

If they aren't installed, the skill will tell you and offer to walk you through it, then fall back to Claude's built-in web search — the report just won't be as deep.

**Installing them in Claude Code:**

```
/plugin marketplace add anthropics/claude-plugins   # if not already added
/plugin install exa
/plugin install firecrawl
```

Then restart the session. (In Claude desktop/Cowork, add Exa and Firecrawl as connectors / MCP servers under **Settings → Connectors**.)

## Install

### Claude Code

Copy the skill folder into your personal skills directory:

```bash
cp -r "product-scout" ~/.claude/skills/
```

The skill (e.g. `product-scout`) sits directly under `~/.claude/skills/`, containing its `SKILL.md`. Start a new session and it's available — Claude will trigger it automatically when you ask what to buy, or you can invoke it by name.

To install `product-scout`, use the folder at `Product Research Skill/product-scout`.

### Claude on the desktop or web (for friends not using Claude Code)

Skills work in regular Claude too — including **Cowork** sessions — on Pro, Max, Team, and Enterprise plans with code execution enabled.

1. **Zip the skill folder** so the folder itself is at the root of the zip (not just its contents). For product-scout, zip the `product-scout` folder inside `Product Research Skill/`.
2. On **claude.ai**, go to **Settings → Customize → Skills → Upload** and upload the zip. Claude reads the `SKILL.md` and shows the skill's name and description.
3. Enable the skill. **Cowork sessions load whatever skills are enabled on your claude.ai account** (synced at session start), so once it's uploaded and enabled it's available in both chat and Cowork.

For a whole team, an admin can upload it once under **Organization Settings → Skills** to provision it to everyone.

## How skills work, in one line

A `SKILL.md` is Markdown with a little YAML header; Claude loads it when the task matches, and follows the steps inside. Larger skills push detail into extra files (this repo's `product-scout` keeps its research, report, and review protocols in separate files it loads only when it reaches that phase) so the main instructions stay short. See Anthropic's [Agent Skills docs](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) for the full format.

## Note on generated reports

Running a skill produces output locally (e.g. `product-research/<category>/report.html`). Those files are **git-ignored** — they're personal output and embed third-party product images, so they're not committed to this public repo.
