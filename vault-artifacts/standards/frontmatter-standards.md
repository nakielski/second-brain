---
title: "Frontmatter Standards"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

**Required (all notes):** uid, title, type, status, created, updated.
**Required (wiki pages only):** additionally summary, tags.
**Optional:** priority, related, sources, description, plus type-specific fields.

**Type values:** note, project, meeting, decision, daily, concept, entity, source, comparison, standard, skill.
(MOC files use type: note + tag moc.)

**Status values:** active, review, promote, legacy, backlog.

**UID:** SHA-256(creation timestamp + original path), first 6 hex chars, prefixed with creation type. Assigned once, never changed.

This file is the SINGLE SOURCE OF TRUTH for frontmatter.
