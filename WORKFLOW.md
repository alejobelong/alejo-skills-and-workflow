# Symphony Workflow

Symphony runs autonomous implementation from Linear issue contracts. Linear owns execution state. Codex is the only coding agent.

## Entry

- Source: Linear implementation issues configured in `docs/agents/issue-tracker.md`.
- Ready state: mapped `ready-for-agent` on vertical-slice implementation issues only.
- Execution lane: mapped `symphony-execution`.
- Approval: `alejo-run` must preflight selected issues and receive explicit human approval before moving issues into the execution lane.
- PRDs live in Linear Projects, not runnable issues, and are never candidates for Symphony.

## Issue Contract

Each issue in the execution lane must contain:

- Title.
- User-facing behavior.
- Necessary compact context from PRD/SAD/Q&A/`CONTEXT.md`/prototype evidence.
- Acceptance criteria.
- Verification surface: `api`, `ui`, `cli`, or `mcp`.
- Preconditions: required state, data, config, user role, or `None`.
- Dependencies or blockers.
- Required Doppler secret refs by name only, or `None`.
- Slice-relevant quality attributes.
- BDD iteration budget.
- Architectural constraints needed for implementation.
- Slice-owned code organization.
- Readiness label/status proving the issue is approved and ready for autonomous execution.

## Secrets

- Doppler is the only secret provider.
- Issues and artifacts must reference secret names only, never values.
- If `alejo-secrets` confirms, renames, adds, or removes any required secret after issues exist, run `alejo-consistency-propagation` or update the affected Linear issues before `alejo-run`.
- `alejo-run` must fail preflight when issue secret refs do not match the confirmed Doppler names needed by the slice.

## Per-Issue Threads

Fresh Codex threads share artifacts, not transcript context.

- BDD generator reads issue only; writes `scenario.json`.
- Test writer reads issue + `scenario.json` + code; writes failing test only.
- Implementer reads issue + `scenario.json` + code + failing test; writes implementation only.
- Refactor reads issue + `scenario.json` + code + green tests; writes cleanup only.
- Synthetic tester reads issue + `scenario.json` + code; exercises the real surface; writes `recommendation.json` or pass verdict.

## Boundaries

- Do not create or consume Alejo plan files.
- Do not choose agents or models per issue.
- Do not use non-Codex coding agents.
- Do not read PRD/SAD/Q&A/prototype documents during night shift to discover requirements; the issue is the canonical compact context packet.
