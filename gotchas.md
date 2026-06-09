# Gotchas

> Append-only register of failure modes and pitfalls surfaced across lessons. Updated by /10x-course-distill.



## `Read` deny w `.claude/settings.json` nie zatrzyma `cat` w bashu
- **What**: Polityka uprawnień Claude Code działa per-tool po nazwie i argumentach (`Read(./.env)`, `Bash(rm -rf *)`), nie po efekcie na dysku — wbudowane narzędzia i komendy bashowe to dwie różne ścieżki egzekucji.
- **Why**: `Read(./.env)` w `deny` zablokuje agentowi odczyt przez tool `Read`, ale ten sam agent w `Bash` wywoła `cat .env` i przejdzie. Dodatkowo polityka jest probabilistyczna — udokumentowane są obejścia (np. dostęp do `npx` przez `/proc/self/root/usr/bin/npx`). Traktuj `.claude/settings.json` jak próg na podłodze, nie zamek w drzwiach.
- **Source**: [m1l3-ai-powered-bootstrap](./lessons/m1l3-ai-powered-bootstrap/summary.md)
- **Added**: 2026-06-05

## Konsumenckie tiery LLM domyślnie trenują na twoim inpucie
- **What**: Free/Plus/Pro Anthropic, OpenAI i Gemini domyślnie używają twoich rozmów do trenowania modelu. Wyłącz to **przed** pierwszą sesją z kodem firmowym (Anthropic: pop-up; OpenAI: toggle "Improve the model"; Gemini: `myactivity.google.com` → wyłącz "Keep Activity"). Plany API i biznesowe (Team/Enterprise) — domyślnie nie trenują.
- **Why**: "Wyłączę później" znaczy, że pierwszy commit z firmowymi sekretami albo IP klienta już poszedł do treningu. Gemini Advanced jako subskrypcja **nie zmienia** polityki treningu — toggle żyje pod kontem Google'a. Chińscy dostawcy (DeepSeek, Alibaba/Qwen) działają w jurysdykcji bez prawa do odmowy udostępnienia danych państwu — niezależnie od ustawień.
- **Source**: [m1l3-ai-powered-bootstrap](./lessons/m1l3-ai-powered-bootstrap/summary.md)
- **Added**: 2026-06-05

## Context drift to przewidywalna własność systemu, nie zły dzień modelu
- **What**: Po kilkunastu wymianach w sesji agent zaczyna mieszać nazwy z różnych slice'ów, „pamiętać" decyzje, których nie podjąłeś, i pisać kod pod model danych z dwóch tematów wcześniej. To nie chwilowy spadek formy — to architektura transformerów.
- **Why**: Chroma "Context Rot" (2025) na 18 modelach (GPT-4.1, Claude Opus 4, Gemini 2.5) — jakość spada z długością wejścia, **zanim** okno się zapełni. Środek kontekstu dostaje statystycznie mniej uwagi (lost-in-the-middle), semantycznie podobne fragmenty mylą model jak dystraktory. Reakcja: **NIE** „popraw to jeszcze raz" — otwórz świeżą sesję, wczytaj `plan.md` + `## Progress` i kontynuuj fazę z czystego kontekstu. Większe okno problemu nie rozwiąże, bo to własność architektury, nie luka w treningu.
- **Source**: [m2l4-research-i-implementacja](./lessons/m2l4-research-i-implementacja/key-takeaways.md)
- **Added**: 2026-06-09

## "Write tests for this file" — agent idzie po linii najmniejszego oporu
- **What**: Naiwny prompt o testy bez ryzyka kieruje agenta do najłatwiejszych celów: helpery, gettery, formatery, funkcje utility. Coverage rośnie, CI świeci na zielono, krytyczny flow użytkownika nadal goły.
- **Why**: Punkt wejścia musi być **scenariusz biznesowy + impact × likelihood** (M3L1 mapa ryzyk), nie plik. Bez tego dostajesz „testy dla testów" — kilkadziesiąt zielonych, które nie chronią niczego ważnego. Test plan zaczyna od ryzyk, dopiero `/10x-research` mapuje, gdzie ryzyko realnie żyje w kodzie. „Write tests for the auth module" generuje asercje typu „authenticate zwraca to, co zwraca authenticate" — pozornie test, realnie nic.
- **Source**: [m3l1-plan-testow](./lessons/m3l1-plan-testow/key-takeaways.md), [m3l2-implementacja-unitow](./lessons/m3l2-implementacja-unitow/key-takeaways.md)
- **Added**: 2026-06-09

## Połknięty błąd (swallowed error) niewidoczny dla pipeline'u testów i hooków
- **What**: Try/catch łapie wyjątek, loguje warning i zwraca 200 OK z wartością policzoną w pamięci. API zgłasza sukces, trwały zapis padł po cichu. OWASP Top 10 2025 dodał tę klasę jako A10: Mishandling of Exceptional Conditions.
- **Why**: Proaktywny pipeline jakości tego nie złapie. Testy unit/integration sprawdzają trasę, którą tam wpisano — nie wszystkie. Hooki sprawdzają kod źródłowy, a TypeScript jest poprawny. E2E sprawdzają happy path, a API kłamie 200. Sygnał istnieje wyłącznie w monitoringu — i tylko jeśli włączyłeś `captureConsoleIntegration({ levels: ['warn', 'error'] })` w Sentry SDK od początku. Bez tego cichy `console.warn` z handlera nigdzie nie trafia. Reaktywne dochodzenie (M3L5: Sentry → logi → reprodukcja → kod) to nie „dodatkowe narzędzie", tylko siatka bezpieczeństwa pod proaktywnymi testami.
- **Source**: [m3l5-debugowanie](./lessons/m3l5-debugowanie/key-takeaways.md)
- **Added**: 2026-06-09
