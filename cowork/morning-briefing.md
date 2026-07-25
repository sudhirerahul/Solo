# Morning Briefing

**Surface:** Cowork scheduled task
**Cadence:** Daily, 7:00am PT (before the Principal's first meeting)
**Sources:** Google Calendar, Gmail, Slack
**Output:** Slack DM or `#cos` channel message to the Principal

## Prompt

> Pull today's calendar. Flag any back-to-back meetings with less than 10 minutes between them, and any
> double-bookings. For each meeting, note whether it needs prep material (an SFP founder 1:1, an investor
> or operator meeting, a podcast recording) or is routine (internal sync, recurring standing meeting) —
> and for anything needing prep, check Gmail/Slack for related threads and surface anything unread that's
> relevant. Close with the two or three things today that only the Principal can do — meetings or
> decisions no one else on the team can substitute for — and name why each one specifically requires them.
> If nothing today rises to that bar, say so rather than manufacturing three items.

## Config

- `[CONFIGURE]` Slack destination (channel or DM) for delivery
- `[CONFIGURE]` Which calendar(s) count — Principal's primary only, or shared SFP/event calendars too
- `[CONFIGURE]` Definition of "needs prep" may need tuning after week 1 — some recurring meetings (e.g.
  weekly founder office hours) may always need a quick glance even if "routine"

## Calibration notes

_(add findings here after the first week of real runs)_
