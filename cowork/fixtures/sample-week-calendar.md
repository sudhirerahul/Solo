# Fixture — Sample Week Calendar (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real week, not real people, not a real Google Calendar
> export.** It exists to dry-run test `cowork/weekly-time-audit.md` against realistic-shaped data while
> the live Calendar connector is not yet authorized for this session (see `tasks/todo.md`, "Open
> questions for the user"). Every name is fictional, every company is fictional, and every attendee email
> is prefixed `mock-` on the IANA-reserved `example.com` domain so none of it can be mistaken for a real
> person, org, or calendar. **Never point a real automation run at this file, and never copy any name,
> org, or detail from here into a real draft or a real message.**

This fixture stands in for one full work week (Monday–Friday) of Google Calendar events, as the weekly
time audit would read it looking back on "the week just finished." It exercises all 6 categories the
prompt defines, includes enough real durations to make the percentage breakdown arithmetic (not a guess),
and deliberately contains three plausible cut/delegate candidates (one per named reason in the prompt)
plus one founder 1:1 and one investor call that must survive un-flagged because no concrete reason exists
for either.

## Week meta

| Field | Value |
|---|---|
| Week covered | Monday 2026-07-20 – Friday 2026-07-24 |
| Timezone | All times PT |
| Source | Google Calendar (single connected calendar, the Principal's) |
| Attendee key | Principal = the Principal (not named, per `[CONFIGURE]` convention); Jamie Chen = Chief of Staff (internal, attends ops meetings) |

---

## Calendar — Monday 2026-07-20

| Time | Duration | Event | Category | Attendees | Notes |
|---|---|---|---|---|---|
| 9:00–9:30 | 30m | 1:1 — Priya Oyelaran-Nkemdirim (Solstice Robotics) | SFP founder 1:1 | Principal, Priya | Recurring Monday 9am. This week: Principal approved Priya's first ops hire (offer to candidate greenlit). See decision log below. |
| 10:00–10:30 | 30m | CoS weekly sync | Internal ops | Principal, Jamie Chen | Standing sync — priorities for the week. |
| 11:00–12:00 | 60m | Intro call — Marcus Devereux (Two Rivers Fund) | Investor/partner call | Principal, Marcus Devereux | First conversation with a prospective investor, warm intro from a portfolio founder. |
| 1:00–1:30 | 30m | 1:1 — Marcus Whitfield (Fernwood Analytics) | SFP founder 1:1 | Principal, Marcus Whitfield | Recurring Monday 1pm. This week: status update only, no new decision. See decision log below. |
| 3:00–4:00 | 60m | Guest prep call, Episode 42 | Podcast production | Principal, Theo Lindgren (guest booker) | Confirming guest availability and topic outline for Episode 42. |
| 4:30–5:00 | 30m | Venue walkthrough — The Anchorage | Event/dinner logistics | Principal, Ines Roswell (venue coordinator) | Walkthrough for the Aug 14 dinner, Private Room B. |

**Monday total: 240 min** (SFP 1:1: 60 · Investor/partner: 60 · Podcast: 60 · Event logistics: 30 · Internal ops: 30)

## Calendar — Tuesday 2026-07-21

| Time | Duration | Event | Category | Attendees | Notes |
|---|---|---|---|---|---|
| 9:00–9:30 | 30m | 1:1 — Elena Vasquez (Cobalt Health) | SFP founder 1:1 | Principal, Elena Vasquez | Regular weekly 1:1. |
| 10:00–11:00 | 60m | Recording — Episode 42 taping | Podcast production | Principal, guest, Theo Lindgren | Studio recording session. |
| 11:30–12:00 | 30m | Newsletter ideation call | Media/community | Principal, Zara Boone (social/content contractor) | Recurring monthly-ish brainstorm for the Solo Founders newsletter. No agenda, doc, or prep material has ever been requested or circulated ahead of this call in its 6-month history. |
| 1:00–1:30 | 30m | Quarterly check-in — Ravi Chen (Meridian Capital) | Investor/partner call | Principal, Ravi Chen | Lead investor, quarterly cadence per his board-observer arrangement. Substantive: reviewed cohort milestones and runway. |
| 2:00–2:30 | 30m | Hiring pipeline review | Internal ops | Principal, Jamie Chen | Reviewing open ops-hire candidates. |
| 2:30–3:00 | 30m | Contractor onboarding sync | Internal ops | Principal, Jamie Chen | Same two attendees as the 2:00 meeting immediately prior, back-to-back, no other invitees on either. |
| 3:30–4:00 | 30m | Guest list review — Aug 14 dinner | Event/dinner logistics | Principal, Jamie Chen | Reviewing RSVP list ahead of invites going out. |
| 4:30–5:00 | 30m | 1:1 — Sana Iqbal (Petal Health) | SFP founder 1:1 | Principal, Sana Iqbal | Ad hoc, requested by Sana this week re: board deck feedback. |

**Tuesday total: 270 min** (SFP 1:1: 60 · Investor/partner: 30 · Podcast: 60 · Event logistics: 30 · Internal ops: 60 · Media/community: 30)

## Calendar — Wednesday 2026-07-22

| Time | Duration | Event | Category | Attendees | Notes |
|---|---|---|---|---|---|
| 9:00–9:30 | 30m | Weekly metrics/dashboard review | Internal ops | Principal (solo prep block) | Reviewing cohort + podcast metrics ahead of the week. |
| 10:00–10:30 | 30m | 1:1 — Diego Ferreira (Northstar Robotics) | SFP founder 1:1 | Principal, Diego Ferreira | Regular weekly 1:1, new cohort founder. |
| 11:00–12:00 | 60m | Diligence call — Two Rivers Fund | Investor/partner call | Principal, Marcus Devereux, associate | Follow-up from Monday's intro call; discussing terms and timeline. |
| 1:00–2:00 | 60m | Editing coordination — Episode 41 final cut | Podcast production | Principal, Nadia Okonkwo (editor) | Reviewing final cut notes before publish. |
| 2:30–3:00 | 30m | Guest post co-writing session | Media/community | Principal, Zara Boone | Co-writing a guest post for an external outlet's newsletter. |
| 3:30–4:00 | 30m | Catering vendor call — Aug 14 dinner | Event/dinner logistics | Principal, Marchetti Catering Co. | Confirming menu and headcount estimate. |

**Wednesday total: 240 min** (SFP 1:1: 30 · Investor/partner: 60 · Podcast: 60 · Event logistics: 30 · Internal ops: 30 · Media/community: 30)

## Calendar — Thursday 2026-07-23

| Time | Duration | Event | Category | Attendees | Notes |
|---|---|---|---|---|---|
| 9:00–9:30 | 30m | 1:1 — Tobias Lindqvist (Amberlight Systems) | SFP founder 1:1 | Principal, Tobias Lindqvist | Regular weekly 1:1. |
| 10:00–11:30 | 90m | Recording — Episode 43 taping | Podcast production | Principal, guest (an investor), Theo Lindgren | Longer session, two-part interview format. |
| 12:00–12:30 | 30m | Follow-up call — Owen Castellan (Rivermouth Partners) | Investor/partner call | Principal, Owen Castellan | One-off follow-up on a cap-table question; not a recurring meeting. |
| 1:30–2:00 | 30m | Expense/ops admin review | Internal ops | Principal, Jamie Chen | Routine monthly expense reconciliation. |
| 2:30–3:00 | 30m | Podcast social clips review | Media/community | Principal, Zara Boone | Reviewing clip cuts for social from Episode 42. |
| 4:00–4:30 | 30m | Headcount follow-up — Aug 14 dinner | Event/dinner logistics | Principal, Ines Roswell | Confirming final headcount trend with the venue ahead of Friday's lock. |

**Thursday total: 240 min** (SFP 1:1: 30 · Investor/partner: 30 · Podcast: 90 · Event logistics: 30 · Internal ops: 30 · Media/community: 30)

## Calendar — Friday 2026-07-24

| Time | Duration | Event | Category | Attendees | Notes |
|---|---|---|---|---|---|
| 9:00–9:30 | 30m | CoS weekly sync #2 / week wrap planning | Internal ops | Principal, Jamie Chen | Second standing sync, closing out the week. |
| 10:00–10:30 | 30m | 1:1 — Amara Osei (Driftwood Labs) | SFP founder 1:1 | Principal, Amara Osei | Regular weekly 1:1. |
| 11:00–11:30 | 30m | Intro call — Lena Cho (Cho Family Office) | Investor/partner call | Principal, Lena Cho | First conversation with a prospective investor/advisor. |
| 12:00–1:00 | 60m | Content batch recording | Media/community | Principal, Zara Boone | Recording a batch of short-form clips for Instagram/Twitter. |
| 2:00–2:30 | 30m | Final headcount + seating lock — Aug 14 dinner | Event/dinner logistics | Principal, Ines Roswell, Jamie Chen | Locking the final list and seating chart. |
| 3:00–3:30 | 30m | Guest booking call, Episode 44 | Podcast production | Principal, Theo Lindgren | Sourcing and booking the next episode's guest. |
| 4:00–4:30 | 30m | Weekly retro / lessons log update | Internal ops | Principal (solo) | Closing out the week's open loops. |

**Friday total: 240 min** (SFP 1:1: 30 · Investor/partner: 30 · Podcast: 30 · Event logistics: 30 · Internal ops: 60 · Media/community: 60)

---

## Week totals by category (for verification only — not given to the executor running the dry run)

| Category | Minutes | Share of 1,230 total |
|---|---|---|
| SFP founder 1:1s | 210 | 17.07% |
| Investor/partner calls | 210 | 17.07% |
| Podcast production | 300 | 24.39% |
| Event/dinner logistics | 150 | 12.20% |
| Internal ops | 210 | 17.07% |
| Media/community | 150 | 12.20% |
| **Total** | **1,230** | **100%** |

---

## Decision log — recurring 1:1s (evidence for the cut/delegate test cases)

**Priya Oyelaran-Nkemdirim (Solstice Robotics) — Monday 9:00am, recurring — must NOT be flagged as cuttable:**
- 2026-07-06: Decided against raising a bridge note; chose to extend runway via cost cuts instead.
- 2026-07-13: Finalized pricing-tier changes for enterprise customers.
- 2026-07-20 (this week): Approved the offer to Solstice's first ops hire.
Three consecutive occurrences, three distinct concrete decisions. No attendee overlap with any other
meeting this week (Priya attends nothing else on the calendar). No basis exists in this fixture for
flagging this meeting as cuttable or delegable — it is deliberately the control case.

**Marcus Whitfield (Fernwood Analytics) — Monday 1:00pm, recurring — legitimate cut/delegate candidate:**
- 2026-07-06: Status update only. Marcus recapped the same metrics as the prior week; no decision requested or made.
- 2026-07-13: Status update only. Principal reiterated the same hiring guidance already given the week before; no new ask.
- 2026-07-20 (this week): Status update only. Marcus recapped the same two open items from the prior two weeks; nothing new surfaced.
Three consecutive occurrences with no clear decision made in any of them — this is the "recurring with no
clear decision made in the last 3 occurrences" case the prompt names explicitly, and it has become exactly
the kind of status-update-only meeting the prompt gives as its own example of one the CoS could collect
instead.

## Edge cases this fixture deliberately contains

- **A founder 1:1 that must NOT be flagged as cuttable despite being recurring** (Priya
  Oyelaran-Nkemdirim, Monday 9am) — three consecutive real decisions, no attendee overlap, no prep-request
  gap. Tests that the prompt does not flag a core-leverage meeting just because it repeats weekly.
- **A founder 1:1 that IS a legitimate cut/delegate candidate via the "no clear decision in the last 3
  occurrences" reason** (Marcus Whitfield, Monday 1pm) — three consecutive status-update-only
  occurrences, matching the prompt's own worked example of a "status-update the CoS could collect
  instead."
- **An investor call that must NOT be flagged as cuttable despite being a repeat contact** (Ravi Chen,
  Tuesday 1pm) — quarterly cadence (not weekly-recurring-with-no-decision), substantive agenda (cohort
  milestones, runway), no red flags. Tests that the prompt doesn't treat "investor call" as inherently
  suspect just because the same person appears again.
- **An attendee-overlap cut/delegate candidate** (Tuesday 2:00–2:30 hiring pipeline review and 2:30–3:00
  contractor onboarding sync) — identical two attendees (Principal + Jamie Chen), back-to-back, no other
  invitees on either. Tests the "attendee overlap with another meeting" reason named in the prompt.
- **A no-prep-material cut/delegate candidate** (Tuesday 11:30am newsletter ideation call) — recurring for
  6 months with no agenda or prep document ever requested or circulated. Tests the "no prep material was
  ever requested for it" reason named in the prompt.
- **Enough real durations across all 6 categories to make the percentage breakdown genuine arithmetic**
  (1,230 total minutes across the week; see "Week totals by category" above) rather than an eyeballed
  guess — the dry run's own computed percentages can be checked against this table line by line.
