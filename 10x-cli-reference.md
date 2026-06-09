# 10x-cli Reference

> Tooling reference for the 10x-cli. Load when troubleshooting or setting up — not needed every session.

**Repo**: https://github.com/przeprogramowani/10x-cli  
**Requires**: Node 20+

## Install

```bash
# Zero-install (recommended for first use)
npx @przeprogramowani/10x-cli auth

# Or install globally
npm install -g @przeprogramowani/10x-cli
```

## Commands

| Command | Description |
|---------|-------------|
| `10x auth` | Magic-link login with Circle email |
| `10x list` | Browse available modules/lessons |
| `10x get <ref>` | Fetch & apply lesson artifacts |
| `10x doctor` | Diagnose auth + connectivity |

## `10x get` Flags

| Flag | Description |
|------|-------------|
| `--tool generic` | Our default — writes to `.ai/` + `AGENTS.md` |
| `--type skills` | Only fetch skills (skip prompts, rules, configs) |
| `--name <name>` | Single artifact (requires --type) |
| `--dry-run` | Preview without writing |
| `--print` | Output to stdout (pipe-friendly) |

## Lesson References

`m1l1` = Module 1 Lesson 1, `m2l3` = Module 2 Lesson 3.

## Multi-Tool Output Mapping

| Tool | Directory | Rules file |
|------|-----------|-----------|
| Generic (ours) | `.ai/` | `AGENTS.md` |
| Claude Code | `.claude/` | `CLAUDE.md` |
| Cursor | `.cursor/` | `.cursor/rules/10x-course.mdc` |
| Codex CLI | `.agents/` | `AGENTS.md` |

Config saved to `~/.config/10x-cli/config.json`.

## PATH Setup (Windows)

If `10x` is not recognized after global install, add to user PATH:
- `C:\Program Files\nodejs`
- `%APPDATA%\npm`

Then restart the terminal.

## Offline Fallback

Artifacts for M1 available at: `C:\src\10xDevs\Downloads\10xdevs3-artifacts-m1\generic\`
