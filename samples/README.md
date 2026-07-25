# Samples — Synthetic Test Fixtures

Everything under `samples/` is **SYNTHETIC test data** — invented guests, invented companies, invented
transcripts, invented sources — created solely to dry-run-test the `guest-research-one-pager` and
`show-notes-drafting` prompts before they handle real data.

**Nothing here is real. Nothing here should ever be pasted into a real brief, cited, or published.**

## Fixture sets

- `guest-research-one-pager/fixture-synthetic-guest-corpus.md` — an invented source corpus (a fabricated
  founder, fabricated company, and numbered `[S1]`-`[S6]` fabricated sources) for dry-running the guest
  research one-pager prompt. This corpus is the *only* information that dry-run test is allowed to draw
  from — a generated brief that cites anything not traceable to a numbered source here has failed the
  test.
- `show-notes-drafting/fixture-synthetic-transcript.md` — an invented podcast episode transcript
  (fabricated host, fabricated guest, fabricated companies/people/tools) for dry-running the show notes
  drafting prompt.

Dry-run *output* (the actual generated brief or show notes produced by running a prompt against these
fixtures) is created separately, by whoever executes the test — not stored here as part of authoring the
fixtures.
