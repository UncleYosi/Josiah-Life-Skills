---
name: product-scout
description: Find the best product to buy in a category — scope the category, grill the user into a brief, research the market and owner reports, deliver an HTML buying report. Use when the user asks what to buy, which model is best, wants options compared or shortlisted, or is deciding on a purchase.
---

# Product Scout

Buying advice is only as good as the brief behind it. Run the phases in order — **scoping**, **grilling**, **research**, **report**, **fact-check** — and do not let a later phase start early.

## Pace

Once the brief is confirmed, the user is waiting. Target **≤10 minutes from the end of grilling to the delivered report**. A saturated market (dozens of live models) may run a little longer — but that means fanning out **parallel** background agents, not searching longer serially. Depth comes from breadth-in-parallel and from stopping when the answer is clear, never from a slow serial crawl. Time spent is a cost the user feels; treat it like one.

## Tools

This skill is built to run on **Exa** and **Firecrawl** — they do the deep, semantic web research and full-page scraping that make the output good. Prefer them throughout Phase 3.

If they are not installed, do not silently degrade. Tell the user once, up front, that the research will be **shallower without them**, and offer the one-line install (see `RESEARCH.md` for the walk-through). Then, if they decline or want to proceed anyway, **fall back to `WebSearch`/`WebFetch`** and run the skill regardless — flag in the final report that it was produced without the deep-research tools.

## Phase 1 — Scoping

Before asking the user anything, learn enough of the category's own language to ask good questions. A handful of plain `WebSearch` queries is the whole budget — the heavy tools stay holstered until Phase 3.

Establish:

- The **feature axes** buyers trade off in this category, in the words owners actually use.
- The **price bands** the market sorts into, and what moves a product between them.
- The dedicated **subreddit(s)** and forums for the category — or the finding that none exist.
- The **incumbents**: the two or three products people name reflexively when this question is asked.

Scoping is groundwork for good questions, not a shortlist. Do not evaluate products yet.

**Done when** you can state the feature axes, the price bands, and the community sources — and the user has seen a short scoping summary that names them.

## Phase 2 — Grilling

Interview the user relentlessly until you reach a shared understanding of what they want and why. Walk down each branch of the decision tree, resolving dependencies one at a time.

Ask **one question at a time** and wait for the answer. Multiple questions at once is bewildering. For each question, give your recommended answer, drawn from scoping — especially for budget, where the user is often anchored to nothing.

The **brief** is complete when it covers:

- **Purpose** — what the product is for, and the underlying reason they want it. Push past the first answer; "I want an e-ink phone" is a solution, "I want to stop doom-scrolling in bed" is the purpose.
- **Non-negotiables** — features that disqualify a product if absent.
- **Nice-to-haves** — ranked, so trade-offs can be made against them.
- **Dealbreakers** — the inverse: what rules a product out.
- **Budget** — a band, with your recommendation from the scoped price bands.
- **Country** — where they are buying and using it, which decides pricing, warranty, and availability.
- **Sourcing** — who they will buy from and how long they will wait for it. An AliExpress white-label arriving in three weeks and a known brand on Amazon arriving tomorrow are different products; find out which end they sit at, and whether local warranty and returns matter.
- **Timeline** — buying now, or able to wait for something unreleased.
- **Incumbent** — what they use today and what's wrong with it.

Facts you can look up, look up. Decisions are the user's — put each one to them.

**State implied constraints out loud as they emerge.** When an answer forces a downstream consequence — "Beeper and an authenticator both need full Android, so the walled-OS phones are out" — say it in the moment and fold it into the brief. Surfacing the deduction sharpens the brief and eliminates whole branches before research, rather than leaving it to luck.

**Done when** you have written the brief back to the user as a numbered list and they have confirmed it. Do not begin research before that confirmation.

## Phase 3 — Research

Read `RESEARCH.md` and follow it.

## Phase 4 — Report

Read `REPORT.md` and follow it. Build the file, but do **not** deliver it yet — it is a draft until Phase 5 clears it.

## Phase 5 — Fact-check

Read `REVIEW.md` and follow it. Only after the reviewer's findings are resolved do you surface the report to the user.
