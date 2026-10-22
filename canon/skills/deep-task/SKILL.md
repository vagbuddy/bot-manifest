---
name: deep-task
description: >-
  Refines and deepens prompts or tasks using first principles (depth over breadth).
  Trigger when the user asks to deepen a task/prompt ("make this deeper not bigger",
  "deep task", "углуби задачу", "first-principles refinement"), or when an exploratory
  engineering inquiry is underspecified but seeks deep investigation.
---

# Deep Task (First-Principles Task Refinement)

When exploring complex problems, resist the failure mode of expanding *broadly* (generating generic checklists, superficial recommendations, or boilerplate scaffolding). Instead, anchor the inquiry *deeply* through the 4-part Depth Protocol before rewriting the prompt or executing.

## 4-Part Depth Protocol

1. **Unspoken Professional Practice (Скрытый стандарт сеньора):**
   - Identify what an elite practitioner in this specific domain would examine or guarantee that was not explicitly requested (e.g. concurrency races, lock contention, memory allocation hot spots, cache-line bouncing, failure recovery invariants).
2. **Raw Ground Truth (Первоисточник данных / сырой материал):**
   - Name the rawest, unmediated starting data or artifacts to inspect instead of pre-digested summaries, synthetic mocks, or high-level abstractions (e.g. `pprof` CPU/heap profiles, raw database transaction logs, kernel tracepoints, binary packets, AST dumps, strict RFC specifications).
3. **Specific Tooling & Methods (Точечный профессиональный инструментарий):**
   - Specify the exact diagnostic, profiling, or analytical tools and flags required (e.g. `EXPLAIN (ANALYZE, BUFFERS)`, `strace -c`, `perf record`, `dlv`, `pytest -vv -s --durations=0`, strict type/borrow checkers).
4. **Independent External Falsifiability (Внешний объективный критерий истинности):**
   - Define what objective external evidence—independent of the agent or user's subjective impression—will demonstrate that the result is correct (e.g. p99 latency target under deterministic load, reproducible stress test passing without data races, database consistency invariant verified via SQL assertion).

## Output & Prompt Reformulation

Conclude by synthesizing steps (1)–(4) into a rewritten, precise, first-principles prompt:
- **Title:** Narrow, unambiguous problem definition.
- **Inputs & Raw Artifacts:** Exact logs, traces, or schemas needed.
- **Target Invariant / Exit Metric:** What constitutes success.
- **Actionable Execution Plan:** Direct instructions asking for exactly that deep investigation.
