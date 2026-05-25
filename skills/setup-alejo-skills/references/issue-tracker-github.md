# Issue Tracker: GitHub

Issues, PRDs, and vertical slices live in GitHub Issues. Use the `gh` CLI from inside this repo.

## Conventions

- Create: `gh issue create --title "..." --body-file <file>`
- Read: `gh issue view <number-or-url> --comments`
- List: `gh issue list --state open --json number,title,body,labels,comments`
- Comment: `gh issue comment <number-or-url> --body "..."`
- Label: `gh issue edit <number-or-url> --add-label "..." --remove-label "..."`
- Close: `gh issue close <number-or-url> --comment "..."`

When an Alejo skill says "publish to the issue tracker", create a GitHub issue. When it says "fetch the relevant ticket", read the GitHub issue body, comments, and labels.
