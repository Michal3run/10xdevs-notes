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
