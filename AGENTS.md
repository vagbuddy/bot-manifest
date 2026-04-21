# bot-manifest

Portable **rules**, **skills**, and **persona** for coding agents. This repository is not an application codebase.

## Read order

1. **`canon/rules/`** — policies (locale, architecture, security). Files use `.mdc` with YAML frontmatter: treat frontmatter as metadata, follow the markdown body as policy.
2. **`canon/persona/`** — communication style (Concise / Logical / Adaptive).
3. **`canon/skills/<name>/SKILL.md`** — procedural skills. Use `description` in frontmatter to decide relevance.
4. **Optional dated snapshots** — `YYYYMMDD/rules/` for frozen baselines when you pin a pack.

## Optional locale in other projects

When you consume these packs from an **application** repository, you may add **`bot-manifest.locale.{yaml,yml,json}`** at that repo’s root; see `examples/bot-manifest.locale.yaml`.

## Tooling

| Tool | How this repo maps |
|------|---------------------|
| **Cursor** | Copy or import `.mdc` rules; copy `canon/skills/*` into `~/.cursor/skills/` if you want native skills. |
| **GitHub Copilot** | Repository + IDE pick up **`.github/copilot-instructions.md`**; see also this file for agents. |
| **Claude (Code / CLI)** | Root **`CLAUDE.md`** (this file’s sibling) describes how to apply `canon/` for Anthropic tooling. |
