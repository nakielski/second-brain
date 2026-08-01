---
title: "04 — Vault Structure"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

## VAULT STRUCTURE

Create this folder structure:

```
<VAULT-ROOT>/
├── AGENTS.md                           # Agent protocol (session start/work/end)
├── VAULT.md                            # Operating contract (front door)
├── Home.md                             # Main MOC (links to all areas)
├── .lock                               # Session lock file (created by writing agent)
├── .gitignore
├── .obsidian/                          # Obsidian base config
│
├── raw/                                # LAYER 1: Immutable sources
│   ├── articles/                       # Web articles, blog posts
│   ├── papers/                         # Academic papers
│   ├── repos/                          # Code repository snapshots
│   ├── meetings/                       # Meeting notes/transcripts
│   ├── conversations/                  # Chat logs, conversations
│   └── assets/                         # Images, PDFs, data files
│
├── wiki/                               # LAYER 2: Agent-generated knowledge
│   ├── index.md                        # Content catalog for humans (Dataview)
│   ├── index.json                      # Content catalog for agents (machine)
│   ├── open-questions.md               # Register of flagged contradictions
│   ├── queue.md                        # Persistent backlog of deferred work
│   ├── log/                            # Append-only operation log
│   │   └── YYYY-MM.md                  # Current month's log
│   ├── concepts/                       # Concept pages (one per key idea)
│   ├── entities/                       # Entity pages (people, orgs, tools)
│   ├── sources/                        # Source summaries
│   └── comparisons/                    # Comparison pages (X vs Y)
│
├── 00-inbox/                           # Capture zone — unprocessed
├── 01-projects/                        # Active work with deadlines
├── 02-areas/                           # Ongoing responsibilities
├── 03-notes/                           # Permanent atomic notes (manual)
├── 04-resources/                       # Reference material (manual)
├── 05-people/                          # People notes
├── 06-archive/                         # Inactive / completed
├── Daily/                              # Daily notes (per Q4)
│
└── 90-system/                          # LAYER 3: Schema and infrastructure
    ├── CLAUDE.md                       # Schema: page templates, naming, operations
    ├── Templates/                      # Note templates (9 files)
    ├── Standards/                      # Rules and conventions (3 files)
    ├── Operations/                     # Procedure files (6 files)
    ├── eval/                           # Golden questions
    ├── agent-memory/                   # Agent memories (5 subfolders)
    ├── session-logs/                   # Session summaries
    ├── Skills/                         # Agent skills (2 files)
    └── user-context.md                 # "Who is the user" — for agents
```
