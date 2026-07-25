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
> blocking a founder vs. an internal nice-to-have). Do not draft the nudge messages themselves here — that
> belongs to whoever owns follow-through; this is a digest, not an outreach tool.

## Config

- `[CONFIGURE]` Notion DB URL (same tracker as post-meeting-action-extraction.md)
- `[CONFIGURE]` Delivery destination — Slack DM to Principal, or a shared `#cos` channel

## Calibration notes

_(add findings here after the first few runs)_
