# Claude — bot-manifest

This repository stores **portable** agent guidance: rules (`.mdc`), persona (`.mdc`), skills (`SKILL.md`), and optional dated snapshot folders.

## What to load

1. **`canon/rules/**/*.mdc`** — Treat YAML frontmatter as metadata; apply the markdown body as policy. Respect `alwaysApply` and `globs` when deciding relevance to the current files.
2. **`canon/persona/**/*.mdc`** — Communication style; same frontmatter convention as rules.
3. **`canon/skills/<skill-name>/SKILL.md`** — When the user task matches a skill’s `description`, follow that file for execution expectations.
4. **`YYYYMMDD/rules/**`** — Optional frozen packs; use only if the user pins a date folder.

## Locale

Human-language for explanations is governed by **`canon/rules/00-user-locale.mdc`** (explicit request → workspace `bot-manifest.locale.{yaml,yml,json}` → inference → fallback). Do not assume a fixed natural language from persona alone.

## Shared entry points

- **`AGENTS.md`** — Short human-oriented map of this repo (also used by other agents).
- **`.github/copilot-instructions.md`** — GitHub Copilot–specific mirror of loading rules (keep in sync conceptually with this file when you change high-level loading behavior).
