# Todo — Solo Founders CoS Automation Stack

## Done
- [x] Scaffold repo structure (`cowork/`, `routines/`, `tasks/`)
- [x] Write `CLAUDE.md` — company context, surface decision rule, automation catalog, guardrails
- [x] Draft all 12 Cowork prompt files (versioned source-of-truth, paste into Cowork's scheduling UI)
- [x] Scaffold 2 repo-based Routines (SOP drift check, show notes drafting)

## Next — rollout, one per week, per the build order in CLAUDE.md
- [ ] Fill in `[CONFIGURE]` placeholders throughout `cowork/*.md` and `routines/*` (Slack channel IDs, Notion DB URLs, calendar accounts, cohort tracker location, principal's name)
- [ ] Connect Cowork to Slack, Gmail, Calendar, Google Drive, Notion (do this in the Cowork UI — connectors can't be wired from this repo)
- [ ] Week 1: stand up `morning-briefing.md` OR `sop-drift-check` only (pick the lower-risk starting point) — run for a week, calibrate prompt against real output
- [ ] Week 2: add the next task per the build order — do not stand up more than one per week
- [ ] After each new automation runs 3-5 times, log any prompt corrections to `tasks/lessons.md`
- [ ] Item 5 (onboarding status tracker) — blocked on connectors, see "Open questions" below
- [ ] Item 6 ("who's stuck" report) — blocked on connectors, see "Open questions" below

## Open questions for the user — BLOCKER (connectors point at the wrong workspace)

**(a) What's actually connected right now:**
- Notion: an unrelated GovTech sales-intelligence workspace, plus unused starter templates. No SFP content.
- Slack: `claude-c1p4553.slack.com` — 3 channels (#social, #new-channel, #all-claude), all empty except
  join events. No founder activity.
- Neither is the real Solo Founders Program workspace. Confirmed by direct connector query this session
  (2026-07-25) — do not re-assume these are live SFP sources without re-checking.

**(b) What unblocks it:** the user needs to either (1) connect the correct SFP Notion/Slack workspaces to
this session, or (2) tell us where cohort data actually lives if not Notion/Slack.

**(c) Exact fields still needed once unblocked:**
- [ ] Cohort onboarding-checklist Notion DB URL
- [ ] Current cohort start date
- [ ] Founder roster of record (source of truth for who's "in" this cohort)
- [ ] Slack channel ID(s) that count as cohort-active
- [ ] Principal's name / preferred DM target for these two reports
