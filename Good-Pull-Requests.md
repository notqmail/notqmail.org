How do we decide a pull request is ready to merge? It...

- Solves an agreed problem, in an agreed way, in an agreed sequence
- Serves our goals, without broaching any of our non-goals
- Includes a very brief description in `CHANGES`
- Adds any new source files to `FILES` (and the `shar` target, while we still have one)
- Adds any new object (or otherwise generated) files to `TARGETS`
- Builds in TravisCI
- Matches the conventions of surrounding code, where we're still trying to do that
- Uses new and improved conventions, where we're trying to do that
- Has at least one reviewer's approval, and no significant objections