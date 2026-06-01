---
name: alejo-review
description: Run a contrarian production-readiness review of a built codebase or Ready for Human Symphony handoff against an Alejo Linear Project's PRD.xml, SAD.xml/SAT.xml, Q&A.xml decisions, CONTEXT.xml, prototype.xml, ADRs, and implementation issues. Use when the user wants an implementation audit, gap analysis, readiness review, review of Ready for Human Linear issues, or confirmed movement of passing handoffs to Done.
---

# Alejo Review

Audit whether the built repo truly matches the Alejo planning stack. Be contrarian: assume the system is not ready until real code, real verification, and real product behavior prove otherwise. Do not reward plausible code, closed Linear issues, happy-path demos, or intent without evidence.

The bar is high: the implementation must align with the PRD, SAD/SAT, prototype evidence, Q&A decisions, CONTEXT.xml language, ADRs, and issue contracts. Do not fix code or create issues unless the user asks. When reviewing `Ready for Human` issues, treat the state as a claim that an agent handoff is ready; verify the claim before recommending `Done`.

## Process

1. Gather artifacts from the current context first, then Linear Project Documents and local mirrors: `PRD.xml`, `SAD.xml`/`SAT.xml`, `Q&A.xml`, `CONTEXT.xml`, `prototype.xml`, ADRs, `docs/questions/`, `docs/prototypes/`, and all relevant Linear implementation issues.
2. Read repo instructions and inspect the codebase: app entrypoints, routes/UI, API surfaces, data model, migrations/storage, integrations, auth, secrets/config, tests, CI, deployment, and operational docs.
3. Extract binding claims from the artifacts: PRD user journeys, SAD/SAT architecture and quality attributes, prototype states/interactions, Q&A decisions, domain terms, security/privacy rules, integrations, secret refs, issue contracts, and ADR constraints.
4. Compare each claim to code and verification evidence. Mark each as `implemented`, `partial`, `missing`, `contradicted`, or `not evidenced`. Treat missing evidence as a gap, not a pass.
5. Run reasonable verification when available: install/build/lint/test, seed or migration checks, CLI/API smoke tests, and browser checks for UI flows. Report commands and failures; do not hide broken setup.
6. Actively look for shortcuts: mocks, fake providers, stubbed SDK responses, skipped tests, TODO-only paths, unwired UI, architecture drift, prototype drift, Q&A decision drift, and behavior that works only in the easiest demo path.
7. Produce the review report. If the user asks to turn gaps into work, hand the approved gaps to `alejo-issues` as behavior-first vertical slices.

## Ready For Human Review Flow

Use this flow when the user asks to review `Ready for Human` issues, finish handoffs, approve Symphony output, or move reviewed work to `Done`.

1. Fetch the relevant Linear issues. Prefer explicit user refs; otherwise inspect the current Alejo Project's `Ready for Human` issues.
2. For each issue, read the active `## Codex Workpad`, attached branch/PR/deploy links, run artifacts, BDD behaviours, validation evidence, and latest Linear comments.
3. Verify the handoff packet:
   - 3 to 5 Given/When/Then behaviours exist and map to acceptance criteria.
   - Real-surface validation passed: Playwright/browser evidence for UI, real MCP calls for MCP, HTTP/contract calls for API, command/job evidence for CLI or workers.
   - Doppler/provider validation names required secret keys without exposing values.
   - No-mock audit covers touched product paths and found no fake providers, stubbed SDK responses, placeholders, skipped tests, or knowingly unwired code.
   - Branch, commit, PR, deploy, or direct-main evidence matches the issue's expected handoff path.
   - Merge/deploy requirements are complete when the issue contract requires them before `Done`.
4. Classify each issue:
   - `pass`: no P0/P1/P2 gaps, required validation passes, and merge/deploy requirements are satisfied or not required.
   - `rework`: implementation is runnable but behaviour, tests, no-mock audit, review comments, merge, or deploy evidence is incomplete.
   - `needs-info`: blocked by missing requirements, secret names, provider access, test data, account setup, or a human product decision.
5. Present a confirmation table before changing Linear unless the user's current request already explicitly authorizes the exact action. Include issue ID/title, review result, evidence summary, target state, and why it is or is not eligible for `Done`.
6. Move an issue from `Ready for Human` to `Done` only after explicit user confirmation for that specific issue or for "all passing Ready for Human issues". Before moving it, re-fetch the issue and confirm it is still `Ready for Human`.
7. Never move `Ready for Agent`, `Night Shift Queued`, or `In Night Shift` directly to `Done`. Those states must first complete the Symphony handoff and review gate.
8. For failed reviews, do not mark `Done`. Recommend `Ready for Agent` for rework-ready issues, `Needs Info` for external blockers, or leave `Ready for Human` with the failed review evidence if the user wants to inspect first.

## Report Shape

Lead with findings, not a narrative summary.

```md
# Alejo Review: {Project}

## Verdict
{ready | not ready | unknown because setup is blocked}

## Critical Gaps
- [P0] {gap}: {why it prevents a fully running system}
  Evidence: {artifact claim} vs {code/test evidence}
  Needed: {smallest behavior-first fix}

## Required Gaps
- [P1] {documented behavior or contract not fully reflected in code}

## Quality / Operations Gaps
- [P2] {tests, observability, security, config, deployment, performance, or resilience gap}

## Coverage Matrix
| Source claim | Code evidence | Status | Needed |

## Ready For Human Decisions
| Issue | Review result | Evidence | Recommended state | Confirmation |

## Verification
- `{command}`: {pass/fail/not run and why}

## Issue Candidates
- {thin vertical slice title}: {observable outcome}
```

Severity:

- `P0`: cannot run, deploy, authenticate, store data, or complete the core journey.
- `P1`: required PRD/SAD/prototype/Q&A/issue behavior is missing, contradicted, or not evidenced.
- `P2`: quality, security, ops, test, or maintainability risk for a real system.
- `P3`: polish or cleanup that should not block launch.

## Rules

- Ground every finding in both a source artifact and code or verification evidence.
- Verdict is `ready` only when there are no P0/P1/P2 gaps and required verification passes or is explicitly impossible for a stated reason.
- Prefer concrete missing behavior over vague advice.
- Respect `CONTEXT.xml` terminology, Q&A decisions, ADRs, SAD/SAT constraints, and prototype evidence.
- Treat closed/done Linear issues as claims to verify, not proof of implementation.
- Treat `Ready for Human` Linear issues as handoff packets to audit, not proof of completion.
- Move `Ready for Human` issues to `Done` only when the review passes and the user explicitly confirms the move in the current request or follow-up.
- Treat "not found yet" as `not evidenced`; do not soften it into ready.
- Do not create horizontal backlog items. Missing work should become vertical slices when converted to issues.
- If artifacts contradict each other, report the contradiction before judging the code.
