# Gemini & Antigravity — bot-manifest

This repository is the canonical source of truth for **portable agent guidance**: architecture and security rules, release versioning, git safety, communication persona, and executable skills.

---

## 1. What is in this manifest

### `canon/rules/` — Engineering and Safety Policies
Living rules formatted as `.mdc` with YAML frontmatter. The markdown body represents authoritative policy:

- `00-architecture-and-security.mdc` — Zero-trust baseline, security boundaries, reproducibility, build/test verification.
- `00-user-locale.mdc` — User-facing locale resolution; identifiers stay English.
- `01-dependencies-and-established-patterns.mdc` — Existing abstractions, manifests, codebase inspection, documentation.
- `02-code-simplicity.mdc` — Subtraction over accretion, domain invariants, SLAP, mechanical sympathy.
- `05-git-remotes.mdc` — Push only on explicit turn instruction; staging scope.
- `10-versioning-and-releases.mdc` — SemVer release tags without `v` prefix (except Go).
- `15-code-documentation.mdc` — Documentation integrity and preservation.
- `20-*-conventions.mdc` — Go, Python, React/TypeScript standards.

### `canon/persona/` — Communication Style
- `00-voice-clear.mdc` — Tone and structure (Concise / Logical / Adaptive).

### `canon/skills/` — Procedural Workflows
Self-contained skills (`SKILL.md`) for multi-step execution workflows:
- `hybrid-stack-verification` — Cross-stack verification between backend contracts and frontend clients.

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

---

## 4. Execution & Network Boundaries (Gemini & Antigravity Only)

- **No unauthorized network/port probing:** Never perform network scanning, port probing (`Test-NetConnection`, `nc`, `nmap`, ping sweeps), DNS probing, or arbitrary remote host / SSH exploration unless explicitly requested by the user in this specific turn.
- **Local workspace scope only:** Shell commands are strictly restricted to local repository inspection, development, and building (e.g. pytest, git status/diff, npm build, local unit tests).
- **Immediate stop on missing service:** If a command or script fails because an external, remote, or containerized service (database, docker, cluster) is unreachable locally, **immediately stop**. Do not attempt to find alternative network routes or scan the LAN/WAN. State the failure clearly and output the query/command for the user, or ask how to proceed.
- **Pre-exposure security & protocol boundaries (Предупреждение ДО экспозиции):** Never expose or guide the operator to expose a service to the public internet (via Cloudflare Tunnels, reverse proxy rules, firewall, port forwarding, or public DNS) without explicitly stating the security posture and exposure scope **BEFORE** the exposure step is executed:
  1. *Unauthenticated setup wizards:* If a service initializes with an unauthenticated setup wizard, default credentials, or initial admin creation form (e.g. `/setup`), warn the operator and require completing initial admin setup locally (or provisioning credentials via config/environment) **before** routing public traffic to it. Publishing an uninitialized setup page to the internet is an immediate takeover vulnerability.
  2. *Protocol and perimeter transparency:* Explicitly state in advance what will and will not be accessible from the internet (e.g. "Web UI is exposed over HTTPS via the tunnel, but native TCP/SSH/SFTP protocols remain internal to LAN/VPN"). Never leave the operator to discover security caveats or protocol limitations after public routing is already active.
