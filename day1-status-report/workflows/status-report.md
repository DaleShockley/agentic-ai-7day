# Workflow: Weekly Status Report

**Input:** a report date (YYYY-MM-DD), e.g. "draft the status report for 2026-10-02".
**Output:** a draft report in `reports/` and a snapshot in `state/`.
All paths below are relative to `day1-status-report/`.

## Steps

### 1. Read the inputs
- Project brief: `../sample-project/project.md`
- This week's update: `../sample-project/updates/<date>.md`
- Rubric: `reference/rag-rubric.md`
- Template: `reference/report-template.md`

### 2. Validate the inputs
- If the update file doesn't exist or is empty: **stop.** Don't write a report. Tell me which file was missing.
- For each milestone and blocker, check that the required fields are present:
  - Milestone: committed date, forecast/actual date, status
  - Blocker: owner, opened date, target resolution
- A missing field is a **data gap.** Never fill it in or guess. Apply the rubric's data-gap rule and list it under "Data gaps" in the report.

### 3. Score every item
Apply `reference/rag-rubric.md` to each milestone and each open blocker. For each item, record:
- its color
- **the exact rule that fired** (quote it), plus the numbers used (e.g. "forecast 9 days after committed date")

Resolved blockers aren't scored; list them as closed.

### 4. Set the overall status
Overall = the worst color among all scored items.

### 5. Compare with last week
- Find the most recent snapshot in `state/` dated *before* this report's date.
- If there isn't one: write "Week 1 baseline, no prior report to compare." and move on.
- Otherwise list: overall color change, each item whose color changed, new blockers, closed blockers, and forecast dates that moved.

### 6. Draft the report
Fill in `reference/report-template.md`. Every **Red** item must have a specific ask: who needs to do what, by when.
Use only the sections in the template. Don't add, drop or rename sections.

### 7. Save
- Report: `reports/<date>-status-DRAFT.md`
- Snapshot: `state/<date>-snapshot.json` in this shape:

```json
{
  "report_date": "2026-10-02",
  "overall": "Red",
  "items": [
    { "id": "M2", "type": "milestone", "color": "Amber", "rule": "...", "committed": "2026-10-09", "forecast": "2026-10-18" },
    { "id": "B2", "type": "blocker", "color": "Red", "rule": "...", "owner": "unassigned", "opened": "2026-09-29", "target": null }
  ],
  "closed_blockers": ["B1"],
  "data_gaps": ["B3: owner field missing"]
}
```

Running the workflow twice for the same date overwrites the same two files.

### 8. Stop
Don't send or publish anything. Reply with the two file paths and a 3-line summary: overall color, the biggest change, and the top ask.
