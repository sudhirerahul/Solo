# Dry Run — Weekly Time Audit — 2026-07-26

Manual dry run of `cowork/weekly-time-audit.md`'s prompt, executed exactly as written (no prompt changes
made before running it), against `cowork/fixtures/sample-week-calendar.md`. The live Google Calendar
connector is not authorized for this session (see `tasks/todo.md`), so this is a by-hand simulation of
what the prompt would produce, done to calibrate it before it's wired to a real calendar. Nothing here was
sent anywhere.

## Section A — Dry-run output (as the automation would produce it)

### Percentage breakdown of the week (2026-07-20 to 2026-07-24)

Total scheduled time across the week: **1,230 minutes (20.5 hours)**.

| Category | Minutes | Share |
|---|---|---|
| Podcast production | 300 | 24% |
| SFP founder 1:1s | 210 | 17% |
| Investor/partner calls | 210 | 17% |
| Internal ops | 210 | 17% |
| Event/dinner logistics | 150 | 12% |
| Media/community | 150 | 12% |

Podcast production was the single biggest draw on calendar time this week (two recordings totaling 150
min, an editing-coordination call, a guest-prep call, and a guest-booking call). SFP founder 1:1s,
investor/partner calls, and internal ops are tied at 17% each. Event logistics and media/community are
tied at the low end, 12% each.

*(Rounded shares sum to 99%, not 100% — a rounding artifact of five categories each rounding down from an
x.07%/x.20%/x.39% raw share, not an arithmetic error. See Section C for the unrounded check.)*

### Flagged for delegation or cutting next week

1. **1:1 — Marcus Whitfield (Fernwood Analytics), Monday 1:00–1:30pm, recurring.** Cut/delegate candidate.
   Reason: the last 3 occurrences (2026-07-06, 2026-07-13, 2026-07-20) were each a status update only,
   with no decision made in any of them — Marcus recapped the same open items each time and the Principal's
   guidance didn't change week to week. This is a concrete instance of the prompt's own example: "a
   founder 1:1 that's become a status-update the CoS could collect instead." Recommend the CoS collect
   this as an async or CoS-run check-in and free the Monday 1pm slot, with an explicit standing
   escalation path back to a live 1:1 the moment a real decision is on the table.

2. **Tuesday 2:00–2:30pm (hiring pipeline review) and 2:30–3:00pm (contractor onboarding sync).**
   Cut/delegate candidate. Reason: identical attendees (Principal + Jamie Chen) back-to-back with no other
   invitees on either meeting — this is the "attendee overlap with another meeting" case. Recommend
   merging into a single 30–45 min ops block, or having Jamie Chen run both and loop the Principal in only
   on the hiring decision itself.

3. **Newsletter ideation call, Tuesday 11:30am–12:00pm, recurring.** Cut/delegate candidate. Reason: no
   agenda, doc, or prep material has ever been requested or circulated ahead of this call across its
   6-month history. Recommend Zara Boone (content contractor) draft ideas async and bring the Principal
   only a shortlist to react to, rather than a live ideation slot every time.

### Not flagged, despite being recurring / repeat contact

- **1:1 — Priya Oyelaran-Nkemdirim (Solstice Robotics), Monday 9:00–9:30am.** Not flagged. The last 3
  occurrences each produced a distinct, concrete decision (bridge-note pass in favor of cost cuts on
  2026-07-06; enterprise pricing-tier change on 2026-07-13; ops-hire offer approval on 2026-07-20). No
  attendee overlap and no prep-material gap exists for this meeting. Recurring alone is not a reason to
  flag a founder 1:1 — this one shows no concrete reason to.
- **Quarterly check-in — Ravi Chen (Meridian Capital), Tuesday 1:00–1:30pm.** Not flagged. Substantive
  agenda (cohort milestones, runway), quarterly cadence tied to his board-observer arrangement, not a
  weekly no-decision pattern. An investor call being a repeat contact is not itself a reason to flag it.

## Section B — Explicit check: was the "don't flag by default" rule honored?

Yes. Of the 7 founder 1:1s and 5 investor/partner calls on the week's calendar, only one of each category
type could plausibly be flagged (Marcus Whitfield among the 1:1s), and it was flagged only because a
concrete reason exists (3/3 occurrences with no decision) — the exact category of reason the prompt's own
example describes. The other 6 founder 1:1s and all 5 investor/partner calls, including Priya's and Ravi
Chen's despite both being recurring/repeat, were left unflagged with no reason invented to flag them. The
rule was not just nominally followed — it was tested against a same-category pair (Priya vs. Marcus,
both weekly recurring founder 1:1s) built specifically so a prompt that flagged recurrence alone, rather
than the presence of a concrete reason, would fail this dry run. It did not fail.

## Section C — Arithmetic check (percentage math against the fixture)

Recomputed independently from the per-day tables in `sample-week-calendar.md`, not from the pre-summed
"Week totals" table in that file:

- SFP founder 1:1s: Mon 60 (Priya 30 + Marcus W. 30) + Tue 60 (Elena 30 + Sana 30) + Wed 30 (Diego) + Thu
  30 (Tobias) + Fri 30 (Amara) = **210 min**
- Investor/partner calls: Mon 60 (Two Rivers intro) + Tue 30 (Ravi Chen) + Wed 60 (Two Rivers diligence) +
  Thu 30 (Owen Castellan) + Fri 30 (Lena Cho) = **210 min**
- Podcast production: Mon 60 (guest prep) + Tue 60 (recording) + Wed 60 (editing coordination) + Thu 90
  (recording) + Fri 30 (guest booking) = **300 min**
- Event/dinner logistics: Mon 30 + Tue 30 + Wed 30 + Thu 30 + Fri 30 = **150 min**
- Internal ops: Mon 30 (CoS sync) + Tue 60 (hiring review 30 + contractor sync 30) + Wed 30 (metrics) + Thu
  30 (expense review) + Fri 60 (CoS sync #2 30 + retro 30) = **210 min**
- Media/community: Tue 30 (newsletter) + Wed 30 (guest post) + Thu 30 (social clips) + Fri 60 (content
  batch) = **150 min**

Sum: 210 + 210 + 300 + 150 + 210 + 150 = **1,230 min**, matching the stated week total exactly. Each
category's raw share: 210/1230 = 17.07%, 300/1230 = 24.39%, 150/1230 = 12.20%. The whole-number
percentages reported in Section A (17%, 17%, 17%, 24%, 12%, 12%) are each the correctly rounded value —
**the math checks out.** The 99%-not-100% total is the expected consequence of rounding five numbers down
from x.07/x.20/x.39 fractions, not a computational error, and is called out as such in Section A rather
than silently left to look wrong.

## Section D — A real gap this dry run surfaced (category boundary)

Two Thursday/Friday events sit right on the boundary between "podcast production (recordings, prep,
editing coordination)" and "media/community (everything else public-facing)" as the prompt currently
defines them: **Podcast social clips review** (Thursday, reviewing clip cuts from an already-recorded
episode for social distribution) and **Content batch recording** (Friday, recording short-form
social/Instagram/Twitter clips). Both are downstream of a recorded episode and both are podcast-adjacent,
but neither is "recording, prep, [or] editing coordination" of the episode itself in the narrow sense, and
both are squarely public-facing distribution work. The prompt as written gives no rule for which bucket
wins, so two runs of the same week could plausibly land these in different categories and silently shift
the reported percentages by up to 90 minutes (7% of the week) between "podcast production" and
"media/community" with no visible reason why. This fixture categorized both as media/community (social
distribution, not production of the episode itself) for the output in Section A, but that was a judgment
call the prompt doesn't actually make for the executor. **Fixed directly in `cowork/weekly-time-audit.md`**
— see the Calibration notes entry there for the exact wording added.

## Section E — Guardrail verification table

| Check | Pass/Fail/Concern | Evidence |
|---|---|---|
| 1. Never auto-send | Pass (trivial) | This automation produces no externally-facing draft of any kind — its entire output is an internal percentage breakdown and cut/delegate recommendations for the Principal. There is nothing to send in the first place, so this guardrail has nothing to violate here; noted rather than silently skipped. |
| 2. Never fabricate | Pass | Every minute in the percentage breakdown and every cut/delegate reason traces to a specific calendar row, day, and time in `sample-week-calendar.md` (see Section C for the full arithmetic trace). No invented meeting, decision, or history was introduced — the decision-log entries used to justify flags 1 and the two non-flags all exist verbatim in the fixture's "Decision log" section. |
| 3. Cite the source | Pass | Each of the 3 flagged meetings and both non-flagged control cases names the specific day, time, and (for the recurring ones) the last 3 occurrence dates from the decision log. |
| 4. Voice | Pass | Recommendations are specific to each meeting's actual pattern (Marcus's status-update recap, the Tuesday ops back-to-back, the newsletter call's 6-month no-prep history) rather than generic "consider streamlining your calendar" language. Zero uses of "optimize," "leverage your time," or similar generic productivity-speak across the output. |
| 5. Escalate, don't guess | N/A / Pass | Nothing in this fixture reads as high-stakes (no founder distress signal, no damaged investor relationship, no legal/financial detail) — this automation's domain is lower-stakes than relationship or event automations by design, so there was nothing to escalate rather than a guardrail that was silently satisfied by omission. Noted rather than rubber-stamped. |
| 6. Human-in-the-loop | Pass | All 3 delegate/cut items are framed as "recommend," not as an automatic calendar change — merging the Tuesday ops meetings, moving the newsletter call async, and collecting Marcus's update via the CoS are all presented as the Principal's call to accept or reject next week. |
| 7. No fabricated config | Pass | The `[CONFIGURE]` Notion DB placeholder in `cowork/weekly-time-audit.md` was not touched or filled with an invented URL during this dry run or the prompt fix in Section D. |

## Section F — Special-attention checks (per the task brief)

- **Percentage math correctness**: verified independently in Section C by re-deriving each category total
  from the day-by-day tables (not the fixture's own pre-summed table) and confirming the sum (1,230) and
  each rounded share match what Section A reported.
- **"Don't flag founder 1:1s/investor calls as cuttable by default" rule**: verified explicitly in
  Section B using a same-category control pair (Priya vs. Marcus Whitfield, both weekly recurring founder
  1:1s) built specifically so recurrence alone, if wrongly treated as sufficient reason to flag, would have
  produced a false positive on Priya. It did not.

## Section G — Pending real-world inputs (blocking live wiring)

Consolidated from the `[CONFIGURE]` markers in `cowork/weekly-time-audit.md`:

- Notion DB (or doc) URL to append the weekly breakdown to, so trends are visible over time
- Confirmation, after the first month of real runs, of whether the 6-category list above still matches
  what actually eats the Principal's calendar time, or needs to be added to / merged
