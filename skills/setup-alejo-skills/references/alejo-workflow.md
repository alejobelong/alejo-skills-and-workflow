# Alejo Workflow

Purpose: connect the full Alejo planning stack to Symphony implementation.

## Planning

1. `alejo-questions` resolves domain language and Q&A.
2. `alejo-prd` publishes `PRD` to the Linear Project.
3. `alejo-prototype` publishes `prototype.html` when UI evidence helps.
4. `alejo-sad` publishes `SAD` or `SAT`.
5. `alejo-issues` creates vertical-slice Linear issues.
6. `alejo-secrets` gives Doppler setup steps when needed.
7. `alejo-consistency-propagation` keeps Project Documents and issues aligned.

## Implementation

`alejo-run` is the bridge to Symphony:

1. Read `WORKFLOW.md`, Linear setup docs, and ready Linear issues.
2. Preflight each issue's run contract.
3. Ask for human approval.
4. Move approved issues to the Symphony execution lane.

Symphony then runs fresh Codex threads from the issue contract and repo `WORKFLOW.md`.

## Artifact Homes

- Linear Project Documents: `PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, `prototype.html`
- Linear issues: vertical slices and actionable follow-ups
- Repo docs: `AGENTS.md`, `docs/agents/*`, `WORKFLOW.md`, ADRs, and optional local `CONTEXT.md`
- Doppler: secret values
