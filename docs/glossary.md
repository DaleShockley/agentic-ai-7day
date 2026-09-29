# Engineering-Depth Glossary

My working vocabulary for agentic AI, written **in my own words**. Target: 50+ terms by Oct 15 (Charter goal G3).

For each term:
- **What it is:** a plain definition
- **How it works underneath:** the mechanism, one level deeper than the definition
- **Interview sentence:** how I'd actually use it when describing work I've done

---

## Example

### Tool use (function calling)
- **What it is:** The model's ability to ask for an external function to be run (search, read a file, create a Jira ticket) instead of only replying with text.
- **How it works underneath:** The app gives the model a list of tools, each with a name, a description and an input schema. The model replies with a structured request to call one of them. The app runs the tool and sends the result back, and the model continues from there.
- **Interview sentence:** "The agent had read tools for Jira and GitHub, but write access went through a single scoped tool behind a config-review gate. So the model could *request* a write, but it couldn't make one on its own."

---

## Terms

<!-- Add new terms below, grouped by the day you learned them. -->
1. Steer the Work: In Plan mode, you need to direct  compaction summaries to keep what matters. You can use the rewind menu to revierss and correct issues. there is a Hands-on steering and autonomous goals.

2. Configure Claude: CLAUDE.md files should be kept lean. Claude can follow a lean .md file. Repeat procedures should be skills. Pick the right permissions for each job. NON-negotiable rule should be enforred with HOOKS.

3. Automate Repeat Work: Routines work should be scheduled. Use Headless mode when part of a pipeline.

4. Verify and Share: vERIFY RUNS IN PROPOTION TO HOW LITTLE OF MUCH YOU WATCH THEM. Use Hooks to gate resuilts. "Read the diff rather then toe write-up"

5. Compaction: Claude has no retained memory between turns. Each time a tern is started, Claude must reread the chat log. Longer chats this is measurered in tokens. The model can only hold a limited number at once. Quality drops as the chats get longer. reprocessing everything take longer and costs more to execute. Compaction replaces history with a summary. Details are lost, reasoning behind a decision is lost and the intstructions given mid-session is lost.

6. Claude.md: is text loaded into the chat as context by the model. the Model reads toe text and chooses to follow. It can choose not to follow the instructions, doe to misjudgement wiather the rule applies, conflicts with other intstructions, losses track in a long converstaion and errors.
- Executed by the Model, Can be ignored, good for Judgement, convertions and context and limitations are not guaranteed.

8. Hooks: Are executed by the app. Hooks are scripts that runs at defined points in the lifecycle. The model does not decide whether to hook runs and it cannot stop it, argue with it or forget it. 
- Executed by the Claude Code app, it cannot be ignored, its good for Rules with a mechanical check and it limitations is its only as smart as the script and only fires at lifecycle events.

9. Headless mode: when Claude want to do something risky it checks its permissions,if its allowed it acts, it not cannot act. The prompt is the main safty gardrale. in Headless mode, there is no one to approve so anythng not pre-authorized can's get approved. Approvels must be made in advances and part of configurations. 

### Week 0
<!-- To add from the Anthropic Academy course: agent loop, context window, CLAUDE.md, Plan Mode, MCP, MCP server, skill, hook, subagent, prompt vs. system prompt -->
