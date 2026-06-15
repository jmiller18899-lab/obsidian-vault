---
title: Index
type: index
tags: [moc, index]
---

# 🗂️ Master Index

> [!tip] The catalog of everything
> This is the searchable index of the whole vault — browse by **type**, **tag**, **recency**,
> or find **loose ends**. For curated topic navigation, use [[Maps of Content/Maps of Content|Maps of Content]] instead.
> Live tables below need the **Dataview** plugin; manual links work without it.

## 🧭 Jump to
- [[Home]] — dashboard · [[Maps of Content/Maps of Content|Maps of Content]] — topic hubs · [[Tags|Tag taxonomy]] — controlled vocabulary

---

## 📁 By area (PARA + spaces)
| Section | Index | Type |
|---------|-------|------|
| 📥 Inbox | [[Inbox/Inbox\|open]] | capture |
| 📅 Daily | [[Daily/Daily\|open]] | log |
| 🎯 Projects | [[Projects/Projects\|open]] | actionable |
| 🌱 Areas | [[Areas/Areas\|open]] | actionable |
| 📚 Resources | [[Resources/Resources\|open]] | reference |
| 🗒️ Notes | [[Notes/Notes\|open]] | thinking |
| 🗺️ Maps of Content | [[Maps of Content/Maps of Content\|open]] | navigation |
| 🗄️ Archive | [[Archive/Archive\|open]] | inactive |
| 🤖 Memory | [[Memory/Memory\|open]] | agent |

---

## 📑 By type
```dataview
TABLE rows.file.link AS "Notes", length(rows) AS "Count"
FROM ""
WHERE type AND file.name != "Index"
GROUP BY type
SORT type ASC
```

## 🏷️ By tag
```dataview
TABLE length(rows) AS "Count", rows.file.link AS "Notes"
FROM ""
FLATTEN file.tags AS tag
WHERE tag
GROUP BY tag
SORT length(rows) DESC
```
See [[Tags]] for what each tag means.

## 🆕 Recently updated
```dataview
TABLE type, file.mtime AS "Modified"
FROM ""
WHERE file.name != "Index"
SORT file.mtime DESC
LIMIT 15
```

## 🧩 Loose ends (orphans & stubs)
Notes nothing links to — candidates to connect into a [[Maps of Content/Maps of Content|MOC]] or delete.
```dataview
LIST
FROM ""
WHERE length(file.inlinks) = 0 AND !contains(file.name, "Index") AND type != "dashboard" AND type != "index"
SORT file.name ASC
```

---

## 🔤 A–Z (all notes)
```dataview
LIST
FROM ""
WHERE file.name != "Index"
SORT file.name ASC
```

> [!note] No Dataview installed?
> Use `Ctrl/Cmd + O` (quick switcher) to jump to any note by name, the **tag pane** to browse
> by tag, and the section index notes above to browse by area.
