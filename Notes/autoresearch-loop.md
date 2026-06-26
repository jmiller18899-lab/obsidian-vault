---
title: autoresearch-loop
type: permanent
topic: clawagent
created: "2026-06-26"
tags: [permanent, clawagent/autoresearch]
---

# 🔁 autoresearch-loop

The self-improvement cycle ClawAgent runs on itself: **hypothesize → execute → measure →
keep/discard**. Each pass proposes one change, applies it, scores it against the weighted eval
blend, and commits a verdict to the record.

## Why it matters
Without a logged loop, improvements are anecdotal and regressions are invisible. The loop turns
"I think this helped" into a numeric delta with an explicit **KEEP** or **DISCARD** — and keeps
discarded ideas on the record so the next cycle doesn't re-test a dead end.

## The cycle
- **Hypothesis** — what should improve, and in which direction.
- **Change** — one concrete diff/commit (real SHA).
- **Measure** — before → after on the weighted blend (e.g. `40/30/20/10`). State the delta.
- **Verdict** — KEEP / DISCARD / INCONCLUSIVE (if the eval didn't run), one sentence of why.

One hypothesis per cycle keeps the signal attributable — same narrow-agent rule as the writer.

## 🔗 Links
- Logged by: [[Resources/ClawAgent Vault Pipeline Prompts|Vault Pipeline Prompts]] (AUTORESEARCH_LOG)
- Hub: [[Maps of Content/ClawAgent MOC|ClawAgent MOC]]
- Related: [[Notes/Define the problem before solving it]]
