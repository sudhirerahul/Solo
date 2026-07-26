# Relationship Staleness Check

**Surface:** Cowork scheduled task
**Cadence:** Weekly
**Sources:** Notion (investor/partner CRM), Gmail, Calendar
**Output:** Slack message to the Principal with drafted check-in notes attached per flagged contact

## Prompt

> Preflight: if the investor/partner CRM database is not resolved and accessible, output exactly
> `CANNOT RUN — missing <field>` and stop. Never reconstruct a contact list from Gmail/Calendar activity
> alone — the CRM roster is the only valid source of who's on this list.
>
> Enumerate contacts from the CRM's roster of record — never from whoever happens to have recent
> email/calendar activity. A contact with zero findable activity anywhere is still on the list if the CRM
> says so, and is the highest-risk case, not one to skip.
>
> For each contact, find the last real touchpoint (an email exchange, a call on the calendar, a
> Slack/text mention if tracked) — not just the last time they were added to a list. Every last-touchpoint
> claim must carry a cited source (the specific email thread, calendar event, or tracked mention) plus a
> date. If no source can be found, report that contact's status as `unknown` — never assert a touchpoint
> date without a source, and never quietly drop the contact from the report for lack of data.
>
> Apply a per-tier staleness threshold (see Config) rather than one blanket window. If a contact has no
> tier assigned, use a default 30-45 day window AND explicitly flag the missing tier alongside the
> finding — don't silently fall back to the default without saying so.
>
> Flag anyone past their tier's threshold, plus every `unknown`-state contact regardless of window or
> tier — `unknown` is not "probably fine," it's the least-verified, most-at-risk case and always gets
> surfaced.
>
> For each flagged contact who needs a check-in, draft a short, warm note referencing something specific
> and current (a portfolio update relevant to them, something SFP has shipped recently, a person they'd
> want to be introduced to) rather than a generic "checking in!" Draft only — a human sends.
>
> Group the output by how long it's been stale, longest first. Tiebreak contacts at the same staleness by:
> (1) relationship tier, higher-priority tier first (e.g. lead investor before casual advisor); (2)
> contact name, alphabetically, as the final deterministic tiebreak. Sort every `unknown`-state contact
> above all dated buckets, since an unknown is more urgent than any measured staleness.
>
> Escalation clause: if a contact's staleness reads as an actually damaged relationship — a cooled tone, an
> unanswered pointed question, a dropped commitment — not just an ordinary lapsed cadence, do not fold it
> into a routine check-in draft. Escalate it directly to the Principal as a relationship-risk item, and do
> not quote the sensitive or reputationally-sensitive detail verbatim in the grouped digest; surface that
> the escalation exists and let the Principal pull the thread themselves.
>
> If no one is flagged, say so plainly ("No one flagged this week") — never omit the report even when
> it's empty.

## Config

- `[CONFIGURE]` Notion CRM DB URL for investors/partners — cannot currently be resolved: the connected
  Notion workspace has zero SFP content (searched for "investor partner CRM contact list" this session,
  zero relevant hits — only unrelated GovTech content). See `tasks/todo.md` for the full blocker record.
- `[CONFIGURE]` Relationship-tier taxonomy — needs Principal input on what tiers actually exist (e.g.
  lead investor / casual advisor / operator peer / press contact) and which contacts fall into each; the
  prompt above assumes tiers exist and have a priority ordering, but the real taxonomy isn't defined yet.
- `[CONFIGURE]` Per-tier staleness threshold — once the taxonomy above is confirmed, each tier needs its
  own window (a lead investor vs. a casual advisor probably has a different staleness threshold); contacts
  with no tier assigned fall back to the default 30-45 day window per the prompt above.
- Check-in drafts are drafts only — a human sends.

## Calibration notes

_(add findings here after the first few runs)_

- `[2026-07-25]` Connector blocker re-confirmed via live Notion search this session for "investor partner
  CRM contact list" and "Solo Founders Program" — zero relevant hits, only unrelated GovTech content; see
  `tasks/todo.md`. Prompt hardened ahead of real data becoming available: (1) preflight `CANNOT RUN` abort
  if the CRM isn't resolved; (2) enumerate from the CRM roster of record, never from activity alone; (3)
  every touchpoint claim requires a cited source + date, else `unknown`; (4) per-tier staleness threshold
  with an explicit flag when a tier is missing and the default window is used; (5) `unknown` contacts flag
  regardless of window, ranked above every dated bucket; (6) drafts reference something specific and
  current, never generic; (7) sort by staleness longest-first, tiebreak by tier priority then contact name;
  (8) escalation clause routes actually-damaged relationships to the Principal directly, redacted out of
  the shared digest; (9) explicit "no one flagged" fallback line so the report is never silently omitted.
  A synthetic dry-run was run against this hardened prompt — see
  `cowork/fixtures/sample-investor-partner-crm.md` and Sections E/F/G of
  `cowork/fixtures/dry-run-2026-07-25.md`.
