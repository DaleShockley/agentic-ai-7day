# Day 1: Status Report Drafter, TPM Write-up

## 1. One-pager
- **Problem:** A weekly executive status report takes a TPM about 2 hours: gathering updates, scoring each item, comparing with last week, writing it up. Color calls drift with the author's mood, so executives learn to discount them.
- **Users:** The TPM (author and reviewer); the executive sponsor (reader).
- **Success looks like:**
  - **Accuracy:** 100% of RAG colors match a hand-scored answer key (golden set). A missed Red is a critical failure.
  - **Time:** 2 hours → ≤10 minutes end to end, *including* human review.
  - **Edits:** ≤2 substantive edits per draft (a fact, color or ask changed). Wording tweaks don't count.
- **Out of scope:** Sending or publishing the report; pulling inputs from live systems (Jira etc.); scheduling (Day 6).

## 2. Architecture
```
[TPM asks for a date]
  → [Agent reads workflow + CLAUDE.md]
  → [Reads inputs: project brief, weekly update, rubric, template]
  → [Step 2: validate inputs]  ← automated gate (run by the model, per the workflow)
       missing update file → STOP, no report
       missing field → data gap, Amber, listed in report
  → [Score every item with the rubric, quoting the rule that fired]
  → [Diff against last week's JSON snapshot]
  → [Write draft report + this week's snapshot]
  → [HUMAN GATE: TPM reviews and edits the draft]
  → [Shared with exec, done manually by the TPM, never by the agent]
```

**Two outputs, two readers:** the markdown report is for executives (derived, human-edited view). The JSON snapshot is for next week's run (system of record with a fixed schema, so the week-over-week diff is structured instead of re-interpreting prose).

**Why the human gate is before sharing:** sharing is the irreversible step. Review before is quality control; review after is damage control. The cost is asymmetric. A false Green delays intervention until the problem is bigger. A false Red wastes leadership time. Either one erodes trust, and once an exec doubts one report they discount every report after it.

## 3. Risks and failure modes
| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Missing weekly update → agent reuses last week's data (stale report that looks current) | Med | High | Workflow step 2 says stop. **Tested in the Failure Lab (2026-10-09): agent stopped, wrote nothing.** Guidance only; see "do differently." |
| Agent fabricates plausible updates to fill a gap | Low | Critical | "Never invent data" in CLAUDE.md; every color must quote its rule; human review. Fabrication is dangerous because it *passes* review. |
| Model misapplies the rubric (e.g. treats 9 days late as Red) | Med | High | Rubric is explicit rules, not judgment; report shows the rule and the numbers for each item so the reviewer can check fast. |
| Blank vs. `unassigned` owner treated the same | Med | Med | Rubric separates them: `unassigned` = known, no owner → Red (leadership decision). Blank = unknown → Amber + data gap (fix the input). Snapshot stores `"unassigned"` vs `null`. |
| Agent adds data not in the inputs (e.g. a proposed deadline) | Med | Med | Allowed only if labeled as a proposal. Reviewer decides. |

## 4. Cost and metrics
- **Cost per run:** Interactive run inside an existing Claude subscription; no separate API spend. Per-run token cost gets measured on Day 4 when it's deployed.
- **Metrics I'd track:** color accuracy vs. golden set; minutes from request to approved draft; substantive edits per draft; data gaps per week (a rising count means the *inputs* are degrading).
- **How I'd know it's broken:** a report appears for a date with no update file; a color without a quoted rule; snapshot and approved report disagree; zero data gaps for many weeks straight (suspicious, not reassuring).

## 5. Retro
- **What went well:** The 10/02 run matched the hand-scored answer key on every item (B2 Red, B3 Amber + gap, M2 Amber, overall Red). The missing-input Failure Lab stopped correctly.
- **What broke:** My own predictions. I scored B2 Green, B3 Green and M2 Red. Gut feel and the rubric disagreed, which is the case for rules over judgment.
- **What I'd do differently:**
  - **Enforce "stop on missing input" with a hook**, not just workflow text: a PreToolUse hook on writes to `reports/` that blocks unless `sample-project/updates/<date>.md` exists and isn't empty.
  - **Write the snapshot *after* approval**, not before. Today the snapshot records the unreviewed draft, so if I edit a color, next week diffs against data I didn't sign off on.
  - **Validate with code, not the model:** a script that checks required fields, that dates parse, and that IDs are unique, plus an enum for `color` (Green/Amber/Red only). Planned for Day 4.
- **What I learned (in my own words):**
  - When I predicted RAG colors from gut feel, my calls missed the rubric in *both* directions: I called B2 Green when it was Red (unassigned owner), and M2 Red when it was Amber (9 days late). That's noise, not just bias. A written rubric gives the same answer no matter who runs it, so leadership can trust the color and argue about the data instead of the opinion.
  - The report is for humans to read; the JSON snapshot is for the next run. Saving raw status data each cycle makes week-over-week changes a simple diff instead of a manual reconstruction. It also creates an audit trail: if someone questions a color later, I can show exactly what data produced it.
