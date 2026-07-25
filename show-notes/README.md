# Show Notes

Drafted show notes for each Solo Founders Podcast episode, produced by the show-notes-drafting
Routine (`routines/show-notes-drafting/PROMPT.md`, `.github/workflows/show-notes-drafting.yml`)
from the matching transcript in `transcripts/`.

## Naming convention

```
<ISO-date>-ep-<3-digit-episode-number>-<guest-slug>.md
```

Example: `2026-07-31-ep-001-jordan-vance.md`

**Every show-notes file must have the identical basename to its source transcript in
`transcripts/`, just in this directory instead.** This is the whole pairing/idempotency
mechanism — no front-matter or metadata is used to match a transcript to its show notes. The
workflow treats a transcript as "already drafted" purely by checking whether a file of the same
basename already exists here.

## Provenance

Files here are drafted automatically and always need a human read-through before publishing —
the workflow opens them as a draft pull request rather than committing directly to `main`. Do
not hand-edit a file here without also checking whether the source transcript changed; the
workflow does not re-draft a file that already exists, even if the transcript is later edited.
