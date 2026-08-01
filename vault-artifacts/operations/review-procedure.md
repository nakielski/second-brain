---
title: "Review Procedure"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
priority: 10
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Review Procedure

> Triggered on request. Resolves flagged contradictions, promotes mature notes,
> consolidates concept pages, and transitions page status.

## Steps

1. **Status transitions:**

   | From | To | Condition | Trigger |
   |------|----|-----------|--------|
   | backlog | active | body content, 2+ links, 1+ source | Ingest or Review |
   | active | review | newer contradicting source OR updated >180 days | Lint proposes, Review sets |
   | active | promote | mature note flagged as concept candidate | Review |
   | promote | active | Review decides note should remain a note | Review |
   | review | active | Contradiction in open-questions.md closed | Review |
   | review | legacy | demonstrably outdated, successor exists | Review, after confirmation |
   | legacy | — | Terminal; page is never deleted | — |

2. **Contradiction resolution:** maintain wiki/open-questions.md as a register.
3. **Consolidation:** concept pages restructured and merged. Before consolidation: snapshot to `90-system/agent-memory/snapshots/`. Snapshot frontmatter MUST include `snapshot_of`, `type: note`, `status: legacy`, `tags: [snapshot]`. Disabled if Q5 = No.
4. **Promotion:** notes with status: promote evaluated as concept page candidates.
5. **Work through wiki/queue.md** — resolve deferred items.
6. **Regenerate indexes** — run index-rebuild-procedure.md.

## Rules

- Never delete flagged content silently.
- Always cite sources.
- Log everything.
