# Relationship Staleness Check

**Surface:** Cowork scheduled task
**Cadence:** Weekly
**Sources:** Notion (investor/partner CRM), Gmail, Calendar
**Output:** Slack message to the Principal with drafted check-in notes attached per flagged contact

## Prompt

> Review the investor and partner contact list. For each contact, find the last real touchpoint (an
> email exchange, a call on the calendar, a Slack/text mention if tracked) — not just the last time they
> were added to a list. Flag anyone with no touchpoint in the last 30 to 45 days. For each flagged
> contact, draft a short, warm check-in note referencing something specific and current (a portfolio
> update relevant to them, something SFP has shipped recently, a person they'd want to be introduced to)
> rather than a generic "checking in!" Group the output by how long it's been stale, longest first, so
> the most at-risk relationships are addressed first.

## Config

- `[CONFIGURE]` Notion CRM DB URL for investors/partners (confirm this exists and has last-touchpoint
  data, or whether it needs to be built first)
- `[CONFIGURE]` 30-45 day window may need tuning per relationship tier (a lead investor vs. a casual
  advisor probably has a different staleness threshold)
- Check-in drafts are drafts only — a human sends.

## Calibration notes

_(add findings here after the first few runs)_
