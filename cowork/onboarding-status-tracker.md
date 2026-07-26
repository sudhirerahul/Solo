# Onboarding Status Tracker

**Surface:** Cowork scheduled task (or Routine, if the cohort checklist is repo-tracked instead of Notion)
**Cadence:** Weekly during a cohort ramp, stepping up to 2x/week in the final week before cohort start
**Sources:** Notion (cohort onboarding checklist), Gmail
**Output:** Slack message to the Principal / CoS

## Prompt

> Preflight: if the cohort start date or the onboarding-checklist database is not resolved and accessible,
> output exactly `CANNOT RUN — missing <field>` and stop. Never infer or estimate a start date. This
> abort is at the cohort/database level only — a single founder's own checklist page being missing or
> incomplete is never a report-level abort trigger; it degrades to `unknown` for that founder's items
> (see below), and that founder still appears in the report.
>
> Enumerate founders from the roster of record (the authoritative cohort list) — never from whoever
> happens to have recent Notion/Gmail activity. A founder with zero activity is still on the list if the
> roster says so, including a founder who has no checklist-DB page at all: report all of that founder's
> items as `unknown` rather than omitting them from the report.
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
> (longest-pending first) — a founder with no dated item at all (e.g. no checklist page or Gmail activity
> exists for them) sorts as if maximally stale, ahead of every dated founder at the same count, never
> treated as freshest for lack of data; (3) founder name, alphabetically, as final tiebreaker.
>
> If no one is behind, say so plainly ("No one is behind this week") — do not omit the report.
>
> Every reported status must carry a source link (Notion page or Gmail thread) and a date. If a status has
> no source, it must be reported as `unknown`, never asserted.
>
> Any SAFE or legal-related item that looks ambiguous or contentious routes to escalation — flag it to the
> Principal directly via DM, never present it as a routine line in the shared status report. That item
> still counts toward the founder's pending-or-unknown total and the founder still appears in the flagged/
> sorted list on that basis — only the item's own detail is withheld from the shared report, never the
> founder's presence on the list. The same escalate-and-withhold handling applies to any pending item whose
> underlying source discloses a personal or health-related reason for the delay: report the item generally
> in the shared report (e.g. "pending, personal reason cited — not detailed here") and separately flag the
> specifics to the Principal directly via DM — never quote the sensitive detail verbatim in the shared
> status report.

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
- `[2026-07-26]` Real, persisted dry run against `cowork/fixtures/sample-cohort-onboarding-checklist.md`
  (9-founder synthetic cohort, roster-of-record + checklist DB) — full output and guardrail verification
  in `cowork/fixtures/dry-run-onboarding-status-tracker-2026-07-26.md`. This replaces the earlier
  scratchpad-only dry-run reference, which had no persisted fixture behind it. Sort/bucket logic (count
  descending, oldest-date ascending, name alphabetical), the wide-vs-tight threshold split, and the
  `unknown`-vs-`pending` distinction all checked out correctly against the fixture. Four gaps were found
  and fixed directly in the prompt text above: (1) the preflight `CANNOT RUN` clause didn't explicitly say
  a single founder's missing checklist page degrades to per-item `unknown` rather than a report-level
  abort — now stated explicitly; (2) no privacy/redaction rule existed for a pending item whose source
  discloses a personal/health reason for the delay — now routes the same way SAFE/legal ambiguity does
  (general description in the shared report, specifics escalated directly); (3) the sort spec didn't say
  what happens when a founder has no dated item at all (e.g. zero checklist-DB activity) — now defined as
  maximally stale, never treated as freshest for lack of data; (4) it was unclear whether an escalated
  SAFE/legal item still counts toward a founder's pending-or-unknown total and flagged-list presence — now
  explicit that it does; only the item's own detail is withheld, never the founder's presence on the list.
- `[2026-07-25]` Opus review caught 2 real logic gaps in the initial hardening pass, both fixed: (1) the
  original tiebreaker (days remaining until cohort start) was a no-op since it's identical for every
  founder in one cohort — replaced with oldest-outstanding-item-date then founder name; (2) "behind" was
  only defined inside the 7-day pre-start window, so earlier in a ramp the report could never flag anyone
  no matter how stuck they were — added a wider 3+-items threshold for the full ramp, tightening to 2+
  inside 7 days.
