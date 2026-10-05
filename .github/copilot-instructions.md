# GitHub Copilot — bot-manifest

This repository holds **portable agent guidance** (markdown). When this workspace is open—or when these files are attached as context—treat the following as **authoritative**.

## Rules (`canon/rules/**/*.mdc`)

- Apply the **markdown body** of every `.mdc` file under `canon/rules/`.
- YAML frontmatter is **metadata** (for example `description`, `alwaysApply`, `globs`). If `globs` is present and the active file matches, prioritize that rule; if `alwaysApply` is true, keep it in mind for the whole session.
- **Core engineering & safety rules:**
  - `00-architecture-and-security.mdc` — Zero-trust baseline, security boundaries, reproducibility, build/test verification.
  - `00-user-locale.mdc` — Language resolution (chat override → `bot-manifest.locale.*` → inference → fallback to `en`). Identifiers stay English.
  - `01-dependencies-and-established-patterns.mdc` — Respect existing workspace abstractions, codebase inspection, documentation verification.
  - `02-code-simplicity.mdc` — Subtraction over accretion, domain invariants, SLAP, mechanical sympathy, cognitive load limits.
  - `05-git-remotes.mdc` — Push only on explicit turn request; stage only relevant files.
  - `10-versioning-and-releases.mdc` — SemVer release tags without `v` prefix (except Go modules).
  - `15-code-documentation.mdc` — Preserve existing comments and docstrings.
  - Stack conventions: `20-go-conventions.mdc`, `20-python-conventions.mdc`, `20-react-typescript-conventions.mdc`.

## Persona (`canon/persona/**/*.mdc`)

- Same convention as rules: follow the body; use frontmatter as hints about scope.

## Skills (`canon/skills/**/SKILL.md`)

- Multi-step procedural workflows (e.g. `hybrid-stack-verification`). Read `SKILL.md` when the user’s request matches the skill’s `description` in frontmatter.

## Dated snapshots

- Top-level folders matching `20*` (e.g. `20260422/`) are **optional frozen** packs. Use **one** snapshot only when the user asks for that date.

## Locale

- Natural language for user-facing prose is resolved by **`canon/rules/00-user-locale.mdc`** (chat override → workspace `bot-manifest.locale.*` → inference → fallback). Do not assume a fixed human language from persona alone.

## Other agents

- **Claude (Code / CLI):** see repository root **`CLAUDE.md`** for the same loading contract in Anthropic-oriented tooling.
