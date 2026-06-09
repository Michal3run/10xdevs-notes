# Week 3 Overview — M3: AI Development Quality & Maintenance

> Test plan → unit/integration → hooki → E2E → debugowanie. Łańcuch: `context/foundation/test-plan.md` (mapa ryzyk + cookbook) → `/10x-research` + `/10x-plan` + `/10x-implement` lub `/10x-tdd` → hooki per-edit/pre-commit → `/10x-e2e` → reaktywne dochodzenie z monitoringu. Proaktywny pipeline łapie znane ryzyka, monitoring + diagnostyka domykają lukę po tym, co przeoczył.

---

## m3l1 — Plan testów z AI: quality gates, test-plan i priorytety
**Skille wprowadzone:**
- `/10x-test-plan` — tworzy i pielęgnuje `context/foundation/test-plan.md` (mapa ryzyk impact × likelihood, fazy rollout'u, cookbook §6, quality gates); flagi `--status` i `--refresh`

**Main idea:** Mapa ryzyk poprzedza testy. „Write tests for this file" → agent idzie po linii najmniejszego oporu (helpery, gettery), coverage rośnie, krytyczny flow goły. Test plan to **sygnał, nie diagnoza** — wskazuje obszar wysokiego churnu lub krytycznego flow z PRD; konkrety w kodzie należą do `/10x-research` w fazie rollout'u. Bezpieczeństwo (IDOR, walidacja, sekrety, rate-limit) dorzuć ręcznie — agent rzadko zaproponuje sam, bo „happy path" nie obejmuje atakującego.

---

## m3l2 — Od planu do testów: implementacja unitów z agentem
**Skille wprowadzone:**
- `/10x-tdd <change-id> phase N` — opcjonalna alternatywa dla `/10x-implement`: cykl RED → GREEN → REFACTOR; mieszać z `/10x-implement` w jednym `plan.md` (wspólny `## Progress`)
- Stryker (mutation testing) — `npx stryker run` z `--mutate "src/srs.ts:1-40"`; mutation score = (killed + timeout) / (killed + timeout + survived + no-coverage)

**Main idea:** Vibe Testing („Write tests for the auth module") = trzy antywzorce: mirror implementacji, happy path, brak edge case'ów. Wyrocznia musi pochodzić **spoza testowanego kodu** (z PRD, kontraktu, specyfikacji). Coverage słabo koreluje z wykrywaniem błędów; agent rzadko zostawia kod **niepokryty**, częściej **pokryty, ale nieobroniony asercją**. Stryker pokazuje tę różnicę liczbą i konkretnym żywym mutantem — ale nie goń mutation score'u do 100%, bo zaczniesz pisać kruche mirrory. `/10x-tdd` zatrzymuje agenta na asercji zanim ten zacznie produkować implementację.

---

## m3l3 — Hooki i triggery: agent, który sam reaguje na błędy
**Skille wprowadzone:**
- Hooki narzędzia AI (np. PostToolUse w Claude Code, `afterFileEdit` w Cursorze, `[hooks]` w Codex `config.toml`) — cykl `Trigger → Matcher → Handler → Sygnał (exit code)`; reguła `CLAUDE-m3l3` doklejana do `CLAUDE.md`
- Pre-commit przez Lefthook / lint-staged (Husky) / pre-commit framework — bramka na staged files niezależna od agenta

**Main idea:** Trzy warstwy lokalnej jakości plus CI: per-edit (sekundy, agent widzi feedback), pre-commit (na staged files), pre-push (cięższe sprawdzenia), CI (integracje, środowiska). Heurystyka warstwy: jeśli check trwa >kilka sekund, zejdź wyżej. Hooki to warstwa **deterministyczna** — przeżyją kompresję kontekstu i „zapomnienie" przez model, w przeciwieństwie do reguł w `CLAUDE.md`. Wzorzec trigger→match→check→signal przenosi się między narzędziami; różnice (Codex hash trust, Copilot camelCase, brak context injection w Windsurfie) to detale implementacyjne.

---

## m3l4 — Testy E2E: Playwright, MCP i multimodalne scenariusze
**Skille wprowadzone:**
- `/10x-e2e <change-id> phase N` — pętla PLAN → GENERATE → REVIEW → VERIFY z bramką kwalifikacji fazy; współdzieli `## Progress` z `/10x-implement` i `/10x-tdd`. Reguła `CLAUDE-m3l4` doklejana do `CLAUDE.md`
- Playwright CLI (`@playwright/cli`) — drzewo dostępności jako YAML z element refs, snapshoty na dysku, ~27K tokenów na scenariusz vs ~114K przez MCP
- Playwright Test Agents (od v1.56) — Planner / Generator / Healer
- Playwright MCP `--caps=vision` — tryb wizyjny dla weryfikacji wąskich asercji UI (z-index, overlap, animacja)
- `storageState` (`playwright/.auth/user.json`) — login raz, wstrzykiwany do każdej sesji testowej

**Main idea:** Co pokażesz w `seed.spec.ts`, to dostaniesz w generowanych testach — Generator powiela wzorce. Pięć antywzorców E2E od agenta: naiwna asercja, kruchy selektor, współdzielony stan, `waitForTimeout`, brak cleanup. VERIFY to nie zielony — odwróć w kodzie produkcyjnym chronione zachowanie i potwierdź, że test pada (cofnij, nie commituj). Bramka kwalifikacji E2E: ryzyko musi przechodzić przez wiele granic systemu lub istnieć tylko w wyrenderowanym UI; jeśli unit/integracja by wystarczyła — wracaj do `/10x-tdd`. Healer pomaga przy zmianie selektora, **szkodzi przy zmianie logiki biznesowej** (maskuje buga dopasowaniem asercji).

---

## m3l5 — Debugowanie z AI: od stack trace do gotowego fixa
**Skille wprowadzone:**
- Sentry MCP (`@sentry/mcp-server`) — `search_issues` + `get_sentry_resource` (URL mode / Explicit mode); `captureConsoleIntegration` przekazuje `console.warn`/`error` do issues
- `wrangler pages deployment tail` (Cloudflare) lub odpowiednik (`flyctl logs` / `vercel logs` / `aws logs tail`) — runtime logs jako sygnał skali
- Playwright CLI/MCP jako narzędzia diagnostyczne — `browser_console_messages`, `browser_network_requests`, `browser_network_request` (core, bez `--caps`)
- Test-driven bugfixing — prowadzony przez `/10x-tdd` (unit/integration) lub `/10x-e2e` (UI bug)
- VLM (vision model) z otwartym pytaniem diagnostycznym dla bugów wyłącznie wizualnych — kategorie: frontier / Gemini Flash / Qwen-VL

**Main idea:** Diagnostyka to synteza z **wielu źródeł**: monitoring → lokalizacja, logi → skala, reprodukcja → klient/serwer odgraniczone, kod → root cause. Połknięty błąd (swallowed error, OWASP A10:2025) to klasa, której proaktywny pipeline nie widzi: API zwraca 200 z wartością policzoną w pamięci, trwały zapis padł po cichu. Test reprodukujący buga **przed fixem** sprawdza zapisany stan w bazie, nie odpowiedź API. Weryfikacja fixa to lustrzane odbicie dochodzenia — każde źródło, które pokazało problem, musi pokazać brak. „Tests can't catch what they don't know to look for" (Charity Majors) — diagnostyka jest siatką bezpieczeństwa pod proaktywnymi testami, nie ich konkurencją.
