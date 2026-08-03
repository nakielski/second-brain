# Contributing to second-brain

Thanks for your interest in improving this project. This is a community
template — contributions are welcome and appreciated.

## What kind of contributions are helpful

**Bug reports** are the most valuable contribution. If the bootstrap
manifest produces unexpected results — broken links, missing files,
incorrect folder structure, failed acceptance checks — please open
an [Issue](../../issues) with:

- Which AI agent you used (Claude, Cursor, Gemini, other)
- The 7 setup answers you provided (Q1-Q7)
- What you expected vs. what happened
- The relevant section of the bootstrap output

**Template improvements** — better wording, clearer instructions,
missing edge cases in the manifest chapters. These are the core of
the project and the highest-impact contributions.

**New page templates or standards** — if you have a note template or
convention that works well with the three-layer architecture, propose
it via an Issue first so we can discuss fit before you build a PR.

**Documentation fixes** — typos, unclear passages, missing steps.

## What doesn't fit

- **Personal vault content** — this is a generic template, not a place
  for domain-specific notes or personal configurations.
- **Runtime code** — the manifest is deliberately platform-independent
  (no Python, Node, or Bash). Don't add scripts that require a runtime.
- **Agent-specific logic** — the manifest works with any capable LLM.
  Don't hardcode behavior for a specific AI tool.

## How to submit a change

1. **Fork** the repository.
2. **Create a branch** from `main`: `git checkout -b fix/short-description`.
3. **Make your change.** Keep commits focused — one logical change per commit.
4. **Test manually:** run the bootstrap with your change using your preferred
   AI agent. Verify the acceptance test in `manifest/08-acceptance-test.md` passes.
5. **Open a Pull Request** against `main`. Describe what you changed and why.

## Manifest file conventions

- Each chapter file in `manifest/` should stay under **5,000 characters**
  (8,000 max with justification). Large files exceed agent context budgets.
- Every file under `vault-artifacts/` must have exactly one mapping row in
  `manifest/07-file-mapping.md`. If you add or remove an artifact, update
  the mapping.
- `{{DOUBLE_BRACES}}` = setup tokens (replaced by Q1-Q7 answers).
  `<% tp.something %>` = Templater syntax (copied verbatim). Never mix them up.
- System files (VAULT.md, AGENTS.md, CLAUDE.md, Operations, Templates,
  Standards, Skills) are always English. User-facing content follows Q1.
- After structural changes, run through `manifest/08-acceptance-test.md`
  Part A (manifest integrity) to verify nothing is broken.

## Reporting security concerns

If you find a way the bootstrap could overwrite existing files or
otherwise cause data loss, please **do not open a public Issue**.
Message me privately via GitHub instead.

## License

By contributing, you agree that your contributions will be licensed
under the [MIT License](LICENSE).
