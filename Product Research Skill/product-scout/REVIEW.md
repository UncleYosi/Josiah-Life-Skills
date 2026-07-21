# Fact-check

The report is written by the agent that did the research, so it inherits every belief that research formed — including the wrong ones. A **fresh reviewer** that never saw the research can't rationalise a shaky claim; it can only check whether the source says what the report says. That independence is the point.

Keep it **fast and focused**: one round, headline claims only. This is a sanity check, not an audit — it must not blow the time budget.

## Dispatch the reviewer

Spawn **one** subagent (`general-purpose`, low reasoning effort) with a **clean context** — it gets only the report path and the confirmed brief. Do not summarise your findings for it; a summary re-imports your assumptions.

## The reviewer's task

> You are sanity-checking a buying report you did not write, fast. Do **not** verify every detail — check only the load-bearing claims, in about 5–10 minutes:
> 1. The **verdict** and each **runner-up** — does it actually clear every non-negotiable in the brief?
> 2. The **verdict's price** and its buy link — right ballpark, real listing?
> 3. Each **ruled-out** product — is it eliminated on a *true* premise, or a wrong one?
> 4. Any claim that would **change the decision** if false.
>
> Open the cited source only for those. Skip minor specs, wording, and secondary sources. Return a short list, each tagged **must-fix** (a headline claim that is wrong or contradicts its source/the brief) or **note** (worth a glance, non-blocking). Ignore anything already hedged as uncertain. Do not edit the report — only report.

## Resolve and deliver

Fix every **must-fix** — substantiate from a source or remove the claim; softening the wording alone does not close one. Glance at the **notes** and fix what's quick. If a fix moves the verdict, say so; a reversed verdict is the check working.

**One round only.** Do not re-dispatch unless a must-fix actually changed the verdict or a rule-out — in which case run one more quick pass on just what changed. Then surface the report with `SendUserFile` (`display: "render"`), telling the user it passed a fact-check and naming anything that moved.

**Skipping this phase** is allowed when the user asks for speed above all: say you are skipping the independent check and that figures are single-sourced, then deliver.

**Done when** the headline claims are verified, must-fixes are resolved, and the report is delivered.
