# A pull request is ready when it...

- Solves an agreed problem, in an agreed way, in an agreed sequence
- Describes the costs, risks, and benefits it addresses and/or introduces
- Serves our goals, without broaching any of our non-goals
    - (Rare but not impossible: adjusting our goals instead of the proposed patch)
- Includes a very brief description in `CHANGES`
- Adds any new object (or otherwise generated) files to `TARGETS`
- Builds in TravisCI
- Matches the conventions of surrounding code, where we're still trying to do that
- Uses new and improved conventions, where we're trying to do that
- Has at least two reviewers' approval, and no significant objections

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

- Click the popup menu for "Merge pull request"
- Choose "Rebase and merge"