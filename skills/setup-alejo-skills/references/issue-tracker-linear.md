# Issue Tracker Linear Project Document Shape

Use this XML shape for the Linear Project Document `issue-tracker.md`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<linear_setup>
  <purpose>Tell every Alejo skill where to publish planning artifacts, where to create implementation issues, and how alejo-run hands ready issues to Symphony.</purpose>
  <configured_project name="{Linear Project name}" url="{Linear Project URL}">
    <team name="{Linear team name}" key="{Linear team key}" />
    <access_method>{Codex Linear MCP connector | Linear CLI | Linear API/SDK}</access_method>
  </configured_project>
  <setup_documents>
    <document name="AGENTS.md" />
    <document name="issue-tracker.md" />
    <document name="triage-labels.md" />
    <document name="alejo-workflow.md" />
    <document name="WORKFLOW.md" />
  </setup_documents>
  <project_documents>
    <document name="PRD.xml" />
    <document name="SAD.xml" alternate="SAT.xml" />
    <document name="Q&amp;A.xml" />
    <document name="CONTEXT.xml" />
    <document name="prototype.xml" />
  </project_documents>
  <linear_issues>
    <purpose>Use Linear issues for vertical-slice implementation work and actionable follow-ups.</purpose>
    <required_contract_format>XML</required_contract_format>
    <required_fields>
      <field>user-facing behavior</field>
      <field>compact context from XML Project Documents</field>
      <field>acceptance criteria</field>
      <field>surface: api, ui, cli, or mcp</field>
      <field>preconditions and dependencies</field>
      <field>Doppler secret names only, if needed</field>
      <field>quality attributes and BDD budget</field>
      <field>slice-owned code organization</field>
      <field>readiness status</field>
    </required_fields>
  </linear_issues>
  <symphony_handoff>
    <description>alejo-run reads ready Linear issues, preflights their XML run contract, then moves passing issues into the Symphony lane without approval prompts.</description>
    <status_map alejo_role="ready-for-agent" linear_status="Ready for Agent" />
    <status_map alejo_role="symphony-execution" linear_status="Night Shift Queued" />
    <status_map alejo_role="in-symphony" linear_status="In Night Shift" />
    <status_map alejo_role="done" linear_status="Done" />
  </symphony_handoff>
  <source_of_truth>Linear Project Documents own Alejo setup and planning docs. Repo WORKFLOW.md owns the Symphony runtime contract and is mirrored to Linear. Linear issue state owns implementation readiness and Symphony handoff.</source_of_truth>
  <no_local_copies>Do not maintain repo-local AGENTS.md or docs/agents/* generated setup copies.</no_local_copies>
</linear_setup>
```
