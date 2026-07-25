# RSVP and Reminder Tracking

**Surface:** Cowork scheduled task
**Cadence:** Scheduled around event dates (e.g. 7 days out, 2 days out, day-of) for each dinner/event
**Sources:** Gmail, Google Calendar, Notion (guest list, if tracked there)
**Output:** Draft reminder emails/Slack messages for review, plus a capacity flag to the Principal / CoS

## Prompt

> Check RSVP status for the upcoming dinner or event against the guest list, which lives in the Notion
> database **"Events — Guest List."** Read these properties per guest: RSVP Status, Invited On, Last
> Reminded On, Plus-one. This is a read-only check — never write back to Notion (don't update RSVP Status,
> don't log a "reminded" timestamp back into the DB; that's a human or a separate system's job).
>
> Treat a blank or missing RSVP Status as **"No response."** Never infer it as confirmed, and never guess
> a status from other fields (an invite date alone is not a status). Draft (do not send) a short, warm
> reminder for anyone whose status is "No response" or "Tentative" — including blank-status rows —
> personalized enough that it doesn't read as a mail-merge. Do not draft a reminder for anyone "Declined"
> or already "Confirmed."
>
> If a guest is missing a field needed to draft a good reminder or run the capacity math (no email/Slack
> handle, no company/role to personalize against), say so explicitly and skip that guest rather than
> inferring or fabricating the missing value.
>
> Flag capacity issues explicitly, and show the arithmetic: confirmed count, tentative count, and the
> venue capacity supplied for this run. Count confirmed **and** tentative together against capacity, since
> a tentative guest may still show up — don't judge capacity off confirmed alone. If confirmed + tentative
> is at or over capacity, say so and present closing RSVPs, starting a waitlist, or expanding capacity as
> options for the Principal to choose between — don't pick one. If RSVPs are running well under target
> with the event close, flag that too — that changes what the Principal might want to do (invite a few
> more people, or accept a smaller room).
>
> Per-run inputs — event name, date, venue capacity, RSVP deadline, and days-out stage — are supplied at
> schedule time for each specific event. Never hardcode these into the prompt itself.

## Config

- `[CONFIGURE]` Notion DB URL for "Events — Guest List" — confirm before scheduling
- `[CONFIGURE]` Venue capacity, supplied per run/per event (varies per event — never hardcode a single
  number into this prompt; confirm it's actually being passed at schedule time before trusting the
  capacity flag)
- `[CONFIGURE]` Slack channel or DM destination for the capacity flag to the Principal / CoS, if it's
  delivered via Slack rather than email
- Reminder drafts are drafts only — a human sends, per the guardrails in the root `CLAUDE.md`
- This prompt is read-only against Notion — it never writes RSVP status, reminder timestamps, or anything
  else back to the guest-list DB

## Calibration notes

Findings from the dry run against `cowork/fixtures/sample-dinner-event.md`
(`cowork/fixtures/dry-run-2026-07-25.md`), before this ever touches a live connector:

- The fixture's blank-status row (Ibrahim Saleh) exposed that without an explicit rule, a blank RSVP
  Status could plausibly get skipped or misread as confirmed. Change made: added the explicit "blank =
  No response, never confirmed" rule to the prompt above, before running the dry run. The dry run confirms
  it fires correctly — Ibrahim gets a reminder draft, not silent inclusion in the confirmed headcount.
- The original prompt judged capacity off "confirmed RSVPs" alone. The fixture was built so confirmed
  sits exactly at capacity (8 of 8) with one tentative guest on top — a confirmed-only read would have
  missed that the room is already oversubscribed once tentative is counted. Change made: capacity math now
  explicitly sums confirmed + tentative against the venue number.
- Devon Park's Plus-one field reads "Unknown" in the fixture, not blank and not "No" — a genuinely
  ambiguous middle state. Change made: added the explicit "missing/ambiguous field → say so and skip
  rather than infer" line, confirmed in the dry run's "Could not determine" block.
- Read-only was implicit before, not stated. Since Cowork's Notion connector can technically write, added
  an explicit read-only line to both the prompt and the Config section rather than leaving it assumed.
- Nothing needed changing in the reminder-drafting logic itself — the dry run's four drafts (Ana, Devon,
  Sana, Ibrahim) came out specific and non-generic without further prompt changes, which validates the
  "personalized enough that it doesn't read as a mail-merge" line as originally written.
