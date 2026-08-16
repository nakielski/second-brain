---
title: "00 — Index"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Manifest Index — v1.1

Read this file first, then follow the order below.

## Reading order

1. `01-interactive-setup.md` — ask Q1–Q8.
2. `04-vault-structure.md` — create the folder tree.
3. `07-file-mapping.md` — copy `vault-artifacts/` to the vault.
4. `05-conditional-rules.md` — skip/remove files per answers.
5. `06-import-procedure.md` — only if Q6 = Import.
6. `08-acceptance-test.md` — run Part A before bootstrap, Part B after.
7. `09-execution-summary.md` — output template.

## Reference chapters (not in the bootstrap path)

- `02-architecture.md` — three-layer system, 5 core operations, 6 procedure files, 7 Lint checks.
- `03-ownership-matrix.md` — canonical matrix lives in `VAULT.md`; this file is a pointer.
- `10-migrations.md` — migration notes for existing vaults; not read during bootstrap.
- `11-proposed-extensions.md` — Semantic Search, Claim-Level Provenance — DECISION-REQUIRED; not read during bootstrap.
- `12-write-rule-enforcement.md` — Three-layer write rule enforcement patterns (atomic writes, checklists, post-write verification).
- `13-write-log.md` — Append-only vault write log (`.vault-write-log.jsonl`): format, rules, conflict detection, and what post-write verification reads.
- `14-unattended-writes.md` — Policy for automated vault writers (cron jobs, watchdogs): deliver-don't-write, exception rules, verification.

## Key features

- Manifest split into Orchestrator (`VAULT_BOOTSTRAP_MANIFEST.md`) + `manifest/` chapters + `vault-artifacts/`.
- Legacy index-generation script removed; replaced by `Index Rebuild Procedure.md`.
- Lint expanded from 6 to 7 checks (index drift).
- `BOOTSTRAP-STATE.template.md` introduced for resumable bootstraps.
- `manifest/` is NOT copied into the vault after bootstrap.
- AGENTS.md template includes atomic write pattern and 3-column checklist (since v1.1).