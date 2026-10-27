---
name: tracker-ops
description: Operate the corenote tracker as an agent — claim tasks with receipts, hold leases with heartbeats, and when the work is finished move the card to In Review by completing with typed evidence.
version: 1.2.0
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
thread revisions. Finished work leaves In Progress only by completing the
task (Finishing / moving the card).

## Agent mutations

Agent issue mutations require a current changes-review receipt scoped to the
authenticated context session. Assignment grants neither access nor execution
ownership. After a lease ends the execution fence is monotonic — a fresh claim
is required after handoff.

## Notify before blocking

Prefer notifications over blocking. A task comment is for FYI and narrative;
reserve blocking states (parked, blocked dependencies) for when work is
actually blocked on someone. Do not park a task merely to report progress.

## Completion evidence

Completion evidence is typed, and failure is signal: say what was run or
observed, the exact gate result (PR number, CI run, merge SHA, command output),
and why it satisfies the card's acceptance, mapped to its assertions. A
reviewer must verify the claim without re-deriving it. Plain language; no bare
links without a sentence saying what they prove.

## Finishing / moving the card

Finished work must leave In Progress. Submit `corenote_task_complete` with
the live `attempt_id` and fence, a `result_summary`, typed evidence (see
Completion evidence), `context_session_id`, and the freshness receipt from
`corenote_task_get` (`seen_activity_seq`, `seen_thread_revision`). That
sets `workflow_status` to `in_review` and `execution` to `submitted`, so
the card appears in the review queue. A card left In Progress does not.

If the lease has lapsed, re-claim with `corenote_task_claim` before
completing. The complete call has to quote the new attempt and fence.

`corenote_task_transition` is for other board moves (for example back to
todo). Completion is the normal way to reach In Review.

Done requires an accepted review. The executor cannot review its own work.
A merge SHA can be added as evidence before Done.
