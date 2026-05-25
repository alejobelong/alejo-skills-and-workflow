# Issue Tracker: Linear

Linear Projects are the planning container. Linear Project Documents/Resources are the canonical home for Alejo planning artifacts. Vertical slices and actionable follow-ups live as Linear issues.

Use the Linear workspace/team/project configured for this repo. The setup skill must anchor this file to a Linear Project URL so Alejo artifacts and issues have a complete destination. If the URL is not discoverable from existing docs, issue/project links, branch names, remotes, or available Linear tooling, ask the user for the Linear Project URL before writing setup files. Do not write `TODO: fill Linear ...` placeholders for workspace/team/project.

## Conventions

- Required setup fields: Linear Project URL, workspace, team or project context, issue destination, Project Document destination, and access method/tooling.
- Planning artifacts: create or update Linear Project Documents/Resources for `PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, and `prototype.html`. Do not create issues for these artifacts.
- PRD: create or update a Linear Project and publish the PRD Markdown to the Project document named `PRD`. Use the project overview/detailed description only if Project Documents are unavailable in the active tooling.
- SAD/SAT: publish the architecture document to the Project document named `SAD` by default, or `SAT` only when the repo/user already uses that term.
- Q&A: publish the final Alejo Questions log to the Project document named `Q&A`.
- Context: keep the repo `CONTEXT.md` or `CONTEXT-MAP.md` as the working glossary source when needed, and sync the relevant glossary content to the Project document named `CONTEXT.md`.
- Prototype: keep disposable local files under `.scratch/prototypes/` for browser verification, then publish the final HTML prototype to the Project document named `prototype.html` as a fenced `html` code block. If the prototype report is materially different from the HTML, include its summary in the same document or a nearby Project document named `Prototype report`.
- Create issue: create a Linear issue in the configured team, with the Alejo Markdown body as the description.
- Read: read the Linear issue title, description, comments/activity, labels, workflow status, relations, and URL.
- List: list open Linear issues using the configured team/project plus the mapped `ready-for-agent` label/status.
- Comment: add a Linear comment to the issue.
- Label/status: use the canonical mappings in `docs/agents/triage-labels.md`; workflow statuses track readiness/execution and labels categorize issue type/surface. Do not use `prd`, `sad`, `sat`, `qa`, `context`, or `prototype` as issue labels for planning artifacts.
- Dependencies: use Linear issue relations when available, and keep the `## Blocked by` section in the issue body.
- Close: comment with the final result, then move the issue to the team's Done/Completed workflow status.
- Symphony lane: `alejo-run` moves approved issues into the configured Symphony execution workflow status after explicit human approval.

When a planning skill says "publish", create or update the appropriate Linear Project Document. When implementation skills say "publish to the issue tracker", create a Linear issue. When a skill says "fetch the relevant ticket", read the Linear issue description, comments/activity, labels, workflow status, relations, and URL.

Linear issue state is authoritative for day-shift readiness and Symphony handoff. Do not use GitHub issue commands for Linear issues.

## Linear References

- Project overview/resources/documents: https://linear.app/docs/project-overview
- Project documents: https://linear.app/docs/project-documents
- Create issues: https://linear.app/docs/creating-issues
- Labels: https://linear.app/docs/labels/
- Issue status/workflows: https://linear.app/docs/configuring-workflows
- Comments: https://linear.app/docs/comment-on-issues
