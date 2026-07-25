# Show Notes Drafting (Routine variant)

**Surface:** Claude Code Routine, implemented as a GitHub Actions workflow
(`.github/workflows/show-notes-drafting.yml`) using `anthropics/claude-code-action@v1`
(https://code.claude.com/docs/en/github-actions).

**Decision (2026-07-25):** transcripts are committed to this repo; the Cowork variant
(`cowork/show-notes-drafting.md`) was retired in favor of this Routine.

**Trigger:** A push to `main` touching `transcripts/**`, or manual `workflow_dispatch`. See
`.github/workflows/show-notes-drafting.yml` for the exact trigger config.

**Sources:** The transcript file(s) in `transcripts/` that don't yet have a matching file in
`show-notes/` (matched by identical basename — see `transcripts/README.md`).

**Output:** A show-notes file at `show-notes/<same-basename>.md`, opened as a draft pull request
for human review (Claude itself has no Bash access and cannot commit or push — see the workflow
file for how the PR gets opened).

## Prompt

> Take the episode transcript and draft: (1) a short summary (2-3 sentences, written to make
> someone want to listen), (2) timestamps for major topic shifts with a short label each, and (3)
> full show notes covering key points, any people/companies/resources mentioned by name (spelled
> correctly), and a pull-quote worth highlighting. Write the result to
> `show-notes/<same-basename-as-the-transcript>.md` — do not commit it yourself and do not write
> anywhere else; a separate workflow step handles the commit and pull request. Match the voice
> guardrail from the root `CLAUDE.md`: specific to this conversation, not generic podcast-notes
> boilerplate.

## Config

- **Transcript / show-notes paths and naming:** `transcripts/<ISO-date>-ep-<3-digit-episode-number>-<guest-slug>.md`,
  paired with `show-notes/<identical-basename>.md`. Full convention documented in
  `transcripts/README.md` and `show-notes/README.md`.
- **Trigger/schedule syntax:** defined in `.github/workflows/show-notes-drafting.yml`, using
  `anthropics/claude-code-action@v1`. That workflow file is currently inert — see its header
  comment for the prerequisites (GitHub remote, `ANTHROPIC_API_KEY` secret, Claude GitHub App,
  Actions PR-creation setting) that must exist before it can actually run.

## Output spec (checkable — used by an independent tester)

Each generated `show-notes/<basename>.md` must follow this exact skeleton, in this order:

```
# <episode title>
**Host:** <host name> **Guest:** <guest name>, <guest's stated role/company>
## Summary
## Timestamps
## Show Notes
## Pull Quote
```

- **Title line:** a level-1 heading with the episode title.
- **Byline line:** directly under the title, naming the host and the guest (with the guest's stated
  role/company), matching the transcript's own names/spelling.
- **Summary:** exactly 2-3 sentences.
- **Timestamps:** one entry per major topic shift, each with a short label, each timestamp
  matching a real `[HH:MM:SS]` mark that actually appears in the source transcript (no invented
  or approximated times), listed in strictly increasing order.
- **Show Notes:** covers the episode's key points in prose, and every person, company, and named
  resource mentioned is spelled exactly as it appears in the transcript — no normalization, no
  guessed spellings.
- **Pull Quote:** exactly one, and it must be verbatim (character-for-character) from the
  transcript, not paraphrased or lightly edited.

## Calibration notes

A synthetic dry run on 2026-07-25 (fixture transcript, `samples/show-notes-drafting/`) confirmed the
prompt correctly matched every timestamp, name, and the pull-quote to the fixture transcript. One
ungrounded phrase was found in the sample output (an invented detail about who was asking about a
co-founder) and corrected in this pass (2026-07-25); the output skeleton above was also added as a
result, so repeat runs format consistently.
