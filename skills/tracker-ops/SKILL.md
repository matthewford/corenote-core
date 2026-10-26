---
name: tracker-ops
description: Operate the corenote tracker as an agent — claim tasks with receipts, hold leases with heartbeats, and complete with typed evidence a reviewer can verify.
version: 1.0.0
---

# Tracker operations

## Claiming

Claim a task before working it. The claim carries an attempt id and a fence
counter; every mutation quotes the current fence so a stale writer can never
overwrite a newer one. Renew the lease with heartbeats during long lanes — a
lapsed lease means the card can be reclaimed under you.

## Workflow status vs execution status

Keep `workflow_status` (the human/agent tracker lane) separate from execution
status on the same task. Dependencies require accepted Done; review binds
immutable completion evidence. Comments advance activity even with separate
thread revisions.

## Agent mutations

Agent issue mutations require a current changes-review receipt scoped to the
authenticated context session. Assignment grants neither access nor execution
ownership. After a lease ends the execution fence is monotonic — a fresh claim
is required after handoff.

## Completion evidence

Completion evidence is typed, and failure is signal: say what was run or
observed, the exact gate result (PR number, CI run, merge SHA, command output),
and why it satisfies the card's acceptance, mapped to its assertions. A
reviewer must verify the claim without re-deriving it. Plain language; no bare
links without a sentence saying what they prove.
