# Open Commitments Digest

**Surface:** Cowork scheduled task
**Cadence:** Weekly, Monday morning
**Sources:** Notion (commitments tracker from post-meeting-action-extraction)
**Output:** Slack message to the Principal / CoS

## Prompt

> Review the commitments tracker. Flag anything overdue (deadline has passed, status still "Open") and
> anything unowned (no clear owner logged, or owner is ambiguous). Group overdue items by owner so a
> single nudge can cover everything one person is behind on. Produce a short list of who needs a nudge
> this week and on what, ordered by how overdue or how consequential the commitment looks (a commitment
> blocking a founder vs. an internal nice-to-have). Every item in the list must cite its source meeting,
> not just the overdue/unowned ones — the point is a ten-second lookup, and that only works if the
> citation is on every row. Do not draft the nudge messages themselves here — that belongs to whoever owns
> follow-through; this is a digest, not an outreach tool.

## Config

- `[CONFIGURE]` Notion DB URL (same tracker as post-meeting-action-extraction.md)
- `[CONFIGURE]` Delivery destination — Slack DM to Principal, or a shared `#cos` channel

## Calibration notes

[2026-07-25] Ran against the synthetic tracker built for `post-meeting-action-extraction.md`'s
calibration (7 rows, labeled Notion sandbox, see `eval/post-meeting-action-extraction/`).
Independently verified: overdue set (4/4) and unowned set (1/1) both matched an independently
recomputed answer, grouping by owner was correct, and no outreach/nudge text was drafted. One real
gap found: the digest cited the source meeting only for the unowned item, not for the four overdue
entries — fixed in the prompt text above (every item now must cite its source meeting). Re-test
this specific fix before trusting citation coverage.
