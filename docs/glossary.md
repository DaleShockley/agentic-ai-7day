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

### Week 0
<!-- To add from the Anthropic Academy course: agent loop, context window, CLAUDE.md, Plan Mode, MCP, MCP server, skill, hook, subagent, prompt vs. system prompt -->
