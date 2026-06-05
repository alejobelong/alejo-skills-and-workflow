---
name: alejo-run-v2
description: Compact Alejo Run v2 workflow for autonomously executing ready Linear vertical-slice issues through the WORKFLOW.md Symphony contract, Codex Goal mode, Symphony runtime gates, Doppler-safe secret recovery with alejo-secrets-v2, real-surface verification, and a clean alejo-review subagent gate. Use when ready Alejo issues should be run until production-grade without mocks, approvals, or human-in-the-loop pauses.
---

# Alejo Run v2

Autonomously run ready Linear implementation issues until they are production-grade. Repo `WORKFLOW.md` is the official Symphony contract; the Linear Project Document `WORKFLOW.md` is only its mirror for Alejo discovery. Linear owns issue state. Doppler owns secret values. Codex is the only coding agent.

Do not ask for approval, permission, confirmation, or clarifying questions. Proceed when the gates pass; stop only for true blockers.

## Goal Mode

When Codex Goal mode is enabled, the goal is incomplete until every selected issue is:

- implemented through its real `api`, `ui`, `cli`, or `mcp` surface;
- verified by real tests and synthetic real-surface checks;
- free of mocks, fake providers, stubbed SDK responses, placeholders, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, and unwired UI;
- reviewed clean by a fresh `alejo-review` subagent with no relevant P0/P1/P2 gaps;
- moved or reported correctly in Linear.

Do not mark the goal complete for lane movement, code changes, green unit tests alone, or partial handoff.

## Sources

Use canonical Linear and repo evidence:

1. `AGENTS.md`: source-of-truth map.
2. `issue-tracker.md` and `triage-labels.md`: Linear project, states, labels, and lane mapping.
3. `alejo-workflow.md`: Alejo planning-to-implementation lifecycle.
4. Repo `WORKFLOW.md` plus its Linear mirror: Symphony YAML front matter, per-issue prompt template, Alejo execution rules, verification artifacts, and boundaries.
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
   - parse the official Symphony YAML front matter and prompt body;
   - verify `tracker.kind`, `tracker.api_key`, `tracker.project_slug`, `tracker.active_states`, `tracker.terminal_states`, `workspace.root`, `agent`, and `codex.command`;
   - confirm active states include the configured Symphony execution lane and running lane;
   - resolve repo-declared tests, synthetic verification, artifacts, and review evidence from the prompt body, issue contract, and repo instructions;
   - use `doppler run -- <command>` when secrets or environment-backed config are required;
   - never print secret values, dump broad environments, or run unsafe debug output;
   - run repo-declared tests for the selected `api`, `ui`, `cli`, or `mcp` surface;
   - run the documented Symphony launch or resume command when the preflight passes;
   - verify Symphony status, artifacts, logs, handoff evidence, and synthetic tester verdicts from the documented artifact sink;
   - for UI/browser behavior, require Playwright against the running app;
   - for jobs, queues, workers, schedulers, or async flows, verify the repo-declared command, state transition, failure behavior, and observable output.
6. Show a short preflight table: issue, surface, providers, secrets, dependencies, BDD budget, Symphony/runtime verdict, target lane, and blocker if any. Do not ask for approval.
7. Move passing issues into the configured Symphony execution lane and run the documented launch/resume command if one exists.
8. Drive the production loop until done or blocked:
   - generate `scenario.json` with 3 to 5 behaviours including persona, objective, prompts/actions, wait expectations, failure modes, and evidence needs;
   - implement against failing tests and real provider/runtime paths;
   - run Symphony/runtime checks, surface tests, and synthetic verification from `WORKFLOW.md`;
   - for UI/chat/managed-agent work, Playwright must use the real app as a real user and prove the answer/effect is not canned, mocked, stubbed, or disconnected;
   - feed failures into the next BDD repair iteration until the issue budget is exhausted;
   - after each cycle, spawn a fresh subagent whose only job is to run `alejo-review` against planning artifacts, selected issues, code, and verification results;
   - iterate on every relevant P0/P1/P2 review gap until the report is clean or a true blocker is reached.
9. Complete only when real-surface verification, synthetic verification, Symphony/runtime gates, and the review subagent are clean. Otherwise leave the issue out of the done lane and report the exact blocker.

## Blockers

Stop only for:

- missing unsafe or human-required secrets;
- missing non-derivable product, architecture, provider, or environment decisions;
- exhausted BDD budget;
- unavailable required external systems or authenticated provider access;
- missing or conflicting repo/Linear `WORKFLOW.md`, lane mapping, runtime command, or Linear write access;
- Symphony/runtime commands that are required but unavailable or unsafe to run;
- review gaps outside the selected issue scope.

Report blocker details with issue id, failed surface, failed acceptance criterion, commands/evidence attempted, repair attempts, and next required action.

## Rules

- Do not create `plan.md` or local planning artifacts.
- Do not choose models, agents, branches, concurrency, or slice order unless `WORKFLOW.md` explicitly delegates that choice.
- Do not override `WORKFLOW.md` front matter, prompt body, verification artifacts, or boundaries.
- Do not ask for approvals, permissions, confirmations, or clarifying questions.
- Do not expose secret values in chat, files, commands, logs, Linear, summaries, or commits.
- Do not advance issues with missing unsafe secrets.
- Do not mark work complete because code was written, tests are green, or issues moved lanes.
- Do not accept UI/browser behavior without Playwright real-browser verification.
- Do not run `alejo-review` inline; always use a fresh subagent.
- Do not ignore relevant P0/P1/P2 review findings.
- Do not accept mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, unwired UI, or half-working behavior.
