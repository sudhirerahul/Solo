# "Who's Stuck" Report

**Surface:** Cowork scheduled task
**Cadence:** Weekly during an active cohort
**Sources:** Notion (meeting notes), Slack
**Output:** Slack message to the Principal / CoS

## Prompt

> Enumerate founders from the roster of record (the authoritative cohort list) — never only from whoever
> happens to show up in Slack or Notion. A founder absent from every scanned source is still on the list
> if the roster says so, and must be reported, not silently skipped.
>
> Scan recent notes and Slack mentions from current SFP cohort founders. Sort every founder into exactly
> one of three buckets — if a founder's signals could fit more than one, **blocked takes precedence over
> quiet** (a stated obstacle is a stronger signal than reduced activity), and either takes precedence over
> no-coverage the moment ANY source shows presence:
> - **blocked** — mentioned a specific obstacle (technical, hiring, fundraising, personal) without a
>   stated next step, in any scanned source.
> - **quiet** — present in at least one scanned source but activity has dropped off versus their own
>   baseline, and no blocked-type signal was found.
> - **no coverage** — absent from every scanned source (no Slack activity in any cohort channel, no
>   Notion presence at all). Report this distinctly from "quiet" — "quiet" implies presence without
>   recent activity; "no coverage" means we can't observe them at all, which is a different problem (fix
>   the source list, don't assume they're fine).
>
> For every **quiet** flag, state the baseline it's being compared against, inline (e.g., "no posts in 14
> days vs. their usual ~3/week"). If no baseline exists yet for a founder, output `baseline unknown — not
> flagged` instead of guessing a default — never flag on absolute volume alone.
>
> For each flagged founder (blocked or quiet), quote or summarize the specific signal that triggered the
> flag (don't just say "seems stuck" — say what was actually said or what activity dropped off) and
> suggest who on the team is best positioned to check in, based on who they've worked with most closely.
> Treat blocked and quiet differently in the suggested action: a blocked founder needs a substantive
> check-in; a quiet founder might just need a casual ping; a no-coverage founder needs the source gap
> fixed before anything else.
>
> If the flagged signal involves a personal, health, or legal matter, do not include full detail in the
> shared-style report. Instead route it to the Principal directly, DM-style, minimal detail: name the
> founder and recommend a private check-in, without repeating the sensitive substance.
>
> Every quoted or summarized signal (in the shared report) must carry a permalink and a date.
>
> If no one is flagged this week, say so plainly rather than omitting the report.

## Config

- `[CONFIGURE]` Notion DB / Slack channels that count as "cohort" sources (which channels are founders
  actually active in?) — cannot currently be resolved: the connected Slack/Notion workspaces have no SFP
  content. See `tasks/todo.md` for the full blocker record.
- `[CONFIGURE]` "Usual cadence" baseline will need calibration per founder — some are naturally quieter
  than others; don't flag on volume alone once real data shows the range

## Calibration notes

_(add findings here after the first few runs — false positives on naturally-quiet founders are the main
risk to watch for)_

- `[2026-07-25]` Connector blocker discovered — connected Slack workspace (claude-c1p4553.slack.com) has
  zero founder activity; see `tasks/todo.md`. Prompt hardened (three-bucket blocked/quiet/no-coverage
  split, baseline-required, privacy routing) ahead of real data becoming available.
- Dry-run against synthetic fixture (scratchpad only, not real data): the three-bucket split, the
  baseline-required quiet-flag rule, and the empty-result line all resolved cleanly and stayed
  distinguishable across test cases (no-coverage founder never got folded into quiet; a within-baseline
  founder correctly went unflagged with the baseline stated inline). One ambiguity worth closing before
  real data arrives: unclear whether the "permalink and date" sourcing requirement applies to the
  privacy-routed escalation copy or only to the shared-style report — attaching a raw permalink to a
  "minimal detail" DM could itself leak the sensitive content the redaction was meant to avoid; should be
  scoped to the shared report only.
