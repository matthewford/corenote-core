# corenote-core

The Corenote platform skills bundle (CORE-404). Each directory under
`skills/` holds one `SKILL.md`; the runtime pins this repository and
materializes the skills at boot.

The pi guidance in this release follows the tools currently offered by
Corenote. It preserves controller ownership, admitted commands and
independent review. A skill never grants authority that the server refuses.

Publish changed instructions under a new immutable tag or commit and update
the consuming runtime pin after review. Preserve existing tags: changing a
branch does not update a worker pinned to an older tag. Existing sessions
keep their original skill receipts; a fresh admitted run uses the new pin.
