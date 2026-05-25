# Triage Labels

Alejo skills speak in canonical roles. Map those roles to the exact tracker labels, workflow statuses, or local status values used by this repo.

## Linear Default

For Linear, prefer workflow statuses for readiness and execution lanes. Use labels only for stable issue classification.

| Canonical role | Tracker label/status | Meaning |
|---|---|---|
| `needs-triage` | `Needs Triage` workflow status | Maintainer needs to evaluate |
| `needs-info` | `Needs Info` workflow status | Waiting on the reporter or product owner |
| `ready-for-human` | `Ready for Human` workflow status | Needs human implementation or judgment |
| `ready-for-agent` | `Ready for Agent` workflow status | Fully specified and AFK-ready |
| `symphony-execution` | `Night Shift Queued` workflow status | Approved for Symphony autonomous execution |
| `in-symphony` | `In Night Shift` workflow status | Currently running through autonomous execution |
| `wontfix` | `Won't Fix` or `Canceled` workflow status | Will not be actioned |

Recommended Linear issue labels:

| Label | Meaning |
|---|---|---|
| `vertical-slice` | Thin end-to-end implementation issue |
| `hitl` | Human-in-the-loop issue |
| `sad-follow-up` | Actionable architecture follow-up issue, not the SAD itself |
| `surface:cli` | CLI surface slice |
| `surface:api` | API surface slice |
| `surface:ui` | UI surface slice |
| `surface:mcp` | MCP surface slice |
| `secrets-required` | Issue references required runtime secrets by name |

Do not use `prd` or `sad` as issue labels when PRDs/SADs live as Linear Projects, project docs, or repo docs. PRDs and SADs are artifacts; Linear issues are vertical slices or actionable follow-ups.

## Non-Linear Default

If the tracker cannot model workflow statuses, use labels or local status values with the same canonical roles:

- `needs-triage`
- `needs-info`
- `ready-for-human`
- `ready-for-agent`
- `symphony-execution`
- `wontfix`

When a skill mentions a canonical role, use the mapped tracker value.
