---
title: hot-cache
type: permanent
topic: clawagent
created: "2026-06-26"
tags: [permanent, clawagent/memory]
---

# 🔥 hot-cache

The **read-first working set** — the small list of most-recent/active notes the agent loads
before anything else, stored in `hot.md`. It's the agent's short-term memory: a bounded window
over the vault so it doesn't have to scan everything to act.

## Why it matters
The whole vault is too large to read every turn. The hot cache gives the agent a cheap,
always-current view of what's relevant *now*. Its biggest failure mode is the cache going
missing or stale — when `hot.md` breaks, the read protocol breaks, so the pipeline must keep it
valid on every write.

## Maintenance rules
- New note → prepend to the top.
- Trim back to the most recent **N** entries (`HOT_CACHE_MAX`).
- Drop notes whose `status` is `superseded`.
- Never duplicate an entry; never delete a section header.

## 🔗 Links
- Maintained by: [[Resources/ClawAgent Vault Pipeline Prompts|Vault Pipeline Prompts]] (MOC_INDEX_UPDATE)
- Lives alongside the agent's working memory: [[Memory/Memory|Memory (ClawAgent)]]
- Hub: [[Maps of Content/ClawAgent MOC|ClawAgent MOC]]
