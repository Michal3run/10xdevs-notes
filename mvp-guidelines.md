# MVP Project Guidelines

> Extracted from prework lesson 4.2 "Dobry i zły projekt kursowy"

## The Rule

**If your first working user flow takes more than a week of after-hours work, shrink the MVP.**

## What a good course project needs

1. **Access control** — auth or user differentiation (not an anonymous demo page)
2. **Data management** — CRUD that makes sense for the domain (not bolted-on)
3. **Business logic** — the app makes a domain decision (classifies, recommends, validates, generates, scores). Describe it in one sentence or it's too vague.
4. **Project artifacts** — PRD, specs, plans, AI context (modules 1–3)
5. **At least one user-flow test** — proves the key flow works
6. **CI/CD** — pipeline that builds + runs tests. Public deploy is bonus, not priority.

## Quick evaluation table

| Criterion | Good | Bad |
|-----------|------|-----|
| User | Know who uses it and why | "For everyone" |
| Problem | One specific pain | General platform |
| MVP | 1–2 key flows | Feature roadmap |
| Data | Emerges from domain | Artificial CRUD |
| Business logic | App makes a domain decision | Records just sit in DB |
| Stack | Known, well-documented, agent-friendly | Niche or chosen out of curiosity |
| Test | Can verify main flow | Nothing meaningful to test |
| CI/CD | Auto build + test | Needs full infra setup first |

## Red flags (bad project patterns)

- **High zero-to-one threshold** — weeks of setup before anything works (auth integrations, unknown frameworks, external APIs before basic flow exists)
- **Bloated MVP** — starts simple, grows to 10 features in 5 minutes of brainstorming
- **Empty CRUD** — add/edit/delete with no domain decision (fix: add a rule — recommendation, scoring, classification, validation, workflow)

## Decision heuristic

Between two ideas, pick the one with a shorter path to first working flow and more obvious business logic. Impressive comes later.

## Certification deadlines

| Milestone | Date |
|-----------|------|
| Course ends | 2026-06-19 |
| 1st deadline | 2026-07-05 (feedback by 07-19) |
| 2nd deadline | 2026-08-10 (feedback by 08-25) |
| 3rd deadline | 2026-09-14 (feedback by 09-30) |

## Inspiration

- [Demo Day 1st edition](https://www.youtube.com/watch?v=b-gOI128G2s)
- [Demo Day 2nd edition](https://www.youtube.com/watch?v=duTuGy1xF-Q)

Look for: clear problem, working flow, simple story ("user does X, app helps achieve Y").
