# Tips

> Append-only register of positive patterns surfaced across lessons. Updated by /10x-course-distill.



## Deleguj do autorytatywnego CLI, gdy istnieje
- **What**: Zamiast pozwalać agentowi rekonstruować boilerplate z pamięci modelu, każ mu zawołać oficjalny CLI (`npm create`, `docker init`, `prisma migrate dev`, `ng generate`, `cargo new`).
- **Why**: Dane treningowe mieszają wersje sprzed wielu wydań — agent z pamięci wygeneruje pół-działający `package.json` ze starymi peer-depami i deprecated polami. Oficjalny CLI z `npm view <pkg>` zawsze pociągnie aktualny stack. To samo serce mechaniki `/10x-bootstrapper` (cmd_template + ekspozycja na harness).
- **Source**: [m1l3-ai-powered-bootstrap](./lessons/m1l3-ai-powered-bootstrap/summary.md)
- **Added**: 2026-06-05

## Projektuj skille wokół trzech bramek egzekucji
- **What**: Każdy nietrywialny skill rozbij na pre-execution (kontrakt + recency check), in-execution (delegacja do CLI/kodu, harness pyta o uprawnienia), post-execution (audyt wyniku, zapis raportu plikowego).
- **Why**: Daje wspólny szkielet dla różnych domen (bootstrap, health-check, deploy, review) i jasny punkt halt: jeśli pre-bramka nie spełnia kontraktu, skill odmawia bez improwizacji; jeśli in-bramka pada non-zero, skill stopuje i zostawia ślad. Bez tego skille rozjeżdżają się w prompt-monolit, w którym nie wiadomo, co audytować.
- **Source**: [m1l3-ai-powered-bootstrap](./lessons/m1l3-ai-powered-bootstrap/summary.md)
- **Added**: 2026-06-05

## Po każdej egzekucji skilla czytaj plikowy raport
- **What**: Skill zapisuje na dysku trwały ślad (`verification.md`, `health-check.md`, `change.md`) — przeczytaj go zanim przejdziesz do następnego kroku, nawet jeśli summary w czacie wygląda OK.
- **Why**: Czat ginie po session reset; raport plikowy mówi za tydzień, dlaczego Phase 1 jest na `warned` i co dokładnie skill skipnął. Status `passed/warned/failed/skipped` jest jednoznaczny tylko w pliku — w czacie agenci często łagodzą sformułowania.
- **Source**: [m1l3-ai-powered-bootstrap](./lessons/m1l3-ai-powered-bootstrap/summary.md)
- **Added**: 2026-06-05

## Plan, research i test żyją w plikach repo, nie w rozmowie
- **What**: `plan.md`, `plan-brief.md`, `research.md`, `test-plan.md`, `## Progress` — każdy istotny artefakt agentowego workflow trafia na dysk w `context/`. Rozmowa to medium ulotne; plik w repo jest trwałym kontraktem.
- **Why**: Plan Mode / chat history giną z sesją. Plik przeżyje session reset (M2L4 context drift), hand-off do innego programisty albo do innej sesji za dwa tygodnie. Bez tego co fazę zaczynasz od „opowiadania od początku", a po pierwszym `/clear` agent miesza decyzje z różnych slice'ów. Cross-lesson: M2L2 (plan), M2L4 (research), M3L1 (test plan), M3L5 (## Progress jako pamięć dochodzenia).
- **Source**: [m2l2-implementacja-z-agentem](./lessons/m2l2-implementacja-z-agentem/key-takeaways.md), [m2l4-research-i-implementacja](./lessons/m2l4-research-i-implementacja/key-takeaways.md), [m3l1-plan-testow](./lessons/m3l1-plan-testow/key-takeaways.md)
- **Added**: 2026-06-09

## Wyrocznia testu pochodzi z kontraktu zewnętrznego, nie z testowanego kodu
- **What**: Oczekiwany wynik testu (asercja) musi pochodzić z PRD, kontraktu API, specyfikacji, ryzyka biznesowego — nigdy z kodu, który właśnie testujesz. Test plan opisuje **zachowanie** chronione (np. „płacący użytkownik widzi swoją treść"), nie „funkcja X zwraca Y".
- **Why**: Klasyczny **oracle problem** — agent z pamięcią obciążoną kodem zapisuje asercję, która odbija implementację (`expect(calculateDiscount(order)).toBe(0.15)` bo „tyle zwraca funkcja"). Jeśli w funkcji siedzi błąd, test go zabetonował i każda przyszła próba naprawy „psuje test", choć to test jest zły. Coverage rośnie, ochrona = zero. Cross-lesson: M3L1 (test plan na poziomie zachowania), M3L2 (oracle problem na funkcji `getNextInterval`), M3L4 (asercja behawioralna w E2E).
- **Source**: [m3l2-implementacja-unitow](./lessons/m3l2-implementacja-unitow/key-takeaways.md), [m3l1-plan-testow](./lessons/m3l1-plan-testow/key-takeaways.md), [m3l4-testy-e2e](./lessons/m3l4-testy-e2e/key-takeaways.md)
- **Added**: 2026-06-09

## Sprawdź, czy test potrafi zawieść (celowe psucie kodu)
- **What**: Po napisaniu testu zepsuj na chwilę kod produkcyjny — odwróć logikę, zwróć złą wartość, usuń filtr. Jeśli test pada — chroni. Jeśli zostaje zielony — asercja niczego nie pilnuje, popraw lub usuń. Cofnij zepsucie, **nie commituj**.
- **Why**: Najtańsza prywatna mutacja, którą ma sens odpalać per fazę bez Strykera w CI. Łapie testy-mirrory implementacji, których raporty coverage'u nie widzą — bo „zostaje zielony" znaczy „agent napisał asercję, która powtarza co kod robi, a nie co powinien robić". Cross-lesson: M3L2 (manual mutation per faza), M3L4 (VERIFY w pętli `/10x-e2e` — celowe psucie chronionego zachowania zanim test trafi do repo).
- **Source**: [m3l2-implementacja-unitow](./lessons/m3l2-implementacja-unitow/key-takeaways.md), [m3l4-testy-e2e](./lessons/m3l4-testy-e2e/key-takeaways.md)
- **Added**: 2026-06-09
