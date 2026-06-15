---
title: Resources
type: index
tags: [moc, resources]
---

# 📚 Resources

> [!info] PARA · R = Resources
> Topics or interests that may be useful in the future — reference material, not tied to a
> specific project. Examples: "Cooking recipes", "Productivity", "Python", "Books to read".

## ➕ New resource
Use the **[[Templates/Resource|Resource template]]** or **[[Templates/Literature Note|Literature Note]]** for books/articles/videos.

## Browse resources

```dataview
TABLE topic, source, file.mtime AS "Updated"
FROM "Resources"
WHERE file.name != "Resources"
SORT file.mtime DESC
```

*(No Dataview? Group resources by topic below.)*

### Topics
- _[[Productivity]]_
- _[[Programming]]_

### Reading list
- [ ] _Book / article to read_
