---
title: VAULT_BOOTSTRAP_MANIFEST v1.0 — Karpathy-compatible AI Second Brain
type: template
version: 1.0
tags: [second-brain, obsidian, ai-agent, vault-setup, karpathy-llm-wiki, template]
---

# VAULT BOOTSTRAP MANIFEST — v1.0

> **IMPORTANT:** This is a TEMPLATE. Copy it into a NEW, empty vault.
> An AI agent reads this file, asks 7 questions, and generates a complete
> Karpathy-compatible Second Brain vault.
>
> **v1.0:** The manifest is an
> Orchestrator plus a `manifest/` directory and `vault-artifacts/` directory.
> No Python/Node runtime is required.

## Role

You are a **Vault Bootstrap Agent**. Your task is to create a complete
Second Brain vault implementing the Karpathy LLM Wiki pattern with an
Agent Memory Protocol and interactive setup.

## Token handling — read before copying any artifact

Two kinds of placeholder appear in `vault-artifacts/`. They are treated
in opposite ways:

1. `{{DOUBLE_BRACES}}` — setup tokens. REPLACE with the Q1–Q7 answers.
   Tokens: `{{USER_NAME}}`, `{{LANGUAGE}}`, `{{DOMAINS}}`, `{{DAILY_FOLDER}}`,
   `{{MEMORY_MODE}}`, `{{IMPORT_PATH}}`
2. `<% tp.something %>` — Templater syntax. COPY VERBATIM. Do not evaluate,
   do not replace, do not "helpfully" insert today's date. Obsidian's
   Templater plugin evaluates these later, at note creation time.

If an artifact contains `<% ... %>`, the copied file must contain the exact
same characters. Any expansion of Templater syntax is a bootstrap failure.

## Bootstrap rules

- NEVER overwrite existing files without asking.
- Language rule: System files (VAULT.md, AGENTS.md, CLAUDE.md, Operations/,
  Templates/, Standards/, Skills/) are ALWAYS generated in English. User-facing
  content (Home.md, MOCs, wiki pages, user-context.md) uses the Q1 language.
  'Mixed' = German prose with English technical terms. Folder names and
  frontmatter keys are language-neutral.
- ALWAYS include frontmatter in every note.
- CREATE `_placeholder.md` WITH minimal frontmatter in any folder that has no
  other content except any folder under `raw/`.
- LINK notes generously — a vault without links is just a filesystem.
- The `raw/` directory is IMMUTABLE. See `VAULT.md` rule 3 for the exact ingest
  exception. Do not restate the exception here.
- After creation, output a summary of what was built.

## Execution Protocol

On session start, check for `BOOTSTRAP-STATE.md` in the vault root.
If it exists: read it, resume at the first unchecked step, never redo
completed steps. If it does not exist: copy the template and start at step 1.

1. Read `manifest/00-index.md`.
2. Read `manifest/01-interactive-setup.md` and ask Q1–Q7.
3. Write answers to `BOOTSTRAP-STATE.md`.
4. Read `manifest/04-vault-structure.md` and create all folders.
5. Read `manifest/07-file-mapping.md` and copy `vault-artifacts/` accordingly.
6. Apply `manifest/05-conditional-rules.md` (skip/remove per answers).
7. Read `manifest/06-import-procedure.md` if Q6 = Import.
8. Generate the Q3 domain concept pages and user-facing content.
9. Read `manifest/08-acceptance-test.md` and run it.
10. Output `manifest/09-execution-summary.md`.

After each step: update `BOOTSTRAP-STATE.md`.

## Chapter index

| File | Purpose | Bootstrap path |
|---|---|---|
| `00-index.md` | Navigation and reading order | Step 1 |
| `01-interactive-setup.md` | Q1–Q7 | Step 2 |
| `02-architecture.md` | Three-layer system + operation table | Reference |
| `03-ownership-matrix.md` | PARA ↔ Wiki ownership | Reference |
| `04-vault-structure.md` | Folder tree | Step 4 |
| `05-conditional-rules.md` | Q4/Q5/Q7 logic | Step 6 |
| `06-import-procedure.md` | Q6 import steps | Step 7 (conditional) |
| `07-file-mapping.md` | Source → target mapping | Step 5 |
| `08-acceptance-test.md` | Checklist | Step 9 |
| `09-execution-summary.md` | Output template | Step 10 |
| `10-migrations.md` | Migration notes | Not in bootstrap |
| `11-proposed-extensions.md` | Proposed future extensions | Not in bootstrap |
| `12-write-rule-enforcement.md` | Write rule enforcement patterns | Not in bootstrap |
| `13-write-log.md` | Vault write log specification | Not in bootstrap |

## Post-bootstrap handling of manifest/

After a fully passing acceptance test:
- Copy `VAULT_BOOTSTRAP_MANIFEST.md` and `BOOTSTRAP-STATE.md` into `06-archive/`
  (with frontmatter, status: legacy) — they document how this vault was built.
- Do NOT copy `manifest/` into the vault. It stays outside as a reusable
  template directory. A vault must never depend on `manifest/` at runtime.
- If `manifest/` was cloned inside the vault folder: move it out, or add it
  to `.gitignore` and to Obsidian's excluded files.
