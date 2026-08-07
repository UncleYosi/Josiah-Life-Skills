---
name: product-scout
description: Research a purchase and deliver an HTML buying report naming three picks.
disable-model-invocation: true
---

# Product Scout

Buying advice is only as good as the brief behind it. Run the phases in order — **scoping**, **grilling**, **research**, **report**, **check** — and let no later phase start early.

## Pace

Once the brief is confirmed, the user is waiting. Target **≤8 minutes from the end of grilling to the delivered report**. Depth comes from fanning out parallel background agents, and from stopping the moment a candidate clearly wins or clearly fails — never from a slow serial crawl. Each phase below carries a hard cap: treat it as a budget you spend, not a floor you must reach.

## Tools: run deep, or run shallow

Check your available tools for **Exa** (`web_search_exa`, `exa:search`) and **Firecrawl** (`firecrawl_search`, `firecrawl_scrape`, `firecrawl_map`). They do the semantic sweeps and full-page scraping that make the research good.

Whatever you find, **start the run anyway**. Missing either puts you in **shallow mode**: `WebSearch` and `WebFetch` instead, weaker semantic sweeps, some JS-heavy retailer and Reddit pages unreadable — so lean harder on the review sources the user names in grilling. Carry that fact to the report's footnote and one line at delivery, where the user can weigh it against the finished work instead of being stopped at the door.

### When a tool starts refusing

Rate limits, spent quotas and blocked pages are normal mid-run. The cheap response is to **step down the ladder**:

`firecrawl_scrape` / `web_search_exa` → `WebFetch` → `WebSearch` snippet → record the field as *unverified, source blocked* and move on.

**One retry per call, then step down.** A failing call re-run in a loop is the single most expensive thing this skill can do. When a whole tool is gone for the session — monthly quota spent, plan limit hit — drop to shallow mode for the remainder, note it in the footnote, and keep going. A delivered report that names three picks and flags two unverified figures beats a run that dies at 80%.

Fanning out multiplies this: six agents scraping at once will hit a free-tier per-minute limit that one agent never would. Expect it, and let them step down rather than retry.

### Browser automation stays off

`claude-in-chrome` sits outside this skill's normal path — its screenshots and page dumps cost more tokens than the entire rest of the run. When one page genuinely decides the verdict and every text tool has failed on it, **ask the user first**, naming the page and what you need from it, and use it only on a yes.

## Phase 1 — Scoping

Learn enough of the category's own language to ask good questions. **Cap: one round of up to four `WebSearch` calls, issued in parallel.** The heavy tools stay holstered until Phase 3.

Establish:

- The **feature axes** buyers trade off, in the words owners actually use.
- The **price bands** the market sorts into, and what moves a product between them.
- The **review sources** for this category — the dedicated subreddit(s), the forums, the YouTube channels and review sites people cite. You put this list to the user in Phase 2, so name them specifically.
- The **incumbents**: the two or three products named reflexively when this question is asked.

Scoping is groundwork for good questions, not a shortlist. Evaluating products comes later.

**Done when** you can state the feature axes, the price bands, and a named list of candidate review sources — and the user has seen a short scoping summary.

## Phase 2 — Grilling

Interview the user until you reach a shared understanding of what they want and why. Walk down each branch of the decision tree, resolving dependencies one at a time.

Ask **one question at a time** and wait for the answer. For each, offer your recommended answer drawn from scoping — especially budget, where the user is often anchored to nothing. **Skip whatever their opening message already answered**: restate it as a confirmed line instead of asking it back.

The **brief** covers:

- **Purpose** — what the product is for, and the underlying reason they want it. Push past the first answer; "I want an e-ink phone" is a solution, "I want to stop doom-scrolling in bed" is the purpose.
- **Non-negotiables** — features that disqualify a product if absent.
- **Nice-to-haves** — ranked, so trade-offs can be made against them.
- **Dealbreakers** — the inverse: what rules a product out.
- **Budget** — a band, with your recommendation from the scoped price bands.
- **Country** — where they are buying and using it, which decides pricing, warranty, and availability.
- **Sourcing** — who they will buy from and how long they will wait. An AliExpress white-label arriving in three weeks and a known brand on Amazon arriving tomorrow are different products.
- **Timeline** — buying now, or able to wait for something unreleased.
- **Incumbent** — what they use today and what's wrong with it.
- **Review sources** — put your scoped list to them: which of these do they trust, and is there one you missed? Their answer decides where Phase 3 mines owner reports, so give it its own question rather than folding it into another.

Facts you can look up, look up. Decisions are the user's — put each one to them.

**State implied constraints out loud as they emerge.** When an answer forces a downstream consequence — "Beeper and an authenticator both need full Android, so the walled-OS phones are out" — say it in the moment and fold it into the brief. Surfacing the deduction sharpens the brief and eliminates whole branches before research.

Close with one logistics question, outside the brief: **how to deliver the report** — a Claude Artifact (a hosted page they can open anywhere and share), an HTML file, or both. Recommend both.

**Done when** you have written the brief back to the user as a numbered list and they have confirmed it, and you know their review sources and their delivery choice.

## Phase 3 — Research

Read `RESEARCH.md` and follow it.

## Phase 4 — Report

Read `REPORT.md` and follow it. Build the file, and hold it as a draft until Phase 5 clears it.

## Phase 5 — Check the pick

The report was written by the agent that did the research, so it inherits every belief that research formed — including the wrong ones. A fresh reader cannot rationalise a shaky claim; it can only check whether the source says what the report says. That independence is the point, and two questions buy most of it.

Send **one** subagent (`general-purpose`, `model: "sonnet"`, low reasoning effort) with a **clean context** — it gets the report path and the confirmed brief, nothing else. Summarising your findings for it would re-import your assumptions. It spawns nothing of its own; say so in its prompt.

> Check two things about the top pick in this buying report, and stop there. First: does it clear every non-negotiable in the brief? Second: is its price and buy link a real, current listing — open the link and look. Return a short list, each tagged **must-fix** (wrong, or contradicts its source or the brief) or **note** (worth a glance, non-blocking). Leave the report unedited; report only.

Fix every **must-fix** by substantiating it from a source or dropping the claim — softened wording does not close one. If a fix moves the pick, say so at delivery; a reversed pick is the check working, and it earns one more pass over just what changed.

When the user has asked for speed above all, skip this phase, tell them the figures are single-sourced, and deliver.

**Done when** the pick's non-negotiables and price are verified, must-fixes are resolved, and the report is delivered the way the user chose.
