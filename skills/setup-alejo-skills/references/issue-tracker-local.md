# Issue Tracker: Local Markdown

Issues, PRDs, and vertical slices live as Markdown files under `.scratch/`.

## Conventions

- One feature per directory: `.scratch/<feature-slug>/`
- PRD: `.scratch/<feature-slug>/PRD.md`
- SAD, if local instead of docs: `.scratch/<feature-slug>/SAD.md`
- Issues: `.scratch/<feature-slug>/issues/NN-<slice-slug>.md`
- Triage state: `Status: <label>` near the top of each issue file.
- Comments: append under `## Comments`.

When an Alejo skill says "publish to the issue tracker", create or update a Markdown file under `.scratch/`. When it says "fetch the relevant ticket", read the referenced Markdown file.
