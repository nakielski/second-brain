---
title: "01 — Interactive Setup"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

## INTERACTIVE SETUP

Ask the user these questions before creating anything:

### Q1: Language
> Which language should your vault be in?
> Options: German / English / Mixed (German notes, English tech terms)
> Default: Mixed

### Q2: User Name
> What is your name? (Used in templates, user context, and agent instructions)

### Q3: Primary Domains
> What are your main areas of interest / work? (3-7 domains)
> Examples: Software Architecture, AI/ML, Cloud, Career, Personal Development
> The agent creates a wiki concept page for each domain.
> Validation: if fewer than 3 or more than 7 domains are given, ask ONCE to
> narrow/expand; if the user insists, proceed with the given set.

### Q4: Daily Notes
> Do you want daily notes? Which folder?
> Options: Daily/ / Journal/ / 00-inbox/Daily/ / None
> Default: Daily/

### Q5: Agent Memory
> Should the vault include an Agent Memory Protocol?
> Options: Yes (full) / Yes (minimal) / No
> Default: Yes (full)

### Q6: Existing Vault
> Is there existing content to import?
> Options: Fresh start / Import from path (specify)
> Default: Fresh start

### Q7: Dataview Plugin
> Do you use the Obsidian Dataview plugin? (recommended — index.md and MOCs are
> then Dataview-rendered; otherwise index.md gets a static note. index.json is
> always generated regardless of this choice.)
> Options: Yes / No
> Default: Yes

### Q8: Vector Database / External Memory
> Does your setup include a vector database or external memory store that
> references vault notes (for semantic search, agent memory, or knowledge
> retrieval)?
> Options: None / Provider name + connection details (e.g. Qdrant, Chroma,
> a session-memory service, a RAG pipeline)
> Default: None
>
> Why this matters: external stores keep their own record of vault paths. The
> answer is recorded in the vault header and EVERY rename or move must update
> those references too (see Operations: Rename and Move Procedure). Without
> this answer, renames silently leave dead pointers behind.
