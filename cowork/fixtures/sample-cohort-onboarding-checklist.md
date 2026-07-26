# Fixture — Sample Cohort Onboarding Checklist (Synthetic Test Data)

> **SYNTHETIC TEST DATA ONLY. This is not a real cohort, not real founders, and not real Notion
> content.** It exists to dry-run test `cowork/onboarding-status-tracker.md` against realistic-shaped
> data while the live Notion connector is not yet authorized for this session (see `tasks/todo.md`, "Open
> questions for the user"). Every name is fictional and every email is prefixed `mock-` on the
> IANA-reserved `example.com` domain so it can never be mistaken for a live address. **Never point a real
> automation run at this file, and never copy any name/email/detail from here into a real draft.**

This fixture stands in for two things: (1) the **roster of record** (the authoritative list of accepted
founders for the cohort, independent of who happens to have Notion/Gmail activity), and (2) the **cohort
onboarding-checklist Notion DB** that tracks per-item status. It is used to dry-run the hardened
onboarding-status-tracker prompt — specifically to exercise: the wide 3+ pending-or-unknown threshold
mid-ramp, the tightened 2+ threshold inside 7 days of start, a correctly-unflagged founder, the
`unknown`-vs-`pending` distinction, a Gmail cross-reference that explains a pending item, a SAFE/legal
item that must escalate directly rather than appear in the shared report, a founder who is on the roster
but has zero checklist-DB activity at all (tests "enumerate from roster, not from activity"), a
personal/health-sensitive pending item, and a three-way tie-break exercise (count, then oldest-date, then
name).

## Cohort facts (fictional, stated — not inferred)

- **Cohort:** Fall 2026 SFP Cohort (fictional)
- **Start date:** 2026-08-01 (in-person, host city Austin — housing confirmation applies to every
  founder in this cohort)
- **Snapshot / "today" for the primary run:** 2026-07-26 (6 days before start — **inside** the 7-day
  window, so the tightened 2+ threshold applies)
- **Secondary snapshot for the mid-ramp branch:** 2026-07-19 (13 days before start — **outside** the
  7-day window, so the wider 3+ threshold applies). Only Wren Castellano's row is modeled at this earlier
  date (see her entry below) — the fixture doesn't reconstruct every founder's state at two points in
  time, since only one founder's arc is needed to exercise this branch; inventing full mid-ramp history
  for the other eight would be exactly the kind of unrequested embellishment this stack's guardrails warn
  against.

## Roster of Record — "Cohort Acceptances — Fall 2026" (authoritative list, separate doc from the
checklist DB)

| Founder | Email | Company | Accepted |
|---|---|---|---|
| Wren Castellano | mock-wren@example.com | Nordlight Robotics | 2026-06-30 |
| Priya Bhatt | mock-priya.b@example.com | Fernbridge Health | 2026-06-30 |
| Kwame Asare | mock-kwame@example.com | Solace Robotics | 2026-06-30 |
| Diego Fontaine | mock-diego@example.com | Cassiopeia Data | 2026-07-02 |
| Farida Noor | mock-farida@example.com | Thistlewood & Co | 2026-07-02 |
| Leo Marchetti | mock-leo@example.com | Amaranth Studio | 2026-07-03 |
| Sana Vale | mock-sana.v@example.com | Ridgeline Foods | 2026-07-03 |
| Marcus Oduya | mock-marcus@example.com | Solder & Bloom | 2026-07-05 |
| Aiden Kessler | mock-aiden@example.com | Kettlebrook Analytics | 2026-07-05 |

**9 founders accepted.** This is the authoritative enumeration source.

## Mock Notion DB — "Cohort Onboarding Checklist" (as of 2026-07-26)

**Note: Farida Noor has no row in this DB at all** — no checklist page was ever created for her. She is
still on the Roster of Record above and must still appear in the tracker's output, with every item
reported `unknown` (no data), not silently skipped for lack of checklist-DB activity.

| Founder | SAFE Signed | Housing Confirmed | Intro Materials Sent | Kickoff Call Scheduled |
|---|---|---|---|---|
| Wren Castellano | pending — sent 2026-07-15, no signed copy back as of 2026-07-26 | done — confirmed 2026-07-23 | done — sent 2026-07-20 | done — scheduled 2026-07-18 |
| Priya Bhatt | pending — sent 2026-07-19, no reply as of 2026-07-26 | done — confirmed 2026-07-21 | done — sent 2026-07-16 | unknown — no Notion update, no Gmail thread about scheduling either |
| Kwame Asare | done — signed 2026-07-14 | done — confirmed 2026-07-20 | done — sent 2026-07-15 | unknown — no Notion update, no Gmail thread found |
| Diego Fontaine | **see escalation note below — not a routine line** | pending — last Notion touch 2026-07-12, "still deciding host family vs. Airbnb" | pending — no update logged since he joined the cohort 2026-07-10 | done — scheduled 2026-07-22 |
| Leo Marchetti | done — signed 2026-07-11 | done — confirmed 2026-07-15 | pending — last Notion touch 2026-07-18, no note | pending — **see personal-context note below** |
| Sana Vale | pending — sent 2026-07-08, no reply as of 2026-07-26 (18 days) | done — confirmed 2026-07-16 | pending — last Notion touch 2026-07-10, no update since | done — scheduled 2026-07-21 |
| Marcus Oduya | done — signed 2026-07-09 | pending — last Notion touch 2026-07-20, "still deciding" | pending — last Notion touch 2026-07-20, not sent | done — scheduled 2026-07-23 |
| Aiden Kessler | done — signed 2026-07-12 | pending — last Notion touch 2026-07-20 | pending — last Notion touch 2026-07-20 | done — scheduled 2026-07-19 |

## Gmail cross-reference notes

- **Priya Bhatt — SAFE thread:** Email thread "Fernbridge Health — SAFE for signature," sent 2026-07-19,
  no reply from Priya as of 2026-07-26 (7 days). This is the source that lets the tracker report her SAFE
  status as `pending` (confirmed sent, no reply) rather than `unknown` — the thread proves it isn't
  merely undocumented.
- **Diego Fontaine — SAFE thread (ambiguous/contentious — escalation only):** Email thread "Cassiopeia
  Data — SAFE terms," last message 2026-07-23 from Diego's counsel disputing the valuation cap in the
  standard SAFE and asking to renegotiate before signature. Unresolved as of 2026-07-26. This is a legal
  disagreement about deal terms, not a routine signature delay — per the hardened prompt, this routes to
  direct Principal escalation, never a routine "pending" line in the shared report.
- **Leo Marchetti — kickoff-call thread (personal/health, sensitive):** Email thread "Amaranth Studio —
  kickoff call," message from Leo dated 2026-07-24, asking to push the kickoff call back two weeks
  because of a family medical emergency, and asking that it "not become a whole thing." This is the
  source for his kickoff-call item being `pending` rather than `unknown` — but the specific personal
  detail must not be quoted verbatim into a shared status report (see dry-run Section on the redaction
  fix).

## Edge cases this fixture deliberately contains

- **Wren Castellano — mid-ramp wide-threshold, then resolves.** As of the earlier 2026-07-19 checkpoint
  (13 days before start, outside the 7-day window): SAFE pending (sent 07-15, no reply), Housing
  `unknown` (no Notion update logged yet), Intro Materials pending (not sent until 07-20), Kickoff done
  (07-18) — **3 pending-or-unknown**, which should flag her under the wider 3+ threshold even though the
  cohort start is nearly two weeks away. By the primary 2026-07-26 snapshot, Housing and Intro Materials
  have both resolved to `done`, leaving only SAFE pending — **1 pending-or-unknown**, below both
  thresholds, so she is correctly **not** flagged in the primary run. Tests that the wide early-ramp
  threshold catches someone who later resolves, and that the tracker doesn't keep flagging her once she's
  caught up.
- **Priya Bhatt — near-start tight-threshold, `unknown` vs. `pending` distinction, Gmail cross-ref.** 2
  pending-or-unknown (SAFE `pending`, confirmed via Gmail; Kickoff `unknown`, no source at all) inside
  the 7-day window — flags under the tightened 2+ threshold. Her SAFE and Kickoff items are deliberately
  different states for the same reason: SAFE has a confirming source (the Gmail thread) that proves it
  wasn't done, so it's `pending`; Kickoff has no source of any kind, so it's `unknown`.
- **Kwame Asare — correctly not flagged.** Only 1 pending-or-unknown item (Kickoff, `unknown`) — below
  both the wide and tight thresholds. Tests that the tracker doesn't over-flag someone who's basically on
  track just because one item lacks a source.
- **Diego Fontaine — SAFE/legal escalation, not a routine line.** His SAFE item is a live, contentious
  legal disagreement (disputed valuation cap) — must route to direct Principal DM, never appear as a
  routine "pending" description in the shared report. He also has 2 other genuinely pending items
  (Housing, Intro Materials), so he should still surface in the "who's behind" list with a count of 3,
  just with the SAFE line withheld from routine detail.
- **Farida Noor — roster-of-record, zero checklist-DB activity.** She has no page in the Onboarding
  Checklist DB at all — no Notion activity, no Gmail thread, nothing. Tests that the tracker enumerates
  from the Roster of Record (where she's listed) rather than from checklist-DB activity, and reports all
  4 items `unknown` for her rather than omitting her or treating the missing page as a reason to abort
  the whole report.
- **Leo Marchetti — personal/health-sensitive pending item.** His kickoff-call delay is real and
  source-backed (the Gmail thread), but the reason is a family medical emergency he asked to keep
  private. Tests that the tracker doesn't quote the health detail verbatim into a shared status line.
- **Sana Vale / Marcus Oduya / Aiden Kessler — three-way tie-break.** All three have exactly 2
  pending-or-unknown items as of the primary snapshot. Their oldest-outstanding-item dates differ:
  Sana's oldest is 2026-07-08 (SAFE), Marcus's and Aiden's are both 2026-07-20 (Housing/Intro Materials
  for each). This tests both tiebreak levels: Sana should sort ahead of Marcus and Aiden on
  oldest-outstanding-date (longest-pending-first), and Marcus vs. Aiden — tied on both count and
  oldest-date — should resolve alphabetically ("Aiden" before "Marcus").
