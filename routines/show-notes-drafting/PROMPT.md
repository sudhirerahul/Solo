# Show Notes Drafting (Routine variant)

**Surface:** Claude Code Routine — use only if episode transcripts are committed to this repo. If
transcripts live in Notion/Drive instead, use `cowork/show-notes-drafting.md` (see the surface decision
rule in the root `CLAUDE.md`). Don't run both variants for the same episode.
**Trigger:** GitHub event (e.g. a transcript file committed/merged) or API call after transcription
finishes
**Sources:** Transcript file committed to this repo
**Output:** A committed show-notes file (and/or a PR) alongside the transcript

## Prompt

> Take the episode transcript committed in this change and draft: (1) a short summary (2-3 sentences,
> written to make someone want to listen), (2) timestamps for major topic shifts with a short label each,
> and (3) full show notes covering key points, any people/companies/resources mentioned by name (spelled
> correctly), and a pull-quote worth highlighting. Commit the show notes as a new file next to the
> transcript, named to match the episode. Match the voice guardrail from the root `CLAUDE.md`: specific to
> this conversation, not generic podcast-notes boilerplate.

## Config

- `[CONFIGURE]` Repo path/convention for transcripts and where show notes should be committed alongside
  them
- `[CONFIGURE]` Trigger wiring — confirm whether this repo actually receives transcript commits, or
  whether transcripts realistically land in Notion/Drive (in which case delete this Routine and rely on
  the Cowork variant instead — don't maintain both if only one path is real)
- `[CONFIGURE]` Exact trigger/schedule config syntax for Routines — verify against current Anthropic docs
  before wiring up; this is a beta feature and the config schema may have changed since this file was
  written

## Calibration notes

_(add findings here after the first few episodes)_
