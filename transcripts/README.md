# Transcripts

Episode transcripts for the Solo Founders Podcast, committed to this repo so the
show-notes-drafting Routine can run against them (`routines/show-notes-drafting/PROMPT.md`,
`.github/workflows/show-notes-drafting.yml`).

## Naming convention

```
<ISO-date>-ep-<3-digit-episode-number>-<guest-slug>.md
```

Example: `2026-07-31-ep-001-jordan-vance.md`

**The show-notes file for an episode must have the identical basename to its transcript, just
in the `show-notes/` directory instead of `transcripts/`.** This is the whole pairing mechanism —
no front-matter or metadata is used to match a transcript to its show notes. A transcript
`transcripts/2026-07-31-ep-001-jordan-vance.md` pairs with
`show-notes/2026-07-31-ep-001-jordan-vance.md`, and only that file.

## Format

- Files are markdown.
- Speaker turns are labeled `**Name:**` at the start of the line.
- Timestamps, if present, use `[HH:MM:SS]`.

## Automation

Committing a file here to `main` triggers the show-notes-drafting GitHub Actions workflow
(`.github/workflows/show-notes-drafting.yml`), which drafts show notes for any transcript that
doesn't yet have a matching file in `show-notes/` and opens a draft PR for human review.
