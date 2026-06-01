<?xml version="1.0" encoding="UTF-8"?>
<symphony_workflow>
  <purpose>Symphony runs autonomous implementation from Linear issue contracts. Linear owns execution state. Codex is the only coding agent.</purpose>
  <entry>
    <source>Linear vertical-slice implementation issues configured by the Linear Project Document issue-tracker.md.</source>
    <ready_state>Ready for Agent</ready_state>
    <execution_lane>Night Shift Queued</execution_lane>
    <launcher>alejo-run</launcher>
    <coding_agent>Codex only</coding_agent>
    <autonomy>alejo-run is autonomous and does not ask for approval before moving passing issues into the execution lane.</autonomy>
    <prd_boundary>PRDs live in Linear Projects, not runnable issues, and are never candidates for Symphony.</prd_boundary>
  </entry>
  <issue_contract format="XML">
    <field>Title.</field>
    <field>User-facing behavior.</field>
    <field>Necessary compact context from PRD.xml, SAD.xml, Q&amp;A.xml, CONTEXT.xml, and prototype.xml evidence.</field>
    <field>Acceptance criteria.</field>
    <field>Verification surface: api, ui, cli, or mcp.</field>
    <field>Preconditions: required state, data, config, user role, or None.</field>
    <field>Dependencies or blockers.</field>
    <field>Providers and provider resource expectations.</field>
    <field>Required Doppler secret refs by name only, or None.</field>
    <field>Slice-relevant quality attributes.</field>
    <field>BDD iteration budget.</field>
    <field>Production constraints: no mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, TODO-only paths, or unwired UI.</field>
    <field>Representative prompts, inputs, actions, and personas for interactive work.</field>
    <field>Latency, timeout, wait, and user-visible failure expectations.</field>
    <field>Playwright verification requirements for UI or browser-reachable behavior.</field>
    <field>Provider or managed-agent evidence required to prove real integration.</field>
    <field>Review evidence required before completion.</field>
    <field>Architectural constraints needed for implementation.</field>
    <field>Slice-owned code organization.</field>
    <field>Readiness label/status proving the issue is ready for autonomous execution.</field>
  </issue_contract>
  <secrets>
    <rule>Doppler is the only secret provider.</rule>
    <rule>Issues and artifacts must reference secret names only, never values.</rule>
    <rule>If alejo-secrets confirms, renames, adds, or removes any required secret after issues exist, run alejo-consistency-propagation or update the affected Linear issues before alejo-run.</rule>
    <rule>alejo-run must fail preflight when issue secret refs do not match the confirmed Doppler names needed by the slice.</rule>
  </secrets>
  <symphony_runtime>
    <command name="launch">Repo-declared Symphony launch or resume command, or None.</command>
    <command name="status">Repo-declared Symphony status/progress command, or None.</command>
    <command name="test">Repo-declared test command for the selected surface, or None.</command>
    <command name="synthetic_verification">Repo-declared synthetic tester command or pass-verdict source, or None.</command>
    <command name="review">Fresh alejo-review subagent; inline review is not valid.</command>
    <browser_base_url>Repo-declared local browser URL for Playwright, or None.</browser_base_url>
    <artifact_sink>Where Symphony writes scenario.json, recommendation.json, logs, handoff evidence, or pass verdicts.</artifact_sink>
    <rule>Run commands through Doppler when the issue needs secrets or environment-backed config; never print secret values.</rule>
  </symphony_runtime>
  <verification_artifacts>
    <artifact name="scenario.json">BDD behaviours with persona, objective, prompts/actions, wait expectations, failure modes, and evidence needs.</artifact>
    <artifact name="test_output">Repo-declared test output, Playwright evidence, CLI/API/MCP output, or provider-backed evidence for the real surface.</artifact>
    <artifact name="recommendation.json">Synthetic tester pass/fail recommendation or equivalent pass verdict.</artifact>
    <artifact name="alejo_review_report">Fresh review subagent report with no relevant P0/P1/P2 gaps before completion.</artifact>
  </verification_artifacts>
  <per_issue_threads>
    <thread role="bdd_generator">Reads issue only; writes scenario.json.</thread>
    <thread role="test_writer">Reads issue, scenario.json, and code; writes failing test only.</thread>
    <thread role="implementer">Reads issue, scenario.json, code, and failing test; writes implementation only.</thread>
    <thread role="refactor">Reads issue, scenario.json, code, and green tests; writes cleanup only.</thread>
    <thread role="synthetic_tester">Reads issue, scenario.json, and code; exercises the real surface and writes recommendation.json or a pass verdict.</thread>
    <thread role="review_subagent">Reads planning artifacts, selected issues, code, and verification results; runs alejo-review and writes readiness gaps.</thread>
  </per_issue_threads>
  <boundaries>
    <boundary>Do not create or consume Alejo plan files.</boundary>
    <boundary>Do not choose agents or models per issue.</boundary>
    <boundary>Do not use non-Codex coding agents.</boundary>
    <boundary>Implementation threads do not read PRD/SAD/Q&amp;A/prototype XML documents to discover requirements; the issue is the canonical compact context packet. The review subagent may read planning artifacts for final alignment review.</boundary>
  </boundaries>
</symphony_workflow>
