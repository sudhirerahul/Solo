# Weekly Time Audit

**Surface:** Cowork scheduled task
**Cadence:** Weekly, Friday afternoon (reflect on the week just finished)
**Sources:** Google Calendar
**Output:** Doc or Slack message to the Principal, plus a running log in Notion (`[CONFIGURE]` DB)

## Prompt

> Review the past week's calendar. Categorize time spent into: SFP founder 1:1s, investor/partner calls,
> podcast production (recordings, prep, editing coordination), event/dinner logistics, internal ops, and
> media/community (everything else public-facing). Podcast production covers only work on an episode
> itself (booking, recording, editing/production coordination); once an episode is recorded, any
> downstream public-facing distribution of it (social clips, promo posts, newsletter mentions) counts as
> media/community instead, even though it's podcast-adjacent — don't split the same piece of work across
> both categories depending on who's in the room. Give a rough percentage breakdown. Then flag anything
> that could plausibly be delegated to the CoS or cut next week — be specific about which meeting and why
> (recurring with no clear decision made in the last 3 occurrences, attendee overlap with another meeting,
> no prep material was ever requested for it, etc.). Don't flag founder 1:1s or investor calls as
> cuttable by default — those are the Principal's core leverage; only flag them if there's a concrete
> reason (e.g., a founder 1:1 that's become a status-update the CoS could collect instead).

## Config

- `[CONFIGURE]` Notion DB (or doc) to append the weekly breakdown to, so trends are visible over time
- `[CONFIGURE]` Category list above should be reviewed after month 1 — add/merge categories once real
  calendar data shows what's actually eating time

## Calibration notes

**2026-07-26 — synthetic dry run (no real Calendar data exists yet for this automation; connector not
authorized this session, see `tasks/todo.md`).** Built `cowork/fixtures/sample-week-calendar.md` (a
synthetic Mon–Fri week, all 6 categories, 1,230 minutes of scheduled time) and manually executed this
prompt against it as-written; full output and guardrail verification in
`cowork/fixtures/dry-run-weekly-time-audit-2026-07-26.md`. Findings:

- Percentage-breakdown math was independently re-derived from the fixture's day-by-day tables (not its
  own pre-summed rollup) and matched exactly — 210/210/300/150/210/150 minutes across the 6 categories,
  summing to 1,230.
- The "don't flag founder 1:1s/investor calls as cuttable by default" rule was tested with a same-category
  control pair — two weekly recurring founder 1:1s, one with 3 straight real decisions (correctly left
  unflagged) and one with 3 straight status-update-only occurrences (correctly flagged, citing the
  prompt's own worked example) — and held up; recurrence alone did not trigger a false-positive flag.
- Found and fixed a real gap: the prompt gave no rule for podcast-adjacent public-facing distribution work
  (social clip review, short-form content recording from an already-taped episode) — it could plausibly
  land under either "podcast production" or "media/community" depending on who ran the dry run, silently
  shifting the reported percentages by up to ~7% of the week. Fixed by adding an explicit boundary rule to
  the prompt above: podcast production covers only work on the episode itself; downstream distribution is
  media/community.
- The 3 cut/delegate reasons named in the prompt (no-decision-in-3-occurrences, attendee overlap,
  no-prep-material) were each exercised by a distinct fixture meeting and each correctly flagged.

Still needed before this can run for real: live Calendar connector authorization, and the `[CONFIGURE]`
Notion DB URL for the running trend log — neither resolved by this dry run.
