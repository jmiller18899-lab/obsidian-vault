---
title: betweenness-centrality
type: permanent
topic: clawagent
created: "2026-06-26"
tags: [permanent, clawagent/pipeline]
---

# 🕸️ betweenness-centrality

A graph metric: how often a node lies on the **shortest path** between other pairs of nodes.
In a note graph, a high-betweenness note is a **broker** — it connects otherwise-separate
clusters of ideas. Remove it and distant topics become unreachable from one another.

## Why it matters
It's the measurable signal that the WIKILINK_RESOLVER stage of the
[[Resources/ClawAgent Vault Pipeline Prompts|pipeline]] is doing its real job. Adding links
*inside* an already-dense cluster is redundant; adding links
that bridge distant clusters raises betweenness and makes the vault genuinely more navigable.
After a batch of writes, measure broker nodes — if new high-betweenness notes appear, the graph
is integrating, not just accreting.

## Practical read
- **High betweenness** → a hub/bridge; worth protecting and linking through.
- **Zero inlinks/betweenness** → an orphan; a candidate to connect or prune (see [[Index]] loose ends).

## 🔗 Links
- The lever that moves it: [[Resources/ClawAgent Vault Pipeline Prompts|Vault Pipeline Prompts]] (WIKILINK_RESOLVER)
- Hub: [[Maps of Content/ClawAgent MOC|ClawAgent MOC]]
