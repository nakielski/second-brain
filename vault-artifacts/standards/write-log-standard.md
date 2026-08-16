---
title: "Write Log Standard"
uid: standard-20260816-write4b
type: standard
status: active
priority: 10
created: 2026-08-16
updated: 2026-08-16
---

# Write Log Standard

> Runtime specification of the vault write log. The vault root keeps an
> append-only `.vault-write-log.jsonl`. Every write appends one line per file,
> in the same turn as the write.

## Line format

One JSON object per line, UTF-8:

```json
{"ts": "2026-08-16T09:12:44Z", "actor": "main-agent", "layer": "para", "action": "create", "path": "01-projects/foo/bar.md", "uid": "concept-3fa2b9", "related_to": "concept-1c88de"}
```

| Field | Required | Values |
|-------|----------|--------|
| `ts` | yes | ISO-8601 UTC |
| `actor` | yes | stable process identifier; `human` for knowing manual registration |
| `layer` | yes | `raw` \| `wiki` \| `para` \| `system` |
| `action` | yes | `create` \| `modify` \| `rename` \| `archive` \| `delete` |
| `path` | yes | vault-relative path after the action |
| `uid` | no | frontmatter uid, if present |
| `related_to` | no | uid of the work item linking layer entries of one task |

## Rules

1. Append in the same turn as the write. Never batch.
2. Append-only. Corrections are new lines, never edits.
3. Paths and identifiers only — never file content.
4. All layers are logged: raw/, wiki/, para, 90-system (including index regeneration and archive moves).
5. Retain ≥ 90 days of entries.
6. If appending fails: the write may proceed, but the failure must be reported in the session summary.

## What reads the log

- Three-layer compliance checks (para writes must pair with raw/wiki writes by the same actor)
- Conflict detection between concurrent writers
- Index drift detection (wiki writes vs index.json)
- Attribution: files changed without a log entry are human/sync edits and are ignored by verification
