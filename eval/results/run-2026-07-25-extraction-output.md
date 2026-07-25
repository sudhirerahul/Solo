# Run 2026-07-25 — Post-Meeting Action Extraction — First Pass

Prompt applied: `cowork/post-meeting-action-extraction.md`, verbatim in spirit, against the synthetic
Notion sandbox (`🧪 SYNTHETIC Meeting Notes (Eval Fixture)` -> `🧪 SYNTHETIC Commitments Tracker (Eval
Fixture)`). Six meetings read in full; each meeting's prose was read and reasoned over independently, not
copied from `eval/post-meeting-action-extraction/ground-truth.json`.

Before creating anything, the tracker (Database B) was checked and found to contain exactly one
pre-existing row: `[SYNTHETIC] Founder C — Send updated cap table` (Source meeting =
`[SYNTHETIC] Weekly Check-in — Founder C`), pre-seeded per the calibration design to test dedup.

## Per-meeting reasoning

### 1. Onboarding Call — Founder A (2026-07-10)
Checked tracker for `Source meeting = [SYNTHETIC] Onboarding Call — Founder A` — no existing row.
Extracted: **Founder A** committed to **send an updated financial model to the Principal**, deadline
stated explicitly as **2026-07-18** ("by July 18th"). Created.

### 2. Investor Intro — Founder B x Investor X (2026-07-14)
No existing row for this meeting. Extracted: **Founder B** committed to **send the pitch deck to Investor
X**. No deadline was stated anywhere in the notes — the notes explicitly call out "no firm date was
attached to that, just 'soon'" — so per the prompt's instruction not to invent a deadline, Deadline was set
to the literal string **"no deadline given"**. Created.

### 3. Dinner Planning — Summer Dinner (2026-07-08)
No existing row for this meeting. The notes describe a real, concrete task (confirm venue headcount by
July 10th) but explicitly state nobody claimed it — "it got mentioned as something that 'needs to happen'
without anyone saying 'I'll do it'". Judgment call: the prompt requires an owner "by name, not 'the
team'" — since no name exists in the source at all, I did not fabricate one (e.g. did not default it to
"Principal" or "event team"). Instead I extracted the row with Owner recorded honestly as
**"Unclear — no individual named in meeting notes (event team collectively discussed, nobody claimed
it)"**, so the digest step has something concrete to flag as unowned/ambiguous rather than the commitment
silently disappearing. Deadline was stated (2026-07-10). Created, flagged unowned.

### 4. Weekly Check-in — Founder C (2026-07-01)
Checked tracker for `Source meeting = [SYNTHETIC] Weekly Check-in — Founder C` — **found the pre-existing
row** (Owner: Founder C, Commitment: Send updated cap table, Deadline: 2026-07-15, Date extracted:
2026-07-25). Per the prompt's dedup instruction ("skip anything that was already logged from this meeting
in a prior run"), this was **skipped — no new row created**, even though the underlying commitment in the
notes is real and would otherwise have been extracted identically.

### 5. Founder Coaching Session — Founder D (2026-07-16)
No existing row for this meeting. Two candidate statements in the notes:
- **Extracted**: Founder D committed to **draft a board update memo**, deadline stated as **2026-07-30**
  ("have a first version ready by July 30th"). Created.
- **Not extracted**: Founder D's separate remark — "I really want to get better about following up with
  investors going forward" — was judged **not a concrete commitment** and was deliberately excluded. It
  has no deliverable, no deadline, and is not owed to any specific person (contrast with the pitch-deck
  commitment above, which at least names a recipient, Investor X, even without a date). This reads as a
  self-reflective aspiration, not a follow-through item, and creating a tracker row for it would be a
  precision failure — logging a feeling as if it were a task nobody can actually check off.

### 6. Partner Sync — Solo Founders x Partner Org (2026-07-20)
No existing row for this meeting. Two owners, two separate commitments:
- **Owner E** committed to **send partnership terms**, deadline stated as **2026-07-22**. Created.
- **Owner F** committed to **get the joint webinar scheduled**, with **August 15th** given as a target
  date. Judgment call: the notes explicitly hedge this ("more of a target than a hard commitment given it
  depends on both teams' calendars"), so I recorded the underlying commitment (scheduling the webinar) as
  real and extracted it, but preserved the softness of the date by writing the commitment text as
  "Schedule a joint webinar (target date, not a hard commitment per notes)" rather than presenting
  2026-08-15 as an ironclad deadline. The date was still recorded in the Deadline field since it was
  explicitly stated in the notes (not invented) — flagging softness in the commitment text rather than
  omitting the date seemed like the more honest choice, since the digest step still needs a date to
  reason about overdue-ness later.

## Rows created this run: 6

1. Founder A — Send updated financial model — Deadline 2026-07-18
2. Founder B — Send pitch deck to Investor X — Deadline "no deadline given"
3. Unclear owner — Confirm venue headcount — Deadline 2026-07-10 (flagged unowned)
4. Founder D — Draft board update memo — Deadline 2026-07-30
5. Owner E — Send partnership terms — Deadline 2026-07-22
6. Owner F — Schedule joint webinar — Deadline 2026-08-15

## Explicitly skipped as duplicate: 1

- Founder C — Send updated cap table (pre-existing row from a prior run, same source meeting)

## Explicitly decided NOT to extract, and why: 1

- Founder D's "get better about following up with investors going forward" — vague aspiration, no
  deliverable/deadline/named recipient, judged not a concrete commitment.

## Tracker state after this run

7 total rows (1 pre-seeded + 6 new). This matches the golden dataset's 7 real commitments across the 6
meetings (see `eval/post-meeting-action-extraction/ground-truth.json`, gt-001 through gt-007). Zero rows
were created for the negative case (gt-neg-001). See
`eval/results/run-2026-07-25-tracker-snapshot.json` for the full field-by-field snapshot pulled directly
from Notion via `notion-query-database-view`.
