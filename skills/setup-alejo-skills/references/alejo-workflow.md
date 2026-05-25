# Alejo Workflow

This repo is configured for the Alejo skill suite.

## Day Shift Skill Flow

Day shift skills are human-facing planning, clarification, documentation, and approval skills. They run before or around implementation work; they are not injected into coding or testing agents inside Sand Castle.

1. `alejo-questions` stress-tests plans, updates domain language/ADRs, and publishes `Q&A` plus `CONTEXT.md` to the Linear Project.
2. `alejo-prd` turns conversation and repo context into a product-focused PRD and publishes it to the Linear Project document named `PRD`, not an issue.
3. `alejo-prototype` optionally studies reference URLs/images, writes detailed design analysis, builds a disposable HTML prototype, and publishes `prototype.html` to the Linear Project.
4. `alejo-sad` creates a compact Solution Architecture Document with Mermaid diagrams, using prototype evidence when available, and publishes it to the Linear Project document named `SAD` by default.
5. `alejo-issues` turns PRD + prototype + SAD context into the thinnest possible vertical-slice issues.
6. `alejo-secrets` guides the user through required Doppler secrets when slices need credentials, APIs, tokens, or env vars.
7. `alejo-run` preflights ready Linear issues, asks for human approval, and moves approved issues into the Symphony execution lane.

## Day Shift Anytime Skills

- `alejo-consistency-propagation` can be run at any point during the day shift after any Context, Questions, PRD project, prototype, SAD, ADR, issue, secret-name, `WORKFLOW.md`, or scope change. It finds differences, asks the human one decision at a time, and applies only approved consistency updates.

## Night Shift Boundary

Night shift is the autonomous Symphony execution phase after day-shift planning is approved.

- Current night shift entry point: Linear issues moved into the configured Symphony execution lane by `alejo-run`.
- Current night shift input: self-contained Linear issue contracts plus repo `WORKFLOW.md`.
- Current night shift behavior: Symphony creates one isolated workspace per issue and launches Codex through app-server for BDD generation, TDD mini-cycles, synthetic testing, repair loops, merge, issue updates, and reporting.
- Future night-shift skills will be separate skills injected into Symphony's coding, BDD, synthetic testing, or merge threads. Those skills are not defined yet and will be designed later.

Do not treat day-shift skills, including `alejo-consistency-propagation`, as night-shift agent-injected skills unless a future workflow explicitly adapts them.

## Expected Software Workflow

For new software work, use this path:

1. Required once per repo: `setup-alejo-skills`.
2. Usually required for new product work: `alejo-questions` to resolve domain language, decisions, ADRs, and Q&A, then publish `Q&A` and `CONTEXT.md` to the Linear Project.
3. Required for agent-ready product work: `alejo-prd` to publish product intent to the Linear Project document named `PRD`.
4. Optional after PRD, before SAD: `alejo-prototype` when reference-driven UI evidence or a small disposable experiment can reduce uncertainty, then publish `prototype.html` to the Linear Project.
5. Required for non-trivial implementation: `alejo-sad` to turn requirements and prototype evidence into architecture, then publish the Linear Project document named `SAD` or `SAT` if the repo already uses that term.
6. Required before implementation agents: `alejo-issues` to create behavior-first vertical slices.
7. Conditional: `alejo-secrets` when slices need credentials, APIs, tokens, or env vars; it outputs a Doppler-only terminal guide and never writes secret values.
8. Anytime during day shift: `alejo-consistency-propagation` after any artifact changes, contradictions, removals, secret-name changes, or scope drift.
9. Optional autonomous execution path: `alejo-run` after ready Linear issues; it preflights issue contracts, asks for approval, then moves approved issues into Symphony's execution lane.

If `alejo-secrets` confirms, renames, adds, or removes required Doppler secret names after issues exist, run `alejo-consistency-propagation` or update the affected Linear issues before `alejo-run`.

If the user will implement manually, stop after approved issues plus any needed Doppler setup. If the user wants autonomous execution, continue through Alejo Run. Do not create a separate plan artifact.

## Artifact Locations

- Canonical planning artifacts: Linear Project Documents/Resources for `PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, and `prototype.html`.
- Domain glossary: `CONTEXT.md` or paths in `CONTEXT-MAP.md` as working copies, synced to the Linear Project document named `CONTEXT.md`.
- ADRs: `docs/adr/` and context-local `docs/adr/`.
- Alejo Questions logs: Linear Project document `Q&A`; local `docs/questions/YYYY-MM-DD-<topic-slug>.md` may be used as a working copy only when useful.
- Prototype reports and HTML: Linear Project document `prototype.html`, with local `.scratch/prototypes/YYYY-MM-DD-<topic>/` used for disposable browser verification.
- SADs: Linear Project document `SAD` by default, or `SAT` only when the repo already uses that title.
- Secrets: Doppler only. Secret names live in issue run contracts; `alejo-secrets` outputs setup commands in conversation and does not write secret values.
- Symphony workflow: `WORKFLOW.md`.
- Autonomous run state and reports: Linear/Symphony, as configured by `WORKFLOW.md`.
- PRDs: Linear Project document `PRD` configured in `docs/agents/issue-tracker.md`.
- Implementation slices: Linear issues configured in `docs/agents/issue-tracker.md`.

## Vertical Slice Rule

A vertical slice is the smallest complete behavior through its interface, backend logic, data/storage, integrations, and verification. Do not create horizontal layer/module tickets.
