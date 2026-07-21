# Product Research Skill — project notes

**Started**: 21 Jul 2026
**Status**: Built, installed to `~/.claude/skills/product-scout/`, test-run end-to-end
on the e-ink-phone question (verdict: Bigme HiBreak Pro), and fact-check phase (Phase 5)
tested live over two review rounds. Report at
`product-research/eink-phone-2026-07/report.html`.
**Note**: this folder now lives under `ClaudeCode/Josiah-Life-Skills/Product Research Skill/`
(moved from the old `Josiahs-Skill-Creation/` root on 21 Jul). The skill install path
(`~/.claude/skills/product-scout/`) is unaffected by the move.

## What this is

A Claude Code skill (`product-scout`) that takes a question like *"I want an e-ink
mobile phone for use in Australia, what's my best option?"* and turns it into a
researched HTML buying report — via a grilling that pins down what the user
actually wants before any real research starts.

## Layout

```
Product Research Skill/
├── project.md          ← this file
└── product-scout/      ← the skill itself (copy this folder to install)
    ├── SKILL.md        phases 1–2 + pointers to 3–5
    ├── RESEARCH.md     phase 3 protocol (disclosed)
    ├── REPORT.md       phase 4 HTML report spec (disclosed)
    └── REVIEW.md       phase 5 fresh-reviewer fact-check (disclosed)
```

## The four phases

1. **Scoping** — a handful of plain `WebSearch` queries to learn the category's
   vocabulary: feature axes, price bands, the dedicated subreddit, the incumbents.
   Groundwork for good questions, *not* a shortlist.
2. **Grilling** — one question at a time, each with a recommended answer, until a
   nine-field **brief** is written back and confirmed: purpose, non-negotiables,
   ranked nice-to-haves, dealbreakers, budget, country, sourcing, timeline,
   incumbent.
3. **Research** — Exa + Firecrawl sweep of current / upcoming / adjacent products,
   Reddit and forum mining, local availability check, scored against the brief.
4. **Report** — HTML draft to
   `./product-research/<category>-<yyyy-mm>/report.html`, with device photos and
   YouTube-review cards in a sibling `assets/`. Not delivered yet.
5. **Fact-check** — a fresh-context `general-purpose` subagent that never saw the
   research independently verifies every claim/price/spec/link against sources and
   returns must-fix / should-fix findings. Loop until a clean pass, then deliver.

## Decisions made

- **Model-invoked**, not user-invoked — it should fire on "what's the best X"
  without Josiah having to remember the skill exists.
- **Phases 3 and 4 are disclosed to separate files.** Keeping the research
  protocol out of view while grilling is the main defence against the agent
  cutting the interview short to get to the fun part.
- **Scoping uses plain `WebSearch` only.** Exa and Firecrawl are held back for
  phase 3 — the opening pass is cheap context-gathering, not research.
- **Leading words**: *scoping*, *brief*, *specs* vs *owner reports*, *verdict*.
  Owner reports (what buyers say six months later) are weighted hardest on the
  non-negotiables; three unrelated owners with the same complaint is treated as a
  real defect.
- **Sourcing is its own brief field**, separate from timeline — an AliExpress
  white-label in three weeks and a known brand on Amazon tomorrow are different
  products, and a candidate that can't be bought within the sourcing bar is
  dropped like a failed non-negotiable.
- **Lives in this repo only**, not installed to `~/.claude/skills/` yet.

## Test run — 21 Jul 2026 (e-ink phone, Australia)

- Ran cleanly through all four phases. Grilling correctly deduced that Beeper +
  Maps + camera + authenticator require full Android, eliminating the walled-OS
  minimalist phones before research.
- Research found the real decider was VoLTE-on-Telstra + the Oct-2024 IMEI-TAC
  block, not raw specs — surfaced via the AU-specific Whirlpool thread.
- Verdict: Bigme HiBreak Pro (~$690, Amazon.com.au), the one full-Android e-ink
  phone that clears all five non-negotiables and ships domestically.

### Changes made from what the test run exposed

- **SKILL.md** — grilling now tells the agent to *state implied constraints out
  loud as they emerge* (the full-Android deduction happened by luck of phrasing;
  now it's explicit).
- **RESEARCH.md** — new step: for the top three, download a product image and
  find one trustworthy, recent, high-reach YouTube review; save image + thumbnail
  to `assets/`.
- **REPORT.md** — pros/cons block for the top three now leads with the product
  image and a video-review card (thumbnail + channel + views + date). Images live
  in a sibling `assets/` folder, referenced relatively, never hotlinked.

## Fact-check phase test — 21 Jul 2026

Ran Phase 5 live on the e-ink report. The fresh reviewer (clean-context
`general-purpose` subagent) earned its keep:

- **Round 1** caught a wrong camera spec (report said "5+13 MP"; it's 20+5 MP),
  a false Color-model camera differentiator, a logically flawed "domestic
  Amazon purchase sidesteps the IMEI-TAC block" argument (the block is
  TAC/VoLTE-based, not purchase-location-based), an overstated "~$80 import
  saving", and a mis-attributed crashes citation. Confirmed the verdict, the
  ~$690 price, and both rule-outs stand on true premises.
- **Round 2** (fresh reviewer on the corrected report) caught that the Boox
  data-only rule-out was stated as certain but the *cited* sources only said
  "VoIP over data" — added Yanko (which does say data-only) and softened to
  "reported/unconfirmed". Also fixed a stray "B7" band and corrected the
  HiBreak Dual note (original shelved; track the Dual 2).

Judgment call: stopped the loop after round 2 rather than spawn a third
~25-min agent, since the remaining must-fix was a confidence-downgrade that
can't itself be an overstatement. Worth encoding a cheaper final-round option
(self-check vs full agent) if this recurs.

### Lessons for the skill

- Each full agent review took ~24–25 min. For a real run with 5+ candidates
  this is the dominant cost — REVIEW.md may want a "scope the reviewer to
  changed claims on re-runs" note to keep later rounds cheap.
- The reviewer twice flagged *unsourced-but-true* claims. RESEARCH.md's
  specs-vs-owner-reports split is good, but the report step should attach a
  source to every hard spec/price inline as it's written, not post-hoc.

## Next steps

- Re-run to confirm the image + YouTube-review additions render correctly (the
  first test predates them).
- Watch for: does a real run fan out background agents per candidate when >5
  survive? Does it reliably download assets rather than hotlink?
