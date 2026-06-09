# m2l4 — Linki

## Tools

- [Exa.ai](https://exa.ai/) — AI-native search, najwyższa ocena Technical Documentation w benchmarku AIMultiple 05/2026; free tier 1000 zapytań/mc. MCP endpoint do wpięcia w Claude Code/Codex.
- [Context7](https://context7.com/) — live library docs jako MCP/CLI/skille. `resolve-library-id` → `query-docs` z budżetem tokenów; free 1000 wywołań/mc.
- [ts-fsrs (Open Spaced Repetition)](https://github.com/open-spaced-repetition/ts-fsrs) — TS implementacja FSRS użyta w lekcji jako kandydat dla SRS w 10xCards.

## Reference

- [Context Rot (Chroma Research, 2025)](https://research.trychroma.com/context-rot) — badanie na 18 modelach (GPT-4.1, Claude Opus 4, Gemini 2.5): jakość spada z długością wejścia, **zanim** okno się zapełni. Fundament dla "świeża sesja zamiast 'popraw to jeszcze raz'".
- [Effective context engineering for AI agents (Anthropic, 2025)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — write/select/compress/isolate jako odpowiedź na context rot; uzasadnienie dla `research.md` zamiast długiej rozmowy.
- [Agentic search benchmark (AIMultiple 05/2026)](https://aimultiple.com/agentic-search) — 8 graczy (Brave/Firecrawl/Exa/Tavily/Perplexity/Parallel/SerpAPI) na 100 pytaniach z LLM-as-a-judge; czwórka liderów statystycznie nie do odróżnienia, ale per-kategoria różnice są realne.
- [llms.txt proposal (Howard, 2024)](https://llmstxt.org/) — krótki indeks dla agentów w roocie domeny; sygnał, że projekt świadomie pracuje z agentami.
- [Anki FAQ — spaced repetition algorithm](https://faqs.ankiweb.net/what-spaced-repetition-algorithm) — tło SM-2 vs FSRS, opcjonalne przy decyzji ratingu (4 vs 6 stopni) i kształtu `ReviewState`.

## Prework

- [Prework 3.3 — Cykl życia wątku i zarządzanie kontekstem](https://platforma.przeprogramowani.pl/external/10xdevs-3-prework/pl/11) — write/select/compress/isolate w wersji preworkowej; teoretyczne tło dla całej lekcji.
- [Prework 1.2 — Chatbot vs Agent vs Harness](https://platforma.przeprogramowani.pl/external/10xdevs-3-prework/pl/02) — `WebFetch`/`WebSearch` jako tool use w harnessie (nie chatbot).
