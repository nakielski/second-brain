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

Advisory rules alone ("you should write to all layers") do not work. Agents skip steps under context pressure, long sessions, or task complexity. Three enforcement layers are needed.

## Enforcement Layer 1: Atomic Write Pattern

**Rule:** All affected layers MUST be written in the same turn. Not sequentially, not "I'll do raw/ later."

When an agent writes to PARA, it MUST also write to raw/ and wiki/ in the same tool-call batch if the content touches those layers.

### Atomic Write Template

```
Step 1: Pre-write check (search vault for duplicates)
Step 2: Classify layers (raw? wiki? PARA? multiple?)
Step 3: Write ALL layers in one batch:
         - raw/conversations/YYYY-MM-DD <topic>.md
         - wiki/concepts/<topic>.md
         - PARA/<target folder>/<note>.md
Step 4: Register in memory/index (Honcho, decisions log, etc.)
```

A task is NOT complete until ALL affected layers are updated. "I'll write raw/ and wiki/ later" is not acceptable.

## Enforcement Layer 2: Three-Column Checklist

Before any PARA write, the agent must explicitly confirm:

```
Three-Layer Write Check:
- [ ] raw/ — created? path: ...
- [ ] wiki/ — created? path: ...
- [ ] PARA — created? path: ...
```

If a layer is "No" but should be affected: STOP, fix before proceeding.

This checklist should be part of the agent's write protocol (skill, system prompt, or AGENTS.md).

## Enforcement Layer 3: Post-Write Verification (Platform Extension)

Advisory rules and checklists are "soft enforcement." For hard detection, a platform-specific verification step is recommended:

- **Cron job or hook** that checks: did PARA writes happen in the last N hours without corresponding raw/ and wiki/ writes?
- **Alert** (notification, log entry) when a violation is detected
- **Silent** when everything is in order

This is platform-specific and intentionally NOT part of the generic manifest. Each agent platform (Hermes, Claude Code, Cursor, etc.) implements its own verification. The manifest defines the pattern; the platform implements the code.

### Implementation Notes

- Check interval: every 6 hours is sufficient
- Time window: 24 hours (catches violations from the previous day)
- Detection logic: if PARA files were modified but no raw/ or wiki/ files in the same window → alert
- False positive mitigation: only check PARA directories that agents write to (00 Inbox, 01 Projects, 02 Areas, 03 Notes, 04 Resources). Ignore 06 Archive (historical) and Daily (automated).

## Anti-Pattern: Self-Violation

The most common violation pattern: an agent implements the write protocol (adds it to SOUL.md, creates the skill, writes the AGENTS.md entry) and then **immediately violates it** by writing only to PARA.

This is the "protocol self-violation" pattern:
1. Agent writes the protocol documentation
2. Agent writes content following old habits (PARA only)
3. User catches the violation: "Did you also write to raw/ and wiki/?"
4. Agent has to retroactively add the missing layers

**Root cause:** Writing the protocol is not the same as following it. The protocol must be followed from the FIRST write after implementation, not from some future session.

**Prevention:** The atomic write pattern (Layer 1) and the three-column checklist (Layer 2) exist specifically to prevent this. If the agent follows the checklist, the violation cannot happen.

## Relationship to Other Chapters

- `02-architecture.md` defines the three layers and their purposes
- `04-vault-structure.md` defines the folder paths
- `vault-artifacts/root/AGENTS.md` contains the advisory write rule (updated by this chapter to include the atomic pattern and checklist)
- This chapter defines enforcement mechanisms
