---
title: "Ingest Procedure"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
priority: 10
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Ingest Procedure

> When a new source is dropped into raw/ or 00-inbox/, the agent processes it.

## Steps

0. **Inbox handoff:** if the source sits in 00-inbox/, the agent renames it to
   YYYY-MM-DD_original-name.ext and moves it to the matching raw/ subfolder.
   Immutability begins only AFTER the file is placed in raw/.
0b. **Dedup check:** compute SHA-256 over the raw content. Look up the hash in
    wiki/index.json under `content_hash`; also check for a matching `url`. On hit:
    do NOT create a new source page. Report to user and offer to update the
    existing source summary instead.
1. **Read** the source document in raw/. Handle by source type:

   | Source type | Procedure | Extract artifact |
   |-------------|-----------|-----------------|
   | Text/PDF threshold | Read directly | — |
   | PDF > 20 pages / Asset > 1 MB | Extract text ONCE | `<name>.extract.md` |
   | Repo snapshot | Read README + manifest files + directory tree to depth 2. | `<name>.extract.md` |
   | Audio/Video | Transcript required. If missing: abort ingest. | `<name>.transcript.md` |
   | Image | Description + OCR text if available | `<name>.extract.md` |

2. **Identify key concepts** — what is this about? What entities are mentioned?
3. **Create a source summary** in wiki/sources/. Write `content_hash` into frontmatter.
4. **Create or update concept pages** in wiki/concepts/. ADD, don't overwrite.
5. **Create or update entity pages** in wiki/entities/.
6. **Create comparison pages** if the source compares two or more things.
7. **Cascade updates** — HARD LIMIT: 15 pages per ingest; queue remainder.
8. **Regenerate wiki/index.json** via index-rebuild-procedure.md.
9. **Append to wiki/log/**.
10. **Report** to user.

## Rules

- See VAULT.md rule 3 for the raw/ ingest exception.
- ALWAYS cite the source.
- Flag contradictions — don't silently overwrite.
