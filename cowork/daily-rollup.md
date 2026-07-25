# End-of-Day State of Play

**Surface:** Cowork scheduled task
**Cadence:** Daily, end of day (e.g. 6:30pm PT)
**Sources:** Google Calendar, Slack, Gmail
**Output:** Slack message to the Principal

## Prompt

> Pull together what happened across calendar, Slack, and email today. Summarize into three sections:
> **Decisions made** (anything that was actually decided today, by whom), **Open threads** (things raised
> today that don't yet have a resolution or clear owner), and **What needs attention tomorrow morning**
> (anything time-sensitive enough that it should be the first thing looked at, not just everything open).
> Keep this tight — this is meant to be read in under two minutes at the end of a long day, not a
> comprehensive log. If a day was unusually quiet, say so rather than padding the sections.

## Config

- `[CONFIGURE]` Slack destination (DM to Principal, or `#cos` channel)
- `[CONFIGURE]` Which Slack channels/Gmail labels count as in-scope — scanning literally everything will
  produce noise; scope this down after the first week based on what's actually useful

## Calibration notes

_(add findings here after the first week of real runs)_
