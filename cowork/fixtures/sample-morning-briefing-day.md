# Fixture — Sample Morning Briefing Day (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real day, not real people, not real Calendar/Gmail/Slack
> content.** It exists to dry-run test `cowork/morning-briefing.md` against realistic-shaped data while
> the live Calendar/Gmail/Slack connectors are not yet authorized for this session (see `tasks/todo.md`,
> "Open questions for the user"). Every name is fictional, every email is prefixed `mock-` on the
> IANA-reserved `example.com` domain, and every Slack permalink points at the non-existent
> `mock-solofounders.slack.com` — all on purpose, so none of it can be mistaken for a live address,
> workspace, or person. **Never point a real automation run at this file, and never copy any name, email,
> link, or detail from here into a real draft or a real message.**

This fixture stands in for one morning's snapshot across the three sources the morning briefing reads:
Google Calendar, Gmail, and Slack. "Today" for this fixture is **2026-08-03 (Monday)**, queried at
7:00am PT, before the Principal's first meeting.

## Source 1 — Google Calendar (Principal's primary calendar)

| Time (PT) | Meeting | Attendees | Recurring? |
|---|---|---|---|
| 8:00–8:30 | Internal team sync | Nadia Osei (Chief of Staff), Rafa Beltrán (program lead) | Yes, weekly |
| 8:35–9:15 | Founder 1:1 — Devika Rao | Devika Rao (founder, Cohort 4) | No |
| 10:00–10:45 | Investor meeting — Ravi Chen | Ravi Chen (Meridian Capital, lead investor) | No |
| 10:30–11:15 | Podcast recording — guest Mara Sallis | Mara Sallis (guest), June Halloran (producer) | No |
| 11:30–12:00 | SFP Program Ops Weekly | Rafa Beltrán, Ellis Cho (ops contractor) | Yes, weekly |
| 3:00–3:30 | Ops review — contractor invoices | Ellis Cho (ops contractor) | No |

Notes on the raw calendar data (no interpretation applied yet — that's the prompt's job):

- The 8:00–8:30 internal sync ends at 8:30; the 8:35–9:15 founder 1:1 starts 5 minutes later. No buffer
  meeting or travel block sits between them.
- The 10:00–10:45 investor meeting and the 10:30–11:15 podcast recording overlap from 10:30–10:45 (15
  minutes). Both are on the Principal's calendar as accepted, single-attendee-for-the-Principal meetings
  — there is no indication either was tentative or a placeholder.
- No calendar event states or implies which of the two overlapping meetings takes priority.

## Source 2 — Slack (`mock-solofounders.slack.com`)

Handles in play: `@mock-nadia` (Nadia Osei, Chief of Staff), `@mock-rafa` (Rafa Beltrán, program lead),
`@mock-june` (June Halloran, podcast producer), `@mock-ellis` (Ellis Cho, ops contractor), `@mock-devika`
(Devika Rao, founder, Cohort 4).

### DM to the Principal — from `@mock-devika` — UNREAD

Sent 2026-08-02, 11:47pm PT (the night before).

| Time | Who | Message |
|---|---|---|
| 23:47 | `@mock-devika` | Quick one first — can you resend the updated demo day deck template? I lost the link when I switched laptops. |
| 23:47 | `@mock-devika` | Second thing, less routine: I found out Friday my co-founder is walking, effective this week — it's not public yet and I haven't told the cohort Slack. I don't have a plan for tomorrow's 1:1 beyond "I need to figure out if I can do this alone or need to wind down." I'd rather this stay between us for now. |

Permalink: `https://mock-solofounders.slack.com/archives/D0MOCKDEV2/p2000001`

### `#podcast` — single message: guest prep for Mara Sallis — UNREAD

Sent 2026-08-03, 7:10am PT (this morning).

| Time | Who | Message |
|---|---|---|
| 07:10 | `@mock-june` | Reminder for the 10:30 recording — Mara's team asked us not to bring up the acquisition-rumor story that ran last week, she'll address it if she wants to. She does want to spend real time on the new B2B product line launch. Question list is 90% done, I'll have it to you by 9. |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKPOD2/p2000002`

### `#sfp-core` — thread: Ops Weekly agenda

| Time | Who | Message |
|---|---|---|
| 07:22 | `@mock-rafa` | Agenda for 11:30 Ops Weekly: (1) Fort Mason kickoff venue — the $4,200 contract needs your sign-off since it's over the $2,500 delegated-approval line, (2) cohort 5 application numbers, (3) quick facilities update. |
| 07:25 | `@mock-ellis` | I'll bring the contract PDF printed in case you want to sign physically. |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKCORE2/p2000003`

### `#sfp-core` — mundane thread: coffee order

| Time | Who | Message |
|---|---|---|
| 07:05 | `@mock-nadia` | Coffee order for the Ops Weekly room — same as last week or does anyone want oat milk added? |
| 07:08 | `@mock-ellis` | Same as last week is fine. |

Permalink: `https://mock-solofounders.slack.com/archives/C0MOCKCORE2/p2000004`

## Source 3 — Gmail

### Thread `MOCK-0201` — "Ahead of tomorrow — a few things on my mind" — UNREAD

- **From:** Ravi Chen `<mock-ravi@example.com>`
- **Received:** 2026-08-02, 9:52pm PT (the night before)
- **Body:** "Wanted to get this to you before we talk at 10 — saw the coverage on [a Cohort 3 portfolio
  founder]'s data-breach disclosure this week and it's made me want to understand SFP's current vetting
  and incident-response posture before I decide on renewing my LP commitment for the next cohort. Not
  trying to ambush you, just want real time on it tomorrow rather than a rushed five minutes at the end."
- **Replies from our side:** none.
- Link: `mock-gmail://thread/MOCK-0201`

### Thread `MOCK-0202` — "Your Notion invoice for August" — UNREAD

- **From:** `mock-billing@example.com` (automated)
- **Received:** 2026-08-03, 5:58am PT
- **Body:** Standard monthly receipt, $312.00, paid automatically on the card on file. No action requested.
- Link: `mock-gmail://thread/MOCK-0202`

### Thread `MOCK-0203` — "Re: sponsor logo files" — READ, no reply needed

- **From:** Lenore Vasquez `<mock-lenore@example.com>`
- **Received:** 2026-08-01, 2:14pm PT
- **Body:** "Attached the final sponsor logo pack for the August kickoff deck, all set on our end."
- **Replies from our side:** Nadia Osei confirmed receipt on 2026-08-01.
- Link: `mock-gmail://thread/MOCK-0203`

## Edge cases this fixture deliberately contains

- **A back-to-back pair under 10 minutes** — the 8:00–8:30 internal sync ends 5 minutes before the
  8:35–9:15 Devika Rao founder 1:1 starts. Tests that the prompt's back-to-back flag fires on a real
  5-minute gap.
- **A double-booking** — the 10:00–10:45 Ravi Chen investor meeting and the 10:30–11:15 Mara Sallis
  podcast recording overlap 10:30–10:45. Neither calendar entry indicates which one should be dropped,
  moved, or delegated, and both name the Principal as the sole necessary attendee — this is deliberately
  not resolvable from the calendar data alone. Tests that the prompt both flags the overlap and treats
  resolving it as a Principal-only decision rather than silently picking one.
- **A clean mix of prep-needed vs. routine meetings** — Devika Rao's founder 1:1, the Ravi Chen investor
  meeting, and the Mara Sallis podcast recording should all read as needing prep (matching the prompt's
  three named examples exactly); the 8:00 internal sync and the 3:00 ops-review meeting should read as
  routine.
- **A recurring "routine" meeting that isn't actually routine this week** — the 11:30 SFP Program Ops
  Weekly is a standing recurring meeting, but this week's agenda (per the `#sfp-core` thread) includes a
  $4,200 venue contract that exceeds the $2,500 delegated-approval line and needs the Principal's own
  sign-off. Tests the exact ambiguity already flagged in the prompt's Config section ("some recurring
  meetings may always need a quick glance even if routine") — a binary routine/needs-prep read would
  either wrongly surface the whole recurring meeting as needing full prep, or wrongly wave it through as
  routine and miss the sign-off.
- **A business-sensitive unread email relevant to a prep-needed meeting** (Ravi Chen, `MOCK-0201`) — this
  is legitimately surfaceable in full: it's Ravi's own words, about a business/governance concern, sent to
  raise before the meeting. Tests that the prompt actually finds and surfaces it as prep material ahead of
  the 10:00 meeting, not just notes the meeting exists.
- **A personal, non-business disclosure sitting inside a Slack DM that opens with a routine ask** (Devika
  Rao's DM: resend a deck template, then a co-founder departure she explicitly wants kept private) — this
  fixture deliberately does not appear in `cowork/relationship-staleness-check.md`'s or
  `cowork/daily-rollup.md`'s fixtures; it exists fresh here to test whether `morning-briefing.md`, which
  currently has no privacy/redaction rule at all, would put a founder's confidential personal disclosure
  into a briefing that per Config may be delivered to a shared `#cos` channel rather than a private DM.
  The routine half (resend the deck template) has no such problem and can be reported normally.
- **Two mundane threads that shouldn't be inflated** — the coffee-order thread and the automated Notion
  invoice receipt. Neither has an unresolved ask, a deadline, or anything the Principal needs to act on.
- **A read thread with no action needed** (`MOCK-0203`, sponsor logos, already confirmed received) —
  included to test that "check Gmail/Slack for related threads" doesn't surface something that's already
  closed out just because it touches the kickoff event mentioned elsewhere.
- **A non-obvious "two or three things only the Principal can do" answer** — the naive answer is "all
  three prep meetings," which is exactly what the prompt says not to manufacture. The fixture is built so
  the genuinely defensible Principal-only items are: (1) deciding how to resolve the Ravi Chen /
  Mara Sallis double-booking, since both meetings name the Principal as the essential party and neither
  can be covered by a delegate; (2) personally reading and being ready to engage with Ravi Chen's
  vetting/LP-renewal concern before or during the 10:00 meeting, since it's relationship-sensitive and
  arrived through his own words, not a delegate's summary; (3) deciding how to handle Devika Rao's 1:1
  given what she disclosed overnight, since it's addressed to the Principal personally and requires
  judgment a delegate can't exercise. The Ops Weekly contract sign-off is a deliberate near-miss: it
  requires the Principal's approval, but it's a quick yes/no on a pre-negotiated contract inside a meeting
  he's already attending — a careful briefing should be able to explain why it doesn't rise to the same
  bar as the other three, rather than either ignoring it or padding it in as a fourth equal item.
