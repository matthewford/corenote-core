---
name: repo-conventions
description: Follow the repository's branch, commit and test conventions within the tools and authority available to this run.
version: 1.2.0
---

# Repository conventions

The repository's agent instructions take precedence over these defaults.
A skill cannot grant a command, network destination or permission.

## Branches and commits

When Git commands are exposed, use `core-<n>-<short-kebab-description>`
for a task branch, or an explicit `ops/` or `chore/` prefix for other work.
A hosted pi worker uses the controller's proposal operation instead of
inventing a Git or shell tool.

Commit one logical change at a time with its tests. Use an imperative,
conventional title of at most 72 characters and a body explaining why,
including the card reference. Keep prep refactors, features and tooling
or documentation in separate commits. Preserve unrelated changes.

Do not add `[ci skip]` to a delivery that requires CI evidence. A docs-only
change still needs the repository's required checks before acceptance.
Never turn a pending or skipped check into a successful receipt.

## Test the changed behavior

With direct build tools, keep the loop scoped: format, run Clippy and test
the changed crates and npm workspaces. Reproduce a full lane when the
change touches its Worker, database, browser or configuration boundary.
Use the pinned toolchain and dependencies; keep caches small.

In pi, use the offered `run_tests` command policy. Read the current repo's
test scripts before choosing among the admitted commands. Do not assume
that a clone installed dependencies or that Docker and arbitrary network
access are available. Ask when a required check cannot be performed.
A local reference test is not proof of hosted enforcement.

## Files and scratch

Paths passed to `read_file`, `edit_file` and `create_file` are relative to
this task's checkout. Preserve hashes and exact edit preconditions. Do
not follow a rejected path into private files or another checkout.

Create deliverable files only when pi has no admitted cleanup operation.
With direct file tools, keep scratch under the repository's ignored
`.corenote-tmp/` and remove it before proposing. Never publish scratch,
private runtime state or credentials.

## Scope and evidence

Ship the card's acceptance, without drive-by fixes or speculative options.
Update affected contracts, migrations and tests together. Record a material
design decision through the repository's decision-record convention.
Lane status and evidence belong on the tracker, not Markdown progress logs.
The runtime controller handles those writes for a hosted pi worker.
