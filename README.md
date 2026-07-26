# Solo Founders — Chief of Staff Automation Stack

Prompt source and process docs for a Claude-built Chief of Staff function at **Solo Founders** — the
company building the institution around solo founding (community, capital, support system, software,
infrastructure). This repo versions the prompts; most of the actual execution happens inside
[Cowork](https://cowork.anthropic.com) (connector-driven) or as GitHub Actions Routines triggered from
this repo.

**Start here, in order:**

1. **This file** — what's in the repo and how to set it up.
2. **[`CLAUDE.md`](CLAUDE.md)** — full context: why this exists, the automation catalog (all 13, with
   status), the two execution surfaces and when to use which, and the guardrails every automation follows.
3. **[`RUNBOOK.md`](RUNBOOK.md)** — step-by-step: exactly what to paste where and configure to actually
   turn on any given automation.

## What's in here

13 automations for a Chief of Staff function running a founder cohort program: meeting/commitment
tracking, founder onboarding and stuck-founder detection, event RSVP and follow-up, investor relationship
staleness, podcast prep and show notes, and internal process-drift checking. Full list and current status
in `CLAUDE.md`'s automation catalog.

Two kinds of automation live here:

- **Cowork scheduled tasks** (11 of 13) — prompt text in `cowork/*.md`, pasted into Cowork's own
  scheduling UI. Reads live Slack/Gmail/Calendar/Notion via Cowork's connectors.
- **Claude Code Routines** (2 of 13) — GitHub Actions workflows in `.github/workflows/`, using
  [`anthropics/claude-code-action@v1`](https://code.claude.com/docs/en/github-actions). Triggered by a
  repo event (e.g. a transcript commit) or a schedule, and open a draft PR for human review.

## Repo structure

```
README.md                          this file
CLAUDE.md                          full context, automation catalog, guardrails
RUNBOOK.md                         how to actually turn each automation on
tasks/
  todo.md                          current build-order state, open questions
  lessons.md                       corrections log
cowork/                            versioned prompt source for Cowork scheduled tasks
  fixtures/                        synthetic mock data + dry-run outputs used to calibrate each prompt
routines/                          repo-based Claude Code Routines
  sop-drift-check/PROMPT.md
  show-notes-drafting/PROMPT.md
.github/workflows/                 GitHub Actions workflow(s) implementing the Routines
transcripts/                       episode transcripts (triggers show-notes-drafting when committed)
show-notes/                        drafted show notes, paired 1:1 by basename with transcripts/
eval/                              synthetic golden-dataset calibration for two prompts (ground truth +
                                    scored runs)
samples/                           synthetic fixture + output pairs for two more prompts
```

## Setup

### Prerequisites

- A [Cowork](https://cowork.anthropic.com) account with Slack, Gmail, Google Calendar, Google Drive, and
  Notion connectors available to authorize (only connect the ones a given automation actually needs).
- A GitHub account with permission to add repo secrets and install GitHub Apps, if you're standing up
  either of the two Routines.
- `gh` CLI (optional, only needed if you're managing the GitHub side from a terminal).

### 1. Clone this repo

```bash
git clone https://github.com/sudhirerahul/Solo.git
cd Solo
```

### 2. Read the guardrails and current status

Read `CLAUDE.md` in full before turning anything on — it has the guardrails every automation follows
(never auto-send, never fabricate, cite the source, escalate rather than guess, human-in-the-loop by
default) and the current status of all 13 automations. **Do not stand up more than one new automation per
week** — see `CLAUDE.md`'s build order for why.

### 3. Stand up a Cowork task

Follow `RUNBOOK.md`'s Part A: copy the prompt from the relevant `cowork/<name>.md` file into a new Cowork
scheduled task, connect the sources it needs, and resolve every `[CONFIGURE]` placeholder in that file
with a real value before turning the schedule on.

### 4. Stand up a Routine (GitHub Actions)

Follow `RUNBOOK.md`'s Part B:

1. Add the `ANTHROPIC_API_KEY` repository secret (**Settings → Secrets and variables → Actions**).
2. Install the [Claude GitHub App](https://github.com/apps/claude) on this repo.
3. Enable **Settings → Actions → General → "Allow GitHub Actions to create and approve pull requests."**
4. For show notes drafting: commit a transcript to `transcripts/` (see `transcripts/README.md` for the
   naming convention) and push — a draft PR should open in `show-notes/`.
5. SOP drift check additionally needs its trigger/schedule syntax resolved — see the open item in
   `tasks/todo.md`.

### 5. Before trusting any automation with something real

Every prompt in this repo has been calibrated against **synthetic fixtures**, not live data — see
`cowork/fixtures/`, `eval/`, and `samples/` for the fixture + dry-run pairs behind each one, and each
prompt file's own "Calibration notes" section for what was found and fixed. There is currently no real
Solo Founders Slack or Notion workspace connected anywhere (see `tasks/todo.md`); several automations will
correctly output `CANNOT RUN — missing <field>` until real sources exist rather than fabricate anything.
Read a prompt's calibration notes and its fixture/dry-run pair before judging its first real output.

## Contributing to this repo's prompts

- Edit the `cowork/*.md` or `routines/*/PROMPT.md` file directly, then re-paste into Cowork (Cowork
  doesn't read this repo live — it's a copy-paste source of truth, and can drift if edited only in the
  Cowork UI; reconcile drift when noticed).
- Log any real-world correction to `tasks/lessons.md` (format: `[date] | what went wrong | rule to prevent
  it`) so the next calibration pass doesn't relearn the same thing.
- Never fill a `[CONFIGURE]` placeholder with an invented value — leave it as a literal placeholder until
  the real value is known.
