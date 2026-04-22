---
name: hybrid-stack-verification
description: >-
  Before closing a task, checks whether Go or Python backend or contract changes
  require React (or other client) updates; escalates uncertain C# architecture
  refactors for user confirmation. Use for full-stack features, API changes, or
  multi-language PRs.
---

# Hybrid stack verification

- **Backend → frontend:** After edits to **Go** or **Python** services (routes, DTOs, enums, validation, auth, or error shapes), explicitly verify whether **React / TypeScript** clients, generated clients, or OpenAPI-derived types need updates. If the repo has no frontend, note “no client in this workspace” and stop.
- **Contracts:** If the change touches HTTP/JSON/gRPC contracts, trace **call sites** and **shared types** (including any central `types/` barrel) so UI and server stay aligned.
- **C# uncertainty:** If a **C#** change is a large or architectural refactor and patterns are unclear, **ask the user for confirmation** before applying (plan first, then execute after approval—same intent as a “Codex mode” planning pass).
