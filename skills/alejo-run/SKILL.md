---
name: alejo-run
description: Relentless Symphony launcher for Alejo Linear implementation issues, including safe Doppler secret recovery via Alejo Secrets. Use when the user asks to run, build, execute, orchestrate, or keep working through ready Alejo issues until they are production-grade, verified on real surfaces, and free of mocks, fakes, stubs, skipped tests, placeholders, or half-working behavior. Does not create plan files, choose agents/models, or schedule slices.
---

# Alejo Run

Run ready Linear implementation issues through Symphony until they are genuinely production-grade. Linear owns issue state. Repo `WORKFLOW.md` is the official Symphony contract; the Linear Project Document `WORKFLOW.md` is only its mirror for Alejo discovery. Codex is the only coding agent.

Alejo Run is autonomous: do not ask for approval, permission, confirmation, or clarifying questions. When the existing preflight and workflow gates pass, proceed; when they do not, stop and report the blocker.

## Codex Goal Mode

When Codex Goal mode is enabled, treat the active goal as incomplete until every selected issue is production-grade, verified through the real surface, reviewed clean by a fresh `alejo-review` subagent, and moved or reported correctly in Linear. Do not mark the goal complete for lane movement, code changes, green unit tests alone, or partial handoff.

## Goal

The goal is not to move issues to another lane. The goal is to keep working relentlessly until every selected issue is completely working, production-grade, and verified through its real `api`, `ui`, `cli`, or `mcp` surface.

Done means:

- Acceptance criteria are satisfied by real behavior.
- Tests pass without skipped, disabled, fake, or placeholder paths.
- Provider integrations use real production code paths, official sandbox/test accounts, or configured local production services.
- Storage, routes, UI, CLI, MCP, jobs, and provider adapters are wired end to end.
- Synthetic verification exercises the real surface and returns a pass verdict.
- UI or browser-reachable behavior is verified through Playwright in a real browser by performing the end-user workflow against the running app.
- A fresh review subagent running `alejo-review` reports the selected issue scope as ready, with no P0/P1/P2 gaps tied to the implemented behavior.
- No mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, unwired UI, or half-working behavior remain.

If verification fails, keep the repair loop going within the issue's BDD budget. If the budget is exhausted or an unsafe blocker appears, leave the issue out of the done lane and report the exact blocker instead of calling it complete.

## Process

### 1. Read Operating Context

Read Linear Project Documents `AGENTS.md`, `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, repo `WORKFLOW.md`, and the Linear `WORKFLOW.md` mirror when available. Treat repo `WORKFLOW.md` as the canonical Symphony YAML front matter, prompt template, lane, runtime, and verification contract.

Stop and report the blocker if Linear workspace/team/project, execution lane mapping, issue tracker docs, repo `WORKFLOW.md`, or the Linear mirror is missing or conflicting when configured.

### 2. Select Issues

Select candidate Linear implementation issues from the user's refs, or from the mapped `ready-for-agent` queue if the user asks to run all ready issues.

Exclude PRD projects, SAD/SAT follow-ups, Q&A logs, CONTEXT.xml work, prototype XML/reports, planning records, and anything that is not a vertical-slice implementation issue.

### 3. Preflight Issues

For each candidate issue, verify:

- Linear state/label matches `ready-for-agent`.
- Issue body readiness agrees with Linear state.
- It is not `needs-info`, `needs-triage`, `ready-for-human`, `hitl`, blocked, or contradictory.
- Body is a compact XML slice contract with title, behavior, necessary context, acceptance criteria, surface, preconditions, dependencies, providers, secrets refs, quality attributes, BDD budget, architectural constraints, readiness status, production constraints, and code organization.
- Interactive, UI, chat, toolbar, assistant, or managed-agent issues define representative user personas, user objectives, actual prompts/inputs/actions, expected provider/backend evidence, wait or SLA expectations, and user-visible failure modes.
- Chat or managed-agent issues require Playwright verification against the running app and cannot rely only on trivial greetings, SDK config fetches, direct adapter probes, mocked responses, canned samples, local echoes, or prompts that avoid the promised provider capability.
- Preconditions are explicit and satisfiable, or clearly `None`.
- Dependencies are done or included in the same selected run.
- Repo `WORKFLOW.md` defines the Symphony execution flow and lane mapping, and the Linear mirror does not conflict.

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

### 5. Symphony Runtime Preflight

Use the official Symphony `WORKFLOW.md` front matter, prompt body, and repo scripts to verify the execution runtime:

- Use `doppler run -- <command>` when the selected issue needs secrets or environment-backed config.
- Never run commands that print secret values or dump full environments.
- Verify `tracker.kind`, `tracker.api_key`, `tracker.project_slug`, `tracker.active_states`, `tracker.terminal_states`, `workspace.root`, `agent`, and `codex.command`.
- Confirm active states include the configured Symphony execution lane and running lane.
- Resolve the documented test, synthetic verification, artifact, and review gates from the prompt body, issue contract, and repo instructions.
- Run repo-declared tests for the selected `api`, `ui`, `cli`, or `mcp` surface.
- Verify Symphony status, artifacts, logs, handoff evidence, and synthetic tester verdicts from the documented artifact sink.
- Require Playwright for UI or browser-reachable behavior.
- If the slice touches jobs, queues, workers, schedulers, or async flows, verify the repo-declared command, state transition, failure behavior, and observable output.

Stop if a required Symphony/runtime command is missing, unsafe to run, or impossible to verify from repo instructions and `WORKFLOW.md`.

### 6. Present Preflight Table

Show a short preflight table with issue id/title, surface, preconditions, dependencies, providers, secrets refs, BDD budget, Symphony/runtime verdict when applicable, readiness state, secret verdict, preflight verdict, and target Symphony lane.

Do not ask for human approval before changing Linear. Passing issues move forward automatically.

### 7. Hand Off To Symphony

Move or label the selected passing Linear issues into the configured Symphony execution lane.

Do not create `plan.md`, choose agents/models, schedule slices, or launch non-Codex providers. If the repo documents an explicit Symphony launch command, run it without asking for separate confirmation.

### 8. Drive The Production Loop

When the repo documents how to run Symphony, keep working until the selected issues are done or truly blocked:

- Start or resume the documented Symphony run.
- Watch issue progress, test output, implementation results, and synthetic tester verdicts.
- Feed failed verification back into the next BDD repair iteration.
- For every UI or browser-reachable surface, require Playwright to open the running app in a browser, navigate to the relevant page, use the same controls an end user would use, and assert the visible result plus any observable persistence, network, or provider-backed effect needed by the acceptance criteria.
- For chat or managed-agent functionality, Playwright verification must locate the chat UI, adopt the scenario's user persona, begin a real conversation toward the user's objective, allow natural follow-up where needed, wait for the actual backend/managed-agent response within the intended product window, and verify the response content and supporting evidence prove it is not a canned, mocked, stubbed, or disconnected answer.
- If the product claims current-events, web lookup, search, browsing, external knowledge, or tool-backed answering, require at least one representative prompt that needs that capability. If unsupported, the verified behavior must be a clear unsupported-capability response rather than a hang, generic timeout, or unrelated fallback.
- At the end of each cycle, spawn a fresh subagent whose only job is to run `alejo-review` against the repo, planning artifacts, and selected Linear issues.
- Do not run the review inline in the same agent that drove the implementation cycle. If subagents are unavailable, stop and report that the review gate cannot run.
- Read the Alejo Review report as the final production gate for that cycle.
- Feed every relevant P0/P1/P2 review gap back into the next repair iteration until the report is clean for the selected issue scope.
- Keep the issue in the execution lane while repairs are still available.
- Move or report an issue as complete only after real-surface verification passes.
- Move or report the selected run as done only after both synthetic verification and Alejo Review pass cleanly.
- Stop only for missing unsafe secrets, missing non-derivable decisions, exhausted BDD budget, unavailable required external systems, repo/workflow configuration gaps, or review gaps that are outside the selected issue scope.
- Report blockers with the issue id, failed surface, exact failing acceptance criterion, attempted repairs, and next required action.

## Thread Contract

Use repo `WORKFLOW.md` as the canonical Symphony contract. Do not restate, override, or invent execution roles outside that contract.

Alejo Run adds only these execution gates:

- BDD scenarios must include 3 to 5 behaviours with persona, objective, prompts/actions, wait expectation, failure mode, and verification evidence.
- Synthetic verification must exercise the real surface and produce a pass verdict or `recommendation.json`.
- The final review must run in a fresh subagent using `alejo-review`; inline review is not valid.

## Output Rules

- Do not write a plan artifact.
- Do not choose models, agents, branches, concurrency, or slice order.
- Do not override the front matter, prompt body, or artifact contract in `WORKFLOW.md`.
- Do not ask for approvals, permissions, confirmations, or clarifying questions.
- Do not expose secret values.
- Do not advance issues with missing unsafe secrets.
- Do not mark issues complete because code was written; mark them complete only after production-grade real-surface verification and Alejo Review both pass.
- Do not accept UI/browser behavior as verified without a Playwright browser run that performs the real end-user flow against the running app.
- Do not run Alejo Review inline; always run it in its own fresh subagent.
- Do not ignore Alejo Review findings; iterate on relevant P0/P1/P2 gaps until the report is clean or a real blocker is reached.
- Do not accept mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, unwired UI, or half-working behavior.
- Do not wait for a separate launch confirmation when the repo documents an explicit Symphony launch command.
