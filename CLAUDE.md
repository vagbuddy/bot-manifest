# Claude — bot-manifest

This repository stores **portable** agent guidance: rules (`.mdc`), persona (`.mdc`), skills (`SKILL.md`), and optional dated snapshot folders.

## What to load

1. **`canon/rules/**/*.mdc`** — Treat YAML frontmatter as metadata; apply the markdown body as policy:
   - **`00-architecture-and-security.mdc`** — Zero-trust baseline: no hardcoded secrets, injection prevention, XSS prevention, IDOR checks, safe refactoring, workspace isolation, mandatory reproducibility, and pre-exposure security & protocol boundaries (mandatory warnings and local admin setup prior to exposing services via tunnels or proxies).
   - **`00-user-locale.mdc`** — Language resolution (explicit chat override → `bot-manifest.locale.*` → inference → fallback to `en`). Identifiers stay English.
   - **`01-dependencies-and-established-patterns.mdc`** — Respect existing workspace abstractions before adding new dependencies.
   - **`02-code-simplicity.mdc`** — Core engineering craft: subtraction over accretion (simplify from first principles, don't patch bad patterns), domain invariants over heuristics (ban fuzzy matching and speculative fallback chains), single level of abstraction (SLAP), mechanical sympathy (respect execution costs), and bounded cognitive load (classes under 300-500 lines).
   - **`05-git-remotes.mdc`** — Push only on explicit user request in the current turn; commit only relevant files.
   - **`10-versioning-and-releases.mdc`** — SemVer release tags without `v` prefix (except Go modules).
   - **`15-code-documentation.mdc`** — Preserve existing comments and docstrings.
   - Stack conventions: **`20-go-conventions.mdc`**, **`20-python-conventions.mdc`**, **`20-react-typescript-conventions.mdc`**.
2. **`canon/persona/**/*.mdc`** — Communication style (Concise / Logical / Adaptive).
3. **`canon/skills/<skill-name>/SKILL.md`** — When the user task matches a skill’s `description`, follow that file for execution expectations.
4. **`YYYYMMDD/rules/**`** — Optional frozen packs; use only if the user pins a date folder.

## Locale

Human-language for explanations is governed by **`canon/rules/00-user-locale.mdc`** (explicit request → workspace `bot-manifest.locale.{yaml,yml,json}` → inference → fallback). Do not assume a fixed natural language from persona alone.

## Shared entry points

- **`AGENTS.md`** — Short human-oriented map of this repo (also used by other agents).
- **`.github/copilot-instructions.md`** — GitHub Copilot–specific mirror of loading rules (keep in sync conceptually with this file when you change high-level loading behavior).
