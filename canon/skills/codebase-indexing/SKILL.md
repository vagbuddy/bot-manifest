---
name: codebase-indexing
description: Maps Go services, Python scripts, and React relationships via broad codebase search; anchors dependency claims using go.mod, package.json, and requirements.txt. Use before refactors or cross-stack edits.
---

# Codebase indexing

- Proactively use **@Codebase** (or equivalent repo-wide search) to understand how Go services, Python scripts, and React components connect before invasive edits.
- Always check **`go.mod`**, **`package.json`**, and **`requirements.txt`** (and lockfiles when present) so suggested libraries and versions match the project.
