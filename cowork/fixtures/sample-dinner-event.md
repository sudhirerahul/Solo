# Fixture — Sample Dinner Event (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real event, not real guests, and not real Notion content.**
> It exists to dry-run test `cowork/rsvp-reminder-tracking.md` and `cowork/post-event-follow-up.md`
> against realistic-shaped data while the live Notion/Slack/Gmail connectors are not yet authorized for
> this session (see `tasks/todo.md`, "Open questions for the user"). Every name is fictional and every
> email is prefixed `mock-` on purpose so it can never be mistaken for a live address. **Never point a
> real automation run at this file, and never copy any name/email/detail from here into a real draft.**

This fixture stands in for two different Notion surfaces at two different moments in the same event's
lifecycle: (1) the guest-list database as it looks a couple of days before the event (for the RSVP
tracking prompt), and (2) the event-notes page as it looks the day after (for the post-event follow-up
prompt). Both describe the same fictional dinner — treat them as two independent snapshots used for two
independent dry runs, not a real minute-by-minute timeline.

## Event meta

| Field | Value |
|---|---|
| Event name | Solo Founders Dinner — SF Summer Cohort, Session 3 |
| Date | 2026-07-27 |
| Venue | The Anchorage, Private Room B (San Francisco) |
| Venue capacity | 8 |
| RSVP deadline | 2026-07-26 |
| Days-out stage | 2 days out |

## Mock Notion DB — "Events — Guest List"

Snapshot as of 2026-07-25 (2 days out from the event).

| Name | Email | Company / Role | RSVP Status | Invited On | Last Reminded On | Plus-one | Notes |
|---|---|---|---|---|---|---|---|
| Jordan Reyes | mock-jordan@example.com | Founder, Kindling AI | Confirmed | 2026-07-15 | 2026-07-20 | No | Met at Q2 demo day, building dev tools |
| Priya Nandakumar | mock-priya@example.com | Investor, Basecamp Ventures | Confirmed | 2026-07-15 | | Yes (+1 Sam) | Asked about intro to fintech founders |
| Marcus Webb | mock-marcus@example.com | Founder, Fieldnote | Declined | 2026-07-15 | 2026-07-18 | No | Traveling, said maybe next cohort dinner |
| Ana Costa | mock-ana@example.com | Operator, Lighthouse Labs | No response | 2026-07-16 | 2026-07-20 | No | |
| Devon Park | mock-devon@example.com | Founder, Ridgeline | No response | 2026-07-16 | | Unknown | First-time invite, referred by Jordan |
| Sana Iqbal | mock-sana@example.com | Founder, Petal Health | Tentative | 2026-07-15 | 2026-07-20 | No | May have a conflicting board meeting |
| Leo Tran | mock-leo@example.com | Investor, North Slope Capital | Confirmed | 2026-07-15 | 2026-07-19 | No | Wants to hear a pitch from a logistics founder |
| Wren Okafor | mock-wren@example.com | Founder, Batch & Bloom | Confirmed | 2026-07-15 | 2026-07-19 | Yes (+1 Reese) | |
| Ibrahim Saleh | mock-ibrahim@example.com | Founder, Cursive Robotics | | 2026-07-17 | | | Invited late, added by Principal directly |
| Chidi Anand | mock-chidi@example.com | Operator, Solo Founders alum | Confirmed | 2026-07-15 | 2026-07-19 | No | Coming to reconnect with cohort |
| Talia Grant | mock-talia@example.com | Founder, Nightjar | Confirmed | 2026-07-15 | 2026-07-19 | No | Asked if she could bring a slide for feedback |

Headcount math for the capacity flag (see dry run in `dry-run-2026-07-25.md` for the worked arithmetic):
confirmed = 8 (Jordan, Priya + Sam, Leo, Wren + Reese, Chidi, Talia), tentative = 1 (Sana), venue capacity = 8.

## Mock Notion event-notes page (post-event)

Snapshot as of 2026-07-28 (the day after the event) — a separate mock page, not the same page as the
guest-list DB above.

### Attendance

- Jordan Reyes — attended
- Priya Nandakumar — attended, with plus-one Sam Whitfield
- Wren Okafor — attended, with plus-one Reese Calloway
- Chidi Anand — attended
- Talia Grant — attended
- Sana Iqbal — attended (was Tentative, showed up)
- Ibrahim Saleh — attended (blank RSVP status on the guest list, showed up anyway)
- Leo Tran — **confirmed RSVP, did not attend, no message received (no-show)**
- Nora Fitch — **walk-in, not on the original guest list**, arrived with Chidi

### Per-attendee notes

- Jordan Reyes — passed along a draft of Kindling's seed deck for a sanity check ahead of their raise;
  wants written feedback by Friday.
- Priya Nandakumar — confirmed she wants an intro to a fintech-focused founder in the cohort; mentioned
  Basecamp closes new fund commitments end of Q3.
- Wren Okafor — said Batch & Bloom hit its first $10k retail order this week; asked if the podcast would
  ever cover consumer CPG.
- Talia Grant — mentioned Nightjar's bridge round fell through and she's personally covering payroll for
  one more month; asked that this not go further for now. Separately, and unrelated to that, asked for
  feedback on a slide deck she brought.
- Nora Fitch — building a solo ops tool for restaurant owners; asked good questions about the cohort's
  application process.

No notes on file for: Sam Whitfield, Reese Calloway, Chidi Anand, Sana Iqbal, Ibrahim Saleh.

### Room / general notes

Room ran a bit warm partway through; nobody seemed to mind. Conversation at the back half of the table
was dominated by the fintech-intro thread between Priya and Jordan. Good energy overall; ran about 30
minutes past the scheduled end time and nobody left early.

### Asks & intros

- Priya Nandakumar asked for an intro to a fintech-focused founder in the cohort.
- Talia Grant asked for feedback on a slide deck (the deck ask only — not the bridge-round detail above).
- Nora Fitch asked about the cohort's application process.

## Edge cases this fixture deliberately contains

- **Blank RSVP Status** (Ibrahim Saleh) — must be treated as "No response," never inferred as confirmed.
- **Blank / "Unknown" Plus-one fields** (Devon Park, Ibrahim Saleh) — must not be fabricated into a
  headcount or a named guest.
- **Confirmed + tentative at or over capacity** (8 confirmed + 1 tentative = 9, against a capacity of 8) —
  the capacity flag has a genuine reason to fire, not a hypothetical one.
- **Confirmed guest recorded as a no-show** (Leo Tran) — should be flagged, not drafted a thank-you.
- **Walk-in never on the original guest list** (Nora Fitch) — should still get a thank-you draft because
  notes exist for her, testing that "not on the list" and "no notes on file" are different conditions.
- **Attendees with no notes on file** (Sam Whitfield, Reese Calloway, Chidi Anand, Sana Iqbal, Ibrahim
  Saleh) — tests that no draft gets fabricated for them.
- **A high-stakes / ambiguous note mixed with a routine ask in the same bullet** (Talia Grant: a fundraise
  / personal-finance detail sitting next to an unrelated, harmless slide-feedback ask) — tests that the
  sensitive half gets escalated and never appears in a draft, while the routine half can still be used.
- **A declined guest** (Marcus Webb) — should get no reminder draft at all.
