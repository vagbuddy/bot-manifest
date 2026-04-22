---
name: terminal-execution
description: Runs go build/test, pytest, and npm run build to validate changes; reads logs and fixes failures until green within task scope. Use when implementing features, fixing bugs, or verifying compilation.
---

# Terminal and execution

- Run `go build`, `go test`, `go mod tidy` (after Go dependency edits), `pytest`, and `npm run build` when they materially validate the change.
- On failure, read the compiler or test output, fix the underlying code, and re-run until passing (stay within the requested task; escalate if the failure is environmental).
