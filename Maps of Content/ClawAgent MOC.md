---
title: ClawAgent MOC
type: moc
topic: clawagent
created: "2026-06-26"
tags: [moc, clawagent]
---

# 🤖 ClawAgent MOC

> [!info] Map of Content
> The hub for everything about **ClawAgent** — the agent that turns its own work into durable
> vault notes via the GitHub-as-vault transport (agent commits markdown → `jmiller18899-lab` repo
> → iPad syncs). Stateless Railway container, no VOLUME; the repo *is* the memory.

## 🧠 The system
- [[Memory/Memory|Memory (ClawAgent)]] — the auto-managed folder the agent reads/writes as working memory
- [[Resources/ClawAgent Vault Pipeline Prompts|Vault Pipeline Prompts]] — the writer prompts that produce notes

## 🔧 Pipeline stages (one job, one KPI, one acceptance test)
1. **NOTE_SYNTHESIS** — work event → one atomic note
2. **MOC_INDEX_UPDATE** — keep `index.md` + `hot.md` (Hot Cache) valid
3. **WIKILINK_RESOLVER** — connect the new note into the graph
4. **DEDUP_MERGE** *(gate)* — UPDATE existing vs. create NEW
5. **AUTORESEARCH_LOG** — log each self-improve cycle as a dated lab-note

> Full prompt text + integration order: [[Resources/ClawAgent Vault Pipeline Prompts|Vault Pipeline Prompts]].

## 📐 Principles
- **Atomic notes** — the synthesis output mirrors [[Notes/Atomic notes beat long documents]]
- **Anti-fabrication** — assert only what the evidence payload contains; unknown field → omit
- **Verified increments** — ship one stage behind its acceptance test before the next

## 🌱 Concepts to capture (stubs the pipeline references)
- `[[autoresearch-loop]]` — the hypothesize → execute → measure → keep/discard cycle *(note not yet written)*
- `[[hot-cache]]` — the read-first working set in `hot.md` *(note not yet written)*
- `[[betweenness-centrality]]` — graph metric for broker nodes the resolver creates *(note not yet written)*

## 🔗 Related
- [[Maps of Content/Maps of Content|All Maps of Content]] · [[Index]] · [[Tags]]
