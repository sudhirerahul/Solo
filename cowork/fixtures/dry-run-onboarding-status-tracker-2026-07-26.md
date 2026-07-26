# Dry Run — Onboarding Status Tracker — 2026-07-26

Manual dry run of `cowork/onboarding-status-tracker.md` **as originally written** (no prompt improvements
made before running it) against the new fixture `cowork/fixtures/sample-cohort-onboarding-checklist.md`.
Live Notion/Gmail connectors are not authorized for this session (see `tasks/todo.md`), so this is a
by-hand simulation done to calibrate the prompt before real connector wiring. Nothing here was sent
anywhere; the "who's behind" report below is exactly that — a report, never auto-sent. This replaces the
prior vague "dry-run against synthetic fixture (scratchpad only, not real data)" bullet in the prompt's
Calibration notes, which had no persisted fixture or output behind it.

## Section A — Preflight

Cohort start date (2026-08-01) and the onboarding-checklist DB (the fixture's "Cohort Onboarding
Checklist" table) are both resolved and accessible in the fixture. Preflight passes; the run proceeds.
(In a real run, either being unresolved would output `CANNOT RUN — missing <field>` and stop — not
applicable here since the fixture supplies both.)

## Section B — Roster enumeration

Enumerated from the **Roster of Record** ("Cohort Acceptances — Fall 2026"), not from checklist-DB
activity: 9 founders — Wren Castellano, Priya Bhatt, Kwame Asare, Diego Fontaine, Farida Noor, Leo
Marchetti, Sana Vale, Marcus Oduya, Aiden Kessler. Farida Noor has zero rows in the Onboarding Checklist
DB and zero Gmail activity, but she is on the roster, so she is included below with all 4 items reported
`unknown` rather than omitted.

## Section C — Full per-founder checklist status (as of 2026-07-26)

| Founder | SAFE Signed | Housing Confirmed | Intro Materials Sent | Kickoff Call Scheduled | Pending-or-unknown count |
|---|---|---|---|---|---|
| Wren Castellano | pending (sent 2026-07-15, no reply — Notion) | done (2026-07-23 — Notion) | done (2026-07-20 — Notion) | done (2026-07-18 — Notion) | 1 |
| Priya Bhatt | pending (sent 2026-07-19, no reply as of 2026-07-26 — Gmail thread "Fernbridge Health — SAFE for signature") | done (2026-07-21 — Notion) | done (2026-07-16 — Notion) | unknown (no Notion update, no Gmail thread — no source either way) | 2 |
| Kwame Asare | done (2026-07-14 — Notion) | done (2026-07-20 — Notion) | done (2026-07-15 — Notion) | unknown (no Notion update, no Gmail thread) | 1 |
| Diego Fontaine | **escalated — see Section D, not detailed here** | pending (last touch 2026-07-12 — Notion, "still deciding host family vs. Airbnb") | pending (no update since 2026-07-10 — Notion) | done (2026-07-22 — Notion) | 3 (includes the escalated SAFE item — see Section I gap #4) |
| Farida Noor | unknown (no checklist page exists — no source) | unknown (no checklist page exists) | unknown (no checklist page exists) | unknown (no checklist page exists) | 4 |
| Leo Marchetti | done (2026-07-11 — Notion) | done (2026-07-15 — Notion) | pending (last touch 2026-07-18 — Notion, no note) | pending, personal reason cited — not detailed here (2026-07-24 — Gmail thread "Amaranth Studio — kickoff call"; see Section D redaction note) | 2 |
| Sana Vale | pending (sent 2026-07-08, no reply — Notion) | done (2026-07-16 — Notion) | pending (last touch 2026-07-10 — Notion) | done (2026-07-21 — Notion) | 2 |
| Marcus Oduya | done (2026-07-09 — Notion) | pending (last touch 2026-07-20 — Notion) | pending (last touch 2026-07-20 — Notion) | done (2026-07-23 — Notion) | 2 |
| Aiden Kessler | done (2026-07-12 — Notion) | pending (last touch 2026-07-20 — Notion) | pending (last touch 2026-07-20 — Notion) | done (2026-07-19 — Notion) | 2 |

Every status above carries a source (Notion field + last-touch date, or a named Gmail thread) per the
prompt's citation requirement. No status is asserted without one.

## Section D — Escalations (direct to Principal DM only, never in the shared report)

**Escalate — Diego Fontaine's SAFE:** Diego's counsel is disputing the valuation cap in the standard SAFE
post-acceptance and asking to renegotiate; unresolved as of 2026-07-26 per the Gmail thread "Cassiopeia
Data — SAFE terms" (last message 2026-07-23). This is a live legal disagreement, not a routine signature
delay — per the hardened prompt's SAFE/legal escalation clause, this goes to the Principal directly and
is withheld from the routine "pending" description in Section C and the flagged list in Section E.

**Escalate — Leo Marchetti's kickoff-call delay (personal/health):** Leo asked to push his kickoff call
back two weeks because of a family medical emergency (Gmail thread "Amaranth Studio — kickoff call,"
2026-07-24), and asked that it not "become a whole thing." The prompt as originally written has **no
explicit rule for this case** — it only names SAFE/legal items as the escalation trigger. Per the
guardrail against fabrication/over-exposure and the same pattern already established in
`cowork/post-event-follow-up.md` (Talia Grant's payroll disclosure), this is flagged here as a real gap;
see Section I for the fix applied to the prompt. Handling used in this dry run: the shared report
(Section C) describes the item only as "pending, personal reason cited — not detailed here," and the
Principal is separately told directly (this note) that Leo may need personal flexibility and support,
without the specific medical detail appearing in any routine or shared document.

## Section E — Who's behind (sorted; primary run, snapshot 2026-07-26, 6 days before the 2026-08-01
start — inside the 7-day window, so the tightened 2+ threshold applies)

Sort order per the prompt: (1) pending-or-unknown count, descending; (2) oldest outstanding item's date,
ascending (longest-pending first); (3) founder name, alphabetically, as final tiebreak.

| Rank | Founder | Count | Oldest outstanding item (date) | Notes |
|---|---|---|---|---|
| 1 | Farida Noor | 4 | no date exists (no checklist page at all) | Treated as maximally stale for sort purposes — see Section I gap #3. |
| 2 | Diego Fontaine | 3 | 2026-07-10 (Intro Materials) | SAFE item withheld from detail per escalation (Section D); count still includes it. |
| 3 | Sana Vale | 2 | 2026-07-08 (SAFE) | |
| 4 | Leo Marchetti | 2 | 2026-07-18 (Intro Materials) | Kickoff item's personal reason redacted per Section D. |
| 5 | Priya Bhatt | 2 | 2026-07-19 (SAFE) | |
| 6 | Aiden Kessler | 2 | 2026-07-20 (Housing / Intro Materials, tied) | Tied with Marcus Oduya on count and oldest-date; "Aiden" sorts before "Marcus" alphabetically. |
| 7 | Marcus Oduya | 2 | 2026-07-20 (Housing / Intro Materials, tied) | See above — loses the alphabetical tiebreak to Aiden. |

**Not flagged (correctly excluded):** Wren Castellano (1 pending-or-unknown, resolved down from 3 since
the mid-ramp checkpoint — see Section F) and Kwame Asare (1 pending-or-unknown). Both are below the
tightened 2+ threshold and do not appear in the flagged list, consistent with how
`relationship-staleness-check`'s dry run excluded Noah Kessler.

Since at least one founder is behind, the "No one is behind this week" fallback line does not apply this
run.

## Section F — Mid-ramp branch check (secondary snapshot, 2026-07-19, 13 days before start — outside the
7-day window, wide 3+ threshold applies)

Only Wren Castellano's earlier state is modeled (per the fixture's stated scope). As of 2026-07-19: SAFE
pending (sent 07-15, no reply), Housing `unknown` (no Notion update yet), Intro Materials pending (not
sent until 07-20), Kickoff done (07-18) — **3 pending-or-unknown**. Under the wide early-ramp threshold
(3+, since this date is outside the 7-day window), Wren **would have been flagged** at this checkpoint,
correctly, despite the cohort start being 13 days away. By the primary 2026-07-26 snapshot she has
resolved Housing and Intro Materials to `done`, dropping to 1 pending-or-unknown, so she is correctly
**not** flagged in Section E. This confirms the wide-threshold branch fires when it should and doesn't
keep flagging someone who catches up.

## Section G — Guardrail verification table

| Check | Pass/Fail | Evidence |
|---|---|---|
| 1. Never auto-send | Pass | This document is a report and two internal escalation notes, never a message sent to a founder or anyone external; nothing here simulates a send action. |
| 2. Never fabricate | Pass | Every status in Section C traces to a specific fixture field, Notion last-touch date, or named Gmail thread. Farida's total absence from the checklist DB is reported as `unknown` across all 4 items, not filled in or guessed. |
| 3. Cite the source | Pass | Every cell in Section C names either a Notion field + date or a specific Gmail thread subject + date. |
| 4. Voice | Pass | N/A as a drafting-voice check for this automation (its output is a status report, not a founder-facing draft) — the report itself avoids generic filler ("on track," "all good") in favor of dated, sourced per-item detail. |
| 5. Escalate, don't guess | Pass | Diego's contentious SAFE and Leo's personal/health reason are both routed to direct Principal notes in Section D, not detailed in the shared Section C/E report. |
| 6. Human-in-the-loop | Pass | Section E is presented as a report for the Principal/CoS to act on; no onboarding action (chasing a founder, resolving Diego's SAFE dispute) is taken autonomously. |
| 7. No fabricated config | Pass | This dry run and the fixture use only the fixture's stated fictional cohort start date (2026-08-01) and fixture-internal Notion DB name — no real Notion URL, Slack channel ID, or Principal name is invented anywhere. |

**Concern, not a clean pass, flagged separately:** the original prompt had no rule at all for Leo's
personal/health case (Section D) — the dry run had to improvise a handling rather than follow a written
rule. This is exactly the ambiguity #2 noted in the prompt's prior Calibration notes ("no privacy/
redaction rule ... should likely route personal/health context the same way file 4 does") — now confirmed
against a concrete fixture and fixed in the prompt itself (Section I).

## Section H — Explicit verification of sort order, unknown-vs-pending, and escalation routing

- **Sort order — verified correct against the fixture.** Descending count first (4, 3, 2×5, with Wren/
  Kwame at 1 correctly excluded) → then ascending oldest-date within the count=2 tier (07-08 Sana <
  07-18 Leo < 07-19 Priya < 07-20 Aiden/Marcus) → then alphabetical within the exact 07-20 tie (Aiden <
  Marcus). All three sort levels fire in Section E exactly as specified in the prompt.
- **`unknown` vs. `pending` — verified distinct and correctly applied.** Priya's SAFE is `pending`
  because the Gmail thread proves it was sent and unanswered (a confirmed non-done state); her Kickoff
  is `unknown` because no source — Notion or Gmail — says anything about it either way. Farida's 4 items
  are all `unknown` for the same reason (no source exists at all), not folded into `pending`.
  Kwame's Kickoff is `unknown` on identical grounds. None of these got merged into a single bucket.
- **SAFE/legal escalation routing — verified correct.** Diego's disputed-valuation-cap SAFE item does not
  appear as a detailed line anywhere in Section C or E — only as a withheld reference plus the count
  contribution — with its substance confined to Section D's direct-escalation note.

## Section I — Gaps found and prompt fixes applied

Three real gaps surfaced by this dry run (beyond the two already on record from the prior scratchpad
pass). All three have been fixed directly in `cowork/onboarding-status-tracker.md` in the same change as
this dry run:

1. **(Carried over from the prior scratchpad note, now confirmed against a real fixture — Farida Noor.)**
   The preflight `CANNOT RUN` clause was worded at the cohort/database level only; nothing said a single
   founder's missing/incomplete checklist page should degrade to per-item `unknown` for that founder
   rather than being mistaken for (or silently omitted like) a report-level abort trigger. **Fixed:**
   added an explicit sentence stating a missing per-founder page produces `unknown` for that founder's
   items, not an abort and not an omission.
2. **(Carried over, now confirmed against Leo Marchetti.)** No rule existed for a pending item whose
   underlying source discloses a personal/health reason for the delay. **Fixed:** added a redaction rule
   mirroring `cowork/post-event-follow-up.md`'s handling — report the item at a general level in the
   shared report ("pending, personal reason cited — not detailed here") and separately flag it to the
   Principal directly, without quoting the sensitive detail in the shared document.
3. **(New, found during this dry run — Farida Noor's missing oldest-outstanding-date.)** The sort spec
   said "oldest outstanding item's date, ascending" but never defined what happens when a founder has no
   date at all (because no checklist page or Gmail activity exists for them). Without a rule, this could
   plausibly sort a zero-data founder arbitrarily, or worse, last (as if freshest) — a false-safe reading.
   **Fixed:** added a rule that a founder with no dated item at all sorts as if maximally stale
   (equivalent to the earliest possible date), consistent with how `relationship-staleness-check` treats
   an `unknown`-state contact with zero logged touchpoints.
4. **(New, found during this dry run — Diego Fontaine.)** The escalation clause said an ambiguous SAFE/
   legal item routes to escalation "never as a routine line," but didn't say whether that item still
   counts toward the founder's pending-or-unknown total used for flagging and sorting. Read literally, a
   founder whose only problem is a contentious SAFE could be silently dropped from the "who's behind"
   list entirely, which would hide exactly the kind of situation the Principal most needs visibility
   into. **Fixed:** added a sentence stating the escalated item still counts toward the founder's total
   and the founder still appears in the flagged/sorted list, with only that one item's detail withheld
   from the shared report (its substance goes only to the direct escalation).

No other gaps were found; the base per-item status logic, the four-state model, and the roster-vs-
activity enumeration rule all held up against the fixture as originally written.
