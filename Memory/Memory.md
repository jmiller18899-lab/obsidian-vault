---
title: Memory
type: index
tags: [moc, memory]
---

# 🤖 Memory (ClawAgent)

> [!warning] Auto-managed
> Notes in this folder are read and written by **ClawAgent** via the GitHub API.
> Avoid heavy manual edits here — treat it as the agent's working memory.

## What lives here
- Persistent facts and context the agent should remember across sessions
- Summaries the agent generates from the rest of the vault

> [!info] How it's produced
> Notes here are written by the pipeline in [[Resources/ClawAgent Vault Pipeline Prompts|Vault Pipeline Prompts]].
> For the whole system, see [[Maps of Content/ClawAgent MOC|ClawAgent MOC]].

## Stored memory

```dataview
LIST
FROM "Memory"
WHERE file.name != "Memory"
SORT file.mtime DESC
```

*(No Dataview? Browse the `Memory/` folder directly.)*
