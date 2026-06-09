# m1l1 — Key Takeaways

- Idź po kolei: `/10x-shape` → `/10x-prd` → wybór stacku. Bezpośredni "wygeneruj PRD" da ładny dokument z decyzjami, których nigdy nie podjąłeś.
- Każdy FR przepuść przez sokratejskie pytanie "co musiałoby być prawdą, żeby ten FR był błędny". Brak odpowiedzi = FR jeszcze niegotowy.
- "User dodaje rekordy i je przegląda" = pusty CRUD. Wymuś konkretną regułę domenową (gate, generacja, scoring, recommendation) zanim ruszysz dalej — bez tego produkt jest pusty.
- Brownfield: odpalaj `/10x-shape` w istniejącym repo — skill wykryje markery i przerzuci pytania na deltę. Spodziewaj się sekcji `## Current System` i `## Constraints & Preserved Behavior` w shape-notes.
- W PRD nie wkładasz tech-stacku, planu testów ani deploymentu. To wejścia kolejnych skilli (M1L2 stack-selector, M1L3 bootstrapper, M1L5 deploy) — zaśmiecony PRD myli późniejsze kroki.
