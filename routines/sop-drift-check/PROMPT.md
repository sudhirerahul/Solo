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

## Config

- `[CONFIGURE]` Path to the SOP docs this scans (which repo/directory — confirm SOPs are actually
  repo-tracked before wiring this up; if they live in Notion instead, this belongs in `cowork/` as a
  Cowork task, not here)
- `[CONFIGURE]` How "how the team actually operated" gets fed in — meeting notes export, Slack export, or
  a manual weekly input file committed alongside this Routine
- `[CONFIGURE]` Exact trigger/schedule config syntax for Routines — verify against current Anthropic docs
  before wiring up; this is a beta feature and the config schema may have changed since this file was
  written

## Calibration notes

_(add findings here after the first few runs)_
