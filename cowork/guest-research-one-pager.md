# Guest Research One-Pager

**Surface:** Cowork scheduled task
**Cadence:** A few days before each Solo Founders Podcast recording
**Sources:** Web search, Gmail (any prior correspondence with the guest), Notion (past episode topics, to
avoid repeat questions)
**Output:** One-page prep brief delivered to the Principal ahead of the recording

## Run Input

Before kicking off each run, the Principal fills in:

- **Guest name** (required)
- **Company / role** (required)
- **Recording date** (required)
- **Episode number** (required)
- **Known links** (optional) — guest's site, a prior interview, X handle
- **Angle to pursue** (optional) — anything the Principal already wants to dig into

**Future enhancement:** auto-populate this Run Input from the recording's calendar invite (event title/
description) once that reading pattern and a calendar-title naming convention are established. Not wired
up yet — it depends on a connector and a naming convention that don't exist today, so it stays a future
enhancement rather than a launch blocker.

## Prompt

> Research the upcoming podcast guest using the Run Input above: background, current company (if a
> founder, especially anything relevant to solo founding specifically — did they build alone, when did
> that change, what pushed them to start), notable public statements (interviews, blog posts, tweets/X
> posts, podcast appearances elsewhere), and anything topical they've said recently that's worth reacting
> to live.
>
> Check past Solo Founders Podcast episode topics (see Config below) so questions don't repeat ground
> already covered with a different guest. **If that source isn't available when this runs, say so
> explicitly in the brief** — add a line under `## Gaps and open questions` reading "Repeat-question check
> not performed — past-episode source unavailable" — rather than silently skipping the check.
>
> Produce the brief in exactly this shape, in this order. A single-line Run Input header (guest,
> company/role, recording date, episode number — for the Principal's quick reference) may precede
> `## Bio`; if present, that line does not count toward the word bound below:
>
> ```
> ## Bio
> ## Why this is a solo-founding story
> ## Questions
> ## Sources
> ## Gaps and open questions
> ```
>
> - **Length:** the brief body (`## Bio` through the end of `## Gaps and open questions`, excluding the
>   `## Sources` list and excluding the optional Run Input header line above) must be ≤600 words total,
>   where "words" means prose words only — a `wc -w`-equivalent count of whitespace-separated tokens,
>   excluding inline citation markers like `[S1]`/`[S2]` and excluding the `## Sources` section itself.
>   This is what makes "one page" checkable rather than vibes.
> - **Citations:** every factual claim about the guest carries an inline marker like `[S1]`, `[S2]`, etc.,
>   each resolving to a numbered entry in `## Sources` with title, publisher/outlet, URL, and date. A claim
>   that can't be sourced does not go in the brief — it goes in `## Gaps and open questions` instead.
> - **Bio:** short, cited paragraph(s).
> - **Why this is a solo-founding story:** 3-4 bullets on what makes their story specifically relevant to
>   solo founding.
> - **Questions:** 5-7 questions, ordered from warm-up to sharpest. The first question is a warm-up. The
>   last is the sharpest — meaning most likely to produce a non-rehearsed answer, not the most
>   adversarial one.
> - **Sources:** numbered list, one entry per `[Sn]` marker used above, with title, publisher/outlet, URL,
>   and date for each. If a source states no publication date, omit the date field for that entry and note
>   the omission (in the entry itself or a footnote) rather than inferring or approximating one — never
>   invent a date.
> - **Gaps and open questions:** anything that couldn't be sourced, the repeat-question fallback line if
>   triggered, and anything reputationally sensitive about the guest (litigation, a failed company,
>   health, a public falling-out) — flagged here for the Principal's judgment call. Never assert
>   reputationally sensitive material as fact and never turn it into a question without a solid citation.

## Config

- `[CONFIGURE]` Notion database or doc listing past episode guests, topics covered, and questions already
  asked. Supplied by the Principal — no Notion connector is authorized for this yet and no URL has been
  given, and inventing one (even an obviously fake-looking placeholder) would violate the never-fabricate
  guardrail and risks getting copy-pasted into a real config later. Without it, this automation cannot
  reliably avoid repeat questions across episodes; until it's supplied, every run must use the explicit
  "Repeat-question check not performed" fallback specified in the Prompt above rather than skip the check
  silently.

## Calibration notes

A synthetic dry run on 2026-07-25 (fixture corpus, `samples/guest-research-one-pager/`) confirmed the
prompt correctly grounded every factual claim in the fixture corpus with a resolvable `[Sn]` citation, and
correctly routed the guest's deliberate pre-founding biographical gap to `## Gaps and open questions`
rather than inventing an employer or role to fill it. That same dry run surfaced two prompt gaps — the
≤600-word bound had no precise counting method and didn't account for the sample's Run Input header, and
the Sources citation format had no exception for sources with no stated publication date — both fixed in
this pass (2026-07-25); see the Length and Sources bullets above.
