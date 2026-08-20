# second-brain

> **Interactive Bootstrap Manifest for AI-agent-driven Obsidian Second Brain vaults.**
> Implements the Karpathy LLM Wiki pattern. Platform-independent — no Python, Node, or Bash required.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## What is this?

A modular template system that an AI agent (Claude, Cursor, Gemini, or any capable
LLM) reads and executes to create a complete Obsidian Second Brain vault from
scratch — with three-layer architecture, five core operations, an Agent Memory
Protocol, and interactive setup.

```
VAULT_BOOTSTRAP_MANIFEST.md    ← Orchestrator (5K, the entry point)
manifest/                      ← 12 chapter files (instructions for the agent)
vault-artifacts/               ← 42 template files (copied into the vault)
```

## Quick Start

### Prerequisites

- **Obsidian** installed (free from [obsidian.md](https://obsidian.md))
- An **AI agent** that can read files and create folders/files
- **Optional but recommended:** Dataview and Templater community plugins

### Installation (3 steps)

#### Step 1 — Get the manifest

```bash
git clone https://github.com/nakielski/second-brain.git
cd second-brain
```

Or download the ZIP and extract it.

#### Step 2 — Create an empty vault folder

```bash
mkdir ~/my-second-brain
```

Open this folder in Obsidian: **Settings → Vault → Open folder as vault**.

> **Important:** The vault folder must be empty. The manifest never overwrites existing files.

#### Step 3 — Run the bootstrap

Open your AI agent, point it at this repository, and say:

> Read `VAULT_BOOTSTRAP_MANIFEST.md` and execute it.
> Create the vault in `~/my-second-brain`.

The agent will ask 8 questions, then build the full vault.

### Setup Questions (Q1–Q8)

| # | Question | Options | Default |
|---|----------|---------|--------|
| Q1 | Language? | German / English / Mixed | Mixed |
| Q2 | Your name? | (used in templates) | — |
| Q3 | Primary domains? | 3–7 domains | — |
| Q4 | Daily notes? | Daily/ / Journal/ / None | Daily/ |
| Q5 | Agent Memory? | Yes (full) / Yes (minimal) / No | Yes (full) |
| Q6 | Existing content? | Fresh start / Import | Fresh start |
| Q7 | Dataview plugin? | Yes / No | Yes |
| Q8 | Vector DB / external memory store? | None / provider + connection | None |

## Architecture

```
raw/     →  Immutable sources (human curates, agent reads, NEVER modifies)
wiki/    →  Agent-generated knowledge (agent writes, human reads)
system/  →  Schema and operations (defines rules, agent follows)
```

## Five Core Operations

| Operation | Trigger | What happens |
|-----------|---------|-------------|
| **Ingest** | Drop source in `raw/` | Agent creates wiki pages, cascades updates |
| **Query** | Ask a question | Agent searches wiki, answers with citations |
| **Lint** | User request | Health checks: contradictions, orphans, drift |
| **Review** | User request | Resolves contradictions, promotes notes |
| **Eval** | After major ingest | Golden questions → quality metrics |

**Working with agents:** Point your agent at `AGENTS.md` in the vault root — it
defines the session protocol, layer classification, and write rules. Prefer one
agent session as the single write path for vault content, including content
triggered by automations (they deliver, the agent writes — see
`manifest/14-unattended-writes.md`). If multiple agents share the vault, the
append-only write log (`.vault-write-log.jsonl`) is the coordination surface:
conflicts are detected from overlapping log entries, not lock files.

## Design Principles

This project is built on principles that go beyond "it works":

- **Vendor-agnostic by design** — Pure Markdown. No runtime, no CLI, no install
  script. Works with any LLM that can read and write files. Switch agents anytime.
- **Interactive, not static** — 7 setup questions personalize the vault before a
  single file is created. Language, domains, memory depth, and daily notes are
  all configurable.
- **Tested, not assumed** — A formal acceptance test validates structure, frontmatter,
  JSON validity, and links before the vault is declared done.
- **Governed, not improvised** — 11 enforceable rules in `VAULT.md` with a defined
  precedence chain. Privacy protections, concurrency control, and immutability
  guarantees are explicit, not implicit.
- **Measurable, not subjective** — The Lint health score uses a published formula.
  Raw counts are reported alongside the score for full transparency.
- **Resumable, not fragile** — Interrupted bootstraps pick up where they left off
  via `BOOTSTRAP-STATE.md`. No start-over penalty.
- **Comprehensive, not fragmented** — PARA + Zettelkasten + MOC + Karpathy Wiki
  in one vault, unified by an Ownership Matrix that defines who owns what.
- **Concurrency-ready** — append-only write log with actor attribution; conflicts between concurrent writers are detected from overlapping log entries, and Git branching supports multi-user setups.

These are not features bolted on after launch. They are architectural decisions
made before the first file was written.

## Post-Bootstrap

1. **Open in Obsidian** — register templates folder in Templater settings
2. **Drop a source** into `raw/articles/`
3. **Tell your agent:** "Ingest the new source in raw/articles/"
4. **Ask:** "What does the wiki say about [topic]?"
5. **Weekly:** "Lint the wiki"

## License

MIT