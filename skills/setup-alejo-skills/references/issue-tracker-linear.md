# Linear Setup

Purpose: tell every Alejo skill where to publish planning artifacts, where to create implementation issues, and how `alejo-run` hands ready issues to Symphony.

## Required Setup

- Linear Project URL
- Linear team or project context
- Access method/tooling available in the repo

## Project Documents

Publish planning artifacts at the Linear Project level:

- `PRD`
- `SAD` or `SAT`
- `Q&A`
- `CONTEXT.md`
- `prototype.html`

## Linear Issues

Use Linear issues for vertical-slice implementation work and actionable follow-ups.

Each agent-ready issue needs:

- user-facing behavior
- compact context from the Project Documents
- acceptance criteria
- surface: `api`, `ui`, `cli`, or `mcp`
- preconditions and dependencies
- Doppler secret names only, if needed
- quality attributes and BDD budget
- slice-owned code organization
- readiness status

## Symphony Handoff

`alejo-run` reads ready Linear issues, preflights their run contract, asks for human approval, then moves approved issues into the Symphony lane.

Default status mapping:

- `ready-for-agent` -> `Ready for Agent`
- `symphony-execution` -> `Night Shift Queued`
- `in-symphony` -> `In Night Shift`
- done -> `Done`

Linear issue state is the source of truth for implementation readiness and Symphony handoff.
