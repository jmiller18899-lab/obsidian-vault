---
title: Projects
type: index
tags: [moc, projects]
---

# 🎯 Projects

> [!info] PARA · P = Projects
> A **project** is a series of tasks linked to a **goal**, with a **deadline**.
> Examples: "Launch personal website", "Plan Q3 trip", "Write thesis chapter 2".
> When a project is done or abandoned → move it to **[[Archive/Archive|Archive]]**.

## ➕ New project
Use the **[[Templates/Project|Project template]]** (`Ctrl/Cmd + T` if Templates plugin is on).

## Active projects

```dataview
TABLE status, deadline, file.mtime AS "Updated"
FROM "Projects"
WHERE file.name != "Projects" AND status != "done"
SORT deadline ASC
```

*(No Dataview? List active projects manually below.)*
- _[[Example Project]]_

## Done / archived
See **[[Archive/Archive|Archive]]**.
