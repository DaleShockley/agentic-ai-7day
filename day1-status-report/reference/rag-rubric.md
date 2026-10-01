# RAG Rubric

Rules for assigning Green, Amber, or Red to each item and to the overall report. Apply them exactly as written. If a rule does not cover a case, flag it as a data gap rather than guessing.

## Definitions

- **Report date:** the date given in the inputs for this week's report. All ages and lateness are measured against it, never against today's date.
- **Committed date:** the milestone date the team agreed to. It does not change when the plan slips.
- **Forecast date:** the team's current best estimate for an open milestone.
- **Actual date:** the date a milestone was completed.
- **Days late (milestones):** calendar days, calculated as follows:
  - Completed milestone: actual date minus committed date.
  - Open milestone: the later of (forecast date, report date) minus committed date. A forecast date that is already in the past is stale, so use the report date instead.
  - Zero or negative means not late.
- **Blocker age:** business days (Monday to Friday, holidays ignored) after the opened date, up to and including the report date. The opened date itself does not count. Example: opened Tuesday, report date Friday of the same week = 3 business days.
- **Owner field:**
  - `unassigned` means the team knows no one owns it.
  - Blank or missing means the data was not provided.

## Item rules

Check Red first, then Amber. An item is Green only if no Red or Amber rule applies.

### Red (needs leadership intervention)

- A milestone is more than 14 days late.
- A blocker's owner is `unassigned`.
- A blocker is more than 10 business days old.
- A slip moves a committed external date (customer, contract, or public commitment).

### Amber (at risk, team can recover)

- A milestone is 1 to 14 days late.
- A blocker is more than 5 business days old.
- A blocker has an owner but no target resolution date.
- A blocker's owner field is blank. Also add a **data gap** flag.
- An open milestone has no forecast date, or any milestone has no committed date. Also add a **data gap** flag.

### Green (on track)

- None of the Red or Amber rules apply.

## Overall status

- Overall status is the worst color of any item. No averaging.
- Missing data never produces Green. Unknown is at least Amber.

## Reporting requirements

- Every Red item must have a specific ask for leadership in the Asks section.
- Every data gap must be listed in the report so a human can fix the input.
- For each item that is not Green, state the rule that set its color.