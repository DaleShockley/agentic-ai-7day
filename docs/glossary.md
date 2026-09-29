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
- **Interview sentence:** *TODO*

#### CLAUDE.md
- **What it is:** A project instruction file that is loaded into the conversation as context.
- **How it works underneath:** It is loaded automatically at the start of every session *[added]*. The model reads the text and *chooses* to follow it. It can fail to follow it because it misjudges whether a rule applies, the rule conflicts with other instructions, it loses track in a long conversation, or it just makes an error. Because it is loaded every session, it costs context on every turn, so it should stay lean *[added]*.
  - Executed by: the model. Can be ignored: yes. Good for: judgment, conventions, context. Limitation: not guaranteed.
- **Interview sentence:** *TODO*

#### Hook
- **What it is:** A script that runs at defined points in the agent's lifecycle.
- **How it works underneath:** Hooks are executed by the app, not the model. The model doesn't decide whether a hook runs, and it can't stop it, argue with it or forget it. A hook that runs *before* a tool call (`PreToolUse`) can block it: if the script exits with a block signal, the tool call never happens and the script's reason is sent back to the model so it can adjust *[added]*.
  - Executed by: the Claude Code app. Can be ignored: no. Good for: rules with a mechanical check. Limitations: it's only as smart as the script, and it only fires at lifecycle events.
- **Interview sentence:** *TODO (start here)*

#### Headless mode
- **What it is:** Running Claude without a human at the keyboard, for example as one step in a pipeline or a scheduled job.
- **How it works underneath:** When Claude wants to do something risky, it checks its permissions: if the action is allowed it proceeds; if not, it can't. In an interactive session, the main safety guardrail is the **permission prompt** (the "Allow Claude to run this?" dialog a human answers). In headless mode there is no one to approve, so anything not pre-authorized can't be approved. Approvals have to be made in advance, as part of the configuration: allow/deny rules in a settings file, e.g. allow `git status`, deny `git push` *[added]*.
- **Interview sentence:** *TODO*

<!-- Still to add: agent loop, context window, Plan Mode, MCP, MCP server, skill, subagent, rewind, permissions, routine, prompt vs. system prompt -->

---

## Course notes: Claude Code in Action

Key takeaways, in my words. These are principles rather than terms; the terms they mention get their own entries above.

1. **Steer the work.** Direct compaction summaries to keep what matters. Use the rewind menu to reverse and correct issues. There is hands-on steering, and there are autonomous goals.
2. **Configure Claude.** Keep CLAUDE.md files lean; Claude follows a lean file better. Repeat procedures should be skills. Pick the right permissions for each job. Non-negotiable rules should be enforced with hooks.
3. **Automate repeat work.** Routine work should be scheduled. Use headless mode when Claude is part of a pipeline.
4. **Verify and share.** Verify runs in proportion to how little you watch them. Use hooks to gate results. "Read the diff rather than the write-up."
