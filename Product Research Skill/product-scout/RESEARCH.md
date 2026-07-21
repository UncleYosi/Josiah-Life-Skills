# Research

The brief is confirmed. Now find everything on the market that could serve it — and do it **fast and wide**. Fan out parallel background agents rather than crawling serially; the target is a delivered report within ~10 minutes of the brief. Stop researching a candidate the moment it clearly wins or clearly fails a non-negotiable.

## Tools: prefer Exa + Firecrawl, fall back gracefully

Check whether the **Exa** and **Firecrawl** skills/tools are available. They are what make this research deep.

If either is missing, tell the user once and offer the walk-through:

- **Claude Code** — install the plugins from the marketplace, e.g. `/plugin install exa` and `/plugin install firecrawl` (or add via `/plugin marketplace`), then restart the session. Exa can also run via its MCP server at `https://mcp.exa.ai/mcp`.
- **Claude Cowork / desktop** — add Exa and Firecrawl as connectors/MCP servers in Settings, then reopen.

If the user installs them, great. If not, **proceed with `WebSearch` + `WebFetch`** — the skill still runs, just shallower (weaker semantic sweeps, some JS-heavy retailer/Reddit pages unreadable). Note that limitation in the final report so the user can weigh it.

Two kinds of evidence, and you need both:

- **Specs** — what the maker claims: manufacturer pages, retailer listings, reviewer benchmarks.
- **Owner reports** — what people who bought it say six months later: Reddit, category forums, long-form reviews. Owner reports are where the specs go to die. Weight them hardest on the user's non-negotiables.

## Sweep the market

Cast wide before narrowing. Search along the **feature axes** from scoping, not just the category name — the best fit is often a product the category name doesn't reach.

- Exa (`exa:search` skill, or `web_search_exa` / `web_fetch_exa`) for semantic, meaning-based sweeps: "phone that does X without Y", competitor-of queries, review round-ups.
- Firecrawl (`firecrawl-search`, `firecrawl-scrape`, `firecrawl-map`) for pulling full page content: manufacturer spec pages, retailer listings with live prices, review sites that block plain fetches.

Cover:

1. **On the market now** — everything currently buyable that clears the non-negotiables.
2. **Upcoming** — announced, in pre-order, at CES/IFA/Kickstarter, or credibly rumoured with a date. Flag anything the user could wait for, with how firm the date is.
3. **Adjacent** — products from a neighbouring category that solve the *purpose* even though they miss the category. Name these explicitly; they are often the real answer.

## Mine the community

Go to the subreddit(s) and forums found in scoping. Search them directly rather than hoping general web search surfaces them:

- `firecrawl-search "<product> site:reddit.com/r/<subreddit>"`, and scrape `old.reddit.com` URLs — they render more reliably.
- Chase the recurring threads: "X vs Y", "one year later", "regret buying", "what I wish I knew", "don't buy".
- Note **failure patterns** — the same complaint from three unrelated owners is a real defect, not a lemon.

Record who said it and when. A 2019 complaint about a product revised in 2024 is noise.

## Check local availability

For every candidate that survives, in the user's country:

- Which retailers stock it, and whether those clear the brief's **sourcing** bar — a marketplace white-label fails a brief that asked for a known brand with local returns.
- Current price in local currency, from a named retailer, with the date checked.
- Realistic delivery time to the user, against the wait they said they would tolerate.
- Warranty and returns as actually offered by that retailer, plug/band/voltage/certification compatibility, and import duty or shipping if it must come in.

A product that cannot be bought within the sourcing bar is not a candidate — say so and move on.

## Gather visuals and a video review

For the top three candidates (the verdict and the two runners-up), collect two things the report will show:

- **A product image** — a clean shot of the device, ideally from the manufacturer or a review site. Download it into `./product-research/<category>-<yyyy-mm>/assets/` as a working file; the report will embed it as a base64 data-URI so the final file stands alone.
- **One trustworthy YouTube review** — recent (ideally within a year of the report) and from a channel with real reach (high view count or subscriber base, not a drop-shipper's 200-view upload). Capture the video URL and download its thumbnail into `assets/` too. Prefer a hands-on review that speaks to the user's non-negotiables over a spec-read.

Verify each downloaded file is a real image (`file` says JPEG/PNG, size is kilobytes not bytes) — a 404 often saves as a tiny HTML stub. A broken asset is worse than none.

A weak or ancient video is worse than none — if the only reviews are thin, say so and skip the link rather than lend a bad one your authority.

## Score against the brief

Build a table: candidates as rows, the brief's non-negotiables and ranked nice-to-haves as columns. Every cell is backed by a source you actually read.

Anything failing a non-negotiable is out. State it and why, once — the user should see that it was considered.

**Parallelise by default.** As soon as you have a candidate list, dispatch background agents to deep-dive them concurrently — one per candidate (or per cluster) — each returning a filled, sourced row plus its image and video link. Serial research is the main thing that blows the time budget; only work through candidates one-by-one if there are just one or two.

**Done when** every surviving candidate has a scored row with sources, a local price, and at least three independent owner reports — and you can name the **verdict** and say what would change it.
