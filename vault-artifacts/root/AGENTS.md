---
title: "Agent Protocol"
uid: note-20260729-b7e2f4
type: note
status: active
tags: [agents, protocol]
created: 2026-07-29
updated: 2026-08-06
---

**Session Start:**

1. Read VAULT.md (rules + ownership matrix).
2. Task routing — read ONLY what the task requires:

| If the task is… | then read |
|-----------------|----------|
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
| **PARA/** | `00-inbox/`, `01-projects/`, `02-areas/`, `03-notes/`, `04-resources/`, `05-people/`, `06-archive/`, `Daily/` | Human-curated notes, project docs, reference material | Human/Agent mix |

A single piece of work may touch ALL THREE layers. Example: documenting a migration = raw/conversations/ (session record) + wiki/concepts/ (knowledge) + wiki/log/ (operation log) + PARA (human-readable reference).

**Atomic Write Pattern:**

All affected layers MUST be written in the same turn. Before any PARA write, confirm:

```
Three-Layer Write Check:
- [ ] raw/ — created? path: ...
- [ ] wiki/ — created? path: ...
- [ ] PARA — created? path: ...
```

If a layer is "No" but should be affected: STOP, fix before proceeding. "I'll write raw/ and wiki/ later" is not acceptable. A task is NOT complete until ALL affected layers are updated.

**Write log (MANDATORY, same turn as every write):** Append one line per written file to `.vault-write-log.jsonl` in the vault root — after each write, not batched at session end. Format and rules: `90-system/Standards/Write Log Standard.md`. Every layer is logged (raw/, wiki/, para, 90-system), including index regeneration and archive moves.

**Unattended writers:** Automated processes (cron jobs, watchers) must not write vault content directly — they deliver, and an agent performs the structured write.

For enforcement details (post-write verification, platform extension points, anti-patterns), see `manifest/12-write-rule-enforcement.md`.

**Session End** (only if files were actually modified):
1. Write session log to 90-system/session-logs/.
2. Update memory-index.md if memories were created.
3. Regenerate index.json files via Index Rebuild Procedure.md.
4. Append to wiki log if any operation was performed.
5. Summarize in 2–3 sentences.

If nothing changed: no writes.

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