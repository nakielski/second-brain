---
title: "07 — File Mapping"
type: note
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

← Back to [[00-index]]

# File Mapping

Copy every file from `vault-artifacts/` to the vault target path.

| Source (`vault-artifacts/`) | Target in vault | Rename | Condition |
|---|---|---|---|
| `operations/ingest-procedure.md` | `90-system/Operations/Ingest Procedure.md` | Title Case | always |
| `operations/query-procedure.md` | `90-system/Operations/Query Procedure.md` | Title Case | always |
| `operations/lint-procedure.md` | `90-system/Operations/Lint Procedure.md` | Title Case | always |
| `operations/review-procedure.md` | `90-system/Operations/Review Procedure.md` | Title Case | always |
| `operations/eval-procedure.md` | `90-system/Operations/Eval Procedure.md` | Title Case | always |
| `operations/index-rebuild-procedure.md` | `90-system/Operations/Index Rebuild Procedure.md` | Title Case | always |
| `page-templates/concept-template.md` | `90-system/Templates/Concept Template.md` | Title Case | on demand |
| `page-templates/entity-template.md` | `90-system/Templates/Entity Template.md` | Title Case | on demand |
| `page-templates/source-template.md` | `90-system/Templates/Source Template.md` | Title Case | always |
| `page-templates/comparison-template.md` | `90-system/Templates/Comparison Template.md` | Title Case | on demand |
| `page-templates/note-template.md` | `90-system/Templates/Note Template.md` | Title Case | always |
| `page-templates/project-template.md` | `90-system/Templates/Project Template.md` | Title Case | always |
| `page-templates/meeting-template.md` | `90-system/Templates/Meeting Template.md` | Title Case | on demand |
| `page-templates/decision-template.md` | `90-system/Templates/Decision Template.md` | Title Case | on demand |
| `page-templates/daily-note-template.md` | `90-system/Templates/Daily Note Template.md` | Title Case | always |
| `standards/frontmatter-standards.md` | `90-system/Standards/Frontmatter Standards.md` | Title Case | always |
| `standards/naming-conventions.md` | `90-system/Standards/Naming Conventions.md` | Title Case | always |
| `standards/tag-taxonomy.md` | `90-system/Standards/Tag Taxonomy.md` | Title Case | always |
| `skills/ingest-agent.md` | `90-system/Skills/Ingest Agent.md` | Title Case | always |
| `skills/vault-steward.md` | `90-system/Skills/Vault Steward.md` | Title Case | always |
| `mocs/projects-moc.md` | `01-projects/_Projects MOC.md` | Prefix `_` | always |
| `mocs/areas-moc.md` | `02-areas/_Areas MOC.md` | Prefix `_` | always |
| `mocs/notes-moc.md` | `03-notes/_Notes MOC.md` | Prefix `_` | always |
| `mocs/resources-moc.md` | `04-resources/_Resources MOC.md` | Prefix `_` | always |
| `mocs/people-moc.md` | `05-people/_People MOC.md` | Prefix `_` | always |
| `wiki/index.md` | `wiki/index.md` | none | always |
| `wiki/index.json` | `wiki/index.json` | none | always |
| `wiki/open-questions.md` | `wiki/open-questions.md` | none | always |
| `wiki/queue.md` | `wiki/queue.md` | none | always |
| `wiki/log/YYYY-MM.md` | `wiki/log/YYYY-MM.md` | current month | always |
| `root/VAULT.md` | `VAULT.md` | none | always |
| `root/AGENTS.md` | `AGENTS.md` | none | always |
| `root/Home.md` | `Home.md` | none | always |
| `root/user-context.md` | `user-context.md` | none | always |
| `system/CLAUDE.md` | `90-system/CLAUDE.md` | none | always |
| `agent-memory/memory-index.md` | `90-system/agent-memory/memory-index.md` | none | Q5 ≠ No |
| `agent-memory/memory-index.json` | `90-system/agent-memory/memory-index.json` | none | Q5 ≠ No |
| `session-logs/session-log-skeleton.md` | `90-system/session-logs/YYYY-MM-DD_session-topic.md` | date + topic | at Session End |
| `eval/golden-questions.md` | `90-system/eval/golden-questions.md` | none | always |
| `extras/gitignore` | `.gitignore` | dot prefix | always |
| `extras/obsidian-base-config.md` | `.obsidian/` (config) | none | always |
| `extras/_placeholder.md` | `_placeholder.md` | none | every empty non-raw folder |

Q3 domain concept pages are generated during step 8, not copied from vault-artifacts/.
