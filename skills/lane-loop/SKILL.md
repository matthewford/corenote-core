---
name: lane-loop
description: Run a corenote implementation lane end to end — branch in your clone, red-first TDD, atomic commits, PR with green CI lanes, merge and cleanup.
version: 1.1.0
---

# The lane loop

## Branch

Your container clone is already yours alone — nobody else works in it. Branch
directly in it from the latest main:

```
git fetch origin
git checkout -b core-<n>-<slug> origin/main
```

Do not create git worktrees: they exist to protect a shared checkout, and your
clone is not shared.

## Build red-first

Write the failing test that proves the gap, then the implementation that turns
it green. Record test names and one-line red-to-green evidence for the PR body.

## Land

1. Push and open a PR referencing the card (`CORE-xxx`), with a plain-language
   body: what and why, design decisions, evidence.
2. Watch every CI lane; all must be green before merge. Infra flakes get one
   rerun; your own diff gets a fix on the branch.
3. Merge with a merge commit. Record the merge SHA.
4. Clean up: delete the branch on the remote. Your clone goes away with the
   session; leave nothing behind in the repo itself.

## Stay honest

Distinguish proposed, implemented, tested and deployed behavior. A reference
test is not proof that RLS, search or cloud storage enforce the same policy.
Report acceptance evidence, limitations, and the next unmet delivery gate.
