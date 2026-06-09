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
