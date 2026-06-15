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

## Stored memory

```dataview
LIST
FROM "Memory"
WHERE file.name != "Memory"
SORT file.mtime DESC
```

*(No Dataview? Browse the `Memory/` folder directly.)*
