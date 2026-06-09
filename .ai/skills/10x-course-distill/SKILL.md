---
name: 10x-course-distill
description: Extract cross-lesson tips and gotchas from lesson notes into the global append-only registers. Run on-demand (typically end-of-week or end-of-module), not per-lesson.
---

# /10x-course-distill — Extract Tips & Gotchas from Lesson Notes

Read `key-takeaways.md` from one or more lessons, extract candidate entries for `tips.md` (positive patterns) and `gotchas.md` (failure modes), and append confirmed entries with backlinks.

## When to run

This skill is **on-demand**, not per-lesson. In a light-theory course (10xDevs), most lessons don't yield distillation candidates — that's expected. Recommended cadences:

- After a week's 5 lessons are complete — scan for cross-lesson patterns
- After a module ends (e.g. all of M2) — scan for module-level patterns
- When you personally feel a tip/gotcha worth recording emerged in a single lesson

If you find no good candidates, the right answer is "Skip all" — the skill working correctly. **Zero entries from a week is a fine outcome.**

## Initial Response

When this skill is invoked:

1. **If a lesson folder was specified** (e.g. `/10x-course-distill m2l3-solo-code-review`), read just that folder.
2. **If a week was specified** (e.g. `/10x-course-distill week2`), read all `lessons/m2l*/` folders.
3. **If nothing was specified**, find the most recently modified folder under `lessons/` and use that.
4. Respond with:

```
I'll extract tips and gotchas from <folder(s)>.

Reading:
- lessons/<folder>/key-takeaways.md

I'll propose candidate entries one at a time. For each you can Accept, Edit, or Skip.
Zero candidates is a valid outcome.
```

Then proceed to Step 1.

## Process

### Step 1: Read lesson notes

Read `lessons/<folder>/key-takeaways.md` for each target folder. If the file is missing, note it and stop with "Write key-takeaways first." If running on a week, skip folders missing key-takeaways and continue with the rest.

Do NOT read `lessons-raw/` — that content is course IP and may not be paraphrased into the append-only registers.

### Step 2: Extract candidates

From the lesson content, identify:
- **Tips** — positive patterns, "do X", "always Y", reusable techniques
- **Gotchas** — failure modes, "watch out for X", "don't W", common mistakes

Aim for 0–3 candidates **per lesson**. Quality over quantity — most lessons should yield zero. Skip anything too lesson-specific or obvious from the skill name alone.

### Step 3: Present candidates one at a time

For each candidate, show:

```markdown
## <Imperative title>
- **What**: <one-sentence rule or warning>
- **Why**: <reason, ideally with a concrete failure shape>
- **Source**: [<lesson-folder>](./lessons/<lesson-folder>/key-takeaways.md)
- **Added**: <today's date YYYY-MM-DD>
```

And the target file (tips.md or gotchas.md).

Ask:
- **Accept** — append as shown
- **Edit** — let me revise before saving
- **Skip** — discard this candidate

One candidate at a time. Do not batch.

### Step 4: Append confirmed entries

For each accepted entry, append it to the target file (`tips.md` or `gotchas.md`).

**Self-bootstrap**: if the target file doesn't exist, create it with the canonical header:

For tips.md:
```
# Tips

> Append-only register of positive patterns surfaced across lessons. Updated by /10x-course-distill.

```

For gotchas.md:
```
# Gotchas

> Append-only register of failure modes and pitfalls surfaced across lessons. Updated by /10x-course-distill.

```

Append after the last line. Never reorder, reword, or deduplicate existing entries.

### Step 5: Summary

After all candidates are processed, print:
```
Done. Added X tip(s) and Y gotcha(es) from <lesson-folder(s)>.
```

If `X + Y == 0`, print:
```
Done. No new entries from <lesson-folder(s)> — that's a fine outcome.
```

## Notes

- **Append-only.** Never edit existing entries through this skill.
- **One entry at a time.** Each candidate gets its own confirm prompt.
- **Backlinks required.** Every entry must have a Source linking to its lesson folder.
- **No duplicate detection.** If the user thinks an existing entry covers it, they Skip. Don't auto-deduplicate.
- **Scope is course-wide.** This skill lives in the notes repo. It does NOT touch the MVP repo's `context/foundation/lessons.md` (that's `/10x-lesson`'s job).
- **Don't read `lessons-raw/`.** That folder is gitignored course IP. The skill operates only on user-authored `key-takeaways.md`.
- **Zero candidates is a valid outcome.** Don't pad with weak entries to feel productive.
