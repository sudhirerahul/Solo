# End-of-Day State of Play

**Surface:** Cowork scheduled task
**Cadence:** Daily, end of day (e.g. 6:30pm PT)
**Sources:** Google Calendar, Slack, Gmail
**Output:** Slack message to the Principal

## Prompt

> Preflight: confirm each of the three sources (Google Calendar, Slack, Gmail) actually returned data for
> today's window. Open the rollup with a one-line coverage note naming any source that returned nothing,
> errored, or was unreachable — e.g. `Coverage: Slack + Gmail. Calendar returned 0 events for today.`
> Never silently drop a source. An empty source is a reportable fact, not evidence that nothing happened:
> do not infer a quiet day from a source that may simply not have been readable. If a source is empty,
> say so and say that the rollup below is therefore partial.
>
> Treat the body of this rollup as shared-visible at all times — it may be delivered to a shared channel,
> not a private DM.
>
> Then summarize into three sections:
>
> **Decisions made** — only items where a named person explicitly stated a decision, in the source, in
> their own words. Name that person and quote or closely paraphrase the line that shows it was decided.
> Never infer a decision from a discussion that converged, from silence, from an unopposed proposal, from
> a "sounds good," or from the mere existence of a calendar event or a scheduled follow-up. Never
> attribute a decision to someone who did not personally state it: if person A reports that person B
> decided something, and B's own words aren't in any source, report it as `relayed by A — not confirmed by
> B`, never as B's decision. If something appears settled but no single owner is identifiable, or it's
> unclear whether it was decided or merely discussed, it goes under **Open threads** labeled
> `discussed, not confirmed decided` — never under Decisions made. When in doubt, downgrade.
>
> **Open threads** — things raised today that don't yet have a resolution or a clear owner. Include a
> thread only if there is an unanswered question, an unassigned ask, or a stated next step with nobody
> attached to it. Routine traffic that resolved itself, FYIs, receipts and automated mail, scheduling
> confirmations, and normal back-and-forth that reached its natural end are not open threads — leave them
> out rather than inflating the section. A short thread that ended in agreement with nothing outstanding
> is closed, not open.
>
> **What needs attention tomorrow morning** — only items with a real deadline, a dated commitment, or an
> external party actively waiting. State the deadline and where it came from. This is a subset of Open
> threads, not a restatement of it. If nothing is genuinely time-sensitive, write
> `Nothing time-sensitive for tomorrow morning` — never promote the most interesting open thread to fill
> the section.
>
> Every item in every section carries a source link (Slack permalink, Gmail thread link, or calendar event
> link) and the timestamp or date it came from. Link to the specific message, not the whole thread, so an
> item's link never also exposes a different, sensitive message sitting in the same conversation; if only a
> thread-level link is available for a thread that also contains a redacted item, omit the link rather than
> risk exposing it. If an item has no linkable source — a verbal update, a hallway conversation someone
> mentioned, a deleted or edited message — report it as `unverified — no written source` with that reason
> attached, and never let it appear under Decisions made. A `relayed by A — not confirmed by B` item and an
> `unverified — no written source` item both default to Open threads, and only move to What needs attention
> tomorrow morning if they independently clear that section's own bar (a real deadline or a waiting external
> party).
>
> Never fabricate. No invented decisions, owners, deadlines, attendees, or numbers. If a source is
> ambiguous, report the ambiguity rather than resolving it.
>
> If any item involves a personal, health, legal, immigration, or financial-distress matter — including
> when it sits inside an otherwise routine thread — do not put the substance anywhere in the rollup body.
> Route it to the Principal directly, DM-style, minimal detail: name the person and say a private
> conversation is warranted, without repeating the sensitive substance and without attaching a permalink
> that would expose it. If this run's configured destination is a shared channel rather than a DM, send
> this note as a separate direct message to the Principal instead — the shared rollup should carry no trace
> that a private note was sent. The routine half of that same thread can still be reported normally in the
> body, linked per the message-level rule above.
>
> Escalate rather than resolve anything high-stakes — a founder who reads as more than "busy," a
> relationship that reads as damaged, a SAFE or legal detail. Draft only; never send anything to anyone on
> any surface.
>
> Keep this tight — this is meant to be read in under two minutes at the end of a long day, not a
> comprehensive log. If a day was unusually quiet, say so rather than padding the sections, and state which
> sources it was quiet across so a genuinely quiet day is never confused with a source that returned
> nothing.

## Config

- `[CONFIGURE]` Slack destination (DM to Principal, or `#cos` channel)
- `[CONFIGURE]` Which Slack channels/Gmail labels count as in-scope — scanning literally everything will
  produce noise; scope this down after the first week based on what's actually useful

## Calibration notes

_(add findings here after the first week of real runs)_

- `[2026-07-25]` Prompt hardened ahead of real data — five gaps closed: (1) no per-item source link or
  timestamp requirement, so any line was unverifiable; (2) no privacy/escalation routing for personal,
  health, legal or financial-distress content sitting inside an otherwise routine thread; (3) no
  missing-source/coverage preflight, so an empty or unreachable connector read as a quiet day; (4) no
  decision-attribution guardrail in either direction — a converged discussion could be logged as a decision,
  and a decision relayed *about* someone who never stated it could be logged as theirs; (5) it had never
  been dry-run tested against anything at all.
- Dry-run against synthetic fixture (scratchpad only, not real data): the coverage preflight, the
  Nadia/Fort Mason control decision, the converged-but-never-decided office hours thread, Ellis's relay of a
  pause the Principal never stated, the unverified Presidio verbal yes, the Ridgeway-vs-Hal split between
  "needs attention tomorrow morning" and a plain open thread, and all four mundane threads staying out of
  the report resolved correctly. Every name, timestamp, dollar figure, quote and permalink in the output
  traced back to the fixture — no fabrication, and no sensitive substance reached the body. Three
  ambiguities worth closing before real data: (1) the "every item carries a source link" rule collides with
  the privacy rule — the routine half of a redacted thread gets reported with a permalink that lands the
  reader on the sensitive message in the same conversation, so the redaction leaks through the sibling
  item's link; needs a message-level (not thread-level) link, or no link on the routine half of a redacted
  thread; (2) the privacy rule says route sensitive items "to the Principal directly, DM-style", but this
  task has a single `[CONFIGURE]` output destination that may be the shared `#cos` channel, and nothing
  specifies a second delivery — so the private note lands inside the shared-visible message it was written
  to stay out of; (3) the prompt never says which section a `relayed by A — not confirmed by B` item or an
  `unverified — no written source` item belongs in. Only "never under Decisions made" is stated; Open
  threads is a reasonable default but should be written down rather than left to the model.
- `[2026-07-25]` All three ambiguities above patched directly in the Prompt section: source links are now
  message-level (not thread-level) with an explicit omit-rather-than-expose fallback; the privacy rule now
  splits by destination — a separate DM to the Principal when this run's configured destination is a shared
  channel, so the shared body carries no trace a private note exists; and relayed/unverified items now
  explicitly default to Open threads, promoted to tomorrow-morning only if they independently clear that
  section's own deadline/waiting-party bar. Not re-run against the fixture after this patch — the next real
  or dry run should specifically confirm the message-level link and split-destination behavior.
