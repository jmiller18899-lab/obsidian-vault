---
title: Tags
type: index
tags: [moc, index, meta]
---

# 🏷️ Tag Taxonomy

> [!info] A controlled vocabulary
> Consistent tags are what make indexing reliable. Pick tags from this list rather than
> inventing new ones on the fly — that keeps the [[Index]] and tag searches clean.
> Add a new tag here first, then use it.

## How to tag
- Put tags in **frontmatter**: `tags: [permanent, pkm]`
- Use **one structural tag** (what kind of note it is) + **any number of topic tags** (what it's about).
- Lowercase, singular, hyphenate multi-word: `#book-summary`, not `#Book Summaries`.
- Prefer **links** (`[[ ]]`) for connecting *ideas*; use **tags** for cross-cutting *categories*.

## Structural tags (note type)
One per note — mirrors the `type:` field.

| Tag | Meaning | Lives in |
|-----|---------|----------|
| `#moc` | Map of Content / index hub | anywhere |
| `#daily` | Daily note | `Daily/` |
| `#project` | Active project | `Projects/` |
| `#area` | Area of responsibility | `Areas/` |
| `#resource` | Reference material | `Resources/` |
| `#literature` | Note from a source (book/article/talk) | `Notes/` or `Resources/` |
| `#permanent` | Atomic evergreen idea | `Notes/` |
| `#meeting` | Meeting notes | anywhere |
| `#person` | Person profile | anywhere |
| `#meta` | About the vault itself | root |

## Status tags (optional, on tasks/projects)
| Tag | Meaning |
|-----|---------|
| `#now` | Active focus this week |
| `#next` | Queued, not started |
| `#waiting` | Blocked on someone/something |
| `#someday` | Maybe later |

## Topic tags (your subjects — grow this list)
Add the themes you actually write about. Starters:
- `#pkm` — personal knowledge management
- `#productivity`
- `#programming`
- `#health`
- `#finance`
- `#career`

## All tags in use
```dataview
TABLE length(rows) AS "Notes"
FROM ""
FLATTEN file.tags AS tag
GROUP BY tag
SORT length(rows) DESC
```

*(No Dataview? Open the **Tag pane** core plugin from the right sidebar to see every tag.)*

## 🔗 Related
- [[Index]] · [[Home]] · [[Maps of Content/Maps of Content|Maps of Content]]
