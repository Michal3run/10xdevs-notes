# m3l4 — Linki

## Tools

- [Playwright CLI](https://playwright.dev/agent-cli/introduction) — komendy, snapshoty YAML z element refs, integracja ze skills.
- [Playwright MCP](https://github.com/microsoft/playwright-mcp) — tryby (`snapshot` domyślny / `--caps=vision` / `--caps=network`), capabilities, konfiguracja.
- [Playwright Test Agents](https://playwright.dev/docs/test-agents) — Planner / Generator / Healer; oficjalna dokumentacja workflow.
- [Playwright Authentication](https://playwright.dev/docs/auth) — `storageState`, global setup, multi-role testing — fundament dla "logujesz się raz".

## Reference

- [Playwright Best Practices](https://playwright.dev/docs/best-practices) — selektory, izolacja testów, auto-waiting, web-first assertions.
- [How I Used AI to Fix Our E2E Test Architecture (Debbie O'Brien, Microsoft/Playwright)](https://dev.to/debs_obrien/how-i-used-ai-to-fix-our-e2e-test-architecture-444a) — rules-file approach dla AI + E2E, źródło wzorca seed test + reguły.
- [Why You Shouldn't Use waitForTimeout (BrowserStack)](https://www.browserstack.com/guide/playwright-waitfortimeout) — before/after dla zamiany hardcoded waits na `waitForResponse`/`toBeVisible`.
- [How to Write E2E Tests for Full Parallelization (QA Wolf)](https://www.qawolf.com/blog/how-to-write-tests-for-full-parallelization) — unique identifiers + cleanup patterns; tło dla `Date.now()` w nazwach.
- [browserbase/stagehand](https://github.com/browserbase/stagehand) — alternatywa: hybryda kodu i języka naturalnego (`act`/`extract`/`agent`), CDP zamiast Playwrighta. Warto znać przy scrapingu.

## Prework

- [Prework 3.1 — LLMy i ich wpływ na codzienną pracę programisty](https://platforma.przeprogramowani.pl/external/10xdevs-3-prework/pl/09) — budżety tokenów i degradacja kontekstu; tu zastosowane do decyzji CLI vs MCP.
