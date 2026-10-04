# GitHub Copilot — bot-manifest

This repository holds **portable agent guidance** (markdown). When this workspace is open—or when these files are attached as context—treat the following as **authoritative**.

## Rules (`canon/rules/**/*.mdc`)

- Apply the **markdown body** of every `.mdc` file under `canon/rules/`.
- YAML frontmatter is **metadata** (for example `description`, `alwaysApply`, `globs`). If `globs` is present and the active file matches, prioritize that rule; if `alwaysApply` is true, keep it in mind for the whole session.
- **Core engineering & safety rules:**
  - **`00-architecture-and-security.mdc`** — Zero-trust baseline: no hardcoded secrets, injection prevention (parameterized queries only), XSS prevention, IDOR checks, workspace isolation, mandatory reproducibility.
  - **`00-user-locale.mdc`** — Language resolution (explicit chat override → `bot-manifest.locale.*` → inference → fallback to `en`). Identifiers stay English.
  - **`01-dependencies-and-established-patterns.mdc`** — Respect existing workspace abstractions before adding new dependencies.
  - **`02-code-simplicity.mdc`** — Fundamental engineering craft:
    - *Subtraction over accretion:* simplify from first principles; do not patch bad patterns with defensive wrappers or fallback cascades.
    - *Invariants over heuristics:* model reality explicitly; ban ad-hoc fuzzy matching and speculative fallback chains.
    - *Single level of abstraction (SLAP):* strictly separate policy/orchestration, pure domain, and low-level mechanics/plumbing.
    - *Mechanical sympathy:* respect runtime and database execution costs; single-pass queries, indexed lookups, no unread sorts or Frankenstein record merges.
    - *Cognitive load & component size:* avoid monolithic classes (keep under 300 lines, strictly under 500 lines); decompose early upon growth.
  - **`05-git-remotes.mdc`** — Git safety: push only on explicit user request in the current turn; stage and commit only relevant files.
  - **`10-versioning-and-releases.mdc`** — SemVer release tags without `v` prefix (except Go modules).
  - **`15-code-documentation.mdc`** — Preserve existing comments and docstrings.

## Persona (`canon/persona/**/*.mdc`)

- Same convention as rules: follow the body; use frontmatter as hints about scope.

## Skills (`canon/skills/**/SKILL.md`)

- Each directory is one skill. Read `SKILL.md` when the user’s request matches the skill’s `description` in frontmatter.
- Skills describe **how to execute** a workflow (terminal, indexing, DB, docs, audit); they do not replace security or architecture rules.

## Dated snapshots

- Top-level folders matching `20*` (e.g. `20260422/`) are **optional frozen** packs. Use **one** snapshot only when the user asks for that date.

## Locale

- Natural language for user-facing prose is resolved by **`canon/rules/00-user-locale.mdc`** (chat override → workspace `bot-manifest.locale.*` → inference → fallback). Do not assume a fixed human language from persona alone.

## Other agents

- **Claude (Code / CLI):** see repository root **`CLAUDE.md`** for the same loading contract in Anthropic-oriented tooling.
