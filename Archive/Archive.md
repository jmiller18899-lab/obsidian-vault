---
title: Archive
type: index
tags: [moc, archive]
---

# 🗄️ Archive

> [!info] PARA · The Archive
> Inactive items from the other three categories: completed projects, areas you no longer
> maintain, resources you stopped following. Nothing is deleted — just **out of the way**.

> [!tip] Why archive instead of delete?
> Search still finds it, links stay intact, and you can resurrect anything later.
> Your active folders stay clean and focused.

## Archived items

```dataview
TABLE type, file.mtime AS "Archived"
FROM "Archive"
WHERE file.name != "Archive"
SORT file.mtime DESC
```

*(No Dataview? Items moved here appear in the file tree under `Archive/`.)*
