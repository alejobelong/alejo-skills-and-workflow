# Linear Statuses And Labels XML Shape

Use this XML shape for `docs/agents/triage-labels.md`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<linear_statuses_and_labels>
  <purpose>Give Alejo skills one shared vocabulary for issue readiness and Symphony handoff.</purpose>
  <workflow_statuses>
    <status alejo_role="needs-triage" linear_status="Needs Triage" />
    <status alejo_role="needs-info" linear_status="Needs Info" />
    <status alejo_role="ready-for-human" linear_status="Ready for Human" />
    <status alejo_role="ready-for-agent" linear_status="Ready for Agent" />
    <status alejo_role="symphony-execution" linear_status="Night Shift Queued" />
    <status alejo_role="in-symphony" linear_status="In Night Shift" />
    <status alejo_role="done" linear_status="Done" />
    <status alejo_role="wontfix" linear_status="Won't Fix" />
  </workflow_statuses>
  <issue_labels>
    <label>vertical-slice</label>
    <label>hitl</label>
    <label>sad-follow-up</label>
    <label>surface:cli</label>
    <label>surface:api</label>
    <label>surface:ui</label>
    <label>surface:mcp</label>
    <label>secrets-required</label>
  </issue_labels>
  <rule>Planning artifacts live in Linear Project Documents. Labels are only for issues.</rule>
</linear_statuses_and_labels>
```
