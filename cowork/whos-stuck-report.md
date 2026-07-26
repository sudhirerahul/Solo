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
> Every quoted or summarized signal in the shared-style report must carry a permalink and a date. This
> requirement applies to the shared report only — the privacy-routed DM to the Principal (personal,
> health, or legal cases) must NOT include a permalink or direct link to the source note. Cite it in
> general terms instead (e.g., "per 1:1 notes, [owner], [date]") — a permalink is a durable, forwardable
> pointer, and attaching one to a "minimal detail" DM would let it be followed straight back to the exact
> sensitive note the redaction was meant to avoid leaking.
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
- `[2026-07-26]` Dry-run against a real, persisted fixture — `cowork/fixtures/sample-cohort-activity.md`
  (7 fictional founders, 1 roster of record, Slack + Notion activity shaped like the real sources) — full
  output and guardrail verification in `cowork/fixtures/dry-run-whos-stuck-report-2026-07-26.md`. All
  branches resolved cleanly and distinguishably: blocked-beats-quiet precedence correctly picked Blocked
  for a founder who independently qualified for both (Devrim Aksoy — stated fundraising obstacle plus an
  11-day activity drop); the no-coverage founder (Marcus Webb) was reported in his own bucket and never
  folded into quiet; the baseline-required rule was honored for a founder with no established cadence yet
  (Tobias Reyes got the literal `baseline unknown — not flagged`, no default guessed); and the
  personal/health founder (Amara Njoku) was fully excluded from the shared report and routed to a private,
  minimal-detail escalation. This run also closed the previously-open ambiguity about whether the
  "permalink and date" sourcing rule applies to the privacy-routed escalation: it's now scoped to the
  shared report only (see the prompt text above) — the private DM cites a named source and date but no
  clickable permalink, since a permalink there would itself be a forwardable leak vector back to the
  sensitive note.
- `[2026-07-25]` Opus review caught 2 real logic gaps in the initial hardening pass, both fixed: (1) the
  three buckets could overlap with no precedence rule (a founder both citing an obstacle and going quiet
  fit two buckets at once) — added blocked-beats-quiet precedence, and clarified no-coverage requires
  absence from every source, not just Slack; (2) this file had no roster-of-record clause unlike its
  sibling, so a founder with zero presence anywhere could never actually be enumerated into no-coverage —
  added the same roster-of-record rule.
