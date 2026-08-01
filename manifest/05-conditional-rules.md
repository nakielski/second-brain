---
title: "05 — Conditional Generation Rules"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

### Conditional Generation Rules

| Answer | Do not create | Remove lines from | Replacement behavior |
|--------|--------------|-------------------|---------------------|
| Q4 = None | Daily/ | Home.md daily note link; AGENTS.md daily routing; .obsidian daily-notes config | — |
| Q5 = minimal | 5 Memory subfolders | — | Flat files in agent-memory/, type field distinguishes; memory-index.md + .json still generated |
| Q5 = No | Entire agent-memory/ | AGENTS.md Memory Types table, session-end memory-index update, routing row; lint last-lint path; review snapshot path; Ownership Matrix Decisions column; Home.md memory-index link | Consolidation disabled; last_lint in wiki/queue.md frontmatter; memory-index.json not generated |
| Q7 = No | — | — | index.md gets static note + pointer to index.json; index.json remains authoritative |
