# m1l4 — Key Takeaways

- Po `/init` (lub `/10x-agents-md` w narzędziu bez własnego generatora) przefiltruj szkic przez **test inkluzji**: jeśli agent wiedziałby to bez tego pliku z danych treningowych albo `README`, usuwaj. Reguły są dla agenta, który zna TypeScript, ale nie zna waszych konwencji.
- Zamień życzenia na sprawdzalne zachowanie. "Pisz czytelny kod" → wyrzuć. "Format błędu API: `{ error: { code, message, context } }`" → zostaw. Reguła bez sygnału akceptacji jest dekoracją.
- Główny `AGENTS.md`/`CLAUDE.md` ≤200 linii, ważne reguły **na górze** (u-shaped attention — środek pliku jest słabiej egzekwowany). Reguły obszarowe → bliżej kodu (`src/api/AGENTS.md`), nie do monolitu.
- Wskazuj plik wzorcowy zamiast kopiować przykład. `@src/features/users/user.service.ts`, `@docs/api-errors.md`, `@migration-template.sql`. Przykład starzeje się raz, nie w dwóch miejscach.
- Powtarzalny błąd agenta w 2-3 zadaniach? Odpal `/10x-lesson` → `context/foundation/lessons.md`. Plik append-only — nie sortujesz, nie deduplikujesz, nie przepisujesz wcześniejszych wpisów.
