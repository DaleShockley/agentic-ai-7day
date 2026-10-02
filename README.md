# Agentic TPM Reporting & Portfolio Builder

An AI assistant, built with Claude Code, that turns raw project updates into executive-ready TPM artifacts: weekly status reports, risk registers and program charters. Every build ships with a TPM-style write-up (scope, architecture, failure modes, metrics, retro), so the repo shows both **what I built** and **how I'd run it as a program**.

Built during the [Agentic AI: 7-Day Build Challenge](https://buildwithagents.vercel.app/). All project data is fictional ("Project Atlas").

📋 [Program charter](docs/00-program-charter.md) · 📝 [Day 1 write-up](docs/day1-tpm-writeup.md) · 📖 [Glossary](docs/glossary.md) · 🎯 Target: Oct 15, 2026

## Shipped so far: Day 1, Status Report Drafter

Reads a project brief and a weekly update, scores every milestone and blocker against an explicit RAG rubric, diffs against last week, and drafts the exec report. A human approves every draft before it's shared.

```
TPM asks for a date
  → agent reads workflow + rubric + inputs
  → validates inputs        (missing update file → STOP; missing field → data gap, Amber)
  → scores each item        (quotes the exact rubric rule that fired, plus the numbers)
  → diffs vs. last week's JSON snapshot
  → writes draft report (for execs) + JSON snapshot (system of record for next week)
  → HUMAN GATE: TPM reviews and edits before anything is shared
```

**Results**
- **Eval:** on the 2026-10-02 run, RAG colors matched a hand-scored golden set on every item (overall Red, unassigned blocker Red, 9-day slip Amber, blank owner flagged as a data gap).
- **Failure test:** asked for a week with no update file; the agent stopped and wrote nothing, instead of reusing stale data.
- **Design flaw found:** the snapshot is written *before* human review, so next week would diff against unapproved data. The fix is in the retro.

**Design choices worth a look**
- **Rules over judgment:** my own gut-feel color calls missed the rubric in both directions, which is the case for a written rubric.
- **Unknown vs. known-bad:** a blank owner (data gap, fix the input) is scored differently from `unassigned` (needs a leadership decision).
- **Two outputs, two readers:** markdown for executives, a fixed-schema JSON snapshot for the next run's diff and audit trail.

Code: [`day1-status-report/`](day1-status-report/) · Sample inputs: [`sample-project/`](sample-project/) · Sample output: [2026-10-02 report](day1-status-report/reports/2026-10-02-status-DRAFT.md)

## Roadmap

| Day | Build | Status | Write-up |
|---|---|---|---|
| 0 | Setup, charter, foundations | 🟡 In progress | [Charter](docs/00-program-charter.md) |
| 1 | Status report drafter | ✅ Built + tested | [Write-up](docs/day1-tpm-writeup.md) |
| 2 | Risk context via Firecrawl MCP | ⬜ Next | |
| 3 | Risk assessment skill | ⬜ | |
| 4 | Status report in the cloud (Trigger.dev) | ⬜ | |
| 5 | Portfolio site + screenshot loop | ⬜ | |
| 6 | Scheduled reporting + risk refresh | ⬜ | |
| 7 | TPM assistant | ⬜ | |
| ★ | TPM Reporting & Portfolio Builder (capstone) | ⬜ | |

## Try it
1. Clone the repo and open it in [Claude Code](https://claude.com/claude-code).
2. `cd day1-status-report`
3. Ask: *"Draft the status report for 2026-10-02."*
4. The draft lands in `day1-status-report/reports/`, and the snapshot in `state/`.

## Repo map
- [`day1-status-report/`](day1-status-report/): workflow, RAG rubric, report template, outputs
- [`sample-project/`](sample-project/): fictional Project Atlas brief and weekly updates
- [`docs/`](docs/): program charter, TPM write-ups, glossary
- [`templates/`](templates/): TPM write-up template
- [`LESSON-PLAN.md`](LESSON-PLAN.md) · [`PROGRESS.md`](PROGRESS.md): learning plan and session log

## Tools
Claude Code · MCP · Firecrawl · Trigger.dev · TypeScript · Git/GitHub
