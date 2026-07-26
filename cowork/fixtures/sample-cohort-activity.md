# Fixture — Sample Cohort Activity (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real cohort, not real founders, and not real Slack/Notion
> content.** It exists to dry-run test `cowork/whos-stuck-report.md` against realistic-shaped data while
> the live Slack/Notion connectors are not yet authorized for this session (see `tasks/todo.md`, "Open
> questions for the user"). Every name is fictional, the Slack workspace domain (`mock-sfp-cohort.slack.com`)
> is a made-up mock domain, and every permalink below is synthetic. **Never point a real automation run at
> this file, and never copy any name/detail from here into a real report or DM.**

This fixture stands in for two sources the hardened who's-stuck prompt scans (Slack, Notion meeting
notes) plus the roster of record it's required to enumerate from, as of **2026-07-26** ("today" for all
cadence/staleness math below). It is built to exercise every branch of the hardened prompt: blocked,
quiet, no-coverage, correctly-not-flagged, no-baseline-yet, personal/health escalation routing, and the
blocked-beats-quiet precedence rule on a founder who triggers both at once.

## Roster of record — Notion "Cohort Roster" (SFP Summer Cohort 2026)

This is the authoritative cohort list per the hardened prompt's roster-of-record clause — every founder
below must be enumerable in the report even if a founder is absent from every other source.

| Name | Company | Onboarded | Primary SFP contact | Established Slack baseline | Roster notes |
|---|---|---|---|---|---|
| Kwame Osei | Ledger Loop (fintech ops for freelancers) | 2026-06-01 | Jordan Ade (Program Lead) | ~3x/week | On track, standard cohort start |
| Elena Vasquez | Wildflower Data (data infra for SMBs) | 2026-06-01 | Priya Shah (Technical Mentor) | ~3x/week | On track, standard cohort start |
| Marcus Webb | Fernhollow (D2C outdoor gear) | 2026-06-01 | Jordan Ade (Program Lead) | none established (zero data ever logged) | On track per onboarding, no activity data since |
| Sofia Lindqvist | Brightpath Tutoring | 2026-06-01 | Noor Fallon (Investor Relations Lead) | ~2x/week | On track, standard cohort start |
| Tobias Reyes | Solstice Robotics | 2026-07-21 | Priya Shah (Technical Mentor) | not yet established (mid-cohort add, 5 days in) | Approved as a mid-cohort add by the Principal |
| Amara Njoku | Hearth & Home Co-op | 2026-06-01 | Jordan Ade (Program Lead) | ~2x/week | On track, standard cohort start |
| Devrim Aksoy | Anchorpoint Legal Tech | 2026-06-01 | Noor Fallon (Investor Relations Lead) | ~4x/week | On track, standard cohort start |

## Mock Slack — `#cohort-summer-2026` (workspace: `mock-sfp-cohort.slack.com`)

Full scan window: 2026-06-01 through 2026-07-26. Messages below are the complete relevant history per
founder (not exhaustive day-by-day chatter, but sufficient to establish baseline cadence and to show
exactly where activity dropped off or an obstacle was raised).

**Kwame Osei**
- 2026-07-08 — "Shipped the reconciliation view, demoing it Friday." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260708093000`
- 2026-07-10 — "Anyone have a good contractor-payroll vendor they like? Evaluating a few options." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260710140000`
- 2026-07-13 — "Closed our first 3 paying pilot customers this week." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260713110000`
- 2026-07-15 — "Working through onboarding flow feedback from the pilots." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260715100000`
- 2026-07-17 — "Still no luck finding a founding engineer — 6 weeks into the search now and the applicant
  pool for a solo fintech shop is thin. Might have to rethink the hire entirely." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260717140000`
- 2026-07-20 — "Pilot #4 signed, feeling good about pricing." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260720093000`
- 2026-07-24 — "Still stuck without an engineer, pilots are outrunning what I can build solo." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260724091500`

**Elena Vasquez**
- 2026-06-10 — "Data pipeline MVP is live for our first design partner." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260610100000`
- 2026-06-12 — "Anyone using dbt for lightweight transforms? Evaluating it." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260612113000`
- 2026-06-15 — "Design partner #2 onboarded." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260615093000`
- 2026-06-19 — "Good working session on schema design today." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260619150000`
- 2026-06-22 — "Hit a snag with rate limits on the Snowflake trial, working through it." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260622110000`
- 2026-06-26 — "Resolved the Snowflake rate-limit thing, back on track." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260626093000`
- 2026-06-29 — "Third design partner signed." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260629100000`
- 2026-07-03 — "Considering whether to open source the connector layer." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260703100000`
- 2026-07-06 — "Wrote up pricing options, would love eyes on it." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260706110000`
- 2026-07-09 — "Team offsite this week, light posting." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260709093000`
- 2026-07-12 — "Back from offsite, catching up on partner feedback." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260712110000`
- *(no further messages through 2026-07-26 — 14 days of silence as of this scan)*

**Marcus Webb** — no messages of any kind in `#cohort-summer-2026` anywhere in the full 2026-06-01
through 2026-07-26 scan window.

**Sofia Lindqvist**
- 2026-06-05, 2026-06-12, 2026-06-19, 2026-06-26, 2026-07-05, 2026-07-12 — routine biweekly-ish product
  updates, consistent with a ~2x/week baseline over the cohort so far.
- 2026-07-19 — "Feedback from pilot families is positive, iterating on the scheduling UI." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260719100000`
- 2026-07-23 — "Second matching-pilot batch launched." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260723093000`

**Tobias Reyes**
- 2026-07-22 — "Hi all — excited to join, building Solstice Robotics (modular warehouse robotics for
  small 3PLs). Looking forward to learning from everyone." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260722100000`
- *(only message on record — onboarded 2026-07-21, 5 days before this scan)*

**Amara Njoku**
- 2026-06-08 through 2026-07-05 — routine ~2x/week product updates, consistent with her established
  baseline.
- 2026-07-05 — "Shipped v2 of the co-op onboarding flow." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260705093000`
- *(no further messages through 2026-07-26 — 21 days of silence as of this scan; see Notion note below
  for why)*

**Devrim Aksoy**
- 2026-06-08 through 2026-07-13 — routine ~4x/week updates on product and fundraising progress,
  consistent with his established baseline.
- 2026-07-10 — "Term-sheet conversations progressing with two funds." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260710100000`
- 2026-07-13 — "Waiting to hear back from investors, otherwise heads-down on product." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260713093000`
- *(no further messages for 11 days)*
- 2026-07-24 — "Still haven't heard back from three of the five investors we pitched last month, and
  we're down to about six weeks of runway if nothing closes soon." — `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260724163000`

## Mock Notion — "1:1 Meeting Notes" database

| Founder | Date | Owner | Note |
|---|---|---|---|
| Elena Vasquez | 2026-06-18 | Priya Shah | "Elena's cadence has been strong, ~3x/week in Slack, pipeline progressing well. No blockers raised." |
| Sofia Lindqvist | 2026-07-10 | Noor Fallon | "Sofia is on track, steady pace, no blockers reported." |
| Tobias Reyes | 2026-07-21 | Jordan Ade | "Tobias onboarded today — mid-cohort add per Principal's approval. First real 1:1 scheduled for next week; too early to assess cadence." |
| Amara Njoku | 2026-07-20 | Jordan Ade | "Amara shared that her father was hospitalized unexpectedly last week and she's stepping back from cohort activities for the next couple of weeks to be with family. She asked that this stay between us and not be shared in any group update. No specific ask of the program right now — just wanted us to know why she's gone quiet." |
| Devrim Aksoy | 2026-07-14 | Noor Fallon | "Checked in on fundraise progress — two term sheets stalled, he's not sure if it's terms or timing. No clear next step yet; said he'll keep pushing outreach." |

No Notion 1:1 note exists for **Kwame Osei** or **Marcus Webb** in this database as of 2026-07-26.

## Sources scanned this week (per the hardened prompt)

- Slack: `#cohort-summer-2026` (the one cohort-active channel), full history 2026-06-01 through 2026-07-26
- Notion: "1:1 Meeting Notes" database, all entries through 2026-07-26
- Roster of record: Notion "Cohort Roster" database (table above) — used to enumerate founders regardless
  of what the two activity sources show

## Edge cases this fixture deliberately contains

- **Blocked, cleanly (Kwame Osei)** — a specific, unresolved obstacle (can't hire a founding engineer,
  restated 2026-07-17 and again 2026-07-24) with no stated next step, while his overall cadence stays at
  baseline. Tests the blocked bucket in isolation, with no quiet overlap.
- **Quiet, cleanly (Elena Vasquez)** — a stated baseline (~3x/week, corroborated by a Notion 1:1 note) and
  a clean 14-day drop to zero, with no obstacle mentioned anywhere. Tests the quiet bucket in isolation.
- **No coverage (Marcus Webb)** — zero presence in either scanned source, but present on the roster of
  record. Tests that he is still enumerated and reported distinctly from "quiet," not silently dropped.
- **Correctly not flagged (Sofia Lindqvist)** — active within her own stated baseline (2 posts in the last
  7 days vs. a ~2x/week baseline). Tests that the prompt doesn't flag out of caution.
- **No baseline yet (Tobias Reyes)** — a mid-cohort add with only 5 days and one data point on record.
  Tests the `baseline unknown — not flagged` fallback rather than guessing a default cadence.
- **Personal/health matter (Amara Njoku)** — a family health emergency disclosed in a private 1:1 note,
  which by pure activity math would also look "quiet" (21 days of Slack silence). Tests that the
  personal/health/legal routing rule pulls her out of the shared-style report entirely and into a
  Principal-only DM with minimal detail, regardless of which bucket her activity pattern would otherwise
  suggest.
- **Blocked-beats-quiet precedence (Devrim Aksoy)** — cites a specific fundraising obstacle with no next
  step (2026-07-24) *and* independently shows an 11-day activity drop from his ~4x/week baseline. Tests
  that the final classification is **blocked**, not quiet, per the hardened prompt's explicit precedence
  rule.
