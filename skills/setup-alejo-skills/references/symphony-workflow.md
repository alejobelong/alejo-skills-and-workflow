# Symphony Workflow

Purpose: define how Symphony runs approved Linear issues with fresh Codex threads.

## Entry

- Source: Linear vertical-slice issues from `docs/agents/issue-tracker.md`.
- Ready status: `Ready for Agent`.
- Execution lane: `Night Shift Queued`.
- Launcher: `alejo-run`.
- Coding agent: Codex only.

## Issue Contract

Each issue must include:

- user-facing behavior
- compact context from Linear Project Documents
- acceptance criteria
- surface: `api`, `ui`, `cli`, or `mcp`
- preconditions and dependencies
- Doppler secret names only, if needed
- quality attributes and BDD budget
- slice-owned code organization

## Thread Flow

Symphony starts fresh Codex threads per issue:

1. BDD generator writes `scenario.json`.
2. Test writer writes the failing test.
3. Implementer writes the implementation.
4. Refactor cleans up after green tests.
5. Synthetic tester exercises the real surface and reports pass/fail.

## Boundaries

- Linear owns issue state.
- Linear Project Documents own planning artifacts.
- Issues own implementation context.
- Doppler owns secret values.
- `alejo-run` moves approved issues into the Symphony lane.
