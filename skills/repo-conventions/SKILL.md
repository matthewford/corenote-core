---
name: repo-conventions
description: How to work in the corenote repo — branch names, atomic why-first commits, and the scoped local test loop.
version: 1.0.0
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

## Hard rules

- No credentials in the repository, documents, prompts, logs or bundles.
- No markdown status logs: lane status and evidence go through the tracker.
- Update schemas, fixtures, migrations, API and tests together when changing a
  contract, and record material design changes in a decision record.
