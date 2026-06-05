---
name: alejo-run-v2
description: Compact Alejo Run v2 workflow for autonomously supervising ready Linear vertical-slice issues through the repo WORKFLOW.md Symphony contract, Codex Goal mode, Doppler-safe secret recovery with alejo-secrets-v2, TDD handoff evidence, BDD real-surface verification, and a clean alejo-review subagent gate. Use when ready Alejo issues should be driven until production-grade and left in Ready for Human without mocks, approvals, Done transitions, or human-in-the-loop pauses.
---

# Alejo Run v2

Autonomously drive ready Linear implementation issues through Symphony and Alejo verification. Symphony is OpenAI's issue runner; repo `WORKFLOW.md` is its contract. Alejo Run v2 does not rewrite `WORKFLOW.md`: it uses the contract, launches or resumes the run, verifies the handoff, repairs failures, and leaves clean work in `Ready for Human`.

Only a human moves issues to `Done`. Do not ask for approval, permission, confirmation, or clarifying questions. Proceed when the gates pass; stop only for true blockers.

## Goal Mode

When Codex Goal mode is enabled, the goal is incomplete until every selected issue is:

- queued and run through repo `WORKFLOW.md`;
- covered by a self-contained XML issue contract and safe Doppler secret refs;
- supported by TDD evidence when `WORKFLOW.md` or repo practice requires test-first implementation;
- verified by BDD real-surface checks through its `api`, `ui`, `cli`, or `mcp` surface;
- free of mocks, fake providers, stubbed SDK responses, placeholders, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, and unwired UI;
- reviewed clean by a fresh `alejo-review` subagent with no relevant P0/P1/P2 gaps;
- left in `Ready for Human` with concise evidence, or reported with an exact blocker.

Do not mark the goal complete for lane movement, code changes, green unit tests alone, partial handoff, or a transition to `Done`. Never move an issue to `Done`.

## Sources

Use canonical Linear and repo evidence:

1. `AGENTS.md`: source-of-truth map.
2. `issue-tracker.md` and `triage-labels.md`: Linear project, states, labels, and lane mapping.
3. `alejo-workflow.md`: Alejo planning-to-implementation lifecycle.
4. Repo `WORKFLOW.md` plus its Linear mirror: Symphony YAML front matter, per-issue prompt template, execution states, verification artifacts, and boundaries.
5. Selected Linear vertical-slice issues and comments.
6. Current repo: code, tests, env/config, providers, migrations, routes, workers, deployment, CI, and documented run commands.
7. Doppler name-only checks and `alejo-secrets-v2` results.

Do not use local planning mirrors as canonical sources.

## Process

1. Resolve the Linear Project, team, issue states/labels, selected issues, repo `WORKFLOW.md`, and its Linear mirror when available. Stop if any required destination, lane, or contract is missing or if the repo file and Linear mirror conflict.
2. Select issues from explicit refs, or from the mapped `Ready for Agent` queue when the user asks to run ready work. Exclude planning documents, PRD/SAD/prototype/Q&A/CONTEXT work, and non-vertical-slice issues.
3. Preflight each issue against `WORKFLOW.md`:
   - readiness state/label is `Ready for Agent`;
   - XML run contract is present and self-contained;
   - surface, acceptance criteria, preconditions, dependencies, providers, Doppler names, quality attributes, BDD budget, production constraints, code organization, representative prompts/actions, Playwright expectations, provider evidence, latency/timeout expectations, and review evidence are explicit;
   - dependencies are done or included in the same selected run;
   - no `needs-info`, `needs-triage`, `ready-for-human`, `hitl`, blocked, contradictory, or planning-only work is included.
4. Recover secrets safely:
   - collect required Doppler names from issue contracts, provider refs, preconditions, and acceptance criteria;
   - run only name-safe checks: `command -v doppler`, `doppler --version`, `doppler secrets --only-names`;
   - if names are missing, use `alejo-secrets-v2`;
   - automatically add only app-owned generated values, exact current-env values, recoverable official-tool values, verified-created provider resources, or public config that can be written without exposing values;
   - stop before lane movement for human-required or unsafe secrets and report the `alejo-secrets-v2` setup steps.
5. Run Symphony/runtime preflight from `WORKFLOW.md`:
   - parse the Symphony YAML front matter and prompt body;
   - verify `tracker.kind`, `tracker.api_key`, `tracker.project_slug`, `tracker.active_states`, `tracker.terminal_states`, `workspace.root`, `agent`, and `codex.command`;
   - confirm active states include the configured execution and running lanes;
   - confirm terminal or handoff states include `Ready for Human`;
   - stop if the contract requires Alejo Run v2 to move issues to `Done`;
   - resolve repo-declared tests, TDD handoff evidence, verification artifacts, and runtime evidence from the prompt body, issue contract, and repo instructions;
   - use `doppler run -- <command>` when secrets or environment-backed config are required;
   - never print secret values, dump broad environments, or run unsafe debug output;
   - run the documented Symphony launch or resume command when preflight passes.
6. Show a short preflight table: issue, surface, providers, secrets, dependencies, BDD budget, Symphony verdict, target lane, and blocker if any. Do not ask for approval.
7. Move passing issues into the configured Symphony execution lane and run the documented launch/resume command.
8. Watch each Symphony run until it reaches `Ready for Human`, reports a blocker, or exits unexpectedly:
   - verify that TDD evidence exists when required: baseline or starting state, RED failure for real missing behavior, GREEN pass, refactor decision, tests run, files changed, and provider/runtime evidence where relevant;
   - reject evidence that only proves configuration, trivial greetings, direct adapter probes, SDK setup, canned samples, local echoes, or mocked behavior;
   - if the run is blocked, leave or move the issue to `Ready for Human` with the exact failed acceptance criterion, attempted commands, and next required action.
9. Run the Alejo BDD gate after the Symphony handoff:
   - derive 3 to 5 behaviours from the issue contract, including persona, objective, prompts/actions, wait expectations, failure modes, and evidence needs;
   - run repo-declared tests and real-surface checks for the selected `api`, `ui`, `cli`, or `mcp` surface;
   - for UI/browser behavior, use Playwright against the running app as a real user;
   - for chat or managed-agent work, verify a representative conversation or action that proves the backend/provider result is not canned, mocked, stubbed, or disconnected;
   - for provider, job, queue, scheduler, CLI, API, or MCP behavior, capture runtime-backed evidence of the real integration.
10. After each BDD cycle, spawn a fresh subagent whose only job is to run `alejo-review` against planning artifacts, selected issues, code, and verification evidence. Inline review is invalid.
11. Repair every relevant BDD failure and P0/P1/P2 review gap by continuing or requeueing the issue through the workflow until the BDD budget is exhausted or the report is clean.
12. Finish by leaving the issue in `Ready for Human` with a concise comment covering tests, BDD evidence, review result, files/PR/branch, residual risk, and the note that the human may move it to `Done`.

## Blockers

Stop only for:

- missing unsafe or human-required secrets;
- missing non-derivable product, architecture, provider, or environment decisions;
- exhausted BDD budget;
- unavailable required external systems or authenticated provider access;
- missing or conflicting repo/Linear `WORKFLOW.md`, lane mapping, runtime command, or Linear write access;
- Symphony/runtime commands that are required but unavailable or unsafe to run;
- required TDD, BDD, provider, Playwright, or review evidence that cannot be produced after the repair budget;
- review gaps outside the selected issue scope.

Report blocker details with issue id, failed surface, failed acceptance criterion, commands/evidence attempted, repair attempts, and next required action.

## Rules

- Do not create `plan.md` or local planning artifacts.
- Do not choose models, agents, branches, concurrency, or slice order unless `WORKFLOW.md` explicitly delegates that choice.
- Do not override `WORKFLOW.md` front matter, prompt body, verification artifacts, or boundaries.
- Do not ask for approvals, permissions, confirmations, or clarifying questions.
- Do not expose secret values in chat, files, commands, logs, Linear, summaries, or commits.
- Do not advance issues with missing unsafe secrets.
- Do not move issues to `Done`; clean work stops at `Ready for Human`.
- Do not call work ready because code was written, tests are green, or issues moved lanes.
- Do not accept UI/browser behavior without Playwright real-browser verification.
- Do not run `alejo-review` inline; always use a fresh subagent.
- Do not ignore relevant P0/P1/P2 review findings.
- Do not accept mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, unwired UI, or half-working behavior.
