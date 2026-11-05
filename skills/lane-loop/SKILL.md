---
name: lane-loop
description: Complete one Corenote task with current authority, admitted tools, real test evidence and a candidate PR for independent review.
version: 1.4.0
---

# The lane loop

Read the card's acceptance clauses and the repository's agent instructions.
Work on that one task and preserve its delivery instructions.

## Use the tools this run offers

A hosted pi worker already has a task attempt and fence. Its controller
renews the lease and records completion. Do not claim another attempt,
operate the tracker on its behalf or assume a shell is available.

For a pi repository task:

1. Use `read_file` with a path relative to the checkout. Start with known
   files such as `README.md`; a directory, an absolute path and a guessed
   missing file are not file contents. A refused read is not evidence of
   the file's contents. Follow a correctable refusal's guidance; stop on
   lost authority or an uncertain operation.
2. Use `edit_file` with the hash and unique text you actually observed,
   or `create_file` for a new deliverable. Keep changes within the card.
3. Use `run_tests` with an admitted command: `npm test`,
   `npm run test:worker`, `npm run test:web` or `cargo test --locked`.
   Other commands and installations need an exposed, approved operation.
   A clone alone does not prepare dependencies. If the required test
   cannot run, ask on the card with `ask_user`; never invent a pass.
4. After a real successful test, call `propose_pr`. The default is a
   normal PR. Use `delivery: "draft_only"` only when requested. A later
   edit needs another test. Keep an explicit request to leave a PR open
   even when the project otherwise permits automatic merging.

Use `read_history` for this session's earlier records and retained output.
Keep command ids when a test continues in the background; use
`command_status` when that tool is offered instead of starting it again.
A refused proposal, pending command or unanswered question is not success.

## Use direct commands only when admitted

Some runs offer a shell, Git or tracker tools. Use them only within their
current grants and the task's authorization. Your container checkout is
exclusive; no additional worktree is needed. Name the branch after the
card, commit one logical change at a time and preserve unrelated work.
Write a failing behavior check before its implementation and retain the
red-to-green evidence. Credentials never enter commands, commits or logs.

## Hand off for review

Report the candidate PR, exact head, real test receipts and unmet clauses.
All required CI checks must pass on that same head. Do not skip CI or count
a skipped or pending check as a pass. A changed head needs fresh checks.
The runtime can wait for CI without another model turn.

An independent reviewer checks the acceptance clauses and the PR's code.
The verdict must name the immutable evidence and the exact checked head.
Green CI, a PR link and a review request are not a verdict. You cannot
review your own work. The worker never merges its PR or marks its card
Done. An authorized controller may merge only after independent acceptance,
the project's gates and any explicit hold are satisfied.

If blocked, ask a concrete question once on the card and retain saved work.
Do not replay an uncertain paid call or write to obtain a clearer error.
Distinguish proposed, implemented, tested, reviewed and serving behavior.
