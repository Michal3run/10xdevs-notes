# 10xDevs Course Context

> Load this file at session start for full course awareness.

## Overview

- **Course**: 10xDevs 3rd edition (Brave Courses / Circle)
- **Duration**: 5 weeks, 25 lessons (5 per week)
- **Goal**: Build an MVP web app using AI-powered agentic workflow
- **Student**: Solo, ~5h/week budget
- **Start date**: 2026-05-19

## Schedule

- **Monday 8:00** — New lessons published (5 per week)
- **Tuesday 19:00** — Live Q&A session
- **Friday 13:00–14:00** — Office hours
- **Personal cadence**: ~1 lesson/day, notes + distill after each

## Module Map

| Module | Lessons | Theme |
|--------|---------|-------|
| M1: Agentic Environment | m1l1–m1l5 | Idea → PRD → Stack → Bootstrap → Deploy |
| M2: 10xDevs Workflow | m2l1–m2l5 | MVP plan → Architecture → Implementation → Review → Multi-agent |
| M3: (TBD) | m3l1–m3l5 | — |
| M4: (TBD) | m4l1–m4l5 | — |
| M5: (TBD) | m5l1–m5l5 | — |

### Module 1 Lessons

1. **m1l1** — Od pomysłu do PRD: Metoda Sokratejska z Agentem
2. **m1l2** — Chatbot vs Agent: tech stack, skille i metaprompting
3. **m1l3** — AI-Powered Bootstrap: boilerplate i bezpieczna praca z Agentem
4. **m1l4** — Agent Onboarding: Reguły dla AI
5. **m1l5** — Od localhost po produkcję - Deployment z Agentem

### Module 2 Lessons

1. **m2l1** — Plan MVP: milestony, zależności i bezwzględne priorytety
2. **m2l2** — Architektura z Agentami: zaplanuj pracę, zanim wygenerujesz kod
3. **m2l3** — Implementacja z AI: 80% ready challenge i kontrola kontekstu
4. **m2l4** — Solo Code Review: weryfikuj kod AI szybko i skutecznie
5. **m2l5** — Innovate: Więcej ficzerów, mniej czekania - wielowątkowa praca z Agentami

## Per-Lesson Workflow

Repeat for every lesson (aim for autopilot by week 3):

1. **Watch/read** lesson on Circle
2. **Paste** lesson markdown into `lessons-raw/Week N/mNlN-<slug>.md` (gitignored) → NotebookLM for audio
3. **Fetch artifacts** — `cd mvp-repo; 10x get mNlN --tool generic`
4. **Run skill chain** — execute the lesson's main skills in the MVP repo
5. **Do practical tasks** — complete hands-on exercises
6. **Write notes** — create `lessons/mNlN-<slug>/` with `key-takeaways.md`, `my-questions.md`, `links.md`. At end of week, write/update `lessons/weekN-overview.md` (title + skills + main idea per lesson)
7. **Distill (optional, on-demand)** — once per week or per module, run `/10x-course-distill weekN` if a cross-lesson pattern emerged. Most weeks → 0–2 entries; sometimes 0 — that's fine
8. **Commit** both repos
9. **Q&A prep** — bring `my-questions.md` to Tuesday session

## Tools & Skills

### 10x-cli

Fetch lesson artifacts: `10x get mNlN --tool generic`  
Full reference: see `10x-cli-reference.md`

### Skills Index (filled as discovered)

| Lesson | Skills |
|--------|--------|
| m0l1 | prompts (prework) |
| m1l1 | /10x-init, /10x-shape, /10x-prd |
| m1l2 | /10x-tech-stack-selector, /10x-stack-assess |
| m1l3 | /10x-bootstrapper |
| m1l4 | /10x-agents-md, /10x-rule-review, /10x-lesson |
| m1l5 | /10x-infra-research + Plan Mode |

### Custom Skills (this repo)

- `/10x-course-distill` — extracts tips/gotchas from lesson notes (append-only)

## AI Working Patterns

Rules for any AI agent working in this course workspace:

1. **Plan Mode for irreversible ops** — always use Plan Mode before destructive actions (deploy, DB changes, force-push)
2. **Never paste secrets into chat** — reference by key name, not value
3. **Append-only for shared docs** — tips.md, gotchas.md, lessons.md are never edited by AI, only appended to
4. **One skill invocation = one outcome** — don't chain skills unless the lesson explicitly says to
5. **Respect course rules** — AGENTS.md in MVP repo contains course-issued rules; don't contradict them
6. **Scratch is throwaway** — anything in `scratch/` can be deleted without asking
7. **Lesson sources are private** — never commit content from `lessons-raw/` (course IP)
8. **Keep notes lean** — max 5 bullets in `key-takeaways.md`, no restating skill mechanics. `weekN-overview.md` is the fast-scan reference; `lessons-raw/` is the depth.

## Repos

| Repo | Purpose | Location |
|------|---------|----------|
| 10xdevs-notes | Study notes, tips, gotchas, custom skills | `C:\src\10xDevs\10xdevs-notes\` |
| mvp-\<name\> | MVP deliverable (created at L1) | `C:\src\10xDevs\mvp-<name>\` |
