# GitHub Copilot — bot-manifest

This repository holds **portable agent guidance** (markdown). When this workspace is open—or when these files are attached as context—treat the following as **authoritative**.

## Rules (`canon/rules/**/*.mdc`)

- Apply the **markdown body** of every `.mdc` file under `canon/rules/`.
- YAML frontmatter is **metadata** (for example `description`, `alwaysApply`, `globs`). If `globs` is present and the active file matches, prioritize that rule; if `alwaysApply` is true, keep it in mind for the whole session.

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
