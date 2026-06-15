---
title: Daily
type: index
tags: [moc, daily]
---

# 📅 Daily Notes

> [!info] Your daily log & scratchpad
> One note per day for journaling, quick capture, tasks, and meeting notes.
> Press the **calendar / "Open today's daily note"** button, or `Ctrl/Cmd + P` → *Daily notes: Open today's note*.

New daily notes are created from the **[[Templates/Daily Note|Daily Note template]]** and land in this folder.

## Recent days

```dataview
LIST
FROM "Daily"
WHERE file.name != "Daily"
SORT file.name DESC
LIMIT 30
```

*(No Dataview? Daily notes are named `YYYY-MM-DD` in this folder.)*

## Why daily notes?
- **Frictionless capture** — there's always somewhere to write.
- **Timeline** — see what you worked on and thought about, by date.
- **Feeder** — distill the good bits into Permanent Notes later.
