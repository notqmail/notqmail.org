# A pull request is ready when it...

- Solves an agreed problem, in an agreed way, in an agreed sequence
- Describes the costs, risks, and benefits it addresses and/or introduces
- Serves our goals, without broaching any of our non-goals
    - (Rare but not impossible: adjusting our goals instead of the proposed patch)
- Includes a very brief description in `CHANGES`
- Adds any new object (or otherwise generated) files to `TARGETS`
- Builds in all our autobuilders
- Matches the conventions of surrounding code, where we're still trying to do that
- Uses new and improved conventions, where we're trying to do that (see below about what that means)
- Has at least three reviewers' approval, and no significant objections

## We'd like to further require...

- Includes tests
- Passes tests
- Passes static analysis
- Passes fuzzing
- Architecture changes (if any) do not break the security model

# To iterate on a PR, we...

- Respond to each piece of feedback
- Squash commits into the sequence we'd want merged to `master`
- Force-push to the feature branch

# To merge a PR, we...

- merge the branch on the commandline if the branch does *not* need rebase (i.e. is a fast-forward), this preserves e.g. signed commits
  - git checkout master
  - git merge --ff-only that-branch
  - git push
- rebase and merge otherwise
  - Click the popup menu for "Merge pull request"
  - choose "Rebase and merge"

# A note on "surrounding code" and conventions

- if a single-line function declaration (i.e. name and all types on the same line) is changed then convert it to C89
- if a function declaration in a header is changed, and the declaration in the .c file either is C89 already or is converted in the same patch by the above rule, then switch the one in the header too (do _NOT_ do that if it would drag in additional headers to the .h file to get the types to avoid more disruptive changes)
- use uid_t and gid_t where appropriate