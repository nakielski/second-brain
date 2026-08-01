---
title: "08 — Acceptance Test"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

# Acceptance Test

## Part A — Manifest integrity (before bootstrap)

- [ ] `manifest/` contains 12 chapter files
- [ ] Every chapter file ≤ 5,000 characters (exceptions justified, ≤ 8,000)
- [ ] Every file under `vault-artifacts/` has exactly one mapping row in `07-file-mapping.md`
- [ ] Every mapping row points to an existing source file in `vault-artifacts/`
- [ ] No runtime keywords (script extension, runtime names, shebang marker) in generated files
- [ ] `VAULT_BOOTSTRAP_MANIFEST.md` (Orchestrator) ≤ 8,000 characters

## Part B — Vault integrity (after bootstrap)

### Structure
- [ ] `raw/` exists with 6 subfolders (articles, papers, repos, meetings, conversations, assets)
- [ ] `wiki/` exists with `index.md`, `open-questions.md`, `log/` (current month file), and 4 type subfolders
- [ ] `90-system/` exists with `CLAUDE.md`, `Templates/`, `Standards/`, `Operations/` (6 files), `eval/`, `agent-memory/`, `session-logs/`, `Skills/`
- [ ] 00-06 numbered folders exist
- [ ] Daily folder exists matching Q4 (skip if Q4 = None)
- [ ] Agent Memory per Q5 answer

### Key Files
- [ ] `VAULT.md` exists with 11 rules + ownership matrix
- [ ] `AGENTS.md` exists (max 80 lines)
- [ ] `90-system/CLAUDE.md` exists
- [ ] `wiki/index.md`, `wiki/index.json` exist
- [ ] `wiki/open-questions.md`, `wiki/queue.md` exist
- [ ] `wiki/log/` has current month file
- [ ] `Home.md` links to all MOCs + wiki
- [ ] `user-context.md` exists
- [ ] `BOOTSTRAP-STATE.md` exists
- [ ] `.gitignore` exists

### Templates
- [ ] 4 Core Templates (Note, Project, Daily Note, Source)
- [ ] 5 Extended Templates (on demand)
- [ ] 3 standards

### Operations (6 procedure files)
- [ ] Ingest, Query, Lint, Review, Eval + Index Rebuild

### Quality
- [ ] Every `.md` file has frontmatter starting at line 1
- [ ] `wiki/index.json` is valid JSON (parseable)
- [ ] `frontmatter-standards.md` is the single source of truth
- [ ] No empty folders outside `raw/`
- [ ] One `wiki/concepts/` page per Q3 domain

Output a checklist with check/cross for each item.
