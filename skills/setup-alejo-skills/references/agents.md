# AGENTS.md

Use this shape for the repo root `AGENTS.md`. Replace every bracketed value before writing. If a non-required value is unknown, omit that line instead of writing a placeholder.

```md
# <Project Name>

This repo uses the Alejo skill suite.

## Alejo Setup

- GitHub: <repo URL>
- Linear Project: <project name> - <project URL>
- Linear team: <team name> (<team key>)
- Planning artifacts live in Linear Project Documents: `Q&A`, `CONTEXT.md`, `PRD`, `prototype.html`, `SAD`/`SAT`.
- Linear issues are only for vertical-slice implementation and actionable follow-ups.
- `WORKFLOW.md` is the Symphony execution contract for approved issues.
- Secret values belong in Doppler, never in repo files or Linear issue bodies.

## Skill Flow

1. `$setup-alejo-skills`: rerun only when Git, Linear, or setup docs are missing.
2. `$alejo-questions`: clarify domain language, product questions, and trade-offs.
3. `$alejo-prd`: publish product intent and user value to Linear.
4. `$alejo-prototype`: publish UI evidence or a throwaway HTML prototype when useful.
5. `$alejo-sad`: publish architecture for non-trivial implementation.
6. `$alejo-issues`: create behavior-first vertical-slice Linear issues.
7. `$alejo-secrets`: provide Doppler setup steps for required secrets.
8. `$alejo-consistency-propagation`: reconcile changed artifacts and issue contracts.
9. `$alejo-run`: preflight ready issues and hand approved work to Symphony.

## Repo References

- `docs/agents/issue-tracker.md`: Linear Project, Project Documents, issue contract, Symphony handoff.
- `docs/agents/triage-labels.md`: Linear statuses and issue labels.
- `docs/agents/domain.md`: glossary, context map, and ADR conventions.
- `docs/agents/alejo-workflow.md`: planning-to-Symphony workflow.
- `WORKFLOW.md`: Symphony execution workflow.
```
