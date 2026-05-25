---
name: alejo-run
description: Human approval and preflight launcher for autonomous implementation from ready Linear issues through Symphony. Use when the user asks to run approved Alejo issues, start the autonomous build, hand issues to Symphony, or launch AFK execution. Does not create plan files, choose agents/models, or schedule slices.
---

# Alejo Run

Approve and hand ready Linear issues to Symphony. Linear owns issue state. Symphony owns orchestration from repo `WORKFLOW.md`. Codex is the only coding agent.

## Process

1. Read `AGENTS.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/alejo-workflow.md`, and repo `WORKFLOW.md`.
2. Select candidate Linear implementation issues from the user's refs, or from the mapped `ready-for-agent` queue if the user asks to run all ready issues. Exclude PRD projects, SAD follow-ups, planning records, and anything that is not a vertical-slice implementation issue.
3. Preflight each issue:
   - Open Linear issue with mapped `ready-for-agent` state/label and an issue-body readiness field that agrees with the current Linear state.
   - Not `needs-info`, `needs-triage`, `ready-for-human`, `hitl`, blocked, or contradictory.
   - Issue body is the compact slice contract: title, user-facing behavior, necessary context, acceptance criteria, surface, preconditions, dependencies/blockers, secrets refs, quality attributes, BDD budget, architectural constraints, readiness label/status, and code organization.
   - Preconditions are explicit and satisfiable, or clearly `None`.
   - Dependencies are done or included in the same approved run.
   - Secret names are present without values; verify with safe Doppler name-only checks when possible, and stop if confirmed secret names changed without being propagated back to the issue.
   - `WORKFLOW.md` defines the Symphony execution flow and lane mapping is known.
4. Present a short approval table: issue id/title, surface, preconditions, dependencies, secrets refs, BDD budget, readiness state, preflight verdict, and target Symphony lane.
5. Ask for explicit human approval before changing Linear.
6. On approval, move or label the selected Linear issues into the configured Symphony execution lane. Do not create `plan.md`, choose agents/models, schedule slices, or launch non-Codex providers.

## Thread Contract

Symphony should hydrate fresh Codex threads with artifacts, not transcript history:

- BDD generator reads issue only; writes `scenario.json`.
- Test writer reads issue + `scenario.json` + code; writes failing test only.
- Implementer reads issue + `scenario.json` + code + failing test; writes implementation only.
- Refactor reads issue + `scenario.json` + code + green tests; writes cleanup only.
- Synthetic tester reads issue + `scenario.json` + code; exercises the real surface; writes `recommendation.json` or pass verdict.

## Output Rules

- Do not write a plan artifact.
- Do not choose models, agents, branches, concurrency, or slice order.
- Do not run Symphony unless the repo documents an explicit launch command and the user separately confirms launch.
- Stop and ask if Linear workspace/team/project, execution lane mapping, or `WORKFLOW.md` is missing.
