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

## Topic tags (your subjects)
These are **your** domains. Use **nested tags** (`parent/child`) so they group in the tag pane —
e.g. tag a note `#career/interview` and it rolls up under `#career`. Add a top-level tag *and*
the most specific child that fits.

### 💼 `#career`
| Tag | Use for |
|-----|---------|
| `#career/job-search` | Applications, openings, leads |
| `#career/interview` | Prep, questions, debriefs |
| `#career/skills` | Skills to build, certifications, learning |
| `#career/networking` | Contacts, conversations, follow-ups |
| `#career/goals` | Reviews, milestones, plans |

### 🧩 `#problem-solving`
| Tag | Use for |
|-----|---------|
| `#problem-solving/decision` | Decisions made + the reasoning behind them |
| `#problem-solving/troubleshooting` | Issues hit and how they were fixed |
| `#problem-solving/framework` | Mental models & repeatable approaches |
| `#problem-solving/lessons` | Lessons learned / "next time I'll…" |

### 🧠 `#memories`
Personal memories & journal (distinct from the agent's `Memory/` folder).
| Tag | Use for |
|-----|---------|
| `#memories/milestone` | Big moments worth remembering |
| `#memories/people` | Memories tied to a person |
| `#memories/place` | Trips, events, locations |
| `#memories/story` | Anecdotes worth retelling |

### ℹ️ `#info`
General information & reference you want to find again.
| Tag | Use for |
|-----|---------|
| `#info/reference` | Facts, specs, numbers, definitions |
| `#info/how-to` | Steps & procedures |
| `#info/contact` | Account details, addresses, key contacts |
| `#info/note-to-self` | Reminders & personal pointers |

> [!tip] Adding a new domain later
> Create a new `## ### Heading` here with its child tags first, then use it. Keeping the list
> here is what stops tag sprawl and keeps the [[Index]] tidy.

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
