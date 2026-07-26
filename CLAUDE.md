# Solo Founders — Chief of Staff Automation Stack

## What this repo is

This is the operating system for a Claude-built Chief of Staff function at **Solo Founders** — the
company building the institution around solo founding (community, capital, support system, software,
infrastructure). See `solofounders.com` and `solofounders.com/report` for the "why now" thesis.

The Principal runs the Solo Founders Program (SFP), meets founders/operators/investors, hosts the
**Solo Founders Podcast**, organizes dinners and events, and builds the broader solo-founder community.
The Principal's time is the constraint on how many founders get helped. Everything in this repo exists
to take that constraint off: throughput on people, follow-through, and software so nothing drops.

This repo is the **source of truth for prompts and process**, even though most of the actual execution
happens inside Cowork (connector-driven) rather than in this git history. Version prompts here so they
can be diffed, improved, and reviewed like code — then paste the current version into Cowork's scheduling
UI, or wire the repo-based ones up as Claude Code Routines.

`[CONFIGURE]` markers throughout this repo and its prompt files mark placeholders that need real values
(Slack channel IDs, Notion DB URLs, the Principal's name, etc.) before an automation is live. Fill these
in before scheduling — don't let Claude guess at them.

Claude Code Routines in this repo are implemented as GitHub Actions workflows using Anthropic's
published `anthropics/claude-code-action@v1` (https://code.claude.com/docs/en/github-actions),
triggered on a relevant repo event (e.g. a transcript commit) and opening a draft PR for human
review. They are **not** the same as the `CronCreate` tool available inside an interactive Claude
Code session — that tool is session-only, in-memory, and auto-expires after 7 days, so it cannot
back durable, always-on repo automation.

## Two execution surfaces — which one, and why

| | Cowork scheduled tasks | Claude Code Routines |
|---|---|---|
| **Trigger** | Schedule, run inside Cowork | Schedule, API call, or GitHub event |
| **Data source** | Connectors: Slack, Gmail, Calendar, Google Drive, Notion | Whatever's in the repo (docs, transcripts, notes committed to git) |
| **Output** | Slack messages, drafts, docs, reports | Commits, PRs, files in the repo |
| **Use for** | Anything that needs live state from Slack/Gmail/Calendar/Notion — i.e. nearly everything below | Only work that's naturally document/process-driven and worth tracking in git history |

**Default to Cowork.** Reach for a Routine only when the artifact belongs in git (a versioned SOP, a
transcript-to-shownotes pipeline where the transcript already lives in the repo) — that's exactly two of
the thirteen automations below (SOP drift check, show notes drafting), and only if transcripts/SOPs are
actually stored in a repo rather than Notion/Drive. For show notes drafting this is now settled: transcripts
are confirmed repo-committed (see `transcripts/README.md`), so SOP drift check remains the only still-unconfirmed one.

Both surfaces are beta / research preview as of mid-2026. Run limits and behavior may shift — treat every
prompt here as a calibration starting point, not a finished product. **Test manually before trusting any
automation with something time-sensitive** (an investor check-in, an RSVP deadline), and watch the first
few real outputs closely.

## Automation catalog

Full prompt text for each lives in `cowork/<name>.md` or `routines/<name>/PROMPT.md`. This table is the
index — status tracks whether it's live, calibrating, or not yet stood up.

| # | Automation | Surface | Cadence | File | Status |
|---|---|---|---|---|---|
| 1 | Morning briefing | Cowork | Daily, AM | `cowork/morning-briefing.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 2 | Weekly time audit | Cowork | Weekly | `cowork/weekly-time-audit.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 3 | Post-meeting action extraction | Cowork | Per-meeting or daily batch | `cowork/post-meeting-action-extraction.md` | Not stood up |
| 4 | Open commitments digest | Cowork | Weekly | `cowork/open-commitments-digest.md` | Not stood up |
| 5 | Onboarding status tracker | Cowork | Weekly during cohort ramp | `cowork/onboarding-status-tracker.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 6 | "Who's stuck" report | Cowork | Weekly during active cohort | `cowork/whos-stuck-report.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 7 | RSVP and reminder tracking | Cowork | Scheduled around event dates | `cowork/rsvp-reminder-tracking.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 8 | Post-event follow-up drafts | Cowork | Day after each event | `cowork/post-event-follow-up.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 9 | Guest research one-pager | Cowork | Few days before each recording | `cowork/guest-research-one-pager.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 10 | Show notes drafting | Routine | After each episode | `routines/show-notes-drafting/PROMPT.md` + `.github/workflows/show-notes-drafting.yml` | Built, inert — needs GitHub remote, ANTHROPIC_API_KEY secret, Claude GitHub App installed, and the "Allow GitHub Actions to create and approve pull requests" repo setting |
| 11 | Relationship staleness check | Cowork | Weekly | `cowork/relationship-staleness-check.md` | Calibrating (dry-run tested, pending live connector wiring) |
| 12 | SOP drift check | Routine | Weekly | `routines/sop-drift-check/PROMPT.md` | Calibrating — dry-run only vs. synthetic fixture; trigger + weekly-input wiring pending (see tasks/todo.md) |
| 13 | Daily rollup | Cowork | Daily, EOD | `cowork/daily-rollup.md` | Calibrating (dry-run tested, pending live connector wiring) |

## Build order — do not stand up all of this at once

1. Pick **one** low-risk, high-value task to start: the morning briefing or the SOP drift check.
2. Let it run for a week. Read every output. Calibrate the prompt against what it actually surfaces —
   real Slack/Notion/Calendar content will expose gaps a hypothetical prompt can't.
3. Add exactly one new task per week from here. Update the status column above as each goes live.
4. A stack of 5-10 tasks working well together is the target — that takes real iteration across weeks,
   not a single setup session. Resist the urge to turn all thirteen on immediately.
5. Log every prompt correction to `tasks/lessons.md` (format: `[date] | what went wrong | rule to prevent it`)
   so the next calibration pass doesn't relearn the same thing.
6. Exception on record: automations #7 and #8 (RSVP and reminder tracking, post-event follow-up drafts)
   were dry-run tested and hardened together, out of the normal one-per-week sequence, at the user's
   explicit request — they're a natural event-lifecycle pair. See `cowork/fixtures/dry-run-2026-07-25.md`.
   This isn't a silent violation of rule 3 above; both remain "Calibrating," not live, until connectors are
   wired.

## Guardrails (apply to every automation in this stack)

- **Never auto-send anything externally facing.** Thank-you notes, investor check-ins, founder nudges —
  always draft, never send. A human (the Principal or CoS) reviews and hits send.
- **Never fabricate.** No invented commitments, deadlines, founder names, metrics, or "who said what."
  If a source document is ambiguous or missing, say so in the output rather than filling the gap.
- **Cite the source.** Every extracted commitment, flagged staleness, or drift finding should point back
  to where it came from (which meeting note, which Slack thread, which doc) so it can be verified in ten
  seconds.
- **Voice**: curious, specific to the source, grounded — never generic corporate output. This applies to
  drafts (thank-you notes, check-ins) especially; a generic draft is worse than no draft.
- **Escalate, don't guess**, on anything that reads as high-stakes: a founder who seems more than "stuck,"
  an investor relationship that reads as actually damaged rather than just stale, a SAFE or legal detail.
- **Human-in-the-loop by default** for anything touching real people's time or money (event capacity,
  investor outreach, cohort onboarding blockers).

## Repo structure

```
CLAUDE.md                          this file
RUNBOOK.md                         step-by-step: how to actually turn on each automation (what to paste
                                    where, what to configure first, what to expect on first run)
tasks/
  todo.md                          current build-order state, open questions
  lessons.md                       corrections log — read at every session start
cowork/                            versioned prompt source for Cowork scheduled tasks (paste into Cowork UI)
  morning-briefing.md
  weekly-time-audit.md
  post-meeting-action-extraction.md
  open-commitments-digest.md
  onboarding-status-tracker.md
  whos-stuck-report.md
  rsvp-reminder-tracking.md
  post-event-follow-up.md
  guest-research-one-pager.md
  relationship-staleness-check.md
  daily-rollup.md
  fixtures/                        synthetic mock data for dry-running Cowork prompts before connectors are live
    sample-dinner-event.md
    sample-investor-partner-crm.md
    sample-daily-rollup-day.md
    sample-morning-briefing-day.md
    sample-week-calendar.md
    sample-cohort-onboarding-checklist.md
    sample-cohort-activity.md
    dry-run-2026-07-25.md            RSVP tracking, post-event follow-up, relationship staleness check
    dry-run-morning-briefing-2026-07-26.md
    dry-run-weekly-time-audit-2026-07-26.md
    dry-run-onboarding-status-tracker-2026-07-26.md
    dry-run-whos-stuck-report-2026-07-26.md
routines/                          repo-based Claude Code Routines
  sop-drift-check/PROMPT.md
  show-notes-drafting/PROMPT.md
.github/workflows/
  show-notes-drafting.yml          GitHub Actions workflow implementing the show-notes-drafting Routine
transcripts/                       episode transcripts committed to this repo (triggers show-notes-drafting)
show-notes/                        drafted show notes, paired 1:1 by basename with transcripts/
samples/                           synthetic dry-run test fixtures/outputs for the two automations below
  guest-research-one-pager/        fixture corpus + synthetic output for the guest research one-pager (#9)
  show-notes-drafting/             fixture transcript + synthetic output for show notes drafting (#10)
```

## Session start (per global workflow)

1. Read `tasks/lessons.md` — apply all lessons before touching anything.
2. Read `tasks/todo.md` — understand current build-order state and open questions.
3. Check the automation catalog status column above against what's actually live in Cowork before
   assuming a prompt file here is the one currently running (Cowork prompts can drift from this repo if
   edited directly in the Cowork UI — treat that as a real risk and reconcile when noticed).
4. Verify connected MCP workspaces (Slack team domain, Notion top-level page/database titles) actually
   belong to Solo Founders Program before treating any connector-derived data as real — do this before
   trusting output from any data-dependent automation or recon task.
