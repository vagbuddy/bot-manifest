# Gemini & Antigravity — bot-manifest

This repository is the canonical source of truth for **portable agent guidance**: architecture and security rules, release versioning, git safety, communication persona, and executable skills.

---

## 1. What is in this manifest

### `canon/rules/` — Engineering and Safety Policies
Living rules formatted as `.mdc` with YAML frontmatter. The markdown body represents authoritative policy:

- **`00-architecture-and-security.mdc`** — Zero-trust baseline: zero tolerance for hardcoded secrets, injection prevention (parameterized queries only), XSS prevention (no `dangerouslySetInnerHTML`), IDOR/authorization checks, internal error masking, safe refactoring, references to git push / staging rules, and **mandatory reproducibility** (zero tolerance for ad-hoc manual state mutations against live databases or containers; all schema/data backfills must be version-controlled idempotent code).
- **`00-user-locale.mdc`** — Resolution order for `userFacingLocale` (explicit chat override → `bot-manifest.locale.*` config → recent chat inference → fallback to `en`). Preserves identifiers and standard technical tokens in English.
- **`01-dependencies-and-established-patterns.mdc`** — Check existing workspace patterns and abstractions before introducing new third-party libraries or frameworks.
- **`05-git-remotes.mdc`** — Git safety & staging scope:
  - **Remotes (Zero-Trust):** Execute `git push`, force-push, or remote branch updates **only** when the current user turn explicitly requests it. "Commit", "save", or prior turn confirmations never carry over.
  - **Commit & staging scope:** Stage (`git add`) and commit **only** files directly relevant to the active user request. Never bulk-sweep unrelated dirty files (`git add .`). Unrelated modified or untracked files are treated as user work-in-progress (WIP) and left untouched in the working tree.
- **`10-versioning-and-releases.mdc`** — SemVer 2.0 release tags without `v` prefix (e.g. `1.0.4`, not `v1.0.4`). Mandatory `v` prefix exception applies **only** to Go modules (`vX.Y.Z`).
- **`15-code-documentation.mdc`** — Documentation integrity: preserve existing comments and docstrings.
- **`20-go-conventions.mdc`** — Go standards: explicit error handling, table-driven tests.
- **`20-python-conventions.mdc`** — Modern Python standards, typing, clean modular structure.
- **`20-react-typescript-conventions.mdc`** — Modern React: functional components, strict TypeScript, no `any`, modern hook patterns.

### `canon/persona/` — Communication Style
- **`00-voice-clear.mdc`** — Tone and structure axes:
  - **Concise:** Brief, dense, direct answers first; no filler or repetitive caveats.
  - **Logical:** Calm, analytical, professional, empathetic to developer context.
  - **Adaptive:** Match the user's technical register and density.

### `canon/skills/` — Procedural Workflows
Self-contained skills (`SKILL.md`) for specialized execution workflows:
- **`codebase-indexing`** — Repository structure and symbol mapping.
- **`database-schema`** — Database migrations and schema inspection.
- **`documentation-web`** — Technical documentation workflows.
- **`hybrid-stack-verification`** — Cross-stack verification between backend and frontend.
- **`security-audit`** — Vulnerability scanning and credential checks.
- **`terminal-execution`** — Safe shell command execution and process management.

### Dated Snapshots (`YYYYMMDD/`)
Frozen snapshots (e.g. `20260422/`) for projects requiring pinned, immutable rule packs.

---

## 2. Gemini & Antigravity IDE Integration

When working with Google Gemini CLI, Antigravity IDE, or Gemini agents:

1. **Global Customizations (`~/.gemini/config/`):**
   - Rules mirror to `~/.gemini/config/rules/*.md`.
   - Skills map to `~/.gemini/config/skills/<name>/SKILL.md`.
2. **Workspace Root (`GEMINI.md` / `AGENTS.md`):**
   - Automatically loaded by Gemini / Antigravity as root workspace instructions.
3. **Workspace Customizations (`.agents/`):**
   - Local overrides and project-specific skills live under `.agents/rules/` and `.agents/skills/`.
4. **Precedence Hierarchy:**
   - Active user prompt instructions in chat (highest priority).
   - Workspace rules (`GEMINI.md`, `.agents/rules/`).
   - Global user rules (`~/.gemini/config/rules/`).
   - Default agent instructions.

---

## 3. Cross-Tool Sibling Files

- **`AGENTS.md`** — Universal human- and agent-readable repo summary.
- **`CLAUDE.md`** — Loading instructions for Claude Code / CLI.
- **`.github/copilot-instructions.md`** — Instructions for GitHub Copilot.
