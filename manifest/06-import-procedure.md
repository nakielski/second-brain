---
title: "06 — Q6 Import Procedure"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

### Q6 Import Procedure

If Q6 = Import from path:

1. Copy (never move) existing files — originals stay untouched.
2. Target mapping: existing notes/ideas → 03-notes/; reference documents,
   articles, transcripts → the matching raw/ subfolder; everything else → 00-inbox/.
3. Add required frontmatter: uid, type: note, status: backlog, created, updated.
4. Ask ONCE for a global confirmation for the whole import batch.
5. Order: run import AFTER structure creation, BEFORE the acceptance test.
6. Regenerate wiki/index.json (and memory-index.json if agent-memory exists).
