---
name: alejo-run
description: Relentless Symphony launcher for Alejo Linear implementation issues, including safe Doppler secret recovery via Alejo Secrets. Use when the user asks to run, build, execute, orchestrate, or keep working through ready Alejo issues until they are production-grade, verified on real surfaces, and free of mocks, fakes, stubs, skipped tests, placeholders, or half-working behavior. Does not create plan files, choose agents/models, or schedule slices.
---

# Alejo Run

Run approved Linear implementation issues through Symphony until they are genuinely production-grade. Linear owns issue state. Symphony owns orchestration from repo `WORKFLOW.md`. Codex is the only coding agent.

## Goal

The goal is not to move issues to another lane. The goal is to keep working relentlessly until every selected issue is completely working, production-grade, and verified through its real `api`, `ui`, `cli`, or `mcp` surface.

Done means:

- Acceptance criteria are satisfied by real behavior.
- Tests pass without skipped, disabled, fake, or placeholder paths.
- Provider integrations use real production code paths, official sandbox/test accounts, or configured local production services.
- Storage, routes, UI, CLI, MCP, jobs, and provider adapters are wired end to end.
- Synthetic verification exercises the real surface and returns a pass verdict.
- `alejo-review` reports the selected issue scope as ready, with no P0/P1/P2 gaps tied to the implemented behavior.
- No mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, unwired UI, or half-working behavior remain.

If verification fails, keep the repair loop going within the issue's BDD budget. If the budget is exhausted or an unsafe blocker appears, leave the issue out of the done lane and report the exact blocker instead of calling it complete.

## Process

### 1. Read Operating Context

Read `AGENTS.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/alejo-workflow.md`, and repo `WORKFLOW.md`.

Stop and ask if Linear workspace/team/project, execution lane mapping, issue tracker docs, or `WORKFLOW.md` are missing.

### 2. Select Issues

Select candidate Linear implementation issues from the user's refs, or from the mapped `ready-for-agent` queue if the user asks to run all ready issues.

Exclude PRD projects, SAD/SAT follow-ups, Q&A logs, CONTEXT.xml work, prototype XML/reports, planning records, and anything that is not a vertical-slice implementation issue.

### 3. Preflight Issues

For each candidate issue, verify:

- Linear state/label matches `ready-for-agent`.
- Issue body readiness agrees with Linear state.
- It is not `needs-info`, `needs-triage`, `ready-for-human`, `hitl`, blocked, or contradictory.
- Body is a compact XML slice contract with title, behavior, necessary context, acceptance criteria, surface, preconditions, dependencies, providers, secrets refs, quality attributes, BDD budget, architectural constraints, readiness status, production constraints, and code organization.
- Preconditions are explicit and satisfiable, or clearly `None`.
- Dependencies are done or included in the same approved run.
- `WORKFLOW.md` defines the Symphony execution flow and lane mapping is known.

### 4. Recover Missing Secrets Safely

Collect all Doppler secret names from each issue's `secrets_refs`, provider credential refs, preconditions, and acceptance criteria. Check availability with safe name-only commands only:

```sh
command -v doppler
doppler --version
doppler secrets --only-names
```

If any required secret name is missing, use `alejo-secrets` to inventory the missing provider credentials and decide whether each one is safe to add automatically.

Safe automatic additions are limited to:

- A new high-entropy application secret that Codex can generate locally, such as app, session, cookie, CSRF, JWT signing, encryption, or webhook test secrets.
- A value already present in the current process environment under the exact required name and transferable to Doppler without printing it.
- A non-secret public config value that the issue explicitly requires in Doppler and that can be verified from repo docs, provider docs, or the issue body.

Use non-printing commands only. Examples:

```sh
openssl rand -base64 48 | doppler secrets set SECRET_NAME --silent
test -n "${SECRET_NAME:-}" && printenv SECRET_NAME | doppler secrets set SECRET_NAME --silent
printf '%s' 'public-config-value' | doppler secrets set SECRET_NAME --silent
```

Never print, log, paste, summarize, or echo secret values. Never put a real secret value in a command argument, issue body, file, or chat message.

Unsafe or not-easy secrets include provider API keys, OAuth client secrets, database passwords, cloud credentials, service account JSON, webhook signing secrets from a real provider dashboard, billing-gated keys, account-owned tokens, or any credential whose value Codex would need to guess, retrieve from a private dashboard, read from files, or ask the user to paste into chat. For these, stop before moving issues and output the `alejo-secrets` Doppler setup guide instead.

After any safe automatic addition, run `doppler secrets --only-names` again. Stop if required secret names are still missing or if confirmed names changed without being propagated back to the issue.

### 5. Present Approval Table

Show a short approval table with issue id/title, surface, preconditions, dependencies, providers, secrets refs, BDD budget, readiness state, secret verdict, preflight verdict, and target Symphony lane.

Ask for explicit human approval before changing Linear.

### 6. Hand Off To Symphony

On approval, move or label the selected Linear issues into the configured Symphony execution lane.

Do not create `plan.md`, choose agents/models, schedule slices, launch non-Codex providers, or run Symphony unless the repo documents an explicit launch command and the user separately confirms launch.

### 7. Drive The Production Loop

When launch is explicitly confirmed and the repo documents how to run Symphony, keep working until the selected issues are done or truly blocked:

- Start or resume the documented Symphony run.
- Watch issue progress, test output, implementation results, and synthetic tester verdicts.
- Feed failed verification back into the next BDD repair iteration.
- At the end of each cycle, run `alejo-review` against the repo, planning artifacts, and selected Linear issues.
- Read the Alejo Review report as the final production gate for that cycle.
- Feed every relevant P0/P1/P2 review gap back into the next repair iteration until the report is clean for the selected issue scope.
- Keep the issue in the execution lane while repairs are still available.
- Move or report an issue as complete only after real-surface verification passes.
- Move or report the selected run as done only after both synthetic verification and Alejo Review pass cleanly.
- Stop only for missing unsafe secrets, missing human decisions, exhausted BDD budget, unavailable required external systems, repo/workflow configuration gaps, or review gaps that are outside the approved issue scope.
- Report blockers with the issue id, failed surface, exact failing acceptance criterion, attempted repairs, and next human action.

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
- Do not expose secret values.
- Do not advance issues with missing unsafe secrets.
- Do not mark issues complete because code was written; mark them complete only after production-grade real-surface verification and Alejo Review both pass.
- Do not ignore Alejo Review findings; iterate on relevant P0/P1/P2 gaps until the report is clean or a real blocker is reached.
- Do not accept mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, unwired UI, or half-working behavior.
- Do not run Symphony unless the repo documents an explicit launch command and the user separately confirms launch.
