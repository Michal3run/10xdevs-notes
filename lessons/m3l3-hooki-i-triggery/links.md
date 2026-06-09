# m3l3 — Linki

## Tools

- [Claude Code Hooks](https://docs.anthropic.com/en/docs/claude-code/hooks) — zdarzenia, handlery, matchery, exit codes, konfiguracja na trzech poziomach (user/project/local).
- [Cursor Hooks](https://docs.cursor.com/configuration/hooks) — `afterFileEdit`, `failClosed`; format `.cursor/hooks.json`.
- [Codex Hooks](https://developers.openai.com/codex/hooks) — `config.toml` vs `hooks.json`, hash-based trust model (komenda `/hooks` do zatwierdzenia).
- [VS Code Copilot Hooks](https://code.visualstudio.com/docs/copilot/customization/hooks) — `chat.hookFilesLocations`, kompatybilność z Claude (matchery ignorowane, camelCase).
- [Vitest CLI](https://vitest.dev/guide/cli.html) — subkomenda `related`, flaga `--changed`, `--run`. Vitest 4.1 + `AI_AGENT=1` dla kompaktowego outputu.
- [Lefthook](https://github.com/evilmartians/lefthook) — agnostyczny stackowo; `{staged_files}`, równoległe komendy, brak zależności od Node.
- [pre-commit framework](https://pre-commit.com/) — standard ekosystemu Pythona z gotowym katalogiem hooków (`ruff`, `black`, `mypy`).

## Reference

- [Git Hooks (oficjalna dokumentacja)](https://git-scm.com/docs/githooks) — `pre-commit`, `pre-push` itd. — fundament, na którym opakowują się Husky/Lefthook/pre-commit.
- [1Password agent-hooks](https://github.com/1Password/agent-hooks) — jeden skrypt instaluje te same hooki do `.cursor/`, `.claude/`, `.windsurf/` — praktyczny dowód konwergencji architektury.

## Prework

- [Prework 2.4 — Agent-Native IDE](https://platforma.przeprogramowani.pl/external/10xdevs-3-prework/pl/07) — dyscyplina bezpieczeństwa, którą hooki automatyzują.
