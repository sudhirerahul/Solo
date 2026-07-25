# Post-Event Follow-Up Drafts

**Surface:** Cowork scheduled task
**Cadence:** Triggered the day after each dinner/event
**Sources:** Notion (guest list, notes from the event if any), Gmail
**Output:** Draft thank-you/follow-up emails per attendee, plus a one-paragraph recap to the Principal

## Prompt

> The context source is one Notion page per event — the event-notes page — with four expected H2
> sections: **Attendance**, **Per-attendee notes**, **Room / general notes**, and **Asks & intros**. Read
> all four before drafting anything.
>
> Draft short, personalized thank-you or follow-up notes only for attendees who have an actual note on
> file in "Per-attendee notes" — reference something specific from the event or the conversation (a topic
> they raised, a founder they met), never a generic "great to see you." If an attendee has no note on
> file, do not draft anything for them and do not invent a plausible-sounding one; instead list them
> separately under a "no draft written — nothing specific on file" heading. That is the correct outcome
> for that attendee, not a gap to be filled — a generic draft is worse than no draft per the voice
> guardrail in the root `CLAUDE.md`.
>
> Cross-check Attendance against the notes: an attendee marked confirmed on the guest list but recorded as
> a no-show gets no thank-you draft — flag the no-show to the Principal instead, don't draft to someone
> who wasn't there. A walk-in who was never on the original guest list still gets a thank-you draft if a
> note exists for them — "not on the list" and "no notes on file" are different conditions, and only the
> second one blocks a draft.
>
> Any note that reads as high-stakes or ambiguous — a legal or fundraise detail, a relationship that reads
> as damaged, anything beyond a routine "good conversation" — gets escalated to the Principal as a flagged
> line and must never appear in an outgoing thank-you draft. If a single attendee's note mixes a routine
> detail with a high-stakes one (e.g. a harmless ask for feedback sitting next to a disclosed financial or
> personal detail), split it: draft the thank-you using only the routine portion, and escalate the
> high-stakes portion separately. Don't suppress the whole draft over the sensitive half, and don't let the
> sensitive half leak into the draft either.
>
> Separately, write a one-paragraph recap for the Principal on how the event went overall and — this is
> the part that matters most — who specifically should be prioritized for a real follow-up this week (a
> promising founder met for the first time, an investor who seemed newly engaged, anyone who asked for an
> intro). Name names; don't just say "several good conversations happened." Note the no-show and any
> walk-in as open items for the Principal rather than resolving them yourself.

## Config

- `[CONFIGURE]` Notion event-notes page location / template link — someone needs to drop quick notes into
  this page during/right after the event (Attendance, Per-attendee notes, Room / general notes, Asks &
  intros) for this prompt to have anything specific to work with. Without that input, per the voice
  guardrail in the root `CLAUDE.md`, attendees without notes correctly get no draft rather than a generic
  one.
- `[CONFIGURE]` Principal's name
- `[CONFIGURE]` Sending Slack/Gmail account these drafts are created in
- Thank-you drafts are drafts only — a human sends.

## Calibration notes

Findings from the dry run against `cowork/fixtures/sample-dinner-event.md`
(`cowork/fixtures/dry-run-2026-07-25.md`), before this ever touches a live connector:

- Talia Grant's fixture note mixed a routine ask (slide feedback) with a high-stakes disclosure (a bridge
  round falling through and her covering payroll personally) in the same bullet. The original hardened
  language only said "escalate the high-stakes note" without saying what to do about the routine half of
  the same note. Change made: added the explicit split-note rule — draft the routine portion, escalate
  the sensitive portion separately — verified in the dry run, where Talia's draft covers only the slide
  feedback and the bridge-round detail appears solely in the escalation line.
- The original prompt had no rule at all for a confirmed guest who no-shows. Without one, the prompt could
  plausibly have drafted a thank-you to Leo Tran even though the fixture's Attendance section records him
  as never actually attending — a real fabrication risk once cross-checked. Change made: added the
  explicit no-show cross-check rule (no draft, flag instead), confirmed in the dry run — Leo appears only
  as an open question, no thank-you drafted.
- Needed to state explicitly that "not on the original guest list" and "no notes on file" are different
  conditions, since Nora Fitch (a walk-in) has notes but isn't a guest-list row. Change made: added that
  line to the prompt; the dry run confirms Nora gets a draft despite being a walk-in.
- The dry run surfaced a real-world gap rather than a prompt gap: Nora Fitch, as a genuine walk-in, has no
  email or Slack handle anywhere in the fixture (walk-ins aren't in the guest-list DB by definition).
  Nothing needed changing in the prompt for this — the existing "say so, don't fabricate" language already
  covers it correctly (the dry run flags the missing contact rather than inventing one). This is carried
  into `tasks/todo.md` as a real operational gap (capture a walk-in's contact info at the door), not a
  prompt fix.
- The "no draft written — nothing specific on file" list (5 of the 10 attendees) came out clean without
  further changes — this validates the original "a generic draft is worse than no draft" language as
  written, no correction needed there.
