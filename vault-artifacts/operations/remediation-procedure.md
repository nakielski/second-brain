---
title: "Remediation Procedure"
uid: standard-20260816-rem91c
type: standard
status: active
priority: 10
created: 2026-08-16
updated: 2026-08-16
---

# Remediation Procedure

> Closing three-layer gaps after post-write verification flagged a violation:
> a PARA write without its raw/ and wiki/ counterparts. Run this procedure when
> an alert arrives — do not wait for the next lint.

## Step 1 — Validate the alert

1. Read the flagged entries in `.vault-write-log.jsonl`. A violation is real
   when a `para` entry by an actor has no `raw`/`wiki` counterparts by the
   same actor for the same work item.
2. **Human-edit check:** the flagged file has no write-log entry at all → a
   person or sync client touched it. Not a violation. Close the alert with a
   short note; never generate raw/wiki layers just to silence a checker.
3. If the write log is empty or missing (pre-log vaults): fall back to asking
   the writing actor or session history; document the evidence basis.

## Step 2 — Collect evidence from primary sources

Do not reconstruct the missing layers from memory. Gather the raw material:

- system logs, command output, live state of the systems involved
- the flagged PARA file itself (what happened, per its own content)
- session records and memory stores referencing the work item

## Step 3 — Write the missing layers

Following the full write protocol (AGENTS.md), in one batch:

4. **raw/**: an evidence record under `raw/conversations/` (dated, verbatim
   excerpts, source paths, "captured by" attribution). Immutable after creation.
5. **wiki/**: the generalized lesson or concept under `wiki/concepts/`
   (not a copy of the PARA note — the reusable knowledge), linked to ≥ 2
   related pages; update `wiki/index.json` and append to `wiki/log/`.
6. **PARA**: extend the flagged note with a short remediation appendix linking
   the new raw/ and wiki/ entries.

## Step 4 — Register and close

7. Append write-log lines for every file written in steps 4–6.
8. Register the remediation in the memory store (Q8) so future sessions find
   the completed gap-closure.
9. Re-run the verification check mentally or via tooling: the flagged entry
   now has same-actor counterparts. The alert is resolved.

## Pitfalls

- **Never fabricate evidence.** If primary sources are gone, the raw/ record
  states what is reconstructed and from which secondary source.
- **One violation, one remediation.** Do not batch-remediate unrelated old
  files during a single alert — that creates unreviewable noise.
- **Unattended writers:** if the actor was an automation, additionally check
  whether it should deliver instead of write (see `14-unattended-writes.md`);
  fixing the writer prevents the next violation.
