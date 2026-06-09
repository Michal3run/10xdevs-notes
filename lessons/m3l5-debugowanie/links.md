# m3l5 — Linki

## Tools

- [Sentry MCP Server](https://github.com/getsentry/sentry-mcp) — `search_issues` + `get_sentry_resource` (URL mode / Explicit mode); pre-1.0, sprawdź repo przed użyciem.
- [Sentry Astro + Cloudflare SDK Guide](https://docs.sentry.io/platforms/javascript/guides/cloudflare/frameworks/astro/) — `@sentry/astro` + `@sentry/cloudflare`, `captureConsoleIntegration`, custom entry point dla Astro 6.
- [Wrangler tail](https://developers.cloudflare.com/workers/wrangler/commands/#deployment-tail) — flagi, format JSON, ograniczenia (10 klientów, brak HTTP status w outpucie, zatrzymuje się przy >100 req/s przez 5 minut).
- [Playwright MCP — diagnostic tools](https://github.com/microsoft/playwright-mcp) — `browser_console_messages`, `browser_network_requests`, `browser_network_request` jako core (bez `--caps`).

## Reference

- [OWASP A10:2025 — Mishandling of Exceptional Conditions](https://owasp.org/Top10/2025/A10_2025-Mishandling_of_Exceptional_Conditions/) — klasyfikacja swallowed errors w OWASP Top 10.
- [Charity Majors — "I Test in Production" (InfoQ 2018)](https://www.infoq.com/presentations/testing-production-2018/) — komplementarność testowania i monitoringu: "tests can't catch what they don't know to look for".
- [Test-Driven Bugfixing](https://evolveum.com/test-driven-bugfixing/) — opis techniki w praktyce TDD; padający test reprodukujący buga przed fixem.
- [VLM Visual Testing (Zak El Fassi)](https://zakelfassi.com/vlm-visual-testing-chrome-extension) — praktyczny test z lokalnym modelem: koszt, ograniczenia (spatial bias, halucynacje), DSL do asercji.

## Prework

- [Prework 2.3 — Claude Code, podstawy operacyjne](https://platforma.przeprogramowani.pl/external/10xdevs-3-prework/pl/06) — MCP servers jako narzędzia agenta; tu zastosowane do zbierania danych diagnostycznych.
- [Prework 3.2 — Wzorce i antywzorce promptowania](https://platforma.przeprogramowani.pl/external/10xdevs-3-prework/pl/10) — structured input jako kontrakt; tu zastosowane do parsowania ticketa.
