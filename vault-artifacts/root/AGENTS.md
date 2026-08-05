---
title: "Agent Protocol"
uid: note-20260729-b7e2f4
type: note
status: active
tags: [agents, protocol]
created: 2026-07-29
updated: 2026-08-05
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

**Three-Layer Write Rule (MANDATORY before every vault write):**
Before writing ANY file to the vault, classify the content into one of three layers:

| Layer | Path | What goes here | Mutability |
|-------|------|---------------|------------|
| **raw/** | `raw/conversations/`, `raw/articles/`, `raw/papers/`, `raw/meetings/` | Original sources, chat transcripts, session records | IMMUTABLE after creation |
| **wiki/** | `wiki/concepts/`, `wiki/entities/`, `wiki/sources/`, `wiki/log/` | Agent-generated knowledge, compiled concepts, session logs | Agent-owned, versioned |
| **PARA/** | `00 Inbox/`, `01 Projects/`, `02 Areas/`, `03 Notes/`, `04 Resources/`, `05 People/`, `06 Archive/`, `Daily/` | Human-curated notes, project docs, reference material | Human/Agent mix |

A single piece of work may touch ALL THREE layers. Example: documenting a migration = raw/conversations/ (session record) + wiki/concepts/ (knowledge) + wiki/log/ (operation log) + PARA (human-readable reference).

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
