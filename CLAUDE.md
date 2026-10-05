# Claude — bot-manifest

This repository stores **portable** agent guidance: rules (`.mdc`), persona (`.mdc`), skills (`SKILL.md`), and optional dated snapshot folders.

## What to load

1. **`canon/rules/**/*.mdc`** — Treat YAML frontmatter as metadata; apply the markdown body as authoritative policy:
   - `00-architecture-and-security.mdc` — Zero-trust baseline, security boundaries, reproducibility, build/test verification.
   - `00-user-locale.mdc` — User-facing locale resolution; identifiers stay English.
   - `01-dependencies-and-established-patterns.mdc` — Existing abstractions, manifests, codebase inspection, documentation.
   - `02-code-simplicity.mdc` — Subtraction over accretion, domain invariants, SLAP, mechanical sympathy.
   - `05-git-remotes.mdc` — Push only on explicit turn instruction; staging scope.
   - `10-versioning-and-releases.mdc` — SemVer release tags without `v` prefix (except Go).
   - `15-code-documentation.mdc` — Documentation integrity and preservation.
   - `20-*-conventions.mdc` — Go, Python, React/TypeScript conventions.
2. **`canon/persona/**/*.mdc`** — Communication style (Concise / Logical / Adaptive).
3. **`canon/skills/<name>/SKILL.md`** — Multi-step procedural workflows (e.g. `hybrid-stack-verification`). Follow when the task matches skill frontmatter description.
4. **`YYYYMMDD/rules/**`** — Optional frozen snapshot packs; use only when explicitly requested.

## Locale

Human-language for explanations is governed by **`canon/rules/00-user-locale.mdc`** (explicit request → workspace `bot-manifest.locale.{yaml,yml,json}` → inference → fallback). Do not assume a fixed natural language from persona alone.

## Shared entry points

- **`AGENTS.md`** — Universal map of this repo across coding agents.
- **`.github/copilot-instructions.md`** — GitHub Copilot instruction mirror.
- **`GEMINI.md`** — Gemini and Antigravity workspace instruction mirror.
