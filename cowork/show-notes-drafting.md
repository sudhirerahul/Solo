# Show Notes Drafting (Cowork variant)

**Surface:** Cowork scheduled task — use this variant if transcripts land in Notion/Drive rather than a
repo. If transcripts are committed to a repo, use `routines/show-notes-drafting/PROMPT.md` instead (see
the surface decision rule in the root `CLAUDE.md`).
**Cadence:** Triggered after each episode is transcribed
**Sources:** Notion or Drive (episode transcript)
**Output:** Draft show notes, timestamps, and a summary for the episode page (Notion/Drive doc, or
directly into whatever CMS hosts the podcast page)

## Prompt

> Take the episode transcript and draft: (1) a short summary (2-3 sentences, written to make someone want
> to listen, not a dry recap), (2) timestamps for the major topic shifts with a short label for each, and
> (3) full show notes covering the key points discussed, any resources/companies/people mentioned by name
> (spelled correctly — cross-check against the guest research one-pager if one exists for this episode),
> and a pull-quote worth highlighting. Match the voice guardrail from the root `CLAUDE.md`: specific to
> this conversation, not generic podcast-notes boilerplate.

## Config

- `[CONFIGURE]` Where transcripts land (which Notion DB / Drive folder) and in what format
- `[CONFIGURE]` Destination for the final show notes (episode page CMS, Notion, Drive doc for the person
  who publishes)

## Calibration notes

_(add findings here after the first few episodes)_
