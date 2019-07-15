# A pull request is ready when it...

- Solves an agreed problem, in an agreed way, in an agreed sequence
- Serves our goals, without broaching any of our non-goals
- Includes a very brief description in `CHANGES`
- Adds any new source files to `FILES` (and the `shar` target, while we still have one)
- Adds any new system-dependent portability headers to `SYSDEPS`
- Adds any new object (or otherwise generated) files to `TARGETS`
- Builds in TravisCI
- Matches the conventions of surrounding code, where we're still trying to do that
- Uses new and improved conventions, where we're trying to do that
- Has at least one reviewer's approval, and no significant objections


# To iterate on a PR, we...

- Respond to each piece of feedback
- Squash commits into the sequence we'd want merged to `master`
- Force-push to the feature branch


# To merge a PR, we...

- Click the popup menu for "Merge pull request"
- Choose "Rebase and merge"