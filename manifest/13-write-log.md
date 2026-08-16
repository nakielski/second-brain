---
title: "13 — Write Log"
type: note
status: active
created: 2026-08-16
updated: 2026-08-16
---

← Back to [[00-index]]

# Write Log

The vault keeps an append-only write log: `.vault-write-log.jsonl` in the vault
root. Every agent write appends one line per written file, in the same turn as
the write itself. Verification tooling reads this log — never file modification
times.

## Why a write log

File modification times cannot distinguish an agent write from a human edit in
Obsidian or a sync client touching a file. Any verification built on mtimes
produces false positives (human edits flagged as violations) and false negatives
(one agent's unrelated layer write excusing another agent's PARA-only write
inside a shared time window). A write log solves both: it records who wrote
what, when, to which layer.

## Format

One JSON object per line, UTF-8, appended to `.vault-write-log.jsonl`:

```json
{"ts": "2026-08-16T09:12:44Z", "actor": "main-agent", "layer": "para", "action": "create", "path": "01-projects/foo/bar.md", "uid": "concept-3fa2b9", "related_to": "concept-1c88de"}
```

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `ts` | string | yes | ISO-8601 UTC timestamp of the write |
| `actor` | string | yes | Stable identifier of the writing process (agent name, automation id, `human` for manual edits registered knowingly) |
| `layer` | string | yes | One of `raw`, `wiki`, `para`, `system` |
| `action` | string | yes | One of `create`, `modify`, `rename`, `archive`, `delete` |
| `path` | string | yes | Vault-relative path after the action |
| `uid` | string | no | Frontmatter uid, when the file has one |
| `related_to` | string | no | uid of the work item this write belongs to (links raw/wiki/para entries of the same task) |

## Rules

1. **Same turn.** Log lines are appended in the same turn as the writes they describe — never batched to "log later".
2. **Append-only.** The log is never rewritten or reordered. Corrections are new lines with a corrected entry, never edits.
3. **Paths only.** The log records paths and identifiers, never file content — it must stay safe to share and sync.
4. **Every layer.** raw/, wiki/, para, and 90-system writes are all logged. Session logs, index regeneration, and archive moves included.
5. **Retention.** Keep at least 90 days of entries. Platforms may rotate older lines into an archive file, but verification needs a window well beyond the check interval.
6. **Fail open on logging errors, but report.** If appending fails, the write may proceed, but the failure must surface in the session summary — an unlogged write is a silent gap in the audit trail.

## What verification reads from it

- **Three-layer compliance:** every `para` entry needs matching `raw` and `wiki` entries by the same actor within the same work item (correlated via `related_to` or timestamp proximity). Entries from other actors do not count.
- **Conflict detection:** two actors writing the same path within a short window is surfaced as a conflict report. Replaces lock-file protocols for concurrent multi-agent setups.
- **Index drift:** `wiki` entries in the log that never made it into `index.json` indicate a missed index regeneration (see `Index Rebuild Procedure.md`).
- **Human edits:** files modified without a log entry are, by definition, not agent writes. Verification ignores their mtimes entirely.

## Platform note

The log format and verification semantics are platform-neutral. Each platform
implements the append hook and the checker. The runtime copy of this
specification lives in the vault at `90-system/Standards/Write Log Standard.md`.
