---
title: Inbox
type: index
tags: [moc, inbox]
---

# 📥 Inbox

> [!tip] Capture first, organize later
> Drop **anything** here without thinking about where it belongs — links, ideas, quotes,
> tasks, half-thoughts. Empty the inbox regularly by moving each item to its real home.

## How to process the inbox
For each item, ask **"Is this actionable?"**
- **Yes, with a goal & deadline** → move to **[[Projects/Projects|Projects]]**
- **Yes, ongoing responsibility** → move to **[[Areas/Areas|Areas]]**
- **No, but worth keeping** → move to **[[Resources/Resources|Resources]]** or distill into a **[[Notes/Notes|Permanent Note]]**
- **No, and not worth keeping** → delete, or send to **[[Archive/Archive|Archive]]**

## Quick add
- [ ] _Write the thing you just thought of here…_

```dataview
LIST
FROM "Inbox"
WHERE file.name != "Inbox"
SORT file.ctime DESC
```

---
*Aim for "inbox zero" weekly. An empty inbox means everything has a home.*
