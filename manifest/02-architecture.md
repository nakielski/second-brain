---
title: "02 — Architecture"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

## ARCHITECTURE: Three-Layer System

This vault implements the **Karpathy LLM Wiki pattern** with three layers:

```
raw/     →  Immutable sources (human curates, agent reads, NEVER modifies)
wiki/    →  Agent-generated knowledge (agent writes, human reads)
system/  →  Schema and operations (defines rules, agent follows)
```

And five core operations:

| Operation | Input | Output |
|-----------|-------|--------|
| **Ingest** | Drop source in raw/ | Agent reads, extracts, creates wiki pages, cascades updates, regenerates index + log |
| **Query** | Natural language question | Agent navigates via index.json, reads relevant pages, synthesizes answer with [[wiki-links]] |
| **Lint** | Triggered on user request | Agent scans for 7 health checks: contradictions, orphan pages, missing concepts, stale claims, investigation gaps, broken UID references, index drift |
| **Review** | Triggered on request | Agent resolves flagged contradictions, promotes mature notes, consolidates concept pages, transitions page status |
| **Eval** | Triggered after major ingest or on request | Agent runs golden questions, reports citation/hallucination/missing-knowledge metrics |

There are **5 core operations** but **8 procedure files** under
`90-system/Operations/`: ingest-, query-, lint-, review-, eval-procedure.md,
plus `Index Rebuild Procedure.md`, `Rename and Move Procedure.md`, and
`Remediation Procedure.md`. The three latter ones are not core operations;
they are shared utilities (index regeneration after writes; path updates on
renames and moves; gap closure after a detected write-rule violation).
