# T3 Code (pingdotgg/t3code)

## Checkout and cleanup (overrides Steps 1.3 and 5.4)

Reuse the checkout assigned to the T3 Code thread. T3 Code normally already
provides an isolated worktree; do not create another just for this loop.
Check out the PR branch there when it is available and the checkout is clean.
If the branch is checked out elsewhere, use its verified head commit in
detached HEAD and push explicitly to the PR's head branch. Preserve local
changes and do not move another checkout's branch. Do not remove a worktree
provided by T3 Code or the user when the loop ends.

## Base branch updates (overrides Phase 2)

Do not merge or rebase onto `main` at startup or merely because the PR falls
behind. This repository does not require PR branches to be up to date:
the active `main` rules had `strict_required_status_checks_policy: false`
when checked on 2026-09-27. Required checks still need to pass.

Update the base only to resolve an actual merge conflict, satisfy a changed
branch rule, or fulfill an explicit user request. If GitHub reports that the
branch is blocked for being behind, inspect the current rules instead of
assuming this recorded setting still applies.

An explicit user request to rebase and force-push overrides the skill's
default prohibition for that operation. Use `--force-with-lease` with the
verified remote head SHA; if the lease fails, inspect the new commits before
retrying. This is not permission to rewrite history during later loop runs.

## Validation

Follow the repository's AGENTS.md: run focused tests, lint, and typechecking
for changed code. Do not run repository-wide checks unless requested. If a
history-only rewrite leaves the tree identical to the already validated
commit, verify that equality rather than rerunning the same checks.
