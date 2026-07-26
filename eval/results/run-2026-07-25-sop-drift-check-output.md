# Run 2026-07-25 — SOP Drift Check — First Pass (Synthetic Dry Run)

**[SYNTHETIC] This entire document is a dry-run exercise against fabricated fixture data. No line below
describes real Solo Founders Program activity.**

Prompt applied: `routines/sop-drift-check/PROMPT.md` (post-2026-07-25 hardening pass — preflight,
synthetic-data gate, evidence rule, classification, status-column check, scope exclusion, silence rule).

SOP corpus read in full: `CLAUDE.md`, all eleven `cowork/*.md` files, both `routines/*/PROMPT.md` files,
and `tasks/lessons.md`.

Weekly input read: the two synthetic fixtures at
`eval/sop-drift-check/golden-weeks/01-week-of-2026-07-20-ops-sync-notes.md` and
`eval/sop-drift-check/golden-weeks/02-week-of-2026-07-20-slack-activity.md`, both frontmatter-tagged
`data_class: synthetic-fixture`.

This reasoning was done by reading the fixture prose and the real repo files directly and applying the
prompt's classification rules fresh — `eval/sop-drift-check/ground-truth.json` was **not** opened or
consulted while doing this pass. (Note for the record: this run's author also authored both fixture
files and the ground-truth file in the same build session, so close agreement between this output and
the ground truth is expected rather than surprising — the value of "not reading it during this step" is
in forcing the classification logic to be re-derived from the prompt's rules and the fixture text each
time, not in blind independence between two different people.)

## Findings

### Finding 1 — multiple automations stood up in one week, catalog not updated

- **SOP quote:** `CLAUDE.md`, `## Build order — do not stand up all of this at once`: "3. Add exactly
  one new task per week from here. Update the status column above as each goes live."
- **Observed:** `01-week-of-2026-07-20-ops-sync-notes.md`, Monday: "let's just turn all three on this
  week and see what happens... Agreed to stand each one up in Cowork directly rather than waiting for the
  usual one-per-week cadence, since none of them touch a blocked connector." Tuesday: morning briefing
  scheduled live. Wednesday: "Daily rollup scheduled live... All three (morning briefing, daily rollup,
  open commitments digest) are now turned on and running in Cowork as of today." Friday: "Nobody in this
  week's sync mentioned updating `CLAUDE.md`'s automation catalog status column for any of morning
  briefing, daily rollup, or open commitments digest — as of Friday the catalog still reads 'Not stood
  up' for all three."
- **Classification: (b) team drifted from a still-correct process — flag only, human call.** The stated
  rationale ("none of them touch a blocked connector") answers a different question than the one the
  one-per-week rule is actually protecting against — per the build order's own item 2, the rule exists so
  each new automation's real output gets read and calibrated before the next one is added, which is a
  capacity/attention constraint, not a connector-availability constraint. Nothing in the connector status
  of these three automations changes that rationale. This reads as an expedient shortcut, not a
  considered decision to retire the one-per-week rule — the SOP still looks correct as written.
- **Recommendation:** flag to the Principal/CoS as a process violation (two-part: skipped cadence, plus
  the separate failure to update the status column even after the fact) for a human call on whether to
  revert to sequential rollout or formally re-approve doing three at once going forward. Do not
  auto-edit `CLAUDE.md`.

### Finding 2 — relationship-staleness check auto-sent six investor emails

- **SOP quote:** `CLAUDE.md`, `## Guardrails`: "**Never auto-send anything externally facing.**
  Thank-you notes, investor check-ins, founder nudges — always draft, never send. A human (the Principal
  or CoS) reviews and hits send." Also directly contradicts `cowork/relationship-staleness-check.md`,
  `## Config`: "Check-in drafts are drafts only — a human sends."
- **Observed:** `02-week-of-2026-07-20-slack-activity.md`, 2026-07-20 11:14: "going to wire the digest
  step straight into a Gmail send so the check-in emails just go out once they're drafted." 2026-07-21
  09:02: "wired it up last night — digest run now pipes straight to Gmail send." 2026-07-23 16:40: "this
  week's relationship staleness run just fired — 6 investor check-in emails went out via the auto-send
  step, all landed fine."
- **Classification: (b) team drifted from a still-correct process — flag only, human call.** This is not
  a case where the new way is "clearly better" — never-auto-send is a guardrail that exists specifically
  because externally-facing sends to real investors carry irreversible reputational risk, and nothing in
  the fixture suggests the Principal signed off on retiring that guardrail. The stated motivation ("saves
  us re-copying them by hand") is a convenience argument, not a case for the guardrail being wrong.
- **Recommendation:** this is the highest-severity finding in this run and, in a live run, should be
  surfaced to the Principal directly rather than sitting only as one bullet among several in a PR
  description — six real investor emails sent without review is exactly the kind of thing the
  escalate-don't-guess guardrail exists for, even though the prompt's own three-way classification schema
  doesn't have a distinct "escalate" bucket beyond (b). Flag prominently; do not auto-edit anything.

### Finding 3 — morning-briefing prompt edited three times directly in Cowork UI, never back-ported

- **SOP quote:** `cowork/morning-briefing.md`, `## Prompt`: "Close with the two or three things today
  that only the Principal can do — meetings or decisions no one else on the team can substitute for —
  and name why each one specifically requires them. If nothing today rises to that bar, say so rather
  than manufacturing three items."
- **Observed:** `02-week-of-2026-07-20-slack-activity.md`, 2026-07-20 14:05: "the 'two or three things'
  line was too narrow... I widened it to five things instead of two or three." 2026-07-21 10:30: "also
  dropped the trailing line about saying so instead of manufacturing three items, it read as boilerplate."
  2026-07-22 08:15: third edit, wording cleanup. 2026-07-22 08:20, in response to "are these edits going
  back into the repo file": "just in Cowork for now, will circle back... at some point."
- **Classification: (b) team drifted from a still-correct process — flag only, human call.** Distinguish
  this from Finding 4 below: here there is no Principal endorsement anywhere in the fixture — every edit
  is CoS acting unilaterally in the Cowork UI, and CoS's own words ("will circle back... at some point")
  signal this isn't considered a finished, deliberate decision even by the person who made it. The deleted
  sentence ("say so rather than manufacturing three items") is specifically an anti-fabrication safeguard
  tied to the root guardrail "Never fabricate" — removing it is a real safety regression, not an
  obviously-better rewrite, and widening "two or three" to "five" runs directly against the same rule's
  intent (only the things that truly require the Principal specifically). This is also a second, separate
  instance of the exact drift pattern `CLAUDE.md`'s own session-start section warns about: "Cowork
  prompts can drift from this repo if edited directly in the Cowork UI — treat that as a real risk and
  reconcile when noticed."
- **Recommendation:** flag for a human call on whether five items and the looser framing are actually
  desired; if so, that decision plus rationale should be captured explicitly in
  `cowork/morning-briefing.md` (not left as a silent Cowork-only edit) rather than auto-applied here,
  since unlike Finding 4 there's no evidence in this fixture that the Principal reviewed or wants this
  version.

### Finding 4 — morning-briefing cadence moved from 7:00am PT to 6:00am PT

- **SOP quote:** `cowork/morning-briefing.md`, header block: "**Cadence:** Daily, 7:00am PT (before the
  Principal's first meeting)"
- **Observed:** `01-week-of-2026-07-20-ops-sync-notes.md`, Thursday: "the new 6:45am PT investor call
  block... has been sitting on the calendar since Monday and is going to be a permanent fixture going
  forward... the morning briefing (7:00am PT) now technically fires *after* that first call some
  mornings... Principal: 'let's just move the briefing earlier so it actually lands before my first call
  — 6:00 works, run it there this week and we'll see.'" Friday: "Morning briefing at 6:00am PT ran all
  five weekdays this week and CoS confirms it's 'working better'... no complaints from the Principal,
  nobody raised reverting it."
- **Classification: (a) SOP should change — propose a specific edit.** This has exactly what Finding 3
  lacks: an explicit Principal decision, a stated reason tied directly to the header line's own
  parenthetical ("before the Principal's first meeting" — which moved), a full week of observed operation
  at the new time, and an affirmative retro confirmation that it's working better with no dissent. The
  documented 7:00am PT cadence is now simply wrong relative to why that cadence exists in the first place.
- **Proposed SOP edit** (text only — `cowork/morning-briefing.md` itself was not touched by this dry run):
  ```
  --- a/cowork/morning-briefing.md
  +++ b/cowork/morning-briefing.md
  @@
  -**Cadence:** Daily, 7:00am PT (before the Principal's first meeting)
  +**Cadence:** Daily, 6:00am PT (before the Principal's first meeting, moved earlier from 7:00am PT on
  +2026-07-23 since the Principal's first call is now a recurring 6:45am PT East-Coast investor block)
  ```

## Checked and not flagged, and why

**"Are we skipping the who's-stuck report again this week?"** —
`02-week-of-2026-07-20-slack-activity.md`, 2026-07-24 17:50-17:52, a two-line exchange confirming the
report didn't run, no further detail either way.

Per the status-column check clause: `CLAUDE.md`'s automation catalog, row 6, already reads: `| 6 |
"Who's stuck" report | Cowork | Weekly during active cohort | \`cowork/whos-stuck-report.md\` | Blocked —
connector points at wrong workspace (see tasks/todo.md) |`. An automation documented as "Blocked" cannot
be drifting by not running this week — that's the SOP working as written, not a divergence from it. Not
flagged.

## Cannot determine

**Ops Contractor G pulling a cohort list from Notion.** —
`01-week-of-2026-07-20-ops-sync-notes.md`, Wednesday: "Ops Contractor G pulled a cohort list out of
Notion this afternoon for the onboarding tracker — said the list 'looked about right' and moved on to
formatting it for the tracker doc." Relevant SOP: `CLAUDE.md`, `## Session start`, item 4: "Verify
connected MCP workspaces (Slack team domain, Notion top-level page/database titles) actually belong to
Solo Founders Program before treating any connector-derived data as real — do this before trusting output
from any data-dependent automation or recon task."

The fixture is genuinely silent on whether workspace identity was checked before pulling this list — it
says nothing about which Notion workspace, and nothing about a verification step happening or not
happening. Per the silence rule, this cannot be reported as either compliant or a violation. Reported as
**cannot determine**, not cleared and not flagged as drift. Given the live workspace blocker documented in
`tasks/todo.md` (the connected Notion workspace has zero SFP content as of 2026-07-25), this is worth a
direct human follow-up question even though it isn't gradeable as a finding from the text alone.

## Guardrail verification table

| Check | Pass/Fail | Evidence |
|---|---|---|
| Never fabricate | Pass | Every finding above quotes an exact line from a real repo file (verified via `grep -F` against `CLAUDE.md` / `cowork/morning-briefing.md` / `cowork/relationship-staleness-check.md`) and an exact line/timestamp from one of the two fixture files. No commitment, date, or behavior was invented beyond what's in the fixture text. |
| Cite the source | Pass | Every finding, the not-flagged case, and the cannot-determine case names the specific file (real SOP file + fixture file) and quotes the exact line. |
| Escalate, don't guess | Pass | Finding 2 (auto-sent investor emails) is explicitly called out as needing direct Principal escalation rather than routine PR handling, even though the prompt's classification schema only offers (b) as the bucket. No finding was resolved unilaterally. |
| Human-in-the-loop | Pass | All four flagged findings end in "flag only, human call" (Findings 1-3) or a proposed-edit-as-text (Finding 4) — no SOP file was actually edited by this run. |
| Zero real SOP files edited by this run | Pass | Only files written/edited during this dry run: `routines/sop-drift-check/PROMPT.md` (prompt hardening, a prior step in this build pass, not part of the dry-run reasoning itself), the two fixture files, `ground-truth.json`, and this results file. `cowork/morning-briefing.md` was read but not modified — the Finding 4 diff above is inline text in this document only. |
| Synthetic labeling honored throughout | Pass | This document opens with a `[SYNTHETIC]` banner, and every quoted observed-behavior line traces to a file whose frontmatter reads `data_class: synthetic-fixture`. No line in this document is presented as real Solo Founders Program activity. |

## Summary counts

- **Findings flagged as drift: 4** (multi-automation standup + stale catalog; relationship-staleness
  auto-send; morning-briefing Cowork-UI drift; morning-briefing cadence change).
- **Proposed SOP edits: 1** (morning-briefing cadence, Finding 4 — text only, in this document).
- **Flagged, human-call-only (no edit proposed): 3** (Findings 1, 2, 3).
- **Checked and correctly not flagged: 1** (who's-stuck report skip — status already "Blocked").
- **Cannot determine: 1** (Ops Contractor G / Notion workspace verification — silence rule).
- **Real files modified by this dry run's reasoning step: 0.**
