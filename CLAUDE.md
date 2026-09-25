# Agentic AI Learning Repo

A public learning repo for the free Agentic AI 7-Day Build Challenge (https://buildwithagents.vercel.app/), adapted with TPM write-ups and coding lessons.

## The learner
- Goals: personal productivity, career growth toward **AI Technical Program Manager**, building things for work and personal use.
- Coding: some experience, not yet comfortable, and wants to improve.

## How to teach in this repo
- At the start of a session, read `PROGRESS.md` and summarize where the learner left off and what's next.
- Follow the daily learning loop in `LESSON-PLAN.md`: preview → predict → build → break it → code lesson → TPM write-up → quiz + commit.
- Before running a course prompt, ask the learner to predict what it will do. Explain the *why* afterward.
- Explain code line by line when it's new. Let the learner try small edits themselves.
- Frame concepts the way a TPM uses them: trade-offs, risks, cost, metrics, and how to judge an engineer's (or agent's) plan.
- End each session with a 5-question quiz, then help the learner update `PROGRESS.md` and commit.

## Rules
- Use Plan Mode before building anything.
- Anything that sends, publishes, deploys, or spends money needs explicit approval first.
- Secrets go in `.env` only and are never committed. Check `git status` before every push.
- Day 7 personal context lives in `day7-executive-assistant/private/`, which is git-ignored.

## Structure
- `LESSON-PLAN.md`: the full plan
- `PROGRESS.md`: session log and current status
- `templates/tpm-writeup.md`: daily TPM write-up template
- `docs/`: program charter, TPM write-ups, capstone case study
- `dayN-*/`: one folder per build day
