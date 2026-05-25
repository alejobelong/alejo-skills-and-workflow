# Alejo Skills And Workflow

This repository versions the Alejo Codex skill suite and the Sand Castle / Symphony workflow that turns Linear planning artifacts into autonomous Codex implementation runs.

Alejo owns the day-shift planning flow: questions, PRDs, prototypes, SADs, issue slicing, secrets guidance, and consistency propagation. Sand Castle / Symphony owns the night-shift execution flow: taking approved Linear vertical-slice issues and running fresh Codex implementation threads from the issue contracts.

## Contents

- `skills/`: Alejo-related Codex skills copied from `~/.codex/skills`.
- `WORKFLOW.md`: Sand Castle / Symphony workflow guide copied from `/Users/alejocasaspro/Belong3/Sand Castle/WORKFLOW.md`.

## How The Workflow Fits Together

1. `setup-alejo-skills` configures a repo for Linear-first Alejo usage.
2. Alejo planning skills publish canonical artifacts to Linear Project Documents: `PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, and `prototype.html`.
3. `alejo-issues` turns those artifacts into self-contained Linear vertical-slice issues.
4. `alejo-run` preflights approved issues and moves them into the Symphony execution lane.
5. Sand Castle / Symphony reads `WORKFLOW.md` plus each Linear issue contract to run autonomous Codex implementation, testing, repair, merge, and reporting.

Linear issues are for implementation slices and actionable follow-ups. Planning artifacts live at the Linear Project level, not as issues.

## Included Skills

- `alejo-consistency-propagation`
- `alejo-issues`
- `alejo-prd`
- `alejo-prototype`
- `alejo-questions`
- `alejo-run`
- `alejo-sad`
- `alejo-secrets`
- `setup-alejo-skills`
