# Post-Meeting Action Extraction

**Surface:** Cowork scheduled task
**Cadence:** Triggered manually right after a key meeting, or as a daily batch catch-all at end of day
**Sources:** Notion (meeting notes), Slack
**Output:** Rows appended to the shared commitments tracker (`[CONFIGURE]` Notion DB)

## Prompt

> Scan today's meeting notes from Notion (and any Slack threads tagged as meeting follow-ups). For each
> meeting, extract every concrete commitment: who owns it (by name, not "the team"), what they committed
> to, and the deadline if one was stated or clearly implied. Do not invent a deadline that wasn't stated —
> mark it "no deadline given" instead. Post each commitment as a new row in the commitments tracker with
> columns: Owner, Commitment, Source meeting, Date extracted, Deadline, Status (default "Open"). Skip
> anything that was already logged from this meeting in a prior run (check existing rows for the same
> source meeting + date before adding duplicates).

## Config

- `[CONFIGURE]` Notion DB URL for the commitments tracker (create it first if it doesn't exist yet — see
  `tasks/todo.md` open question on where this should live)
- `[CONFIGURE]` Where meeting notes actually get taken today (Notion meeting-notes DB? Otter/Granola
  synced into Notion? Manual notes in a doc?) — the source needs to be real before this can run

## Calibration notes

_(add findings here after the first week of real runs — dedup logic especially will need tuning)_
