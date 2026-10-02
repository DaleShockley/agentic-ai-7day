# Program Charter: Agentic AI Build Program

| | |
|---|---|
| **Owner** | Dale Shockley |
| **Dates** | Sep 28 – Oct 15, 2026 |
| **Status** | 🟢 Approved: executing Week 0 |
| **Deliverable** | TPM Reporting & Portfolio Builder (capstone) |

## 1. Why

I've led agentic AI programs at enterprise scale, including co-designing the architecture and governance for an org-wide Claude/MCP bug-triage system at a Fortune 500 fintech. This program closes the gap between *leading* AI programs and *building* them myself. I'll design, build, deploy and operate agentic automations end to end, sharpen my technical vocabulary to engineering depth, and deliver a working **TPM Reporting & Portfolio Builder**. It's a hands-on version of the executive reporting systems I've built as a TPM, such as consolidating 25 fragmented trackers into one reporting cadence.

**Problem statement:** I've led AI programs at the outcome and governance level. This program adds the hands-on build experience and engineering vocabulary to explain *how* these systems work underneath, end to end.

## 2. Goals and success metrics

| # | Goal | Measure of success |
|---|---|---|
| G1 | Hands-on build competence | All 7 builds working; can explain every file in the Day 4 task without notes |
| G2 | TPM Reporting & Portfolio Builder shipped | Generates a status report, risk register and charter from project inputs; runs weekly without me |
| G3 | **Engineering-depth vocabulary** | 50+ terms in [my glossary](glossary.md) in my own words; pass the "Go deeper" drill on 3 standard AI TPM interview questions by Oct 15 |
| G4 | Interview-ready evidence | Public repo with 7 TPM write-ups, a capstone case study and 3 STAR stories |
| G5 | Coding confidence | At least one change made by me, without Claude, on each of Days 4, 5 and 6 |

## 3. Scope

**In scope:** Every build day is themed around the capstone tool. We adapt the [7-Day Build Challenge](https://buildwithagents.vercel.app/) prompts where needed.

| Day | Course build | TPM version |
|---|---|---|
| 1 | Newsletter workflow | Weekly **status report** drafter |
| 2 | Firecrawl MCP | Pull outside context (vendor, industry, dependency news) into risk reviews |
| 3 | Custom skill | **Risk assessment** skill |
| 4 | Cloud deploy | Status report runs in the cloud (Trigger.dev) |
| 5 | Landing page | **Project portfolio** site |
| 6 | Scheduled automation | Weekly report and risk refresh on a schedule, with a review gate |
| 7 | Executive assistant | TPM assistant tying it all together |
| ★ | Capstone | **TPM Reporting & Portfolio Builder** |

**Out of scope:**
- Real employer data. All sample data comes from a **fictional project**.
- Paid tools beyond the budget cap
- Production-grade multi-user features (auth, permissions, UI polish beyond the portfolio site)

## 4. Plan and constraints

| Date | Session |
|---|---|
| Mon 9/28 | Charter + Anthropic Academy "Claude Code in Action" |
| Tue 9/29 | Day 1: status report drafter |
| Wed 9/30 | Day 2: MCP, outside context for risk reviews |
| Thu 10/1 | Day 3: risk assessment skill |
| Fri 10/2 | *Buffer* |
| Mon 10/5 | Day 4: deploy the status report (part 1) |
| Tue 10/6 | Day 4 part 2 / *buffer* |
| Wed 10/7 | Day 5: portfolio site |
| Thu 10/8 | Day 6: scheduled reporting |
| Fri 10/9 | Day 7: TPM assistant |
| Mon 10/12 | Capstone build |
| Tue 10/13 | Capstone case study + 3 STAR stories |
| Wed 10/14 | Mock interview: "Go deeper" drill |
| Thu 10/15 | **Done.** Buffer / polish |

**Constraints**
- **Time:** about 2–2.5 hours per session, more when available. If I'm ahead, pull the next session forward.
- **Budget:** no more than $20 beyond the Claude subscription, with spending caps on every paid service.
- **Confidentiality:** public repo, so generic employer names and fictional sample data only.
- **Governance:** anything that sends, publishes, deploys or spends money needs explicit approval first.

**Cut line:** Days 1–4 plus the capstone and the STAR stories are must-haves. Days 5–7 are nice to have.

## 5. Risks

| # | Risk | L | I | Mitigation |
|---|---|---|---|---|
| R1 | Day 4 (TypeScript + deploy) runs over | H | M | Buffer on Tue 10/6; 20 minutes of TypeScript pre-reading on Day 3 |
| R2 | Job search or interviews take priority | M | H | Weekends as overflow; the cut line protects the must-haves |
| R3 | Claude usage limits on heavy build days | M | M | Plan Mode to reduce rework; split heavy days into two sessions |
| R4 | Copy-pasting without learning, so depth doesn't stick | M | H | Predict before each prompt, daily glossary, "Go deeper" drill, quiz |
| R5 | Confidential employer info leaks into the public repo | L | H | Generic names, fictional data, `git status` review before every push |
| R6 | A third-party service changes its free tier or goes down (Firecrawl, Trigger.dev) | L | M | Fall back to built-in web search, or run locally |
| R7 | Scope creep on the TPM tool | M | M | Capstone minimum: one project input file produces a status report, risk register and charter |

*L = likelihood, I = impact (H/M/L)*

## 6. Change log

| Date | Change |
|---|---|
| 2026-09-28 | Charter created and approved |
