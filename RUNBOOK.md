# Runbook — How to Actually Turn On Each Automation

This is the operational companion to `CLAUDE.md` (which explains *what* each automation is and *why*).
This file is the step-by-step for *how to actually run it* — what to paste where, what to configure first,
and what to expect the first time it fires. Read `CLAUDE.md`'s automation catalog and guardrails first if
you haven't; this doc assumes that context.

**Current reality (2026-07-26):** there is no real Solo Founders Program Slack or Notion workspace
connected anywhere — confirmed directly, not a temporary wrong-workspace issue (see `tasks/todo.md`'s
"Correction" note). Every automation below that reads Notion or Slack has an explicit preflight that
outputs `CANNOT RUN — missing <field>` and stops rather than fabricating, if you turn it on before that
data source is real. That's correct, designed behavior — not a bug to work around.

---

## Part A — Cowork scheduled tasks (11 of 13 automations)

### One-time steps, done once per automation you stand up

1. Open the file in the **"File"** column below.
2. Copy the exact text under that file's **"## Prompt"** section (the `>` blockquote) — nothing more,
   nothing less.
3. In Cowork, create a new scheduled task. Paste the prompt in as the task instructions.
4. Set the cadence to the **"Cadence"** value below.
5. Connect the sources listed in **"Sources"** below to that task.
6. Resolve every `[CONFIGURE]` field listed below with a real value before turning the schedule on. If a
   field can't be resolved yet (most Notion/Slack ones can't, today), leave the schedule **off** rather than
   running it against a placeholder.
7. Follow the build order in `CLAUDE.md`: turn on **one new automation per week**, read every real output
   for that first week, and log anything surprising to `tasks/lessons.md`.

### Per-automation reference

| # | Automation | File | Cadence | Sources | `[CONFIGURE]` fields to resolve first | Will it run today? |
|---|---|---|---|---|---|---|
| 1 | Morning briefing | `cowork/morning-briefing.md` | Daily, 7:00am PT | Calendar, Gmail, Slack | Slack destination (channel/DM); which calendar(s) count | Calendar/Gmail parts can run now if those are your real accounts; Slack prep-check will just find nothing in a non-SFP workspace |
| 2 | Weekly time audit | `cowork/weekly-time-audit.md` | Weekly, Friday PM | Calendar | Notion DB/doc URL for the trend log | Yes, if Calendar is your real account — Notion logging will fail until the DB URL is set |
| 3 | Post-meeting action extraction | `cowork/post-meeting-action-extraction.md` | Per-meeting or daily batch | Notion (meeting notes), Slack | Notion DB URL for the commitments tracker (create it first); where meeting notes actually live | No — preflight-equivalent blocks without a real tracker DB |
| 4 | Open commitments digest | `cowork/open-commitments-digest.md` | Weekly, Monday AM | Notion (tracker from #3) | Notion DB URL (same tracker); delivery destination | No — depends on #3's tracker existing first |
| 5 | Onboarding status tracker | `cowork/onboarding-status-tracker.md` | Weekly during ramp, 2x/week final week | Notion (checklist DB), Gmail | Notion checklist DB URL; cohort start date | No — explicit `CANNOT RUN` preflight without both |
| 6 | "Who's stuck" report | `cowork/whos-stuck-report.md` | Weekly during active cohort | Notion (meeting notes), Slack | Which Notion DB / Slack channels count as "cohort"; per-founder baseline cadence | No real cohort source exists — will report everyone `no coverage` at best |
| 7 | RSVP and reminder tracking | `cowork/rsvp-reminder-tracking.md` | Scheduled around event dates | Gmail, Calendar, Notion (guest list) | Notion "Events — Guest List" DB URL; per-event venue capacity; Slack/DM destination for capacity flag | No — depends on the guest-list DB existing |
| 8 | Post-event follow-up drafts | `cowork/post-event-follow-up.md` | Day after each event | Notion (event notes), Gmail | Notion event-notes page/template location; Principal's name; sending account | No — depends on the event-notes page existing |
| 9 | Guest research one-pager | `cowork/guest-research-one-pager.md` | A few days before each recording | Web search, Gmail, Notion | Notion DB of past episode topics/guests | Partially — web search + Gmail lookup can run without Notion, but repeat-question avoidance won't work until the DB exists. Also needs manual **Run Input** (guest name, company/role, recording date) supplied each time — this one isn't a pure fire-and-forget schedule |
| 11 | Relationship staleness check | `cowork/relationship-staleness-check.md` | Weekly | Notion (CRM), Gmail, Calendar | Notion CRM DB URL; relationship-tier taxonomy; per-tier staleness thresholds | No — explicit `CANNOT RUN` preflight without the CRM DB |
| 13 | Daily rollup | `cowork/daily-rollup.md` | Daily, EOD (e.g. 6:30pm PT) | Calendar, Slack, Gmail | Slack destination; which Slack channels/Gmail labels are in-scope | Partially — will run, but reports Slack/Notion-shaped coverage as thin until real channels are scoped |

**Practical recommendation, per `CLAUDE.md`'s build order:** start with **#1 (morning briefing)** — it's
the one with the most real signal available today (Calendar + Gmail), it's fully dry-run calibrated, and
it degrades gracefully (it'll just find less to say about Slack prep material) rather than hard-failing.
Add the next one a week later, not before.

---

## Part B — Claude Code Routines (2 of 13 automations)

These run as GitHub Actions, not inside Cowork. Both need repo infrastructure that doesn't exist yet.

### One-time setup (needed before either Routine can fire) — **needs your explicit go-ahead**, not done yet

1. Create a GitHub remote for this repo and push to it.
2. Add the `ANTHROPIC_API_KEY` repository secret (Settings → Secrets and variables → Actions).
3. Install the Claude GitHub App: https://github.com/apps/claude
4. Enable **Settings → Actions → General → "Allow GitHub Actions to create and approve pull requests."**

### #10 — Show notes drafting

- **File:** `routines/show-notes-drafting/PROMPT.md` + `.github/workflows/show-notes-drafting.yml`
- **Trigger:** a push to `main` touching `transcripts/**`, or manual `workflow_dispatch` — no schedule to
  configure, it's event-driven.
- **To use it:** after the one-time setup above, commit a real episode transcript to `transcripts/`
  (matching the naming convention in `transcripts/README.md`) and push. A draft PR with the show notes
  should open automatically in `show-notes/`.
- All `[CONFIGURE]` markers in this one are already resolved — nothing else to fill in.

### #12 — SOP drift check

- **File:** `routines/sop-drift-check/PROMPT.md`
- **Trigger:** intended as a weekly schedule, but the exact trigger/schedule syntax for this Routine is
  **still unresolved** — that's an open `[CONFIGURE]` item, separate from the GitHub infra above.
- **Weekly input convention:** one hand-authored file per week (see the PROMPT.md for the exact path
  convention) containing meeting notes / Slack activity for how the team actually operated — this has to
  be supplied weekly, it isn't pulled live from anywhere.
- Needs the one-time GitHub setup above, plus the trigger config resolved, before it can fire on a schedule.

---

## Quick self-check before turning anything on

- [ ] Does the automation's `[CONFIGURE]` list above have every field resolved with a real value?
- [ ] Have you read that automation's fixture + dry-run output in `cowork/fixtures/` at least once, so you
      know what "working correctly" looks like before judging the first real output?
- [ ] Is this the *only* new automation you're turning on this week (per the one-per-week build order)?
- [ ] If it touches Notion/Slack and neither is real yet, are you prepared to see `CANNOT RUN` on the first
      run — and is that acceptable, or should it wait until real data exists?
