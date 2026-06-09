# Week 2 Overview — M2: 10xDevs Workflow

> Roadmapa → change-id → plan → review → implementacja → multi-agent. Łańcuch artefaktów: `roadmap.md` → `context/changes/<change-id>/{change.md, plan.md, plan-brief.md, research.md}` → `## Progress`. Programista wchodzi w buty Technical Project Managera; agent dostaje nie „zbuduj MVP", tylko „to jest faza N slice'a S-XX, kontrakt jest tu".

---

## m2l1 — Roadmapa MVP: milestony, zależności i priorytety
**Skille wprowadzone:**
- `/10x-roadmap` — czyta `prd.md`, audytuje repo (6 warstw), prowadzi minimalny wywiad (`main_goal` / `north_star` / `top_blocker`) → `context/foundation/roadmap.md` z foundations (`F-NN`) i vertical slices (`S-NN`)
- Linear MCP / GitHub CLI — agent z dostępem read/create/update na backlog zewnętrzny

**Main idea:** Vertical-first jako domyślna strategia w epoce agentów: weryfikowalność i ujawnianie konfliktów integracji od pierwszego milestone'a. Każdy `F-NN` musi mieć `Unlocks: S-NN` — fundament bez wskazanego docelowego slice'a to horizontal drift przebrany za fundament. North star nie zawsze jest pierwszym slice'em w kolejce; to moment, w którym teza produktu domyka się end-to-end.

---

## m2l2 — Od roadmapy do kodu: plan, review, implementacja
**Skille wprowadzone:**
- `/10x-new <change-id>` — tworzy folder `context/changes/<change-id>/` i `change.md`
- `/10x-plan <change-id>` — generuje `plan.md` (end state, phases, Intent + Contract per file, Success Criteria, Risks, `## Progress`) plus `plan-brief.md` jako kontrakt decyzji
- `/10x-plan-review <change-id>` — bramka kontroli planu przed kodem (czy fazy wykonalne, czy success criteria sprawdzają zachowanie, czy `## Progress` ma format dla `/10x-implement`)
- `/10x-implement <change-id> phase N` — wykonuje jedną fazę z planu, weryfikuje, robi commit, aktualizuje `## Progress`

**Main idea:** Plan w pliku przesuwa kontrolę wcześniej (shift-left). Plan Mode w UI ginie z sesją; `plan.md` przeżyje session reset, hand-off i powrót po dwóch tygodniach. Architekt/koder split (np. `opusplan`) jest modelem mentalnym, nie obowiązkową konfiguracją. HALT w fazie: jeśli agent odkrywa fakt zmieniający kontrakt planu, wracaj do `plan.md`, nie dokręcaj kolejnym promptem.

---

## m2l3 — Solo Code Review: weryfikuj kod AI szybko i skutecznie
**Skille wprowadzone:**
- `/10x-impl-review` — scorecard 6 wymiarów (Plan Adherence, Scope Discipline, Safety & Quality, Architecture, Pattern Consistency, Success Criteria); zapisuje raport, do którego wracasz przez `/10x-impl-review @path`
- `/10x-lesson` — z review do `context/foundation/lessons.md` przy powtarzalnym wzorcu, który zmieniłby wcześniejsze decyzje

**Main idea:** Triage findingu = decyzja per pozycja: fix now / fix differently / skip / record as lesson. Scorecard działa jak filtr uwagi — najpierw odchylenia od planu i zakresu, dopiero potem drobiazgi. Kolejność czytania diffu: zakres → granice ryzyka (auth, dane, sekrety, migracje) → lokalne wzorce → testy. Zielony test od agenta nie jest dowodem; sprawdzaj, czy asercja pyta o zachowanie wymagane przez PRD/kontrakt, czy odbija to, co właśnie wygenerował.

---

## m2l4 — Research i implementacja: trudniejszy stream z AI
**Skille wprowadzone:**
- `/10x-research <change-id> <query>` — równoległe subagenty (Explore + general-purpose) → `context/changes/<change-id>/research.md` z referencjami `file:line` (jedyny plik, który skill ma prawo zapisać)
- `/10x-frame <change-id>` — koło ratunkowe: rozdziela observation / cause / fix w Frame Brief, gdy mimo prób kontynuacji rozmowy poprawki nic nie zmieniają
- Exa.ai MCP — agentic search (najwyższa ocena Technical Documentation w benchmarku AIMultiple 05/2026)
- Context7 MCP — live library docs (`resolve-library-id` → `query-docs`) wstrzykuje aktualne API zamiast pamięci treningowej

**Main idea:** Trudniejszy slice (10xCards: SRS, czyli kontrakt domenowy z biblioteką, nie kolejny CRUD) wymaga researchu, zanim ruszy plan: external (Exa wybiera, Context7 pobiera) plus internal (`/10x-research` mapuje stan repo). Context drift to przewidywalna własność systemu — dwa źródła: brak przygotowania (zgaduje) i przeciąganie rozmowy (Context Rot, lost-in-the-middle). Reakcja: świeża sesja + wczytaj `plan.md` i `## Progress`, nie „popraw to jeszcze raz".

---

## m2l5 — Innovate: więcej ficzerów, mniej czekania z wieloma agentami
**Skille wprowadzone:**
- `git worktree add ../<dir> -b feature/<branch>` — izolacja katalogu, brancha, sesji agenta i kontekstu zadania per slice
- `/goal "..."` (Claude Code, Codex) — delegowana implementacja z warunkiem zakończenia; mały model-ewaluator po każdej turze decyduje stop/kontynuuj

**Main idea:** Zacznij od dwóch niezależnych slice'ów, nie pięciu agentów. Worktree izoluje stan gita i pliki robocze, ale **nie izoluje całego środowiska** (port dev-servera, lokalna baza, sandbox płatności). Wzorzec orkiestracji (izoluj kontekst → deleguj cel → recenzuj wynik) jest niezmienny — konkretne narzędzia (Cursor Agents, Antigravity, Superset, Conductor) rotują co kwartał. „Nie AI robi wszystko naraz, raczej prowadzę kilka odizolowanych cykli i nie przekraczam własnej przepustowości decyzyjnej."
