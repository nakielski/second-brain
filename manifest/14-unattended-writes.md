---
title: "14 — Unattended Writes"
type: note
status: active
created: 2026-08-16
updated: 2026-08-16
---

← Back to [[00-index]]

# Unattended Writes

Automated processes — cron jobs, schedulers, watchdogs, monitoring scripts —
sometimes want to persist their output in the vault: incident reports, status
snapshots, summaries. This chapter defines how, because unattended vault writes
are the most reliable source of three-layer violations in practice.

## The problem

An unattended writer:

- runs without an interactive session, so nobody performs the pre-write checks (duplicate search, layer classification);
- writes what it has (usually a single finished document) to the most visible place (a PARA folder);
- cannot judge whether the content also requires a raw/ record or a wiki/ entry;
- finishes, and the violation surfaces only when the post-write verification runs — often days later.

The result is an orphaned PARA note without provenance: exactly what the
Three-Layer Write Rule exists to prevent.

## Policy: deliver, don't write

**Automated processes do not write vault content.** They deliver their output
— notification, message, or a report file stored outside the vault — and an
agent session performs the structured vault write:

```
automation → deliver output (message/report outside vault)
                   ↓
agent session → classify layers
              → write raw/ + wiki/ + PARA in one batch
              → append write-log lines
```

This keeps a single write path: every vault write goes through an agent that
runs the full protocol (AGENTS.md), regardless of what triggered the content.

## Exception: unavoidable direct writes

If the platform cannot route an automation through an agent session, a direct
write is acceptable ONLY if the automation:

1. **Classifies layers** and writes ALL affected layers in the same run — never PARA alone;
2. **Logs every write** to `.vault-write-log.jsonl` with its own stable actor id (see `13-write-log.md`);
3. **Delivers a summary** (notification) so the next agent session can verify the write set and remediate gaps.

An automation that cannot meet all three requirements delivers instead.

## Verification

Post-write verification treats automation actor ids exactly like agent actors:
same three-layer correlation requirement (chapter 12). The write log's actor
field is what makes unattended writes auditable — a PARA entry with actor
`monitoring-cron` needs its raw/ and wiki/ counterparts from the same actor or
a follow-up remediation entry by an agent.

## Chapter relationships

- `12-write-rule-enforcement.md` — the enforcement layers this chapter plugs into
- `13-write-log.md` — actor ids and log requirements for direct-writing automations
- `vault-artifacts/operations/Remediation Procedure` — closing gaps after a detected violation
