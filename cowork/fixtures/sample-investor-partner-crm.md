# Fixture — Sample Investor/Partner CRM (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real CRM, not real investors or partners, and not real Notion
> content.** It exists to dry-run test `cowork/relationship-staleness-check.md` against realistic-shaped
> data while the live Notion connector is not yet authorized for this session (see `tasks/todo.md`, "Open
> questions for the user"). Every name is fictional and every email is prefixed `mock-` on purpose so it
> can never be mistaken for a live address. **Never point a real automation run at this file, and never
> copy any name/email/detail from here into a real draft.**

This fixture stands in for the investor/partner CRM database's roster of record as of 2026-07-25. It is
used to dry-run the hardened relationship-staleness-check prompt — specifically to exercise: the
per-tier threshold branch, the same-staleness tiebreak-by-tier branch, the `unknown`-state contact with
zero logged touchpoint, the escalation-not-draft branch for a relationship that reads as damaged rather
than merely stale, and the correctly-excluded contact who's inside their tier's window.

## Mock Notion DB — "Investor / Partner CRM"

Snapshot as of 2026-07-25. "Today" for all staleness math below is 2026-07-25.

| Name | Email | Org / Role | Tier | Last Touchpoint Date | Last Touchpoint Source | Notes |
|---|---|---|---|---|---|---|
| Ravi Chen | mock-ravi@example.com | Meridian Capital, Lead Investor | Lead investor | 2026-05-24 | Email thread — quarterly update reply | Confirmed lead in seed round, has asked for board-observer updates |
| Priyanka Oyelaran | mock-priyanka@example.com | Independent, Advisor | Casual advisor | 2026-05-24 | Calendar — 30 min call | Occasional product feedback, no formal board role |
| Deion Marsh | mock-deion@example.com | Northfall Partners, Lead Investor | Lead investor | 2026-06-04 | Email thread — cap table follow-up | Asked twice why an updated cap table hadn't arrived; our last reply was one curt line, no resolution given |
| Fatima Al-Rashid | mock-fatima@example.com | Cedar Bridge Capital, Partner | Casual advisor | (blank — none found) | (none found) | On the CRM roster (introduced at Q1 demo day) but no logged touchpoint of any kind since |
| Noah Kessler | mock-noah@example.com | Independent, Advisor | Casual advisor | 2026-07-13 | Calendar — coffee chat | Regular monthly catch-up, on track |

Staleness math (today = 2026-07-25): Ravi = 62 days stale, Priyanka = 62 days stale, Deion = 51 days
stale, Noah = 12 days stale (well within any reasonable window), Fatima = unknown / no data (no last
touchpoint date or source exists anywhere for her).

## SFP recent context

Fictional context a check-in draft could reference — for this fixture only, not real:

- The Solo Founders Podcast just published an episode on solo-founder cap table hygiene, featuring a
  founder who renegotiated her seed round terms mid-raise.
- The current SFP cohort just hit its first group milestone: three founders in the Summer cohort crossed
  $5k MRR in the same week.
- SFP is piloting a monthly "office hours" slot for investors who want more visibility into portfolio
  founders between formal updates.

## Edge cases this fixture deliberately contains

- **Two contacts tied at the same staleness (Ravi, Priyanka — both 62 days)** — tests the tier-priority
  tiebreak: Ravi (lead investor) should sort before Priyanka (casual advisor) at the same staleness.
- **A contact with zero logged touchpoint of any kind (Fatima)** — tests that `unknown` is flagged
  regardless of window and sorts above every dated bucket, rather than being treated as "probably fine"
  or silently dropped for lack of data.
- **A relationship that reads as damaged, not just stale (Deion)** — the cap-table follow-up went
  unresolved after two asks and a curt one-line reply; tests that this routes to escalation instead of a
  routine check-in draft, and that the sensitive detail isn't quoted verbatim into a shared digest.
- **A contact well inside their tier's window (Noah, 12 days)** — tests that the prompt correctly excludes
  him entirely rather than flagging him out of an abundance of caution.
