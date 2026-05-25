# Issue Tracker: Linear

PRDs live as Linear Projects. SADs live as project/repo architecture documents unless there is an actionable SAD follow-up. Vertical slices and actionable follow-ups live as Linear issues.

Use the Linear workspace/team/project configured for this repo. If the workspace, team key, project, or access method is unclear, ask the user before publishing.

## Conventions

- PRD: create or update a Linear Project and add the PRD Markdown to the project description/overview/document area. Do not create a PRD issue.
- Create issue: create a Linear issue in the configured team, with the Alejo Markdown body as the description.
- Read: read the Linear issue title, description, comments/activity, labels, workflow status, relations, and URL.
- List: list open Linear issues using the configured team/project plus the mapped `ready-for-agent` label/status.
- Comment: add a Linear comment to the issue.
- Label/status: use the canonical mappings in `docs/agents/triage-labels.md`; workflow statuses track readiness/execution and labels categorize issue type/surface. Do not use `prd` or `sad` as issue labels when those artifacts are Projects/docs.
- Dependencies: use Linear issue relations when available, and keep the `## Blocked by` section in the issue body.
- Close: comment with the final result, then move the issue to the team's Done/Completed workflow status.
- Symphony lane: `alejo-run` moves approved issues into the configured Symphony execution workflow status after explicit human approval.

When `alejo-prd` says "publish the PRD", create or update a Linear Project. When implementation skills say "publish to the issue tracker", create a Linear issue. When a skill says "fetch the relevant ticket", read the Linear issue description, comments/activity, labels, workflow status, relations, and URL.

Linear issue state is authoritative for day-shift readiness and Symphony handoff. Do not use GitHub issue commands for Linear issues.

## Linear References

- Create issues: https://linear.app/docs/creating-issues
- Labels: https://linear.app/docs/labels/
- Issue status/workflows: https://linear.app/docs/configuring-workflows
- Comments: https://linear.app/docs/comment-on-issues
