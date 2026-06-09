# m1l5 — Key Takeaways

- Wybór platformy zapisuj jako `context/foundation/infrastructure.md` (struktura ADR: wybór + uzasadnienie, CLI/MCP/API fit, rollback w X krokach, sekrety, ryzyka). Bez tego artefaktu pierwsza awaria pokaże, że platforma została wybrana za ciebie przez pierwszy poradnik z Google.
- Po `/10x-infra-research` przepuść scoring przez **devil's advocate / pre-mortem / unknown unknowns**, zanim zatwierdzisz. Bez tego model sam potwierdzi twoje przekonania (sycophancy), zamiast je przetestować.
- Nieodwracalne operacje (deploy, migracje, sekrety) zawsze przez Plan Mode (`Shift+Tab` w Claude Code). Plan zostaje w `context/deployment/deploy-plan.md` jako referencja "co miało się stać", gdy coś pójdzie nie tak.
- Dla MVP zacznij od CLI (`wrangler`, `gh`). MCP dorzucasz dopiero, gdy widzisz powtarzający się wzorzec, do którego agent czyta `--help` przy każdej iteracji. Reguła ze społeczności: "CLI when you know what command to run; MCP when the agent decides what to run".
- Token API zawężaj do minimum (jeden projekt, jeden produkt). Token przez env, nigdy w `.mcp.json` w repo. Operacje typu drop bazy / rotate głównego sekretu / zmiana DNS klikasz sam — 30 sekund manualu > godziny sprzątania.
