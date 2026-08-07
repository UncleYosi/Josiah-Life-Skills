# Report

Fill `template.html` — the house style, already designed. Copy it, replace every `{{TOKEN}}`, and leave the CSS alone. Inventing styling is the slowest part of a run and the reason no two reports used to look alike.

Write to `./product-research/<category>-<yyyy-mm>/report.html`. It stays a **draft** until Phase 5 clears it.

## Fill it

Short and sharp beats complete. Every line either changes the decision or stands as the evidence behind one; cut whatever does neither.

- **The pick** — `{{PICK_*}}`. The answer, above the fold: its fit line, a why-paragraph of at most three sentences, local price, retailer, delivery, date checked, buy link.
- **The two alternates** — `{{ALT1_*}}`, `{{ALT2_*}}`. Fit line leads, product name sits below it. **One** pro and **one** con each, both grounded in an owner report rather than an impression. Exactly two alternates — the grid is built for two.
- **Fit lines** — all three read "Best if you …" and name a *situation*, not a feature. "Best if you want a real phone number" beats "Best if you want a SIM slot".
- **What I judged against** — the confirmed brief, one row per line, so a wrong premise shows up immediately.
- **Side by side** — candidates × non-negotiables and top nice-to-haves, plus price. Put `class="row-pick"` on the pick's row. Use `.yes` and `.no` only on non-negotiable columns, so the gold keeps meaning something.
- **Where to buy** — retailer, price, delivery, returns, date checked. Link every retailer.
- **Ruled out** — one line each, naming the non-negotiable it failed. Short, but present: the user should see it was considered.
- **Sources** — grouped by candidate, each with what it contributed.
- **Footnote** — price staleness, the shallow-mode note when Exa and Firecrawl were missing, and any field left *unverified* because a source blocked you.
- **`{{FAVICON_EMOJI}}`** — one emoji for the category (`☕`, `🎧`, `📱`), which becomes the browser-tab icon. It rides inside an inline SVG data URI, so the file stays dependency-free. Use the same emoji for the artifact's `favicon`.

Delete any block you have no data for; a removed section reads better than a placeholder or filler.

## Craft

- Prices in the user's local currency, with the date checked beside them.
- Every claim about a product traces to a linked source. Where owner reports contradict the spec sheet, show both and say which you believe.
- **Everything inline** — every image embedded as a base64 `data:` URI, long edge ~1000px so the file stays a few megabytes. `assets/` is scratch staging; the delivered `report.html` opens with zero dependencies, so it renders identically in a preview pane and when the user forwards the file alone.

## Deliver

Follow the user's Phase 2 choice:

- **HTML file** — `SendUserFile` with `display: "render"`.
- **Artifact** — publish with `Artifact`. The tool supplies its own `<!doctype>`, `<html>`, `<head>` and `<body>`, so publish a copy with those four wrappers stripped and the `<style>` and `<title>` kept. Pass a `favicon` and a one-sentence `description`.
- **Both** — artifact first, then the file, so the user gets a link they can open anywhere and a copy they keep.

**Done when** every `{{TOKEN}}` is replaced, the file opens standalone with all images inline, all three picks carry a distinct fit line, the pick is visible without scrolling, and every table row traces to a linked source.
