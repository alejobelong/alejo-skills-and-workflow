<?xml version="1.0" encoding="UTF-8"?>
<symphony_workflow>
  <purpose>Symphony runs autonomous implementation from Linear issue contracts. Linear owns execution state. Codex is the only coding agent.</purpose>
  <entry>
    <source>Linear implementation issues configured in docs/agents/issue-tracker.md.</source>
    <ready_state>mapped ready-for-agent on vertical-slice implementation issues only</ready_state>
    <execution_lane>mapped symphony-execution</execution_lane>
    <approval>alejo-run must preflight selected issues and receive explicit human approval before moving issues into the execution lane.</approval>
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
    <field>Required Doppler secret refs by name only, or None.</field>
    <field>Slice-relevant quality attributes.</field>
    <field>BDD iteration budget.</field>
    <field>Architectural constraints needed for implementation.</field>
    <field>Slice-owned code organization.</field>
    <field>Readiness label/status proving the issue is approved and ready for autonomous execution.</field>
  </issue_contract>
  <secrets>
    <rule>Doppler is the only secret provider.</rule>
    <rule>Issues and artifacts must reference secret names only, never values.</rule>
    <rule>If alejo-secrets confirms, renames, adds, or removes any required secret after issues exist, run alejo-consistency-propagation or update the affected Linear issues before alejo-run.</rule>
    <rule>alejo-run must fail preflight when issue secret refs do not match the confirmed Doppler names needed by the slice.</rule>
  </secrets>
  <per_issue_threads>
    <thread role="bdd_generator">Reads issue only; writes scenario.json.</thread>
    <thread role="test_writer">Reads issue, scenario.json, and code; writes failing test only.</thread>
    <thread role="implementer">Reads issue, scenario.json, code, and failing test; writes implementation only.</thread>
    <thread role="refactor">Reads issue, scenario.json, code, and green tests; writes cleanup only.</thread>
    <thread role="synthetic_tester">Reads issue, scenario.json, and code; exercises the real surface and writes recommendation.json or a pass verdict.</thread>
  </per_issue_threads>
  <boundaries>
    <boundary>Do not create or consume Alejo plan files.</boundary>
    <boundary>Do not choose agents or models per issue.</boundary>
    <boundary>Do not use non-Codex coding agents.</boundary>
    <boundary>Do not read PRD/SAD/Q&amp;A/prototype XML documents during night shift to discover requirements; the issue is the canonical compact context packet.</boundary>
  </boundaries>
</symphony_workflow>
