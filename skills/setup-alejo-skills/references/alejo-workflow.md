# Alejo Workflow XML Shape

Use this XML shape for `docs/agents/alejo-workflow.md`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alejo_workflow>
  <purpose>Connect the full Alejo planning stack to Symphony implementation.</purpose>
  <planning>
    <step order="1" skill="alejo-questions">Resolve domain language and publish Q&amp;A.xml plus CONTEXT.xml.</step>
    <step order="2" skill="alejo-prd">Publish PRD.xml to the Linear Project.</step>
    <step order="3" skill="alejo-prototype">Publish prototype.xml when UI evidence helps.</step>
    <step order="4" skill="alejo-sad">Publish SAD.xml or SAT.xml.</step>
    <step order="5" skill="alejo-issues">Create vertical-slice Linear issues with XML run contracts.</step>
    <step order="6" skill="alejo-secrets">Give Doppler setup steps when needed.</step>
    <step order="7" skill="alejo-consistency-propagation">Keep XML Project Documents and issues aligned.</step>
  </planning>
  <implementation_bridge skill="alejo-run">
    <step order="1">Read WORKFLOW.md, Linear setup docs, and ready Linear issues.</step>
    <step order="2">Preflight each issue's XML run contract.</step>
    <step order="3">Ask for human approval.</step>
    <step order="4">Move approved issues to the Symphony execution lane.</step>
  </implementation_bridge>
  <symphony>Symphony runs fresh Codex threads from the issue contract and repo WORKFLOW.md.</symphony>
  <artifact_homes>
    <linear_project_documents>PRD.xml, SAD.xml/SAT.xml, Q&amp;A.xml, CONTEXT.xml, prototype.xml</linear_project_documents>
    <linear_issues>vertical slices and actionable follow-ups</linear_issues>
    <repo_docs>AGENTS.md, docs/agents/*, WORKFLOW.md, ADR XML files, and optional local CONTEXT.xml</repo_docs>
    <secrets>Doppler secret values</secrets>
  </artifact_homes>
</alejo_workflow>
```
