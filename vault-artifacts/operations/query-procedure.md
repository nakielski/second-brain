---
title: "Query Procedure"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
priority: 10
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Query Procedure

> When the user asks a question, the agent searches the wiki.

## Steps

1. **Read wiki/index.json** — never parse index.md directly.
2. **Identify relevant pages** based on the question.
   **Fallback:** full-text search across wiki/ and 03-notes/.
3. **Read the relevant pages** — follow [[wiki-links]] to connected concepts.
4. **Synthesize an answer** in natural language.
5. **Cite sources** — every claim links to the wiki page and underlying source.
6. **Offer to save** — if valuable, offer to create a permanent wiki page.
7. **Regenerate indexes** — if files were created or modified.
8. **Append to the wiki log**.

## Rules

- ALWAYS cite specific wiki pages with [[links]].
- If knowledge is missing, say so — don't fabricate.
- If contradictions exist between pages, mention them.
