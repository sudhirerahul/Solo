# Post-Meeting Action Extraction

**Surface:** Cowork scheduled task
**Cadence:** Triggered manually right after a key meeting, or as a daily batch catch-all at end of day
**Sources:** Notion (meeting notes), Slack
**Output:** Rows appended to the shared commitments tracker (`[CONFIGURE]` Notion DB)

## Prompt

> Scan today's meeting notes from Notion (and any Slack threads tagged as meeting follow-ups). For each
> meeting, extract every concrete commitment: who owns it (by name, not "the team"), what they committed
> to, and the deadline if one was stated or clearly implied. Do not invent a deadline that wasn't stated —
> mark it "no deadline given" instead. If no individual is named as owner, do not fabricate one and do not
> skip the commitment either — log the Owner field honestly as unclear (e.g. "no individual named — [who
> discussed it]") so the digest can flag it for an owner to be assigned. Post each commitment as a new row
> in the commitments tracker with columns: Owner, Commitment, Source meeting, Date extracted, Deadline,
> Status (default "Open"). Skip anything that was already logged from this meeting in a prior run — dedup
> key is the same Source meeting title + the same meeting date (the date the meeting happened, NOT the
> Date-extracted run date — keying on run date would let a meeting re-scanned on a later day duplicate).

## Config

- `[CONFIGURE]` Notion DB URL for the commitments tracker (create it first if it doesn't exist yet — see
  `tasks/todo.md` open question on where this should live)
- `[CONFIGURE]` Where meeting notes actually get taken today (Notion meeting-notes DB? Otter/Granola
  synced into Notion? Manual notes in a doc?) — the source needs to be real before this can run

## Calibration notes

[2026-07-25] Ran a synthetic golden-dataset calibration (no real meeting data existed yet) —
6 fixture meetings, 7 ground-truth commitments + 1 negative case, in a labeled Notion sandbox
(see `eval/post-meeting-action-extraction/`). Independently verified (not self-reported): 7/7
recall, 0 fabricated rows, correct "no deadline given" handling, correct honest-unclear-owner
handling, negative case correctly rejected, same-day dedup correctly skipped a pre-seeded
duplicate on both an initial run and a re-run.

Two real gaps this run did NOT prove, flagged by the independent verifier and still open:
- The dedup test only exercised the same-calendar-day case (pre-seeded row's Date-extracted was
  today). The prompt now keys dedup on meeting date, not run date (see prompt text above), but this
  fix itself hasn't been re-tested with a pre-seeded row dated several days earlier.
- The agent that ran the extraction and the agent that verified dedup on the re-run were the same
  agent in the same context — a same-context re-run can't fully rule out recall bias. A cleaner
  re-test would use a fresh agent with no memory of the first pass.
Do not mark dedup logic "trusted" until both are re-tested; this note replaces the old placeholder.
