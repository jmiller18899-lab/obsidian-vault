---
title: ClawAgent Vault Pipeline Prompts
type: resource
topic: clawagent
created: "2026-06-26"
tags: [resource, clawagent/pipeline, clawagent/prompts]
status: active
---

# ClawAgent → Obsidian Vault — Embeddable Prompts

> [!info] What this is
> Drop-in prompt constants for the pipeline that turns agent work into durable vault notes.
> Each one is **one job, one KPI, one acceptance test** — the narrow-agent rule applied to the
> writer itself. See [[Maps of Content/ClawAgent MOC|ClawAgent MOC]] for how this fits the system.

Placeholders use the `{{...}}` convention. Wire each to the GitHub-as-vault transport
(agent commits markdown → repo in `jmiller18899-lab` → iPad syncs). Nothing writes to the
Railway container (stateless, no VOLUME).

> [!warning] Anti-fabrication contract
> Applies to every prompt below: **assert only what the evidence payload contains.** No invented
> file paths, metrics, commit SHAs, or links. If a field is unknown, omit it — never guess.

---

## 1. NOTE_SYNTHESIS_PROMPT

**Job:** turn one work event (bug fix, eval result, decision, research finding) into one atomic markdown note that matches the vault's KB pattern.
**Plugs into:** the writer module, called once per completed unit of work before push.
**Acceptance test:** feed a known commit + diff; output parses as valid markdown with YAML frontmatter, ≤1 concept per note, and zero claims absent from the input payload.

```
You convert a single ClawAgent work event into ONE atomic Obsidian note.

INPUT EVENT:
{{EVENT_PAYLOAD}}   # type, summary, evidence (commit SHA, diff, eval scores, links)

EXISTING VAULT CONCEPTS (titles only, for linking — do NOT restate their bodies):
{{VAULT_INDEX}}

RULES:
- ONE concept per note. If the event spans two ideas, pick the dominant one; note the
  second only as a [[wikilink]] stub reference.
- Output valid markdown with this frontmatter exactly:
    ---
    title: <kebab-or-title-case, unique>
    created: {{TODAY}}
    tags: [<2-4 lowercase tags>]
    status: <draft|active|superseded>
    source: <commit SHA / eval run id / decision id from evidence>
    ---
- Body structure: one-sentence definition → why it matters → the verifiable evidence
  (real SHAs, real eval numbers, real HTTP/Stripe/Lob IDs — copy from payload, never fabricate).
- End with a "Links" section of 2-5 [[wikilinks]] chosen ONLY from VAULT_INDEX above.
- ≤ 200 words of body. Atomic, not a report.
- If the payload lacks evidence for a claim, drop the claim. Unknown field → omit it.

OUTPUT: the markdown file content only. No preamble, no code fences.
```

---

## 2. WIKILINK_RESOLVER_PROMPT

**Job:** keep the graph connected — decide outbound links from the new note AND which existing notes should backlink to it.
**Plugs into:** runs after synthesis, before commit; returns an edit list, not prose.
**Acceptance test:** every returned link target exists in `{{VAULT_INDEX}}`; no self-links; resolver never invents a note title. (This is the lever for your betweenness-centrality graph — measure broker nodes after a batch.)

```
You wire one new note into the existing vault graph. Output edits only.

NEW NOTE:
{{NEW_NOTE_MD}}

VAULT INDEX (canonical titles + one-line summaries):
{{VAULT_INDEX_WITH_SUMMARIES}}

TASK:
1. OUTBOUND: list 2-5 existing titles the new note should [[link]] to. Targets MUST exist
   in the index. No self-link. Prefer links that connect distant clusters over redundant
   links inside an already-dense cluster.
2. BACKLINKS: list existing notes that should gain a [[link]] to the new note, with the
   exact line to append to each.
3. If a natural link target does NOT exist yet, emit it under "MISSING" as a stub-worthy
   concept — do NOT silently link to a nonexistent note.

OUTPUT strict JSON:
{ "outbound": ["..."], "backlinks": [{"file":"...","append_line":"..."}], "missing": ["..."] }
No commentary outside the JSON.
```

---

## 3. MOC_INDEX_UPDATE_PROMPT

**Job:** keep `index.md` (MOC) and `hot.md` (Hot Cache) valid every time a note lands, so the vault's own read protocol never breaks (the missing-`hot.md` failure mode).
**Plugs into:** final step before commit; returns patched files.
**Acceptance test:** after update, `hot.md` lists exactly the N most-recent/active notes, `index.md` contains the new title under the right section, and both still parse.

```
You maintain the vault's entry points after a new note is added.

NEW NOTE TITLE + TAGS:
{{NOTE_TITLE}} | {{NOTE_TAGS}}

CURRENT index.md:
{{INDEX_MD}}

CURRENT hot.md:
{{HOT_MD}}

RULES:
- index.md: insert the new [[title]] under the section matching its primary tag. Keep
  existing structure, ordering, and any MOC headers intact. Don't reorder unrelated entries.
- hot.md (Hot Cache = read-first working set): add the new note at the top; trim the list
  back to the most recent {{HOT_CACHE_MAX}} entries. Drop notes whose status is `superseded`.
- Never delete a section header. Never duplicate an existing entry.

OUTPUT two fenced blocks labelled `index.md` and `hot.md` with the full updated contents.
```

---

## 4. AUTORESEARCH_LOG_PROMPT

**Job:** make the self-improve loop durable — write each hypothesize → execute → measure → keep/discard cycle as a dated lab-note so the autoresearch results become permanent knowledge, not just eval logs.
**Plugs into:** the self-improve loop, one entry per cycle, appended to `lab/` or a dated daily note.
**Acceptance test:** entry contains the metric delta and an explicit KEEP or DISCARD verdict; a discarded hypothesis is still logged (kill bad ideas *on the record*, don't erase them).

```
You log one autoresearch cycle as a dated vault lab-note. Results are the only thing that matters.

CYCLE DATA:
{{CYCLE_PAYLOAD}}   # hypothesis, change made, eval blend before/after (40/30/20/10), pass/fail

WRITE an entry:
- Heading: ## {{TODAY}} — <short hypothesis label>
- Hypothesis: what you expected to improve and the predicted direction.
- Change: the concrete diff/commit (real SHA from payload).
- Measure: before → after on the weighted eval. State the delta numerically.
- Verdict: **KEEP** or **DISCARD**, with one sentence of why, grounded in the delta.
- If DISCARD: still record it — a killed idea logged is signal for the next loop.
- Link [[autoresearch-loop]] and the most relevant concept note from {{VAULT_INDEX}}.

RULES: no fabricated numbers. If the eval didn't run, verdict = INCONCLUSIVE, say so.
OUTPUT: the markdown entry only.
```

---

## 5. DEDUP_MERGE_PROMPT  *(optional gate)*

**Job:** stop near-duplicate concept notes before they fragment the graph.
**Plugs into:** runs before synthesis commits a NEW note; can redirect to an UPDATE instead.
**Acceptance test:** given an event that restates an existing concept, the gate returns `UPDATE <existing>` rather than creating a second note.

```
Decide whether this event needs a NEW note or should UPDATE an existing one.

EVENT SUMMARY: {{EVENT_SUMMARY}}
CANDIDATE EXISTING NOTES (title + summary, top matches): {{CANDIDATES}}

RETURN strict JSON:
{ "action": "NEW" | "UPDATE", "target": "<existing title if UPDATE, else null>",
  "reason": "<one sentence>" }

Bias toward UPDATE when the event is a refinement, new evidence, or status change of an
existing concept. Choose NEW only for a genuinely distinct idea. No commentary outside JSON.
```

---

## Integration order (one verified increment at a time)

1. Ship **NOTE_SYNTHESIS** alone → commits raw notes. Verify the markdown + frontmatter parse.
2. Add **MOC_INDEX_UPDATE** → entry points stay valid. Verify `hot.md` read protocol.
3. Add **WIKILINK_RESOLVER** → graph connects. Measure betweenness; confirm new brokers form.
4. Add **DEDUP_MERGE** gate → vault stays clean under volume.
5. Wire **AUTORESEARCH_LOG** into the self-improve loop last → results compound into the vault.

Each step lands behind its own acceptance test before the next one starts. Stack wins; kill anything that doesn't move the metric.

---

## 🔗 Links
- Hub: [[Maps of Content/ClawAgent MOC|ClawAgent MOC]]
- Target of the pipeline: [[Memory/Memory|Memory (ClawAgent)]]
- Note-shape these prompts emit mirrors: [[Notes/Atomic notes beat long documents]]
- Tag: `#clawagent/pipeline` — see [[Tags]]

> [!note] Naming clash to keep straight
> The `index.md` / `hot.md` in prompt #3 are **the agent's own files inside `Memory/`**, not the
> vault-wide [[Index]] / [[Home]]. Same idea (entry points), different scope.
