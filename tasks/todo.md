# Todo — Solo Founders CoS Automation Stack

## Done
- [x] Scaffold repo structure (`cowork/`, `routines/`, `tasks/`)
- [x] Write `CLAUDE.md` — company context, surface decision rule, automation catalog, guardrails
- [x] Draft all 12 Cowork prompt files (versioned source-of-truth, paste into Cowork's scheduling UI)
- [x] Scaffold 2 repo-based Routines (SOP drift check, show notes drafting)
- [x] `git init` done
- [x] Show Notes Routine built: workflow (`.github/workflows/show-notes-drafting.yml`) + prompt
  (`routines/show-notes-drafting/PROMPT.md`, all `[CONFIGURE]` markers resolved) + directory
  conventions (`transcripts/README.md`, `show-notes/README.md`)
- [x] Cowork show-notes variant retired (`cowork/show-notes-drafting.md` deleted; decision recorded
  in `routines/show-notes-drafting/PROMPT.md` and `CLAUDE.md`)
- [x] Item 9 (guest research one-pager) finalized and synthetic-dry-run tested on 2026-07-25 against
  `samples/guest-research-one-pager/` (fixture corpus + synthetic output); word-count-definition and
  source-date-requirement issues found in review were fixed in the same pass — see "Calibration notes"
  in `cowork/guest-research-one-pager.md`. Status updated to "Calibrating" in `CLAUDE.md`; still not
  live pending connector wiring.
- [x] Item 13 (daily rollup) hardened and dry-run tested on 2026-07-25 against the new
  `cowork/fixtures/sample-daily-rollup-day.md` fixture. Run as an explicit 3-stage pipeline at the user's
  request (Opus plan → Sonnet execute → Opus independent verify, per the orchestrator doctrine — verify
  stage re-read the actual files rather than trusting the execute stage's self-reported dry-run). Verify
  surfaced 3 real prompt-level gaps (message- vs. thread-level source links leaking a redacted sibling
  item; the privacy rule assuming a DM destination when the configured destination may be a shared
  channel; no stated default section for relayed/unverified items) — all three patched directly in the
  prompt afterward, not yet re-dry-run against the fixture post-patch. See "Calibration notes" in
  `cowork/daily-rollup.md`. Status updated to "Calibrating" in `CLAUDE.md`; still not live pending
  connector wiring (Slack still wrong workspace; Calendar not yet authorized in this session either).
- [x] Item 2 (weekly time audit) synthetic-dry-run tested on 2026-07-26 against the new
  `cowork/fixtures/sample-week-calendar.md` fixture (synthetic Mon–Fri week, all 6 categories, 1,230
  min). Percentage-breakdown arithmetic independently re-derived and verified correct; the
  "don't-flag-founder-1:1s/investor-calls-by-default" rule tested with a same-category control pair and
  held up (see `cowork/fixtures/dry-run-weekly-time-audit-2026-07-26.md`). One real gap found and fixed
  directly in the prompt: no rule existed for podcast-adjacent public-facing distribution work (social
  clips, batch content), which could silently land in either "podcast production" or "media/community" —
  added an explicit boundary rule. See "Calibration notes" in `cowork/weekly-time-audit.md`. Still not
  live — pending Google Calendar connector authorization and the `[CONFIGURE]` Notion DB URL for the
  trend log; catalog status in `CLAUDE.md` intentionally left as "Not stood up" (this was a dry run, not
  a live calibration pass).
- [x] Item 6 ("who's stuck" report) given a real persisted fixture and dry run on 2026-07-26, replacing
  the prior vague "scratchpad only" calibration note. New fixture: `cowork/fixtures/sample-cohort-activity.md`
  (7 fictional founders exercising every branch: blocked, quiet, no-coverage, correctly-not-flagged,
  no-baseline-yet, personal/health escalation, and a combined blocked+quiet founder). Dry run:
  `cowork/fixtures/dry-run-whos-stuck-report-2026-07-26.md`. All four explicitly-required checks passed:
  blocked-beats-quiet precedence resolved correctly (Devrim Aksoy), no-coverage founder (Marcus Webb)
  never folded into quiet, baseline-required rule honored (Tobias Reyes got `baseline unknown — not
  flagged`, no default guessed), and the personal/health escalation (Amara Njoku) leaked neither substance
  nor a permalink into the shared report. This run also **resolved** the open permalink-sourcing ambiguity
  previously flagged in `cowork/whos-stuck-report.md`'s Calibration notes: the permalink+date requirement
  is now explicitly scoped to the shared report only; the private DM escalation cites a named source
  (owner + date) with no clickable permalink, since a permalink there would itself be a forwardable leak
  vector. Prompt text updated accordingly. Status remains "Blocked — connector points at wrong workspace"
  in `CLAUDE.md` (unchanged, per instructions) — this is a dry run, not a live calibration pass.
- [x] Item 5 (onboarding status tracker) given a real persisted fixture and dry run on 2026-07-26,
  replacing the prior vague "scratchpad only" calibration note. New fixture:
  `cowork/fixtures/sample-cohort-onboarding-checklist.md` (9 fictional founders exercising every branch:
  wide 3+-threshold mid-ramp that later resolves, tight 2+-threshold near start, correctly-not-flagged,
  `unknown` vs. `pending` distinction, a Gmail cross-ref explaining a pending SAFE, a contentious
  SAFE/legal item requiring direct escalation, a roster-of-record founder with zero checklist-DB activity,
  a personal/health-sensitive pending item, and a three-way sort tie-break). Dry run:
  `cowork/fixtures/dry-run-onboarding-status-tracker-2026-07-26.md`. Sort order (count desc, oldest-date
  asc, name alpha), the wide/tight threshold split, and the `unknown`-vs-`pending` distinction all checked
  out correctly. Four gaps found and fixed directly in `cowork/onboarding-status-tracker.md`: (1) missing
  per-founder checklist page now explicitly degrades to per-item `unknown`, not a report-level abort; (2)
  new redaction rule routes personal/health-sensitive pending items the same way as SAFE/legal escalation;
  (3) a founder with no dated item at all now explicitly sorts as maximally stale, never as freshest for
  lack of data; (4) an escalated SAFE/legal item now explicitly still counts toward its founder's
  pending-or-unknown total and flagged-list presence — only the item's own detail is withheld. Status
  remains "Blocked — connector points at wrong workspace" in `CLAUDE.md` (unchanged) — this is a dry run,
  not a live calibration pass.
- [x] Item 1 (morning briefing) given its first-ever calibration on 2026-07-26 — previously had an empty
  Calibration notes section and no fixture at all. New fixture: `cowork/fixtures/sample-morning-briefing-day.md`
  (synthetic Calendar/Gmail/Slack snapshot exercising a back-to-back pair, a double-booking, a
  needs-prep/routine mix, and an unread thread relevant to each prep-needed meeting). Dry run:
  `cowork/fixtures/dry-run-morning-briefing-2026-07-26.md`, executed against the prompt exactly as it
  stood beforehand. Back-to-back and double-booking flags and the prep/routine split all fired correctly.
  One real gap found and fixed directly in the prompt: no privacy rule existed, so a founder's private,
  high-stakes personal disclosure (surfaced while checking Slack for 1:1 prep material) landed verbatim in
  the briefing body with no regard for a possibly-shared destination — same shape of gap
  `cowork/daily-rollup.md` hit before its own privacy fix. Added a withhold-and-flag rule, with an explicit
  business-sensitive-content carve-out so a legitimate investor concern in the same fixture still surfaces
  in full. Secondary gap also fixed: the routine/needs-prep split was binary with no handling for a
  recurring meeting carrying a real non-routine agenda item this week — added an explicit one-line-flag
  rule. See "Calibration notes" in `cowork/morning-briefing.md`.
- [x] Orchestrator re-ran item 1 (morning briefing) against the same fixture after the two fixes above,
  since the build pass had fixed the prompt but not re-verified it (see Section E of
  `cowork/fixtures/dry-run-morning-briefing-2026-07-26.md`). Confirmed the privacy fix closes the leak in
  both the meeting list and the closing "only you can" section — the worse of the two leak sites, since the
  unpatched run restated Devika Rao's disclosure there too — confirmed Ravi Chen's business-sensitive
  content is unaffected, and confirmed the recurring-meeting flag still fires. Guardrail check 5 now reads
  Pass, was Fail pre-patch.
- [x] `CLAUDE.md`'s catalog status column updated: items 1, 2, 5, 6, and 11 now all read "Calibrating
  (dry-run tested, pending live connector wiring)," matching items 7/8/9/13. Items 5, 6, and 11 previously
  read "Blocked — connector points at wrong workspace," which was accurate but obscured that all three
  already have full persisted synthetic dry-run treatment. Items 3 and 4 remain "Not stood up," untouched by
  this pass — see the eval section below for their separate outstanding items.

## Correction — there is no real Solo Founders Slack or Notion workspace

The user stated directly on 2026-07-26 that no real SFP Slack or Notion workspace exists to connect — this
is not the "wrong workspace, reconnect it" situation the "Open questions" section below was written to
describe. That section (and every "Blocked — connector points at wrong workspace" status this catalog
previously carried) assumed the real workspace exists somewhere and just isn't connected to this session
yet. That premise is now known to be false. Consequences:

- The synthetic-fixture-and-dry-run approach used for items 1, 2, 5, 6, 7, 8, 9, 11, 13 (and the eval
  approach for 3, 4, 12) is not a stopgap ahead of real data arriving — for as long as no real SFP
  Slack/Notion exists, it is the only calibration path available for any of these automations.
- Do not re-ask the user to "reconnect the correct workspace" without first confirming whether one now
  exists — the answer as of 2026-07-26 is that it does not.
- The "Open questions for the user — BLOCKER" section further below should be read in this light: real data
  arrives only if/when the user stands up an actual SFP Slack/Notion, or points these automations at
  wherever cohort/investor data actually lives (a spreadsheet, another tool) — not as a pending reconnection
  this session is waiting on.

## Next — show notes Routine (not done here, needs separate human go-ahead)
- [ ] Create a GitHub remote for this repo and push — **needs explicit human go-ahead**, not done as part of this change
- [ ] Add the `ANTHROPIC_API_KEY` repository secret
- [ ] Install the Claude GitHub App (https://github.com/apps/claude)
- [ ] Enable Settings → Actions → General → "Allow GitHub Actions to create and approve pull requests"
- [ ] Commit a first real transcript once live and confirm a draft PR opens as expected

## Next — rollout, one per week, per the build order in CLAUDE.md
- [ ] Fill in `[CONFIGURE]` placeholders throughout `cowork/*.md` and `routines/*` (Slack channel IDs, Notion DB URLs, calendar accounts, cohort tracker location, principal's name)
- [ ] Connect Cowork to Slack, Gmail, Calendar, Google Drive, Notion (do this in the Cowork UI — connectors can't be wired from this repo)
- [ ] Week 1: stand up `morning-briefing.md` OR `sop-drift-check` only (pick the lower-risk starting point) — run for a week, calibrate prompt against real output
- [ ] Week 2: add the next task per the build order — do not stand up more than one per week
- [ ] After each new automation runs 3-5 times, log any prompt corrections to `tasks/lessons.md`
- [ ] Item 5 (onboarding status tracker) — dry-run tested (see "Done" above), still pending real connector
- [ ] Item 6 ("who's stuck" report) — dry-run tested (see "Done" above), still pending real connector
- [ ] Item 11 (relationship staleness check) — dry-run tested 2026-07-25, still pending real connector

## Dry-run tested, out of sequence — items 7 and 8

Items 7 (RSVP and reminder tracking) and 8 (Post-event follow-up drafts) have already been dry-run
tested against synthetic fixture data — `cowork/fixtures/sample-dinner-event.md` and
`cowork/fixtures/dry-run-2026-07-25.md` — ahead of live connector authorization, and both prompts have
been hardened based on what that dry run surfaced (see "Calibration notes" in each prompt file). This
jumped the normal one-per-week build order at the user's explicit request, since these two are a natural
event-lifecycle pair (RSVP tracking feeds the guest list that post-event follow-up reads back from). They
are **not yet live** — status in `CLAUDE.md`'s automation catalog is "Calibrating (dry-run tested, pending
live connector wiring)" pending the `[CONFIGURE]` gaps listed below.

## Eval / calibration (synthetic, pre-production) — items 3 and 4

Post-meeting-action-extraction (item 3) and open-commitments-digest (item 4) have been calibrated
against a **synthetic** golden dataset ahead of real meeting data, since none exists yet — same
motivation as the item 7/8 dry run above, done because the prompt logic itself could be measured
without waiting on the connector blocker below.

- [x] Built synthetic golden dataset in `eval/post-meeting-action-extraction/` — 6 fixture meetings,
  7 ground-truth commitments, 1 negative case (`ground-truth.json`)
- [x] Created a clearly-labeled synthetic Notion sandbox (parent page `🧪 SYNTHETIC EVAL SANDBOX`,
  two databases, every row tagged `Data Source = Synthetic-Eval-v1`) — never used to fill the real
  `[CONFIGURE]` placeholders in either `cowork/*.md` file (confirmed unedited)
- [x] Ran extraction end-to-end; **independently verified** (not self-reported): 7/7 recall, 0
  fabricated rows, correct "no deadline given" and honest-unclear-owner handling, negative case
  correctly rejected
- [x] Re-ran extraction to test dedup: 0 new rows created on rerun — but this only tested the
  same-calendar-day case; a pre-seeded row dated several days earlier, checked by a fresh agent,
  is still needed before calling dedup fully trusted
- [x] Ran digest against the resulting tracker: overdue (4/4) and unowned (1/1) sets both correct;
  found the digest wasn't citing source meeting on overdue items — fixed in the prompt text
- [x] Logged findings to `tasks/lessons.md` and both prompt files' Calibration notes sections
- [ ] Re-test the two flagged gaps (older-dated dedup case, fresh-agent rerun; source-citation fix)
  before treating this pair as ready for a real-data pilot
- [ ] Once the connector blocker below is resolved and a real tracker/meeting-notes source exists,
  run these two against real data per the normal one-per-week build order — this synthetic pass
  does not substitute for that

## Open questions for the user — BLOCKER (connectors point at the wrong workspace)

**(a) What's actually connected right now:**
- Notion: an unrelated GovTech sales-intelligence workspace, plus unused starter templates. No SFP content.
- Slack: `claude-c1p4553.slack.com` — 3 channels (#social, #new-channel, #all-claude), all empty except
  join events. No founder activity.
- Neither is the real Solo Founders Program workspace. Confirmed by direct connector query this session
  (2026-07-25) — do not re-assume these are live SFP sources without re-checking.
- Re-confirmed this session specifically for the investor/partner CRM (item 11): searched Notion for
  "investor partner CRM contact list" and "Solo Founders Program" — zero relevant hits, same blocker.

**(b) What unblocks it:** the user needs to either (1) connect the correct SFP Notion/Slack workspaces to
this session, or (2) tell us where cohort data actually lives if not Notion/Slack.

**(c) Exact fields still needed once unblocked:**
- [ ] Cohort onboarding-checklist Notion DB URL
- [ ] Current cohort start date
- [ ] Founder roster of record (source of truth for who's "in" this cohort)
- [ ] Slack channel ID(s) that count as cohort-active
- [ ] Principal's name / preferred DM target for these two reports

**(d) Additional fields needed for items 7 and 8** (RSVP tracking, post-event follow-up) — surfaced during
dry-run testing, see `cowork/fixtures/dry-run-2026-07-25.md` Section D:
- [ ] Notion DB URL for the "Events — Guest List" database (guest-list source for item 7)
- [ ] Notion event-notes page location / template link (per-event notes source for item 8)
- [ ] Sending Slack/Gmail account for thank-you drafts (item 8)
- [ ] Slack channel or DM destination for the RSVP capacity flag (item 7)
- [ ] Per-event venue capacity — confirm this is actually supplied at schedule time per event rather than
  hardcoded (item 7)
- Principal's name is already tracked in (c) above — it's also the value item 8 needs; no separate ask.

**(e) Additional fields needed for item 11 (relationship staleness check):**
- [ ] Investor/partner CRM Notion DB URL (with last-touchpoint data), or confirmation it needs to be built
- [ ] Relationship-tier taxonomy (e.g. lead investor / casual advisor / operator peer) and per-tier
  staleness thresholds
