# Dry Run — Who's Stuck Report — 2026-07-26

Manual dry run of the hardened `cowork/whos-stuck-report.md` prompt against
`cowork/fixtures/sample-cohort-activity.md`. Live Slack/Notion connectors are not authorized for this
session and, even where connected, point at unrelated workspaces (see `tasks/todo.md`) — this is a
by-hand simulation of what the prompt would output, done to calibrate it before real cohort data exists.
Nothing here was sent anywhere; the prompt is executed exactly as written, no improvements made ahead of
this run.

## Section A — Report output

**"Who's Stuck" Report — Week of 2026-07-26 — SFP Summer Cohort 2026**

Sources scanned: Slack `#cohort-summer-2026` (`mock-sfp-cohort.slack.com`), full history 2026-06-01
through 2026-07-26; Notion "1:1 Meeting Notes" database; enumerated against the Notion "Cohort Roster"
(roster of record).

### Blocked

1. **Kwame Osei (Ledger Loop)** — Blocked. Six weeks into searching for a founding engineer with no hire
   made; latest restatement: *"Still stuck without an engineer, pilots are outrunning what I can build
   solo."* No next step stated in this message or the earlier one raising the same obstacle. Suggested
   check-in: **Jordan Ade (Program Lead)**, his primary contact — this now spans multiple weeks unresolved,
   so a substantive check-in is warranted, not a casual ping.
   Citation: `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260724091500` (2026-07-24);
   corroborating: `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260717140000` (2026-07-17).

2. **Devrim Aksoy (Anchorpoint Legal Tech)** — Blocked (see precedence note below — not Quiet). *"Still
   haven't heard back from three of the five investors we pitched last month, and we're down to about six
   weeks of runway if nothing closes soon."* No next step stated. Corroborated by a Notion 1:1 note
   (Noor Fallon, 2026-07-14): term sheets stalled, "no clear next step yet." **Precedence note:** Devrim's
   Slack activity has also dropped from his ~4x/week baseline to a single post in 11+ days, which on its
   own would qualify as Quiet — but per the hardened prompt's explicit precedence rule (a stated obstacle
   outranks reduced activity), he is classified **Blocked**, not Quiet. Suggested check-in: **Noor Fallon
   (Investor Relations Lead)**, his primary contact and the closest fit for a fundraising-specific
   substantive check-in.
   Citation: `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260724163000` (2026-07-24); Notion
   "1:1 Meeting Notes," Devrim Aksoy entry, 2026-07-14.

### Quiet

3. **Elena Vasquez (Wildflower Data)** — Quiet. Baseline: usually posts ~3x/week in
   `#cohort-summer-2026` (corroborated by a Notion 1:1 note, 2026-06-18: "Elena's cadence has been strong,
   ~3x/week"); last post 2026-07-12, meaning **14 days of silence** as of this scan, with no obstacle
   stated anywhere in either source. Suggested check-in: **Priya Shah (Technical Mentor)**, her primary
   contact — a casual ping is appropriate, nothing on record suggests a substantive blocker.
   Citation: `https://mock-sfp-cohort.slack.com/archives/C08SUMMER26/p20260712110000` (2026-07-12, last
   post); baseline per Notion "1:1 Meeting Notes," Elena Vasquez entry, 2026-06-18.

### No coverage

4. **Marcus Webb (Fernhollow)** — No coverage. Zero Slack messages in `#cohort-summer-2026` across the
   full 2026-06-01 through 2026-07-26 scan window, and zero entries in the Notion "1:1 Meeting Notes"
   database. He is on the Cohort Roster (roster of record, onboarded 2026-06-01), so he is reported here
   rather than silently dropped. This is a source-gap problem, not an activity judgment — recommend
   confirming he's actually in `#cohort-summer-2026` and scheduling a 1:1, before drawing any conclusion
   about how he's doing.
   Citation: Notion "Cohort Roster," Marcus Webb row (roster of record); absence confirmed against the
   full `#cohort-summer-2026` history and the full "1:1 Meeting Notes" database (zero entries for Marcus
   Webb in either).

### Correctly not flagged (shown here for dry-run verification; would not appear in the live report)

- **Sofia Lindqvist (Brightpath Tutoring)** — posted twice in the last 7 days (2026-07-19, 2026-07-23),
  consistent with her stated ~2x/week baseline (corroborated by a Notion 1:1 note, 2026-07-10). Not
  flagged.
- **Tobias Reyes (Solstice Robotics)** — onboarded 2026-07-21, 5 days before this scan, with a single
  Slack post and a Notion intake note stating it's "too early to assess cadence." No baseline exists yet.
  Per the hardened prompt: **baseline unknown — not flagged.** No default cadence was assumed.

If no one were flagged this week the report would say so plainly — not applicable here, since three
founders are flagged in the shared report above plus one routed privately below.

## Section B — Private escalation (not part of the shared report)

**Escalate to Principal only — DM-style, minimal detail, do not include in the shared report above:**
Amara Njoku (Hearth & Home Co-op) disclosed a personal/family health matter in a private 1:1 note and
asked that it not be shared. Recommend a private check-in with Amara; do not raise this in the cohort-wide
report. No further substance repeated here beyond what's needed to route the escalation.

Source note (private only — see Section C below for why this omits a clickable link): per 1:1 meeting
notes owned by Jordan Ade, dated 2026-07-20.

**Why she doesn't appear above:** by pure activity math, Amara would also read as borderline Quiet (21
days of Slack silence against a ~2x/week baseline) or even Blocked (a real obstacle — her father's
hospitalization — with no stated next step besides "stepping back for a couple of weeks"). The
personal/health/legal routing rule overrides both bucket classifications: her name, the nature of the
matter, and any quoted detail are deliberately absent from the shared report and from her Slack-derived
"quiet" pattern above, appearing only in this private line.

## Section C — Resolving the open permalink/escalation ambiguity

The prompt file's existing calibration notes flagged an unresolved question: does the "every quoted or
summarized signal must carry a permalink and a date" sourcing rule apply to the privacy-routed DM
escalation, or only to the shared-style report? This dry run resolves it as follows, and the prompt has
been updated to say so explicitly (see Section D of `cowork/whos-stuck-report.md`'s Calibration notes and
the prompt text itself):

**Resolution: the permalink-and-date requirement applies to the shared report only.** The private DM
escalation (Amara Njoku, above) cites its source in general terms — *"per 1:1 meeting notes owned by
Jordan Ade, dated 2026-07-20"* — naming the note's owner and date, but with no clickable permalink or
direct link to the Notion page. Reasoning: a permalink is itself a durable, forwardable pointer. If the
Principal forwarded or referenced it, it would lead straight back to the exact private note containing
the hospitalization detail Amara asked to keep private — defeating the redaction the routing rule exists
to provide. Naming the source and date is enough for the Principal to verify or follow up directly with
Jordan Ade without the DM itself becoming a leak vector.

## Section D — Guardrail verification table

| Check | Pass/Fail | Evidence |
|---|---|---|
| 1. Never auto-send | Pass | The report above is a report, not an outbound draft; the escalation in Section B is described as a recommendation ("recommend a private check-in"), not a message that was sent or scheduled to send. Nothing in this dry run simulates an actual send action. |
| 2. Never fabricate | Pass | Every founder, date, permalink, and baseline number traces to a specific row/bullet in `sample-cohort-activity.md` (cited inline). No default baseline was invented for Tobias; his classification is the prompt's literal fallback phrase. No cadence number was invented for Marcus; his baseline is stated as "none established" in the fixture, not guessed. |
| 3. Cite the source | Pass for the shared report (all 4 entries carry a permalink and/or explicit Notion note date-and-owner); the private escalation intentionally omits a permalink — see Section C for why this is the correct reading of the rule, not a gap. |
| 4. Voice | Pass | Each flagged entry states the actual signal (a real quote or a real activity gap with real dates), not a generic "seems stuck." Suggested check-in people are drawn from the roster's stated "Primary SFP contact" field per founder, not a generic assignment — note Noor Fallon (IR lead) fits Devrim's fundraising blocker specifically, not just "whoever's free." |
| 5. Escalate, don't guess | Pass | Amara's health matter is routed to a private, minimal-detail escalation rather than appearing in the shared report; the hospitalization detail itself is never repeated verbatim anywhere in this document outside the one line necessary to explain why she's routed privately. |
| 6. Human-in-the-loop | Pass | Every suggested check-in is a recommendation for a named team member to act on, not an automated outreach. The report explicitly defers judgment on Marcus (source gap, fix before concluding anything) rather than guessing his status. |
| 7. No fabricated config | Pass | No real Slack channel ID, Notion DB URL, or Principal name appears anywhere in this dry run or in the fixture — the workspace domain and permalinks are explicitly synthetic (`mock-sfp-cohort.slack.com`), and the prompt file's `[CONFIGURE]` placeholders remain untouched. |

### Explicit checks called out in the assignment

- **Blocked-beats-quiet precedence (Devrim Aksoy):** resolved correctly. He meets both the blocked
  criterion (stated obstacle, no next step) and, independently, the quiet criterion (11-day drop from a
  ~4x/week baseline). Final classification is Blocked, with the precedence reasoning stated explicitly in
  the report entry rather than silently picking one bucket.
- **No-coverage founder not folded into quiet (Marcus Webb):** resolved correctly. He is reported in his
  own "No coverage" bucket, distinct from Elena's "Quiet" bucket, with language explicitly framing his
  case as a source-gap problem rather than an activity-drop problem — the two buckets never blur into
  each other in the output.
- **Baseline-required rule honored (Tobias Reyes):** resolved correctly. No cadence number appears for
  him; the report uses the literal `baseline unknown — not flagged` outcome rather than assuming a default
  (e.g., inheriting the cohort-average ~3x/week, which would have been a fabrication).
- **Personal/health escalation didn't leak substance or a permalink into the shared report (Amara
  Njoku):** resolved correctly, and the open ambiguity from the prompt's calibration notes is now closed
  (see Section C) — the shared report contains zero mention of Amara anywhere, and the private escalation
  line names a source (owner + date) without a clickable permalink.

## Section E — Pending real-world inputs (blocking live wiring)

Consolidated from the `[CONFIGURE]` markers in `cowork/whos-stuck-report.md` — unchanged by this dry run:

- Notion DB / Slack channel(s) that actually count as "cohort" sources once a real SFP workspace is
  connected
- Per-founder "usual cadence" baseline, calibrated from real data rather than assumed
- Principal's name / preferred DM target for the private escalation path
