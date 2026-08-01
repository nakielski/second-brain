---
title: "Lint Procedure"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
priority: 10
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Lint Procedure

> Periodic health checks. Like eslint for knowledge. Triggered on user request.
> Scope: `lint --scope=full | incremental | <folder>`. Default: incremental.
> Privacy note: 05-people/ and entity_type: person pages checked at METADATA LEVEL ONLY.

## Checks

1. **Contradictions** — conflicting claims between pages. APPEND to wiki/open-questions.md.
2. **Orphan pages** — wiki pages with no incoming links.
3. **Missing concepts** — topics referenced via [[links]] but no page exists.
4. **Stale claims** — assertions that may be outdated based on newer sources.
5. **Investigation gaps** — pages with status: backlog or "TODO: research". APPEND to wiki/queue.md.
6. **Broken UID references** — related/sources entries whose uid does not exist.
7. **Index drift** — files present in wiki/ but missing from index.json, or vice versa.

## Output

```
## Lint Report — YYYY-MM-DD

### Contradictions (N found)
### Orphan Pages (N found)
### Missing Concepts (N found)
### Stale Claims (N found)
### Investigation Gaps (N found)
### Broken UID References (N found)
### Index Drift (N entries)

### Raw Counts
contradictions:        N
orphan_pages:          N
missing_concepts:      N
stale_claims:          N
investigation_gaps:    N
broken_uid_references: N
index_drift_entries:   N

### Health Score: X/100
```

Score formula:
```
score = 100
      - 5  * contradictions
      - 2  * orphan_pages
      - 3  * missing_concepts
      - 1  * stale_claims
      - 1  * investigation_gaps
      - 4  * broken_uid_references
      - 3  * index_drift_entries
score = max(0, score)
```

Append the report to wiki/log/ (current month's file).
