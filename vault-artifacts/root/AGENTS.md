---
title: "Agent Protocol"
uid: note-YYYYMMDD-XXXXXX
type: note
status: active
tags: [agents, protocol]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

**Session Start:**
1. Read VAULT.md (rules + ownership matrix).
2. Task routing — read ONLY what the task requires:

| If the task is… | then read |
|-----------------|-----------|
| a knowledge question | wiki/index.json + relevant pages |
| an ingest request | the raw/ file + Ingest Procedure.md |
| an eval request | Eval Procedure.md + golden-questions.md |
| about the user | user-context.md |
| continuity-dependent | agent-memory/memory-index.md |
| maintenance | Lint/Review/Eval Procedure.md |

3. Do NOT read index.md, the log, the inbox, or daily notes by default.
4. **Context budget:** max 15 files or ~50k tokens per session.

**Session Work:**
- Use templates from 90-system/Templates/.
- Follow ingest procedure when user drops a source.
- Follow query procedure when user asks a question.
- Follow lint/review/eval procedures on request.
- When creating a wiki page: link to at least 2 related pages.
- When making a decision: log in agent-memory/decisions/.

**Session End** (only if files were actually modified):
1. Write session log to 90-system/session-logs/.
2. Update memory-index.md if memories were created.
3. Regenerate index.json files via Index Rebuild Procedure.md.
4. Append to wiki log if any operation was performed.
5. Summarize in 2–3 sentences. If nothing changed: no writes.

Session logs older than 90 days are moved to 06-archive/.

All behavioral rules are defined in VAULT.md. Read VAULT.md first.

**Memory Types:**

| Type | Folder | When to create |
|------|--------|----------------|
| Context | context/ | Background info |
| Decision | decisions/ | Choice made with rationale |
| Mistake | mistakes/ | Something went wrong + lesson |
| Pattern | patterns/ | Recurring solution |
| Snapshot | snapshots/ | State at a point in time |
