---
title: "Eval Procedure"
uid: standard-YYYYMMDD-XXXXXX
type: standard
status: active
priority: 10
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Eval Procedure

> Triggered after a major ingest or on explicit request. Measures query quality
> against a frozen golden-question set.

## Steps

1. **Load** `90-system/eval/golden-questions.md`.
2. **Run each question** through the Query procedure as if the user asked it.
3. **Score** each answer:
   - Correctly cited page(s): +1
   - Hallucination (claim with no source): -1
   - Missing knowledge (relevant page exists but answer says "not in wiki"): -1
4. **Compute** aggregate metrics: proportion correctly cited, proportion
   hallucinations, proportion missing-knowledge.
5. **Append to wiki/log/** — record the eval run, scores, and any drift since
   the last eval.
6. **Report** to user: metrics + failing questions.

## Rules

- Never edit golden questions during a run.
- Always use the same Query procedure the user would see.
- Flag questions whose expected pages no longer exist.
