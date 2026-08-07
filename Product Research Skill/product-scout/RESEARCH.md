# Research

The brief is confirmed and the user is waiting. Find everything on the market that could serve it, **fast and wide**, and stop on a candidate the moment it clearly wins or clearly fails a non-negotiable.

In shallow mode (see `SKILL.md`) the steps are identical — `WebSearch` and `WebFetch` do the work, and the review sources the user named carry more of the weight.

## Fan out once, cheaply

**One wave, at most six agents, one level deep.** Dispatch them the moment you have a candidate list, cluster candidates together when there are more than six, and run no second wave. Serial research blows the time budget; unbounded fan-out blows the token budget, and the second is by far the more expensive mistake.

Dispatch every research agent with `subagent_type: "general-purpose"` and **`model: "haiku"`** — these agents fetch pages and fill in a row, they do not weigh the verdict. You do that when they return.

**Cap: eight candidates** across the whole wave. Past eight, rank by fit against the brief, take the top eight, and say in the report that you stopped there.

Paste this into every research agent's prompt, above the candidate-specific part:

> Work alone: do the digging yourself, and spawn no subagents of your own.
> Use text tools only — `firecrawl_search`, `firecrawl_scrape`, `web_search_exa`, `WebFetch`, `WebSearch`. Browser automation is off for this task.
> When a tool returns a rate limit, a quota error, or a block: step down to the next tool once, and if that fails too, write `unverified — <source> blocked` in the field and move on. Re-running a failing call is the most expensive thing you can do here.
> Return at most 250 words: the filled row you were asked for, each field with its source URL. No narrative, no preamble.

That prompt is the load-bearing part of this section. The agent never reads this file — it only ever sees what you hand it, so the limits have to travel in the prompt.

Two kinds of evidence, and you need both:

- **Specs** — what the maker claims: manufacturer pages, retailer listings, reviewer benchmarks.
- **Owner reports** — what people who bought it say six months later. This is where the specs go to die. Weight them hardest on the user's non-negotiables.

## Sweep the market

Cast wide before narrowing. Search along the **feature axes** from scoping, not just the category name — the best fit is often a product the category name doesn't reach.

- Exa (`web_search_exa`, `exa:search`) for semantic, meaning-based sweeps: "phone that does X without Y", competitor-of queries, review round-ups.
- Firecrawl (`firecrawl_search`, `firecrawl_scrape`, `firecrawl_map`) for full page content: manufacturer spec pages, retailer listings with live prices, review sites that block plain fetches.

Cover:

1. **On the market now** — everything currently buyable that clears the non-negotiables.
2. **Adjacent** — products from a neighbouring category that solve the *purpose* even though they miss the category. Name these explicitly; they are often the real answer.
3. **Upcoming** — only when the brief's timeline says the user can wait. If something credible ships within that window, it belongs in the pick's reasoning as a sentence, not as a section of its own.

## Mine the community

Go to the review sources **the user named in grilling** first — their answer is the whole point of having asked. Search those directly rather than hoping general web search surfaces them.

- `firecrawl_search "<product> site:reddit.com/r/<subreddit>"`, and scrape `old.reddit.com` URLs — they render more reliably. In shallow mode, `WebSearch` the same `site:` queries.
- Chase the recurring threads: "X vs Y", "one year later", "regret buying", "what I wish I knew", "don't buy".
- Note **failure patterns** — the same complaint from three unrelated owners is a real defect, not a lemon.

Record who said it and when. A 2019 complaint about a product revised in 2024 is noise.

## Check local availability

For every candidate that survives, in the user's country:

- Which retailers stock it, and whether those clear the brief's **sourcing** bar — a marketplace white-label fails a brief that asked for a known brand with local returns.
- Current price in local currency, from a named retailer, with the date checked.
- Realistic delivery time, against the wait the user said they would tolerate.
- Warranty and returns as that retailer actually offers them, plug/band/voltage compatibility, and import duty or shipping if it must come in.

A product that cannot be bought within the sourcing bar is not a candidate — say so once and move on.

## Gather visuals for the three picks

For the pick and its two alternates, collect two things the report will show:

- **A product image** — a clean shot, ideally from the manufacturer or a review site. Download it into `./product-research/<category>-<yyyy-mm>/assets/`; the report embeds it as a base64 data-URI so the final file stands alone.
- **One trustworthy YouTube review** — recent, and from a channel with real reach (high view count or subscriber base, not a drop-shipper's 200-view upload). Capture the video URL and its thumbnail into `assets/` too. Prefer a hands-on review that speaks to the user's non-negotiables over a spec-read.

Verify each downloaded file is a real image (`file` says JPEG/PNG, size in kilobytes not bytes) — a 404 often saves as a tiny HTML stub, and a broken asset is worse than none.

Where the only reviews are thin or ancient, say so and skip the link rather than lend a bad one your authority.

## Score against the brief

Build a table: candidates as rows, the brief's non-negotiables and ranked nice-to-haves as columns. Every cell is backed by a source you actually read. Anything failing a non-negotiable is out — state it and why, once, so the user sees it was considered.

Then **name three picks**: the one you would buy, and two alternates. Each carries a **fit line** — the single condition under which it is the right buy, phrased as "Best if you …" and naming a *situation* rather than a feature. The three fit lines have to describe genuinely different buyers. When two collapse into each other you have one pick and a spare, so go find a third that serves a real alternative.

**Done when** the three picks each have a distinct fit line, three independent owner reports, a local price and a buy link; every other surviving candidate has a scored row with at least one source; and you can say what would change the pick.
