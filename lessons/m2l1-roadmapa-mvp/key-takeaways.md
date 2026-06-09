# m2l1 — Key Takeaways

- Każdy `F-NN` musi mieć wypełnione pole `Unlocks: S-NN`. „F-XX kompletny model danych" bez wskazanego docelowego slice'a to horizontal drift przebrany za fundament — wraca na parking, nie do roadmapy.
- North star ≠ pierwszy slice w kolejce. To moment, w którym teza produktu domyka się **end-to-end** (w 10xCards: S-04 sesja powtórek, nie S-01 generowanie). S-01/S-02 są warunkiem koniecznym, ale walidację daje dopiero przepływ przez SRS.
- Pole `Outcome` slice'a zaczyna się od czasownika „user can ..." — to test pionowości. Jeśli nie potrafisz tak go napisać, slice najprawdopodobniej został rozcięty warstwami i wymaga przeformułowania, zanim trafi do agenta.
- Status `blocked` zapala się automatycznie, gdy choć jeden Unknown ma `Block: yes`. To dobra wiadomość — skill mówi wprost, czego nie wiesz, **zanim** zaczniesz kodować. Nie wymuszaj zielonego, dopóki niewiadoma nie jest rozstrzygnięta.
- Przy wpinaniu agenta w issue tracker (Linear MCP, GitHub CLI): token zawężony do jednego projektu i uprawnień read/create/update; akcje destrukcyjne (delete project, mass status update, role change) zawsze przez UI. 30 sekund klikania > godziny sprzątania po automatycznej pomyłce.
