# Symphony Workflow Linear Project Document Shape

Use this XML shape for the Linear Project Document `WORKFLOW.md`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<symphony_workflow>
  <purpose>Define how Symphony runs approved Linear issues with fresh Codex threads.</purpose>
  <entry>
    <source>Linear vertical-slice issues and the Linear Project Document issue-tracker.md.</source>
    <ready_status>Ready for Agent</ready_status>
    <execution_lane>Night Shift Queued</execution_lane>
    <launcher>alejo-run</launcher>
    <coding_agent>Codex only</coding_agent>
  </entry>
  <issue_contract format="XML">
    <field>user-facing behavior</field>
    <field>compact context from XML Linear Project Documents</field>
    <field>acceptance criteria</field>
    <field>surface: api, ui, cli, or mcp</field>
    <field>preconditions and dependencies</field>
    <field>Doppler secret names only, if needed</field>
    <field>quality attributes and BDD budget</field>
    <field>slice-owned code organization</field>
  </issue_contract>
  <thread_flow>
    <step order="1" role="bdd_generator">Read issue only; write scenario.json.</step>
    <step order="2" role="test_writer">Read issue, scenario.json, and code; write failing test only.</step>
    <step order="3" role="implementer">Read issue, scenario.json, code, and failing test; write implementation only.</step>
    <step order="4" role="refactor">Read issue, scenario.json, code, and green tests; write cleanup only.</step>
    <step order="5" role="synthetic_tester">Read issue, scenario.json, and code; exercise the real surface and report pass/fail.</step>
  </thread_flow>
  <boundaries>
    <boundary>Linear owns issue state.</boundary>
    <boundary>Linear Project Documents own setup docs, workflow docs, and planning artifacts.</boundary>
    <boundary>Issues own implementation context.</boundary>
    <boundary>Doppler owns secret values.</boundary>
    <boundary>alejo-run moves approved issues into the Symphony lane.</boundary>
    <boundary>Do not maintain a repo-local WORKFLOW.md copy.</boundary>
  </boundaries>
</symphony_workflow>
```
