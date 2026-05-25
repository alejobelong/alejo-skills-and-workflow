# Issue Tracker: GitLab

Issues, PRDs, and vertical slices live in GitLab Issues. Use the `glab` CLI from inside this repo.

## Conventions

- Create: `glab issue create --title "..." --description "..."`
- Read: `glab issue view <number-or-url> --comments`
- List: `glab issue list -F json`
- Comment: `glab issue note <number-or-url> --message "..."`
- Label: `glab issue update <number-or-url> --label "..." --unlabel "..."`
- Close: post any final note first, then `glab issue close <number-or-url>`

When an Alejo skill says "publish to the issue tracker", create a GitLab issue. When it says "fetch the relevant ticket", read the GitLab issue description, notes, and labels.
