---
title: "Index Rebuild Procedure"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
priority: 10
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Index Rebuild Procedure

> `index.json` is maintained by agents, not by a script. Two modes.
>
> Exception: when the vault is reached through a write-hook server that keeps
> `index.json` in sync on every write (e.g. an MCP server), Mode A is done by the
> server. Agents then do not edit `index.json` at all; Mode B is requested from
> the server's rebuild function or done by the maintainer.

## Mode A — Incremental (default)

Whenever a page under `wiki/` or `90-system/agent-memory/` is created, modified,
moved, or archived: update that page's entry in the corresponding `index.json`
in the same session. The agent already has the frontmatter open — this costs
one additional write.

## Mode B — Full rebuild (on request, or when Lint reports drift)

1. List every `.md` file under `wiki/` (and under `agent-memory/` for `memory-index.json`).
2. For each file, read the frontmatter and take: `path`, `uid`, `title`, `type`,
   `status`, `summary`, `tags`, `created`, `updated`, `related`, `sources`, and for
   `type: source` additionally `content_hash` and `url`.
3. Sort entries by path ascending.
4. Write the array as UTF-8, 2-space indent.
5. Pages without `uid` are NOT given one here — report them as errors instead.

## Rules

- Never invent a `uid`. `uid` is assigned once by the creating agent.
- `index.md` and `memory-index.md` are Dataview-rendered and never edited manually.
- A full rebuild writes exactly the index file(s) — nothing else.
