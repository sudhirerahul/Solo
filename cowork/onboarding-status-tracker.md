# Onboarding Status Tracker

**Surface:** Cowork scheduled task (or Routine, if the cohort checklist is repo-tracked instead of Notion)
**Cadence:** Weekly during a cohort ramp, stepping up to 2x/week in the final week before cohort start
**Sources:** Notion (cohort onboarding checklist), Gmail
**Output:** Slack message to the Principal / CoS

## Prompt

> Preflight: if the cohort start date or the onboarding-checklist database is not resolved and accessible,
> output exactly `CANNOT RUN — missing <field>` and stop. Never infer or estimate a start date.
>
> Enumerate founders from the roster of record (the authoritative cohort list) — never from whoever
> happens to have recent Notion/Gmail activity. A founder with zero activity is still on the list if the
> roster says so.
>
> Check each incoming SFP founder's onboarding checklist: SAFE signed, housing confirmed (if applicable
> for this cohort), intro materials sent, kickoff call scheduled. For each founder, report status per item
> using four states — done / pending / blocked / unknown (no data) — and cross-reference Gmail for any
> outstanding thread (e.g. a SAFE sent but no reply in 5+ days) that explains a pending item. Use `unknown`
> whenever a source can't confirm status either way; never fold `unknown` into `pending` — pending means
> confirmed-not-done, unknown means we can't tell.
>
> Flag who's behind relative to the cohort start date: anyone with 3 or more items still pending-or-unknown
> at any point in the ramp, or 2 or more inside 7 days of start (the threshold tightens as start approaches
> — don't wait until the final week to flag someone who's been stuck the whole ramp). Sort the report by:
> (1) count of pending-or-unknown items, descending; (2) the oldest outstanding item's date, ascending
> (longest-pending first); (3) founder name, alphabetically, as final tiebreaker.
>
> If no one is behind, say so plainly ("No one is behind this week") — do not omit the report.
>
> Every reported status must carry a source link (Notion page or Gmail thread) and a date. If a status has
> no source, it must be reported as `unknown`, never asserted.
>
> Any SAFE or legal-related item that looks ambiguous or contentious routes to escalation — flag it to the
> Principal directly via DM, never present it as a routine line in the shared status report.

## Config

- `[CONFIGURE]` Notion DB URL for the cohort onboarding checklist — cannot currently be resolved: the
  connected Notion workspace has zero SFP content. See `tasks/todo.md` for the full blocker record.
- `[CONFIGURE]` Cohort start date, updated per cohort — cannot currently be resolved (same blocker).
- `[CONFIGURE]` Checklist items above are a best guess from the job posting language ("SAFE signed,
  housing confirmed, intro materials sent") — confirm the real checklist against what SFP actually tracks

## Calibration notes

_(add findings here after the first cohort ramp this runs during)_

- `[2026-07-25]` Connector blocker discovered — connected Notion workspace has zero SFP content; see
  `tasks/todo.md`. Prompt hardened (preflight abort, unknown-state, explicit sort, escalation routing)
  ahead of real data becoming available.
- Dry-run against synthetic fixture (scratchpad only, not real data) surfaced two ambiguities, sort/bucket
  logic itself checked out: (1) the preflight `CANNOT RUN` clause is worded at the cohort/database level,
  but doesn't explicitly say that a single founder's own checklist page being missing/incomplete should
  degrade to per-item `unknown` rather than being mistaken for a report-level abort trigger — worth stating
  explicitly; (2) this prompt has no privacy/redaction rule for cases where the underlying source for a
  pending item (a Gmail or Slack thread) states a personal/health reason for the delay — unlike the
  who's-stuck report, nothing here stops that detail from surfacing verbatim in a routine status line.
  Should likely route personal/health context the same way file 4 does, not just SAFE/legal ambiguity.
