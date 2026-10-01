# Engineering-Depth Glossary

My working vocabulary for agentic AI, written **in my own words**. Target: 50+ terms by Oct 15 (Charter goal G3).

For each term:
- **What it is:** a plain definition
- **How it works underneath:** the mechanism, one level deeper than the definition
- **Interview sentence:** how I'd actually use it when describing work I've done

Text marked *[added]* came from a review session. Rewrite it in my own words once I can explain it without notes.

---

## Example

### Tool use (function calling)
- **What it is:** The model's ability to ask for an external function to be run (search, read a file, create a Jira ticket) instead of only replying with text.
- **How it works underneath:** The app gives the model a list of tools, each with a name, a description and an input schema. The model replies with a structured request to call one of them. The app runs the tool and sends the result back, and the model continues from there.
- **Interview sentence:** "The agent had read tools for Jira and GitHub, but write access went through a single scoped tool behind a config-review gate. So the model could *request* a write, but it couldn't make one on its own."

---

## Terms

<!-- Add new terms below, grouped by the day you learned them. -->

### Week 0

#### Compaction
- **What it is:** Replacing the conversation history with a summary so the session can keep going when it gets too long.
- **How it works underneath:** Claude has no retained memory between turns. Each time a turn starts, the whole chat log is sent to the model again. That log is measured in tokens, and the model can only hold a limited number at once (the context window). As chats get longer, quality drops, and reprocessing everything takes longer and costs more. Compaction swaps the history for a summary. What gets lost: details, the reasoning behind decisions, and instructions given mid-session. I can steer the summary to keep what matters.
- **Interview sentence:** Compaction is a planned handoff: when a session's context fills up, Claude replaces the history with a summary, so I compact at natural breakpoints, tell it what to keep, and put durable rules in CLAUDE.md or a file so nothing critical depends on the summary.

#### CLAUDE.md
- **What it is:** A project instruction file that is loaded into the conversation as context.
- **How it works underneath:** It is loaded automatically at the start of every session *[added]*. The model reads the text and *chooses* to follow it. It can fail to follow it because it misjudges whether a rule applies, the rule conflicts with other instructions, it loses track in a long conversation, or it just makes an error. Because it is loaded every session, it costs context on every turn, so it should stay lean *[added]*.
  - Executed by: the model. Can be ignored: yes. Good for: judgment, conventions, context. Limitation: not guaranteed.
- **Interview sentence:** CLAUDE.md is guidance, not enforcement: the model reads it every session and usually follows it, so I keep it lean, use it for conventions and context that need judgment, and back any rule that can't be broken with a hook.

#### Hook
- **What it is:** A script that runs at defined points in the agent's lifecycle.
- **How it works underneath:** Hooks are executed by the app, not the model. The model doesn't decide whether a hook runs, and it can't stop it, argue with it or forget it. A hook that runs *before* a tool call (`PreToolUse`) can block it: if the script exits with a block signal, the tool call never happens and the script's reason is sent back to the model so it can adjust *[added]*.
  - Executed by: the Claude Code app. Can be ignored: no. Good for: rules with a mechanical check. Limitations: it's only as smart as the script, and it only fires at lifecycle events.
- **Interview sentence:** Hooks are how I turn a rule into a guarantee: the app runs them at fixed points in the agent's lifecycle, so the model can't skip them, and I use them to block unsafe actions and to stop Claude from declaring a task done until the tests actually pass.

#### Headless mode
- **What it is:** Running Claude without a human at the keyboard, for example as one step in a pipeline or a scheduled job.
- **How it works underneath:** When Claude wants to do something risky, it checks its permissions: if the action is allowed it proceeds; if not, it can't. In an interactive session, the main safety guardrail is the **permission prompt** (the "Allow Claude to run this?" dialog a human answers). In headless mode there is no one to approve, so anything not pre-authorized can't be approved. Approvals have to be made in advance, as part of the configuration: allow/deny rules in a settings file, e.g. allow `git status`, deny `git push` *[added]*.
- **Interview sentence:** Headless mode moves oversight from runtime to design time and review time: since no one is there to approve actions, I pre-authorize exactly what the job needs, deny the dangerous operations, enforce hard rules with hooks, run it in a contained environment, and verify the output before anything merges.

#### Agent loop
- **What it is:** The cycle an AI agent repeats to finish a task: decide on an action, call a tool, observe the result, decide what to do next, until it's done.
- **How it works underneath:** Each pass is one model call. The app sends the conversation plus the list of tools; the model replies with either text (done) or a tool request; the app runs the tool, appends the result, and calls the model again. The Day 1 10/02 run was one loop: read 4 files → write 2 files → stop. Errors compound across passes, so checkpoints (like step 2's "stop if the input is missing") and limits matter *[added]*.
- **Interview sentence:** The loop is what separates an agent from a chatbot: it reads, acts and checks results without a human prompting each step. The risks live in the loop too (runaway steps, wrong tool calls, compounding errors), so I design in checkpoints, limits and human approval for any action that changes data.

#### Context window
- **What it is:** The maximum amount of text, measured in tokens, a model can consider at once: instructions, documents, conversation history and its own output.
- **How it works underneath:** The model keeps no memory between turns; the whole conversation is re-sent every turn, so everything loaded (CLAUDE.md, files read, tool results) uses up the window on every turn. Too much irrelevant content lowers quality and raises cost; when it fills, compaction kicks in (see Compaction) *[added]*.
- **Interview sentence:** The context window is the model's working memory, and managing it is a design decision. I filter to what the task needs and pull details on demand through tools, much like preparing a briefing for an executive.

#### Plan Mode
- **What it is:** A Claude Code mode where Claude researches and proposes a step-by-step plan without editing files until I approve it.
- **How it works underneath:** The app restricts Claude to read-only tools; the only file it can write is the plan itself. Edits are unlocked only when I approve the plan. That's enforced by the app, not just promised by the model (compare Hook vs. CLAUDE.md). On Day 1, the plan for the 10/02 run listed the expected colors before running, so it doubled as the answer key *[added]*.
- **Interview sentence:** Plan Mode is "align before you build": for any multi-step or risky change, the agent proposes scope and sequencing and I approve before a file is touched. It's cheaper to correct a plan than to unwind changes, and it keeps the decision with me.

<!-- Still to add: MCP, MCP server, skill, subagent, rewind, permissions, routine, prompt vs. system prompt -->

### Day 1

#### Eval
- **What it is:** A repeatable test that measures how well an AI system does a task, using defined inputs, expected outputs and a scoring method.
- **How it works underneath:** Run the system on fixed inputs, compare each output with the known-correct answer, and score it (e.g. "7 of 7 RAG colors match"). Rerun it after every prompt, rubric or model change to catch regressions *[added]*.
- **Interview sentence:** I treat evals like acceptance criteria for AI. On a status-report drafter I built, I hand-scored an answer key for a week's inputs and checked the agent's RAG colors against it: every item matched. That turns "the output looks good" into a number I can rerun every time I change the prompt or rubric *[added]*.

#### Golden set
- **What it is:** A curated set of inputs paired with known-correct outputs, used as the reference answers for an eval.
- **How it works underneath:** On Day 1 my answer-key table for 10/02 was a golden set of one week. A useful one covers the edge cases that actually break things: `unassigned` vs. blank owner, a milestone exactly 14 vs. 15 days late, a missing update file *[added]*.
- **Interview sentence:** The golden set is the most valuable artifact in an AI project and the one teams underinvest in. If it's wrong or too easy, every score built on it misleads, so I cover real edge cases, version it like code, and add real failures as they happen.

#### Enum
- **What it is:** A field restricted to a fixed list of allowed values, such as Red, Amber or Green.
- **How it works underneath:** Code checks each value against the list and rejects anything else. On Day 1 the snapshot's `color` field accepts any text, so nothing would stop the model writing "Blue". An enum check fixes that; planned for Day 4 *[added]*.
- **Interview sentence:** Enums keep data clean at the source. If status is free text you get "Yellow", "amber", "at risk" and reporting breaks, so when an LLM produces structured output I constrain fields to enums and downstream rollups never have to guess.

#### Schema
- **What it is:** The defined structure of data: which fields exist, their types, which are required, and their allowed values.
- **How it works underneath:** The Day 1 workflow fixes the snapshot's shape (`report_date`, `overall`, `items[]` with `id`, `color`, `rule`, dates), so next week's run can rely on it. A validator can reject any snapshot that doesn't match *[added]*.
- **Interview sentence:** A schema is a contract between whoever produces data and whoever consumes it. I defined the snapshot shape before the first run, so the report, the week-over-week diff and any future dashboard read the same structure, and it makes AI output testable: validate it and reject anything malformed.

#### System of record
- **What it is:** The single authoritative source for a piece of data, where the official value lives.
- **How it works underneath:** In Day 1, the JSON snapshot is the system of record and the markdown report is a derived, human-edited view. Known flaw: the snapshot is written *before* review, so if I edit a color, the two disagree *[added]*.
- **Interview sentence:** At a Fortune 500 fintech, a portfolio-management tool was the system of record for the roadmap and Jira for execution. A lot of my work was getting teams to agree which system owned which fact, so we stopped reconciling spreadsheets that disagreed. My rule: reports and AI tools read from the system of record and never become a competing source of truth.

#### Null vs. explicit value
- **What it is:** Null means a value is unknown or missing; an explicit value (including "none" or `unassigned`) means someone deliberately set it.
- **How it works underneath:** In the Day 1 rubric, `unassigned` (B2) is a known fact: nobody owns it, so Red, and leadership has to decide. A blank owner (B3) is unknown, so Amber plus a data gap: fix the input. The snapshot stores them as `"unassigned"` vs. `null` *[added]*.
- **Interview sentence:** The two need different fixes: one needs a leadership decision, the other a data correction. A system that collapses them either raises false alarms or hides real gaps, so I design rubrics to treat missing data as its own condition.

#### Relative vs. absolute path
- **What it is:** An absolute path gives a file's full location from the root (`C:\Users\...\reports\x.md`); a relative path gives its location from where you are (`../sample-project/updates/x.md`).
- **How it works underneath:** `..` means up one folder; a folder name means go down into it. From `day1-status-report/reports/` it takes `../../` to reach the repo root. Absolute paths break on any other machine, including a cloud container on Day 4, and leak usernames in a public repo *[added]*.
- **Interview sentence:** Absolute paths break when code moves; relative paths are portable but depend on where the script runs from. I anchor paths to the project root so the same automation works for me, a teammate or a scheduled job.

#### Bias vs. noise
- **What it is:** Bias is consistent error in one direction; noise is random variation in judgments that should come out the same.
- **How it works underneath:** You can correct for bias because it's predictable; noise is worse because it isn't. A written rubric removes both, because it gives the same answer no matter who applies it *[added]*.
- **Interview sentence:** When I predicted RAG colors from gut feel and checked them against a rubric, I missed in both directions: an unowned blocker I called Green was Red, and a 9-day slip I called Red was Amber. That's noise, not just bias, and it's why I push for rules-based scoring and keep human judgment for the commentary *[added]*.

---

## Course notes: Claude Code in Action

Key takeaways, in my words. These are principles rather than terms; the terms they mention get their own entries above.

1. **Steer the work.** Direct compaction summaries to keep what matters. Use the rewind menu to reverse and correct issues. There is hands-on steering, and there are autonomous goals.
2. **Configure Claude.** Keep CLAUDE.md files lean; Claude follows a lean file better. Repeat procedures should be skills. Pick the right permissions for each job. Non-negotiable rules should be enforced with hooks.
3. **Automate repeat work.** Routine work should be scheduled. Use headless mode when Claude is part of a pipeline.
4. **Verify and share.** Verify runs in proportion to how little you watch them. Use hooks to gate results. "Read the diff rather than the write-up."
