---
name: repo-conventions
description: How to work in the corenote repo — branch names, atomic why-first commits, and the scoped local test loop.
version: 1.1.0
---

# Repo conventions

## Branches

Name branches after the task they implement: `core-<n>-<short-kebab-description>`
(for example `core-182-project-entities`). Tooling and humans detect the task
and its status from the ref name alone. Branches not tied to a task use an
explicit `ops/` or `chore/` prefix.

## Commits

- One logical change per commit; if the message needs "and", split it.
- Every commit compiles and passes its tests; tests land in the same commit
  as the code they cover.
- Title: imperative mood, present tense, conventional prefix (`fix(store):`,
  `feat(web):`, `docs:`), 72 chars or fewer, no trailing period.
- Body explains WHY — motivation, trade-off, constraint or evidence — plus the
  tracker card ref (`CORE-xxx`). Never narrate what the diff shows.
- Order commits: prep refactor, then feature, then tooling/CI/docs. Fix review
  nitpicks into the commit that introduced the code.

## Local feedback loop

Keep it scoped to what you changed:

```
cargo fmt --all
cargo clippy -p <changed crates>
cargo test -p <changed crate>
```

Run the affected npm workspace's tests too. Full-workspace lanes run in CI;
reproduce them locally only when the change touches the worker/Wasm boundary,
migrations/RLS, wrangler config or the lane itself.

## Build the smallest thing

Ship what the card's acceptance demands — nothing more. Speculative
abstraction, options nobody asked for and "we might need this later" all cost
review time and invite bugs. When you delete code or an implementation, leave
no vestigial traces: dead references, leftover helpers, stale config or
remnants of the old path. A reader of the final diff should see one coherent
change, not an archaeology site.

## Scratch files

Scratch and intermediate files live inside the synced repo under
`.corenote-tmp/` — never outside the repo (the write op refuses outside paths
by design). Delete that directory before you signal done or pr-proposal so
scratch never lands in a diff or proposal.

## Hard rules

- No credentials in the repository, documents, prompts, logs or bundles.
- No markdown status logs: lane status and evidence go through the tracker.
- Update schemas, fixtures, migrations, API and tests together when changing a
  contract, and record material design changes in a decision record.
