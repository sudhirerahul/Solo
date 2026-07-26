# Morning Briefing

**Surface:** Cowork scheduled task
**Cadence:** Daily, 7:00am PT (before the Principal's first meeting)
**Sources:** Google Calendar, Gmail, Slack
**Output:** Slack DM or `#cos` channel message to the Principal

## Prompt

> Pull today's calendar. Flag any back-to-back meetings with less than 10 minutes between them, and any
> double-bookings — if two meetings overlap and both name the Principal as the essential attendee, say so
> explicitly rather than silently assuming one takes priority; resolving it is a Principal-only decision,
> not something to guess at.
>
> For each meeting, note whether it needs prep material (an SFP founder 1:1, an investor or operator
> meeting, a podcast recording) or is routine (internal sync, recurring standing meeting). A recurring
> meeting stays labeled routine by default, but if this week's agenda (per Slack, Notion, or the calendar
> invite itself) includes something that isn't routine — a spend decision above the delegated-approval
> threshold, a contract or personnel sign-off — add a one-line flag naming that specific item rather than
> either treating the whole meeting as needing full prep or waving it through silently.
>
> For anything needing prep, check Gmail/Slack for related threads and surface anything unread that's
> relevant. If what's unread touches a personal, health, legal, immigration, or financial-distress matter —
> a founder's personal situation, not the business content of the meeting — do not put the substance in
> the briefing body, especially since this run's configured destination may be a shared channel rather than
> a direct message. Instead, note only that something personal came up ahead of that meeting and that the
> Principal should check the source directly himself; never quote or summarize the sensitive content into
> the briefing. Business-sensitive content relevant to a meeting (an investor's stated concern, a partner
> raising an issue) is not covered by this rule and should still be surfaced in full.
>
> Close with the two or three things today that only the Principal can do — meetings or decisions no one
> else on the team can substitute for — and name why each one specifically requires them. If nothing today
> rises to that bar, say so rather than manufacturing three items.

## Config

- `[CONFIGURE]` Slack destination (channel or DM) for delivery
- `[CONFIGURE]` Which calendar(s) count — Principal's primary only, or shared SFP/event calendars too
- `[CONFIGURE]` Definition of "needs prep" may still need tuning after a week of real runs — the prompt
  now flags a recurring meeting's real, non-routine agenda item with a one-line callout (see Prompt
  section above, added after the 2026-07-26 dry run); watch whether that one-line flag is enough in
  practice or whether some recurring meetings (e.g. weekly founder office hours) need to be reclassified
  as needing prep entirely.

## Calibration notes

- `[2026-07-26]` First-ever dry run for this automation (previously never calibrated, no fixture existed).
  Built `cowork/fixtures/sample-morning-briefing-day.md` (synthetic Calendar/Gmail/Slack snapshot for a
  fictional 2026-08-03) and manually executed the prompt exactly as it stood beforehand — see
  `cowork/fixtures/dry-run-morning-briefing-2026-07-26.md` for the full output and guardrail table. The
  back-to-back flag (5-minute gap, 8:30→8:35), the double-booking flag (an investor meeting vs. a podcast
  recording, 10:30–10:45 overlap), and the prep-vs-routine split all fired correctly against the fixture on
  the first pass.
- The dry run surfaced one real gap: the prompt had no privacy rule at all, so when it checked Slack for
  material relevant to a founder's 1:1, it surfaced her co-founder's departure and her doubts about
  continuing — a personal, high-stakes disclosure she'd explicitly asked to keep private — directly in the
  briefing body, with no regard for whether the configured destination is a shared `#cos` channel. This
  fails the "escalate, don't guess" guardrail in the same shape `cowork/daily-rollup.md` hit before its own
  2026-07-25 privacy-routing fix. Fixed directly in the Prompt section above: unread content touching a
  personal, health, legal, immigration, or financial-distress matter is now withheld from the briefing
  body and flagged by name only — business-sensitive content (the fixture's investor-concern email is the
  control case) is unaffected and still surfaces in full.
- Secondary finding, also fixed: the routine/needs-prep split was binary, so a recurring "routine" meeting
  with a real, non-routine agenda item this week (the fixture's Ops Weekly meeting carrying a contract
  sign-off above the delegated-approval line) had no defined handling — the dry run had to improvise a
  one-line callout with no prompt guidance to do so. Added an explicit rule so this isn't left to
  improvisation going forward.
- `[2026-07-26]` Re-run against the same fixture after the two fixes above (orchestrator-verified, not
  self-reported by the same pass that made the fixes) — see Section E of
  `cowork/fixtures/dry-run-morning-briefing-2026-07-26.md`. Confirmed: Devika Rao's disclosure no longer
  appears anywhere in the output, including the closing "only you can" section (the exact spot the
  original leak was worst); Ravi Chen's business-sensitive content still surfaces in full, so the carve-out
  didn't overcorrect; the recurring-meeting one-line flag still fires correctly. Guardrail check 5
  (escalate, don't guess) now reads Pass, was Fail pre-patch.
