# AGENTS.md — 10xdevs-notes

> Conventions for AI agents working in this study-notes repo.

## Context

This is a personal course-notes repository for the 10xDevs course. Load `course-context.md` at session start for full course details, schedule, and workflow.

## Conventions

- Per-lesson notes go in `lessons/mNlN-<slug>/` with files: `key-takeaways.md`, `my-questions.md`, `links.md`
- Per-week overview lives at `lessons/weekN-overview.md` (one file per week, consolidating all 5 lessons)
- `tips.md` and `gotchas.md` are **append-only** — never rewrite, reorder, or deduplicate existing entries
- `lessons-raw/` is gitignored course IP. Per-lesson notes (`key-takeaways.md`, `my-questions.md`, `links.md`) summarize and digest from it but **never paraphrase verbatim** or commit large excerpts. The `/10x-course-distill` skill does NOT read `lessons-raw/` at all — it works only on user-authored `key-takeaways.md`. Layout: `lessons-raw/Week N/mNlN-<slug>.md`
- `scratch/` is ephemeral — feel free to create/delete files there

## Skills

- `/10x-course-distill` — run **on-demand** (typically end-of-week or end-of-module) to extract cross-lesson tips/gotchas from `key-takeaways.md` files. Zero entries per week is a valid outcome.

## Note Format

### key-takeaways.md
Max 5 bullets. Each bullet is **either** an imperative ("rób X przed Y") **or** a non-obvious rule worth remembering ("zasada Z, bo W"). No restating mechanics that are obvious from the skill name. What to remember in 6 months.

### my-questions.md
Questions to bring to Tuesday Q&A. Delete answered ones after the session.

### links.md
≤8–10 links, grouped: **Tools** (CLIs, registries) / **Reference** (docs, papers) / **Prework** (course preworks). Trim aggressively — no exhaustive catalogs (e.g. don't enumerate every model on a pricing page; one link to the index suffices).

### weekN-overview.md
One file per week. For each lesson: title, introduced skills (each with ≤1-line role), main idea (1–2 sentences). Fast-scan reference, not a substitute for reading `lessons-raw/`.
