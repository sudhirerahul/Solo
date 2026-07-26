# Fixture — Sample Daily Rollup Day (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real day, not real people, not real Slack/Gmail/Calendar
> content.** It exists to dry-run test `cowork/daily-rollup.md` against realistic-shaped data while the
> live Slack/Gmail/Calendar connectors are not yet authorized for this session (see `tasks/todo.md`,
> "Open questions for the user"). Every name is fictional, every email is prefixed `mock-` on the
> IANA-reserved `example.com` domain, every Slack permalink points at the non-existent
> `mock-solofounders.slack.com`, and every Gmail link uses a `mock-gmail://` scheme that resolves to
> nothing — all on purpose, so none of it can be mistaken for a live address, workspace, or thread.
> **Never point a real automation run at this file, and never copy any name, email, link, or detail from
> here into a real draft or a real message.**

This fixture stands in for one full day of activity across the three sources the daily rollup reads. It is
a single snapshot of a single fictional day, not a running log — treat everything below as "what the three
connectors returned when queried at end of day."

## Day meta

| Field | Value |
|---|---|
| Rollup date | 2026-07-23 (Thursday) |
| Timezone | All times PT |
| Query window | 00:00–18:30 PT, 2026-07-23 |
| Sources queried | Google Calendar, Slack, Gmail |
| Intended output | Slack message to the Principal (destination is `[CONFIGURE]` — may be a DM *or* the shared `#cos` channel) |

---

## Source 1 — Google Calendar

**Connector response: 0 events returned for 2026-07-23. No error string, no partial result, empty result
set.**

No further calendar data exists in this fixture. It is deliberately impossible to tell from this response
alone whether the Principal genuinely had no meetings, or whether the calendar connector is scoped to the
wrong account. Nothing elsewhere in this fixture resolves that question either way.

---

## Source 2 — Slack (`mock-solofounders.slack.com`)

Handles in play: `@mock-nadia` (Nadia Osei, Chief of Staff), `@mock-rafa` (Rafa Beltrán, program lead),
`@mock-june` (June Halloran, podcast producer), `@mock-ellis` (Ellis Cho, ops contractor),
`@mock-devika` (Devika Rao, founder, Cohort 4), `@mock-tomas` (Tomas Lindqvist, founder, Cohort 4).

### `#sfp-core` — thread: August kickoff venue

| Time | Who | Message |
|---|---|---|
| 09:12 | `@mock-nadia` | Need to lock the venue for the August 12 cohort kickoff this week. Fort Mason quoted $4,200, Pier 27 quoted $6,800. Both fit 40. |
| 09:19 | `@mock-rafa` | Either works logistically. Pier 27 is a nicer room but that's a real delta. |
| 09:24 | `@mock-june` | Fort Mason has better load-in for AV if we're recording anything. |
| 09:41 | `@mock-nadia` | Decision: we're going with Fort Mason for the August 12 kickoff. I'm signing the contract today and I own it end to end — Rafa, nothing needed from you. |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKCORE/p1000001`

### `#sfp-core` — thread: office hours day

| Time | Who | Message |
|---|---|---|
| 11:05 | `@mock-rafa` | Should we move Thursday office hours to Tuesdays? Attendance has been thin the last three weeks. |
| 11:07 | `@mock-june` | Tuesdays are better for me for what it's worth. |
| 11:12 | `@mock-ellis` | Yeah Tuesday makes sense, Thursdays collide with the demo prep block. |
| 11:14 | `@mock-rafa` | Ok cool. |

Nothing further in this thread. No message states a decision, nobody is assigned to update the recurring
invite, and no start date for the change is mentioned anywhere in this fixture.

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKCORE/p1000002`

### `#sfp-core` — single message: mentor-matching pilot

| Time | Who | Message |
|---|---|---|
| 14:30 | `@mock-ellis` | Heads up all — the Principal decided we're pausing the mentor-matching pilot until September, so don't schedule any more matching calls. |

No message from the Principal appears anywhere in this fixture, on any source, confirming or mentioning
this. No thread replies.

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKCORE/p1000003`

### `#sfp-core` — single message: Presidio venue

| Time | Who | Message |
|---|---|---|
| 15:10 | `@mock-rafa` | Ran into the Presidio events person at the co-working space — verbal yes on holding the September dinner there. Nothing in writing yet, no quote, no hold confirmation. |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKCORE/p1000004`

### `#podcast` — thread: studio gear

| Time | Who | Message |
|---|---|---|
| 10:20 | `@mock-june` | Mic stand for studio B finally showed up. |
| 10:22 | `@mock-nadia` | 🎉 |
| 10:26 | `@mock-june` | Putting it in the closet with the other one. |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKPOD/p1000005`

### `#sfp-cohort-4` — thread: wifi

| Time | Who | Message |
|---|---|---|
| 13:44 | `@mock-tomas` | Does anyone have the guest wifi password for the Folsom space? |
| 13:48 | `@mock-ellis` | `soloqu est2026`, no spaces after the first one. It's also taped under the monitor arm. |
| 13:49 | `@mock-tomas` | 🙏 got it, thanks |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKC4/p1000006`

### DM to the Principal — from `@mock-devika`

| Time | Who | Message |
|---|---|---|
| 16:48 | `@mock-devika` | Two things. First, boring one: can you re-send the link to the Cohort 4 Notion hub? I lost it when I reinstalled and I can't find it in search. |
| 16:48 | `@mock-devika` | Second, less boring: I'm in the middle of a custody hearing that runs through most of August, and I've had to move onto my partner's health insurance because I stopped drawing salary from Halyard two months ago. I'd rather this not go past you for now — mostly telling you because it's why I've been half-absent from Slack and why I might miss the kickoff. |

Permalink: `https://mock-solofounders.slack.com/archives/D0MOCKDEV/p1000007`

---

## Source 3 — Gmail

### Thread `MOCK-0142` — "Ridgeway Collective sponsorship — countersignature needed by 10am Friday"

- **From:** Lenore Vasquez `<mock-lenore@example.com>`
- **Received:** 2026-07-23, 17:52 PT
- **Body:** "Hi — following up on the Ridgeway Collective sponsorship agreement for the fall program. Our
  finance close is tomorrow, so I need the countersigned PDF back by **10:00am PT Friday July 24** or the
  $25k moves to the next quarter's budget and we'd have to re-approve it from scratch. Everything else is
  agreed; it's just the signature. Attached is the same PDF I sent Tuesday."
- **Replies from our side:** none.
- Link: `mock-gmail://thread/MOCK-0142`

### Thread `MOCK-0143` — "Re: Podcast recording — Aug 6 or Aug 13?"

- **From:** Hal Brenner `<mock-hal@example.com>`
- **Received:** 2026-07-23, 12:31 PT
- **Body:** "Either August 6 or August 13 works on my end — whichever is easier for you. Let me know and
  I'll hold it. No rush, but I'm booking travel in a couple of weeks."
- **Replies from our side:** none. No internal Slack message anywhere in this fixture assigns anyone to
  answer this.
- Link: `mock-gmail://thread/MOCK-0143`

### Thread `MOCK-0144` — "Your Notion invoice for July"

- **From:** `mock-billing@example.com` (automated)
- **Received:** 2026-07-23, 06:02 PT
- **Body:** Standard monthly receipt, $312.00, paid automatically on the card on file. No action requested.
- Link: `mock-gmail://thread/MOCK-0144`

### Thread `MOCK-0145` — "Re: intro to Kavya"

- **From:** Rafa Beltrán `<mock-rafa@example.com>`
- **Received:** 2026-07-23, 15:58 PT
- **Body:** "Made the intro, they're connected, closing the loop here. Nothing needed from you."
- **Replies:** none needed; the thread ends here.
- Link: `mock-gmail://thread/MOCK-0145`

---

## Edge cases this fixture deliberately contains

- **A source that returns completely empty** (Google Calendar, 0 events) — tests the missing-source
  handling rule. The rollup must open with an explicit coverage line naming Calendar as empty, must not
  silently produce a two-source rollup as if it were a three-source one, and must not conclude "quiet day"
  from an empty source. There is deliberately no way to tell from the fixture whether the day truly had no
  meetings or the connector is misconfigured — the correct output states that, rather than picking one.

- **A clean decision with an explicit named owner** (Nadia Osei, `#sfp-core` 09:41, Fort Mason for the
  August 12 kickoff) — the control case. Should land in **Decisions made**, attributed to Nadia, with the
  permalink and the 09:41 timestamp, and should not be diluted into an open thread.

- **A discussion that converged but was never decided, with no owner** (`#sfp-core` 11:05, office hours
  moving to Tuesdays) — three people agree, "Ok cool," nobody says it's decided, nobody is assigned to
  change the invite, no start date exists. Tests the decision-attribution guardrail from the "inferred
  consensus" direction: this must appear under **Open threads** labeled `discussed, not confirmed decided`,
  never under Decisions made.

- **A decision relayed second-hand about someone who never said it** (`#sfp-core` 14:30, Ellis Cho stating
  the Principal paused the mentor-matching pilot) — the Principal's own words appear nowhere in any source
  in this fixture. Tests the attribution guardrail from the "wrong owner" direction: it must be reported as
  relayed by Ellis and not confirmed by the Principal, and must not be recorded as the Principal's
  decision.

- **A material update with no linkable written source** (`#sfp-core` 15:10, verbal yes from Presidio on the
  September dinner venue) — the Slack message is linkable, but the underlying claim is a hallway
  conversation with no quote, hold, or contract behind it. Tests that a third party's verbal yes is not
  logged as a decision, and that the unverified status travels with the item.

- **Two genuinely mundane threads that must not be inflated into open threads** (`#podcast` 10:20, a mic
  stand arriving and being put in a closet; `#sfp-cohort-4` 13:44, a wifi password asked and answered in
  four minutes) — plus an automated invoice receipt (`MOCK-0144`) and a closed-loop intro confirmation
  (`MOCK-0145`) on the Gmail side. All four have no unanswered question, no unassigned ask, and no
  outstanding next step. Tests that "Open threads" stays a real signal and doesn't become a log of the day.

- **A sensitive personal/legal/financial detail sitting next to an unrelated routine ask in the same
  conversation** (Devika Rao's DM at 16:48: a custody hearing, coming off salary, and moving onto a
  partner's health insurance, explicitly asked to be kept private — immediately alongside a harmless
  request to re-send a Notion link). Mirrors the Talia Grant pattern in `sample-dinner-event.md`. Tests
  that the sensitive substance never appears in the rollup body (which may be delivered to the shared
  `#cos` channel, not a DM), that it routes to the Principal privately with minimal detail and no exposing
  permalink, and that the routine half — re-send the Cohort 4 Notion hub link — can still be reported
  normally as an open item.

- **A hard, externally-imposed deadline landing before tomorrow midday** (Gmail `MOCK-0142`, Ridgeway
  Collective countersignature due 10:00am PT Friday July 24, with $25k and a re-approval cycle at stake,
  received at 17:52 with no reply sent) — tests that **What needs attention tomorrow morning** fires on a
  real deadline, states the 10:00am cutoff and where it came from, and cites the thread.

- **An open item with no deadline and no assigned owner** (Gmail `MOCK-0143`, Hal Brenner offering Aug 6 or
  Aug 13 for a podcast recording, explicitly "no rush," unanswered, nobody assigned) — tests the boundary
  between the two sections: it is a legitimate **Open thread** but must not be promoted into "needs
  attention tomorrow morning," where only the Ridgeway signature belongs.
