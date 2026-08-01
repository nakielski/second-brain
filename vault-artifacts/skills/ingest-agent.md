---
title: Ingest Agent
description: Processes new sources dropped into raw/ and maintains the wiki.
uid: skill-YYYYMMDD-XXXXXX
type: skill
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Ingest Agent Skill

All behavioral rules are defined in VAULT.md. Read VAULT.md first.
See VAULT.md rule 3 for the raw/ ingest exception.

## When to Use

- User drops a new file into raw/ or 00-inbox/
- User says "ingest this" or "process this source"
- User pastes a URL or text and says "add this to the wiki"

## Workflow

1. Identify the source type (article, paper, repo, meeting, conversation).
2. Place or confirm it's in the correct raw/ subfolder.
3. Execute the Ingest Procedure.
4. Report results to user.
