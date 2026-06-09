# m1l3 — Key Takeaways

- Po pierwszym `/10x-bootstrapper` ustaw startowe `.claude/settings.json`: allow lokalne `npm/npx/git/node`, ask `git push` i `curl/wget`, deny `rm -rf *`. Klikanie "Yes" na ślepo zostawia bramę otwartą po tygodniu.
- Filtr "Yes, don't ask again": **co ten wzorzec może popsuć poza moim repo?** "Nic" → allow. "Cały dysk / kasa / dane klienta" → deny. Wszystko pomiędzy → ask.
- Niezerowy exit code z CLI? Stop. Naprawiasz na poziomie systemu (sieć, lockfile, env, nazwa katalogu) i odpalasz skill ponownie. Nie pozwalaj agentowi "naprawiać" boilerplate'u promptem — rekonstrukcja z pamięci modelu mieszają wersje sprzed wielu wydań.
- Brownfield = `/10x-health-check`, greenfield = `/10x-bootstrapper`. Mylenie kradnie godziny na rozwiązywanie konfliktów `.scaffold` w katalogach, których tam nie powinno być.
- Konsumencki tier (Claude Pro, ChatGPT Plus, Gemini Advanced) — wyłącz trening modeli **przed** pierwszą sesją z kodem firmowym. Gemini Advanced jako subskrypcja **nie zmienia** polityki: `myactivity.google.com` → wyłącz "Keep Activity". Chińscy dostawcy (DeepSeek, Qwen) działają w jurysdykcji bez prawa odmowy udostępnienia danych państwu — niezależnie od ustawień.
