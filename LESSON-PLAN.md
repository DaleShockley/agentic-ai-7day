# Agentic AI Lesson Plan

A structured path through the free [Agentic AI: 7-Day Build Challenge](https://buildwithagents.vercel.app/) — adapted for three goals at once:

1. **Personal productivity** — automations I actually keep using.
2. **Career growth toward AI TPM** — a TPM write-up for every build, so the repo reads like real program work.
3. **Stronger coding skills** — a small, deliberate coding lesson each day instead of blind copy-paste.

**Theme:** every build day adds a piece of one capstone, a **TPM Reporting & Portfolio Builder**, using a *fictional* sample project. Goals, schedule (target **Oct 15, 2026**), scope and risks are in the [program charter](docs/00-program-charter.md).

> **How to use this file:** Work top to bottom. Tick boxes as you go. Log each session in [PROGRESS.md](PROGRESS.md). To pick up in a new chat, see [Resuming in a new chat](#resuming-in-a-new-chat).

---

## The learning loop (every day)

| Step | What you do | Time |
|---|---|---|
| 1. Preview | Read the day's page on the course site. Write 2–3 sentences: *what do I think we're building and why?* | 10 min |
| 2. Predict | Before pasting each course prompt, say what you expect it to do (or write your own version first). | 5 min per prompt |
| 3. Build | Run the prompts with Claude. Use **Plan Mode** before anything gets built. | 45–90 min |
| 4. Break it | Do the day's Failure Lab. Debugging is where the learning is. | 15 min |
| 5. Code lesson | The day's coding skill-up (see each day). | 15–20 min |
| 6. TPM write-up | Fill in [templates/tpm-writeup.md](templates/tpm-writeup.md) for the day. | 20 min |
| 7. Glossary + Go deeper | Add the day's new terms to [docs/glossary.md](docs/glossary.md) in your own words. Then Claude asks an interview question, you answer, and you rewrite it until it has engineering depth. | 15 min |
| 8. Quiz + commit | Claude quizzes you (5 questions). Commit and push to GitHub. | 10 min |

**Pace:** one day of the course per session, ~2–2.5 hours, following the schedule in the [charter](docs/00-program-charter.md#4-plan-and-constraints). If you're ahead, pull the next session forward.

**Ground rules**
- Anything that **sends, publishes, deploys, or spends money** gets a human approval step.
- **API keys never get committed.** They live in `.env` (already in `.gitignore`).
- Ask "why?" whenever something isn't clear. That's the point.
- Public repo: generic employer names and fictional sample data only.

---

## Week 0 — Setup and foundations (≈3–4 hours)

### Setup checklist
- [x] Create a public GitHub repo named `agentic-ai-7day` (or similar)
- [x] Install **GitHub CLI** from https://cli.github.com, then run `gh auth login`
- [x] Install **Node.js LTS** from https://nodejs.org (needed for Day 2 MCP servers and Day 4 Trigger.dev)
- [ ] Optional: install **VS Code** (the course uses it; the Claude desktop app works too)
- [x] Push this folder to the repo as the first commit
- [x] Set a monthly spending limit on any paid service you sign up for

### Foundations (free, official)
- [x] Anthropic Academy — **Claude Code in Action** (https://anthropic.skilljar.com)
- [ ] Anthropic Academy — **Introduction to Model Context Protocol** (offline, before Day 2)

### Concepts to be able to explain after Week 0
- What an **agent loop** is (model → decides → calls a tool → sees result → repeats)
- What a **tool** is, and what **MCP** adds
- What the **context window** is and why keeping CLAUDE.md short matters
- The difference between a **chatbot**, a **workflow**, and an **agent**

### Coding skill-up
- Terminal basics: `pwd`, `ls`, `cd`, `mkdir`, running a command, reading an error
- Git basics: `git status`, `git add`, `git commit`, `git push` — what each actually does

### TPM deliverable
- [x] [docs/00-program-charter.md](docs/00-program-charter.md) — why, goals, scope, schedule, risks
- [ ] Start [docs/glossary.md](docs/glossary.md) with terms from the Academy course

---

## Day 1 — Your First Workflow *(Beginner)*
**Build:** Weekly **status report** drafter. It reads a fictional project's inputs (milestones, updates, blockers), drafts an executive status report (RAG status, highlights, risks, asks), and saves it to `reports/`. A human reviews it before it's shared.
**Folder:** `day1-status-report/`

**Adaptation:** The course builds a newsletter; use the same prompt structure but point it at the status report. Create the fictional sample project first (`sample-project/`). Use Claude's built-in web search instead of Perplexity if research is needed ($0). No sending; drafts only.

**Concepts:** CLAUDE.md as the project brain · workflows as plain-English recipes · Plan Mode · the WAT model (Workflows, Agent, Tools) · interactive building vs. deployed automation

**Coding skill-up:** Markdown syntax · how folders and relative paths work · reading a file tree

**Failure lab:** Empty research result → make the workflow handle it gracefully.

**TPM write-up focus:** Define success metrics for an automated status report (accuracy against the inputs, time saved, edits needed before sending). Where are the human-in-the-loop gates, and why?

**Done when**
- [ ] CLAUDE.md + `workflows/newsletter.md` exist
- [ ] Plan Mode used before running
- [ ] At least one status report in `reports/`
- [ ] I can explain WAT without notes
- [ ] TPM write-up committed

---

## Day 2 — Using an MCP Server *(Beginner)*
**Build:** Install Firecrawl as an MCP server and use it to pull outside context into risk reviews: vendor status pages, release notes and industry news for the fictional project's dependencies.
**Folder:** `day2-risk-context-mcp/`

**Concepts:** What MCP is (a standard plug for tools) · MCP servers vs. built-in tools · choosing the right tool for the job · API keys and rate limits

**Coding skill-up:** JSON structure (reading an MCP config) · environment variables and `.env` files · why secrets never go in git

**Failure lab:** Extraction returns empty or missing fields.

**TPM write-up focus:** Vendor/dependency risk — what happens if Firecrawl is down, changes pricing, or gets rate-limited? Draft a simple fallback plan.

**Done when**
- [ ] Firecrawl MCP connected (key in `.env`, not in git)
- [ ] One successful scrape saved to a file and summarized as risk input
- [ ] I can explain MCP to a non-engineer in two sentences
- [ ] TPM write-up committed

---

## Day 3 — Building Skills *(Beginner)*
**Build:** A **risk assessment** skill, using the course's 6-step framework and iterated three times. It produces a risk register (likelihood, impact, mitigation, owner) from project inputs, with a reference file for the scoring rubric.
**Folder:** `day3-risk-skill/`

**Concepts:** Skills as reusable prompt templates · reference files · context budget (loading too much hurts quality) · iteration as a product practice

**Coding skill-up:** YAML frontmatter · git branches (make a branch per skill iteration, compare versions)

**Failure lab:** The skill loads too much context → trim it.

**Pre-read for Day 4 (20 min):** TypeScript basics (charter risk R1).

**TPM write-up focus:** Treat each iteration like a release: what changed, how you measured "better," what you'd ship.

**Done when**
- [ ] A working skill with at least one reference file
- [ ] Three iterations recorded (v1 → v3) with what improved
- [ ] TPM write-up committed

---

## Day 4 — Deploying an Automation *(Intermediate)*
**Build:** Convert the Day 1 status report workflow into a TypeScript task on Trigger.dev that runs in the cloud.
**Folder:** `day4-deploy-status-report/`
**Schedule:** Mon 10/5 plus Tue 10/6 as buffer.

**Concepts:** Local vs. deployed · deterministic code vs. an agent improvising · environments (dev/prod) · secrets in production · logs and observability

**Coding skill-up (biggest day):** TypeScript basics — variables, functions, `async/await`, imports · `npm install` and `package.json` · reading a stack trace. Ask Claude to walk through the generated code line by line.

**Failure lab:** Missing production environment variable.

**TPM write-up focus:** A launch checklist — env vars, monitoring, rollback plan, cost per run, who gets alerted when it fails.

**Done when**
- [ ] Task deployed and one successful cloud run
- [ ] I can explain every file in the task folder
- [ ] Launch checklist committed

---

## Day 5 — Website Building *(Intermediate)*
**Build:** Your **project portfolio** site, which showcases the builds and case studies. It uses a frontend design skill plus a screenshot → critique → fix loop.
**Folder:** `day5-portfolio-site/`

**Concepts:** Visual feedback loops · agents evaluating their own output · why concrete acceptance criteria matter

**Coding skill-up:** HTML structure and CSS basics · responsive design (why 375px width matters) · browser dev tools

**Failure lab:** Broken mobile layout → find and fix at least one issue.

**TPM write-up focus:** Write acceptance criteria *before* the build, then grade the result against them. This is the core of AI evaluation ("evals").

**Done when**
- [ ] Page looks right on desktop and mobile
- [ ] Before/after screenshots committed
- [ ] Acceptance criteria + grading committed

---

## Day 6 — Scheduled Automations and Loops *(Advanced)*
**Build:** The weekly status report and risk refresh run on a schedule, with a review gate before anything is shared. Covers loops, local scheduled tasks, remote routines, and a self-improvement loop.
**Folder:** `day6-scheduled-reporting/`

**Concepts:** Unattended agents · review gates · idempotency (safe to run twice) · drift — why automations get worse over time without checks

**Coding skill-up:** Cron syntax (`0 8 * * 1-5` means what?) · logging to a file · reading logs to debug

**Failure lab:** A scheduled task that stops to ask for input → rewrite it to run unattended safely.

**TPM write-up focus:** Operations — what's the on-call story for an automation nobody is watching? Define a failure alert and a weekly review.

**Done when**
- [ ] One scheduled automation running on its own
- [ ] A review gate before anything it changes goes live
- [ ] TPM write-up committed

---

## Day 7 — Your TPM Assistant *(Advanced)*
**Build:** The course's 4-phase EA (home, life, hands, growth), built in layers as a **TPM assistant** that ties together status reports, risk reviews and the charter.
**Folder:** `day7-tpm-assistant/`

**Privacy rule:** Personal context files go in `day7-tpm-assistant/private/` — **git-ignored**. Only the structure, skills, and sanitized examples are public.

**Concepts:** Personal context as a system · keeping context current · composing everything from Days 1–6

**Coding skill-up:** Organizing a multi-folder project · `.gitignore` patterns · writing a clear README

**Failure lab:** Stale or vague context → see how bad the output gets, then fix the context.

**TPM write-up focus:** Data privacy and access — what does the EA know, where is it stored, what can it act on without asking?

**Done when**
- [ ] EA gives a useful daily briefing
- [ ] No personal data in the public repo (double-check `git status` before pushing)
- [ ] TPM write-up committed

---

## Capstone *(after Day 7)*
- [ ] **TPM Reporting & Portfolio Builder** — minimum: one project input file produces a status report, risk register and charter
- [ ] **3 STAR interview stories** built from real specifics in this repo
- [ ] **Mock interview** — "Go deeper" drill on 3 standard AI TPM questions (charter goal G3)
- [ ] **Skill-stack write-up** — what you can now do, with links to each day
- [ ] **Case study** `docs/capstone-case-study.md` in TPM format: problem → approach → architecture → risks → metrics → results → lessons
- [ ] Update the repo README with a summary and a short demo (screenshots or GIF)
- [ ] Next step: Anthropic Academy **Building with the Claude API** (focus on tool use, agents, and evals)

---

## AI TPM interview prep (use your repo as evidence)

After the capstone, you should be able to answer these from your own builds:
- "Walk me through an AI system you shipped." → capstone case study
- "How do you evaluate whether an AI feature is working?" → Day 5 acceptance criteria, Day 3 iterations
- "What are the risks of agentic systems and how do you mitigate them?" → Day 1 approval gates, Day 6 review gates, Day 7 privacy
- "How do you think about cost and reliability?" → Day 2 vendor risk, Day 4 launch checklist

---

## Resuming in a new chat

**In Claude Code (recommended):** open a new session in this repo's folder. Claude reads `CLAUDE.md` automatically. Then say:

```
Let's continue the lesson plan. Read PROGRESS.md and tell me where I left off and what's next.
```

**In any other Claude chat:** paste this and attach or paste LESSON-PLAN.md and PROGRESS.md:

```
I'm working through an agentic AI lesson plan (attached) to grow toward an AI TPM role.
I have some coding experience but want to improve. Teach as we go: explain the why,
have me predict before running prompts, and quiz me at the end. Here's my progress log —
tell me where I left off and what's next.
```
