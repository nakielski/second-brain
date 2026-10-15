---
title: "Rename and Move Procedure"
uid: standard-20260816-mv2c7a
type: standard
status: active
priority: 10
created: 2026-08-16
updated: 2026-08-16
---

# Rename and Move Procedure

> Renaming or moving an existing file, or restructuring folders. Archive moves
> are moves — this procedure applies. Renames without it break incoming links,
> indexes, and every external system that references the old path.

## Before the rename

1. **Justify.** State why the rename is needed. Cosmetic renames are not worth
   the update cost.
2. **Inventory the blast radius.** Collect everything that references the old
   path or name:
   - `[[wikilinks]]` across the vault (Obsidian's backlink pane or a text search)
   - entries in `wiki/index.json` / `memory-index.json`
   - MOCs and index pages listing the note
   - external systems: vector databases, memory stores, session-memory
     providers — anything registered per Q8 in the vault header
3. **Pick the new name** following Naming Conventions.md. UIDs never change —
   a rename must never touch the `uid` field.

## Performing the rename

4. Rename/move the file (or apply the folder restructure).
5. In the SAME session, update every item from step 2:
   - fix all `[[wikilinks]]` to the new path
   - update `wiki/index.json` (path field) and `memory-index.json` if affected
   - update MOCs and index pages
   - re-register or update the entry in every external system from Q8 so
     lookups by old path heal instead of dead-ending
6. A `rename` line per affected file in the write log (actor, old → new path;
   see Write Log Standard.md) — written by the write-hook server when the rename
   goes through it, otherwise appended to `.vault-write-log.jsonl` yourself.

## After the rename

7. **Verify.** A text search for the old path must return zero references.
   Lint must report no new broken UID references and no index drift.
8. If step 5 cannot be completed for an external system (no write access),
   record the stale pointer in `wiki/queue.md` instead of leaving it silent.

## Rule of thumb

A rename is not finished when the file has moved — it is finished when nothing
in the vault or in any registered external system still points to the old path.
