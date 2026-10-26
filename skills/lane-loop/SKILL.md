---
name: lane-loop
description: Run a corenote implementation lane end to end — isolated worktree, red-first TDD, atomic commits, PR with green CI lanes, merge and cleanup.
version: 1.0.0
---

# The lane loop

## Isolate

Never work in the main checkout. Create a worktree under `kb-lanes/` with a
branch named after the task:

```
git fetch origin
git worktree add /path/kb-lanes/core-<n>-<slug> -b core-<n>-<slug> origin/main
```

## Build red-first

Write the failing test that proves the gap, then the implementation that turns
it green. Record test names and one-line red-to-green evidence for the PR body.

## Land

1. Push and open a PR referencing the card (`CORE-xxx`), with a plain-language
   body: what and why, design decisions, evidence.
2. Watch every CI lane; all must be green before merge. Infra flakes get one
   rerun; your own diff gets a fix on the branch.
3. Merge with a merge commit. Record the merge SHA.
4. Clean up: remove the worktree, delete the branch locally and on the remote.

## Stay honest

Distinguish proposed, implemented, tested and deployed behavior. A reference
test is not proof that RLS, search or cloud storage enforce the same policy.
Report acceptance evidence, limitations, and the next unmet delivery gate.
