# Progress Log

**Current phase:** Day 1: Status report drafter (built; review items carry over)
**Next action:** Retake the Day 1 quiz from memory, cover WAT + Markdown basics, then Day 2 (MCP). MCP Academy course before Day 2.
**Target finish:** Oct 15, 2026 (see [charter](docs/00-program-charter.md))

## Status

| Phase | Status | Completed | Write-up |
|---|---|---|---|
| Week 0: Setup + foundations | In progress | | [Charter](docs/00-program-charter.md) |
| Day 1: Status report drafter | Built, review pending | | [Write-up](docs/day1-tpm-writeup.md) |
| Day 2: Risk context (MCP) | Not started | | |
| Day 3: Risk assessment skill | Not started | | |
| Day 4: Deploy status report | Not started | | |
| Day 5: Portfolio site | Not started | | |
| Day 6: Scheduled reporting | Not started | | |
| Day 7: TPM assistant | Not started | | |
| Capstone: TPM Reporting & Portfolio Builder | Not started | | |

## Session log

Add a new entry at the top after each session.

### 2026-10-01 — Day 1: Status report drafter (second run, Failure Lab, write-up)
- What I built: Ran the workflow for 2026-10-02, the first real week-over-week run. The output matched my hand-scored answer key on every item: overall Red (B2 unassigned), M2 Amber (9 days late), B3 Amber + data gap (blank owner), B1 closed.
- What broke and how we fixed it: My predictions missed in both directions (B2 Green → really Red; M2 Red → really Amber). Failure Lab: asked for 2026-10-09 with no update file; the workflow stopped and wrote nothing (correct). Found a design flaw: the snapshot is written *before* human review.
- New concepts I can now explain: eval, golden set, enum, schema, system of record, null vs. explicit value, relative vs. absolute path, bias vs. noise. Also added agent loop, context window, Plan Mode (Week 0 leftovers).
- Coding skill practiced: relative paths (`..`), `test -s` to check a file exists and isn't empty.
- Quiz score: 0/5. Key ideas didn't stick from memory: `unassigned` = Red at any age; days late = forecast − committed; `null` = unknown; CLAUDE.md is guidance, hooks are enforcement.
- Open questions: Pasting answers from another chat sounded polished but didn't build memory. Next time: write first, rough is fine.
- Next action: **Retake the same 5 quiz questions from memory** to start next session. Then cover the WAT model and Markdown basics (Day 1 leftovers), and start Day 2 (MCP). Stretch: build the PreToolUse hook that blocks a report with no source file.

### 2026-09-28 — Week 0: Program charter
- Wrote the program charter: why, goals (G1–G5), scope, schedule to Oct 15, risks (R1–R7).
- Key insight: in interviews my answers sound too high-level. Main thread of the program: **engineering-depth vocabulary** (glossary + "Go deeper" drill).
- Scope decision: every build day is themed toward the capstone, a **TPM Reporting & Portfolio Builder** (option A). Fictional sample data only.
- Confidentiality: past employers referred to generically in this public repo.
- Fixed PATH so gh/node/npx work in Claude (fully quit the app from the system tray).
- Next action: Academy course + glossary, then Day 1.

### 2026-09-25 — Planning
- Chose the 7-Day Build Challenge plus Anthropic Academy courses, with TPM write-ups added.
- Goals: personal productivity + career growth toward AI TPM + improve coding.
- Repo will be public; Day 7 personal data stays git-ignored.
- Installed GitHub CLI + Node.js. Created public repo DaleShockley/agentic-ai-7day and pushed the first commit.

<!-- Template for new entries:
### YYYY-MM-DD — Day N: <title>
- What I built:
- What broke and how we fixed it:
- New concepts I can now explain:
- Coding skill practiced:
- Quiz score: /5
- Open questions:
- Next action:
-->

## Open questions / things to revisit
- Is ~2–2.5 hours per session enough? Revisit after Day 1.
