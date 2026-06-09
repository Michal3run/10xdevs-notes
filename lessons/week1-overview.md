# Week 1 Overview — M1: Agentic Environment

> Pomysł → PRD → Stack → Bootstrap → Onboarding → Deploy. Łańcuch artefaktów: `prd.md` → `tech-stack.md` → repo + scaffold + audit → `AGENTS.md` → `infrastructure.md`. Każdy plik to kontrakt dla następnego skilla.

---

## m1l1 — Od pomysłu do PRD: metoda sokratejska z agentem
**Skille wprowadzone:**
- `/10x-shape` — sesja sokratejska, wynik `context/foundation/shape-notes.md`
- `/10x-prd` — generuje `context/foundation/prd.md` o stałej strukturze ze `shape-notes.md`

**Main idea:** Agent jako facylitator wymusza decyzje, zanim cokolwiek trafi do repo. PRD to kontrakt, na który będą się powoływać wszystkie kolejne skille — bez niego prompty dryfują. Tryb auto-detekcji greenfield/brownfield (markery typu `package.json`, `Cargo.toml`).

---

## m1l2 — Od chatbota do agenta: tech stack, skille i metaprompting
**Skille wprowadzone:**
- `/10x-tech-stack-selector` — czyta `prd.md` + rejestr starterów → `tech-stack.md` (greenfield)
- `/10x-stack-assess` — ocenia istniejący stack przez 4 bramki agent-friendliness (brownfield)

**Main idea:** Agent Skill = folder z `SKILL.md` + opcjonalne `references/`/`scripts/`/`assets/`, ładowany progresywnie (~100 tok metadane → ~5k instrukcje → resources na żądanie). Tabela 53/79/100% Vercela: ważne skille wywołuj jawnie po nazwie — auto-aktywacja jest probabilistyczna.

---

## m1l3 — AI-Powered Bootstrap: boilerplate i bezpieczna praca z agentem
**Skille wprowadzone:**
- `/10x-bootstrapper` — scaffolds projekt z `tech-stack.md`, deleguje do oficjalnego CLI (greenfield)
- `/10x-health-check` — read-only audyt istniejącego repo z werdyktem `healthy/needs-attention/critical-issues` (brownfield)

**Main idea:** Bezpieczeństwo zaczyna się przed pierwszym promptem: deleguj do oficjalnych CLI (nie pamięci modelu), ustaw startowe `.claude/settings.json` (allow/ask/deny), wyłącz trening na konsumenckich tierach. Polityka uprawnień to próg, nie zamek — defense in depth.

---

## m1l4 — Agent Onboarding: reguły dla AI
**Skille wprowadzone:**
- `/10x-agents-md` — alternatywa dla `/init`, generuje `AGENTS.md`/`CLAUDE.md` z analizy repo
- `/10x-rule-review` — werdykt OK/WARN/FAIL po 5 wymiarach (długość, kopie, precyzja, redundancja, kolejność)
- `/10x-lesson` — append do `context/foundation/lessons.md` przy powtarzalnym błędzie agenta

**Main idea:** Reguły dla agenta, który zna TypeScript, ale nie wasze konwencje. Test inkluzji: jeśli agent wiedziałby to bez tego pliku, usuwaj. ≤200 linii, ważne na górze (u-shaped attention — środek pliku jest słabiej egzekwowany). Reguły obszarowe bliżej kodu, nie do monolitu.

---

## m1l5 — Od localhosta na produkcję: deployment z agentem
**Skille wprowadzone:**
- `/10x-infra-research` — wywiad → web research → scored comparison → `context/foundation/infrastructure.md`
- Plan Mode (Claude Code, `Shift+Tab`) — read-only research, plan tekstowy, wykonanie dopiero po akceptacji

**Main idea:** Wybór platformy to decyzja na czas projektu, nie kosmetyka przed deployem. Anti-bias trójka (devil's advocate / pre-mortem / unknown unknowns) chroni przed sycophancy modelu. Dla MVP CLI > MCP; nieodwracalne operacje przez Plan Mode lub manual click. Token API zawężony do minimum, w env nie w repo.
