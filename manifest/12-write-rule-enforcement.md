---
title: "12 — Write Rule Enforcement"
type: note
status: active
created: 2026-08-06
updated: 2026-08-06
---

← Back to [[00-index]]

# Write Rule Enforcement

The Three-Layer Write Rule (defined in `AGENTS.md`) classifies content into raw/, wiki/, and PARA layers. This chapter defines **how to enforce it** — not just as advisory text, but as a verifiable pattern.

## The Problem

Agents frequently write to only one layer (typically PARA) and forget the others. This creates:
- Missing session records in `raw/`
- Missing knowledge entries in `wiki/`
- Orphaned PARA notes without provenance

Advisory rules alone (