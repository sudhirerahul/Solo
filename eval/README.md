# Eval — Synthetic Calibration Fixtures

> **SYNTHETIC TEST DATA ONLY. Nothing under `eval/` is a real meeting, a real founder, or a real
> commitment.** It exists to calibrate two never-yet-run Cowork prompts —
> `cowork/post-meeting-action-extraction.md` and `cowork/open-commitments-digest.md` — against a known,
> hand-authored ground truth before either one is trusted with real Solo Founders Program data.

## Why this exists

Both prompts are drafted but have never executed against real data (see the automation catalog status
column in the root `CLAUDE.md` — both are "Not stood up"). Per the repo's build order, we don't hand an
untested extraction prompt real meeting notes on day one. Instead:

1. We author a small set of synthetic meeting notes with known, deliberately-varied ground truth
   (clean commitments, a no-deadline case, an unowned/ambiguous-owner case, a duplicate/idempotency case,
   and a vague-aspiration negative case that must NOT be extracted).
2. We run the extraction prompt against that synthetic data in a sandboxed Notion structure (titled and
   tagged so it can never be mistaken for production content) and score what came out against the ground
   truth: recall (did it find every real commitment), precision (did it avoid inventing or over-extracting
   anything, especially the aspiration sentence), dedup correctness (did the pre-seeded row stop it from
   creating a duplicate), and idempotency (does a second run create zero new rows).
3. We then run the digest prompt against the resulting tracker and check its overdue/unowned flagging
   against the known-correct answer.

This calibration run does **not** touch the `[CONFIGURE]` placeholders in either `cowork/*.md` file — the
real production Notion source and tracker location are still undecided (see `tasks/todo.md`). Nothing here
should be read as "the automation is now live."

## Layout

```
eval/
  README.md                                     this file
  post-meeting-action-extraction/
    golden-meetings/                            6 synthetic meeting-note fixtures (markdown, YAML frontmatter + prose)
    ground-truth.json                           8 expected outcomes: gt-001..gt-007 (real commitments) + gt-neg-001 (negative case)
  results/                                       raw outputs from each calibration run, written by the run itself
```

## Ground truth summary (`post-meeting-action-extraction/ground-truth.json`)

7 real commitments across 6 meetings, plus 1 negative case (a vague aspiration that must not be
extracted as a commitment):

| id | meeting | owner | deadline | overdue as of 2026-07-25? | edge case |
|---|---|---|---|---|---|
| gt-001 | Onboarding Call — Founder A | Founder A | 2026-07-18 | yes | clean positive |
| gt-002 | Investor Intro — Founder B x Investor X | Founder B | no deadline given | no | no date stated anywhere — must not be invented |
| gt-003 | Dinner Planning — Summer Dinner | *(ambiguous — no single owner)* | 2026-07-10 | yes | unowned/ambiguous owner |
| gt-004 | Weekly Check-in — Founder C | Founder C | 2026-07-15 | yes | pre-seeded in the tracker before the extraction run — must be skipped as a duplicate, not re-created |
| gt-005 | Founder Coaching Session — Founder D | Founder D | 2026-07-30 | no (future) | clean positive |
| gt-006 | Partner Sync — Solo Founders x Partner Org | Owner E | 2026-07-22 | yes | clean positive, multi-owner meeting |
| gt-007 | Partner Sync — Solo Founders x Partner Org | Owner F | 2026-08-15 | no (future) | clean positive, multi-owner meeting, soft/target date |
| gt-neg-001 | Founder Coaching Session — Founder D | Founder D | — | — | vague aspiration ("get better about following up with investors"), no deliverable/deadline/recipient — must NOT be extracted |

Derived scoring facts:
- **4 items overdue** as of 2026-07-25: gt-001, gt-003, gt-004, gt-006.
- **3 items not overdue**: gt-002 (no deadline given, can't be overdue), gt-005 and gt-007 (deadlines still in the future).
- **1 item unowned/ambiguous**: gt-003 (dinner headcount confirmation — notes never attach it to a name).
- **1 negative case**: gt-neg-001 must not appear as a row at all — extracting it would be a precision
  failure (treating a feeling/intention as a commitment).
- **1 dedup case**: gt-004 is pre-seeded into the synthetic Notion tracker before the first extraction run,
  to test that the prompt's "skip if already logged for this source meeting" instruction actually holds.

## How this gets used (calibration steps)

1. Golden meeting fixtures are copied into a sandboxed synthetic Notion database
   (`🧪 SYNTHETIC Meeting Notes (Eval Fixture)`), clearly tagged and prefixed so it's never confused with
   real content.
2. A synthetic commitments tracker (`🧪 SYNTHETIC Commitments Tracker (Eval Fixture)`) is seeded with
   exactly one pre-existing row (gt-004) to test dedup.
3. The post-meeting-action-extraction prompt is applied, verbatim in spirit, against the synthetic Notion
   data — not against this ground-truth file directly — so the run is a genuine test of the prompt's
   language-understanding, not a copy-paste exercise.
4. Raw outputs land in `eval/results/` for inspection against `ground-truth.json`.
5. The same extraction is re-run a second time with no new source data, to confirm idempotency (zero new
   rows expected, since every source meeting is already logged).
6. The open-commitments-digest prompt is applied against the resulting tracker and its overdue/unowned
   output is checked against the "derived scoring facts" above.

## Guardrails specific to this fixture

- Every synthetic Notion page/database is prefixed `🧪 SYNTHETIC` / `[SYNTHETIC]` and tagged
  `Synthetic-Eval-v1` so it can never be mistaken for production content, and so it can be found and torn
  down later without touching anything real.
- Names in the fixtures ("Founder A" through "Founder D", "Investor X", "Owner E", "Owner F") are
  deliberately generic placeholders, not real people.
- This run does not edit the `[CONFIGURE]` lines in `cowork/post-meeting-action-extraction.md` or
  `cowork/open-commitments-digest.md`. Those stay open questions until the real Notion source and tracker
  are decided.
