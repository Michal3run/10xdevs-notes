# m1l2 — Key Takeaways

- Greenfield: `/10x-tech-stack-selector` na `prd.md` → `tech-stack.md`. Brownfield: `/10x-stack-assess` w istniejącym repo. Mylenie kroków = scaffolding rzucony w pustkę albo selektor, który nie umie czytać "co już jest".
- Trzeci podobny prompt na ten sam kontrakt I/O = sygnał kodyfikacji w skilla. Evale (skill-creator) zostaw na moment, gdy skill jest współdzielony albo częścią dłuższego łańcucha.
- Audytuj każdy zewnętrzny skill przed instalacją: `SKILL.md` (cel + `allowed-tools`), `scripts/` (co wykonuje, czego dotyka), źródło i autor. Skill = oprogramowanie, nie tekst.
- Wywołuj ważne skille jawnie po nazwie. Auto-aktywacja jest probabilistyczna (eval Vercela: 53/79/100% w zależności od konfiguracji); model nie wie, czego nie wie.
- Pisząc własny skill: `SKILL.md` blisko ~500 linii, reszta do `references/`, `scripts/`, `assets/`. Progresywne ujawnianie istnieje po to, żeby 20 zainstalowanych skilli kosztowało ~2k tokenów, nie ~100k.
