# SOP Drift Check

**Surface:** Claude Code Routine (this is the one automation in the stack where Routines genuinely
outperform Cowork — it's exactly the documentation-drift pattern the feature is built for)
**Trigger:** Weekly schedule
**Sources:** Internal process docs committed to this repo (or a repo the SOPs live in), plus meeting
notes / Slack exports for how the team actually operated this week
**Output:** A PR (or a committed doc update + flag list) against the SOP docs

## Prompt

> Scan the internal process docs in this repo against how the team actually operated this week, based on
> meeting notes and Slack activity provided as input. For each SOP, check whether the written process
> still matches practice. Flag anywhere they've diverged — be specific: quote the line in the SOP and
> describe the actual behavior observed, don't just say "this seems out of date." For each flagged
> divergence, propose one of two things: (a) a specific edit to the SOP to match new reality, if the new
> way is clearly better/intentional, or (b) a note that the team has drifted from a process that's still
> the right one, if the drift looks accidental rather than an improvement. Open a PR with proposed SOP
> edits for (a) cases; leave (b) cases as a flagged list in the PR description rather than auto-editing,
> since those need a human call on which version is actually correct.
>
> **Preflight.** If no weekly input file exists for the week being checked, output exactly
> `CANNOT RUN — no weekly input file for week ending <date>` and stop. Never infer activity from absence —
> a missing input file is not evidence of a quiet week.
>
> **Synthetic-data gate.** If the input file's frontmatter has `data_class: synthetic-fixture`, prefix
> every output finding with `[SYNTHETIC]`, and never let a synthetic finding be written into this file's
> own `## Calibration notes` section as though it were observed real operation — calibration notes record
> what the *check itself* got right or wrong, not the fabricated content of a fixture.
>
> **Evidence rule.** Every finding must quote the exact SOP line verbatim (with file path + section
> heading) plus the exact contradicting line/message from the weekly input. No finding without both
> halves — a divergence that can't be quoted on both sides doesn't get reported as a finding.
>
> **Classification.** Every flagged divergence gets exactly one of: (a) SOP should change — propose a
> specific edit, only when the new way is clearly better/intentional; (b) team drifted from a still-correct
> process — flag only, this is a human call, never auto-resolved; or insufficient evidence — assert
> nothing either way, say so plainly.
>
> **Status-column check.** Before flagging "automation X didn't run" as drift, check that automation's
> Status in the `CLAUDE.md` catalog table. An automation documented as "Not stood up" or "Blocked" cannot
> be drifting by not running — it was never supposed to be running in the first place.
>
> **Scope exclusion.** `eval/**` is test data — never an SOP source and never evidence of real activity,
> even if it looks like a meeting note or a log. `tasks/todo.md` is state (open questions, in-flight
> checklist items), not process — don't scan it as an SOP and don't treat it as this week's activity input.
>
> **Silence rule.** Where the weekly input is silent on whether a rule was followed, report
> "cannot determine" — never infer compliance from silence, and never infer a violation from silence
> either. Silence is not evidence in either direction.

## Config

- **SOP corpus scanned (resolves `[CONFIGURE]` item 1):** `CLAUDE.md` in full (the surface decision rule,
  the build order, the guardrails section, and the automation-catalog status column all count — status is
  itself a process claim, so a stale status is its own kind of drift); every `cowork/*.md` file, header
  block + `## Prompt` + `## Config` sections all counting as process, not just the prompt blockquote; both
  `routines/*/PROMPT.md` files (this file and `routines/show-notes-drafting/PROMPT.md`); and
  `tasks/lessons.md`, since every entry there is a binding rule already extracted from a past correction,
  not just a narrative log. **Explicitly out of scope:** `eval/**` (synthetic test data, never a live SOP
  source and never real activity) and `tasks/todo.md` (current build-order state and open questions — that
  changes weekly and isn't a rule the team is supposed to follow).
- **Weekly input convention (resolves `[CONFIGURE]` item 2):** one hand-authored file per week at
  `routines/sop-drift-check/weekly-input/YYYY-MM-DD.md`, dated by week-ending date, committed manually by
  the Principal or CoS. Required YAML frontmatter: `week_start`, `week_end`, `source`
  (`manual` | `connector-export`), `data_class` (`real` | `synthetic-fixture`), `author`. Why manual right
  now, stated inline rather than left implicit: connector-derived weekly input isn't available yet — Slack
  and Notion both point at the wrong workspace (see `tasks/todo.md`'s open-questions section), and per the
  `tasks/lessons.md` 2026-07-25 entry on connector workspace identity, connector data can't be trusted as
  real until workspace identity is independently re-verified anyway, so wiring a `connector-export` mode
  today would be premature even before the workspace blocker. **Migration path:** once the real SFP
  Slack/Notion workspaces are connected and verified, flip `source: manual` → `source: connector-export` in
  the frontmatter — the one-file-per-week convention itself does not change, only how that file gets
  populated. The `routines/sop-drift-check/weekly-input/` directory is intentionally **not created** as
  part of this pass — there's no real week to put in it yet; this paragraph defines the convention for
  whenever the first real week arrives.
- `[CONFIGURE]` Exact trigger/schedule config syntax for Routines — deliberately left **unresolved this
  pass**. This run is local dry-run only, no git/GitHub wiring attempted (see the hard constraints for this
  build pass). Resolving this must happen together with the git-init/GitHub-remote decision (see
  `tasks/todo.md` → "Deferred by explicit decision" section) and must be verified against current Anthropic
  Routines docs at that time, since Routines are a beta feature and the trigger/schedule config schema may
  have changed since this file was first written.
- This Routine has so far only run in dry-run mode against a synthetic fixture
  (`eval/sop-drift-check/golden-weeks/`) — it has never seen real weekly activity.

## Dry run / calibration

The only runs of this Routine to date are synthetic dry runs, not live weekly checks. See:

- `eval/sop-drift-check/golden-weeks/` — the synthetic weekly-input fixtures used to calibrate this
  prompt (clearly marked `data_class: synthetic-fixture`, never real Solo Founders Program activity).
- `eval/sop-drift-check/ground-truth.json` — the hand-authored expected findings for those fixtures
  (which divergences should flag, which shouldn't, which are genuinely ambiguous), plus a
  `grading_contract` describing how a run should be scored against it.
- `eval/results/run-2026-07-25-sop-drift-check-output.md` — the first dry-run output, reasoned
  independently from the fixtures and the real repo docs above (not copied from `ground-truth.json`), with
  a guardrail-verification table and summary counts.

## Calibration notes

_(add findings here after the first few runs)_

- `[2026-07-25]` First run: a synthetic dry run against two fabricated fixtures
  (`eval/sop-drift-check/golden-weeks/`), reasoned from the fixture text and the real SOP corpus, not
  copied from `eval/sop-drift-check/ground-truth.json`. Full output at
  `eval/results/run-2026-07-25-sop-drift-check-output.md`. What it got right: the status-column check
  correctly kept the "who's-stuck report skipped again" mention from being flagged as drift (its catalog
  status is already "Blocked"); the silence rule correctly produced a "cannot determine" for the
  Notion-pull mention rather than asserting compliance or a violation either way; the evidence rule held
  throughout — every quote on both the SOP side and the fixture side was independently `grep`-verifiable.
  Prompt ambiguity this run exposed: the (a)/(b) split between the two morning-briefing findings required
  a judgment call the prompt doesn't spell out — both findings touch the same SOP file, but one (the
  cadence change) had explicit Principal sign-off and a week of confirmed-working operation, while the
  other (the widened "two or three things" language and the deleted anti-fabrication sentence) was a
  unilateral, not-yet-finalized Cowork-UI edit with no Principal involvement at all. The prompt's
  classification clause says (a) applies "when the new way is clearly better/intentional" but doesn't say
  *whose* endorsement counts as evidence of "intentional" — this run used "was there an explicit Principal
  decision plus a week of observed, unopposed operation" as the bar, and classified the other case as (b)
  for failing that bar, but that test isn't written into the prompt itself yet and should be, so the next
  run doesn't have to re-derive it. Also worth naming: the never-auto-send violation (Finding 2) doesn't
  fit cleanly into the (a)/(b)/insufficient-evidence scheme at all — it got filed as (b) because that's
  the closest bucket, but a guardrail violation this severe arguably deserves its own classification
  distinct from ordinary process drift, since "flag only, human call" undersells how urgent an unreviewed
  batch of sent investor emails actually is.
