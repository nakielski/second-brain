---
title: "11 — Proposed Extensions"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

> Not read during bootstrap. This file is for open decisions only.

# Proposed Extensions

## Semantic Search

**Status:** DECISION-REQUIRED

A vector index for semantic search across wiki pages. Would enable similarity-based
querying beyond exact tag/UID matches.

**Pros:** Richer search, better contradiction detection.
**Cons:** Requires embedding model, adds complexity, ongoing maintenance.

**Recommendation:** Postpone until vault exceeds ~200 pages.

## Claim-Level Provenance

**Status:** DECISION-REQUIRED

Track provenance at the individual claim level rather than page level.

**Pros:** More precise contradiction detection, finer-grained trust.
**Cons:** High write overhead, verbose frontmatter, steep adoption curve.

**Recommendation:** Postpone until vault exceeds ~200 pages.
