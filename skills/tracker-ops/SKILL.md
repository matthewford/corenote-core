---
name: tracker-ops
description: Preserve current task ownership and submit immutable evidence for an independent decision, using only the tracker operations this run is granted.
version: 1.3.0
---

# Tracker operations

## Know who owns the attempt

A hosted pi worker receives an existing attempt and fence. Its controller
owns renewal, task commands and completion. Use the offered tools and
`ask_user` for a blocking question; do not invent tracker commands, borrow
another identity or claim on the controller's behalf.

For a manually operated task with tracker tools, read current context,
claim through the canonical command and retain the returned attempt,
fence and expiry. Assignment alone grants neither access nor ownership.
Renew while work and review are active, checking each server receipt.
Your comments advance activity: re-read before the next substantive write.

A lost lease, revocation or superseding owner ends the old attempt. Do not
re-claim merely to submit old work or reuse an old fence. Read current
context and let the authorized controller decide whether a fresh attempt
is appropriate. A retry cannot settle an uncertain earlier effect.

## Submit before acceptance

Keep workflow status separate from execution status. Dependencies require
accepted Done. A successful test or PR does not accept the card.

Completion evidence names the candidate PR, immutable head, actual test
and CI receipts, and which acceptance clauses they prove. A PR may remain
open during review; do not merge it to manufacture completion evidence.
Use sentences that explain what each link proves. Keep failed and unknown
outcomes visible, including unresolved usage.

For a hosted pi worker, propose the tested change and report its state.
The controller submits and reads back the immutable completion receipt.
For a manual task, `corenote_task_complete` needs the current attempt,
fence, context session and fresh activity/thread receipts. Confirm its
returned completion id and submitted review state. A lost reply requires
reconciliation with the original key, not another completion namespace.

## Independent review and delivery

A reviewer distinct from the implementer checks the card and code at the
named head and records a pass or a rejection tied to that completion.
An evidence attachment or a requested review is not that decision. Never
approve your own PR or impersonate a human reviewer.

A rejection names the unmet clause and returns work for correction. A new
head needs fresh checks and review. An accepted review still obeys the
project's merge policy and explicit instructions to keep a PR open or draft.
Only an authorized controller performs the merge or final acceptance.
