# Report

A single self-contained HTML file the user can open, read on a phone, and send to someone else — everything inline, no sibling files it depends on.

Write it to `./product-research/<category>-<yyyy-mm>/report.html`. This is a **draft** — the fact-check phase gates delivery, so do not surface it to the user yet.

## Sections, in order

1. **Verdict** — the pick, in the first screen. One sentence on what it is, one on why it wins *this* brief, its local price, and where to buy it. No preamble before this.
2. **The brief** — the confirmed brief, restated. This is what the verdict was judged against, and it lets the user spot a wrong premise immediately.
3. **Runners-up** — two or three, each with the one condition under which it beats the verdict ("if you can live without X", "if your budget stretches to Y").
4. **Comparison table** — candidates × non-negotiables and ranked nice-to-haves, plus local price. Scrolls horizontally inside its own container on narrow screens.
5. **Pros and cons** — per candidate that made the shortlist. Ground each line in an **owner report** or a spec, not in general impressions. For the top three, lead the block with the **product image** and a **video-review card**: the YouTube thumbnail linking to the video, with the channel name and roughly how recent and how popular it is ("MKBHD · 2.1M views · Mar 2026"), so the user can judge the source before clicking.
6. **Ruled out** — one line each, with the non-negotiable it failed. Short, but present.
7. **Worth waiting for** — upcoming products, with expected date and how firm it is. Say plainly whether waiting is worth it given the user's timeline.
8. **Pricing and sourcing** — a table in the user's local currency: retailer, price, date checked, delivery time, warranty and returns, import notes. Link every retailer.
9. **Sources** — every URL used, grouped by candidate, each with what it contributed.

## Craft

- Prices in the user's local currency, with the date checked beside them — they go stale.
- Every claim about a product traces to a linked source. Where owner reports contradict the spec sheet, show both and say which you believe.
- Style it as a document, not a dashboard: readable line length, generous spacing, one accent colour. Light and dark both handled via `prefers-color-scheme`.
- **Everything inline** — all CSS, and every image embedded as a base64 `data:` URI (`data:image/jpeg;base64,…`). No external fonts, scripts, hotlinks, or relative-path files. The `assets/` folder is a scratch staging area; the delivered `report.html` must open with zero dependencies, so it renders identically in a side-panel preview and when the user forwards the file alone.
- Encode each staged image to base64 and paste it into the `src`. Keep photos reasonably sized (long edge ~1000px) so the file doesn't bloat to tens of megabytes.

**Done when** the file opens standalone with every image inline (no `assets/` dependency), every candidate in the comparison table has a matching pros-and-cons block and a linked source, the top three each carry a product image and a video-review card, and the verdict is visible without scrolling.
