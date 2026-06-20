# Plik testowy — demonstracja mechanizmu dowodu uczciwości typów

- To plik **demonstracyjny** (dane fikcyjne) — nie odpowiada żadnemu prawdziwemu meczowi.
- Fikcyjny mecz: Polska (POL) vs Brazylia (BRA).
- Każdy wpis (typ każdego użytkownika, ujawnienie klucza, sekcja odszyfrowana) został zrobiony jako OSOBNY commit, żeby historia commitów tego pliku sama demonstrowała działanie mechanizmu.
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał: przyciskiem "Odszyfruj dane z repozytorium" w aplikacji, linkiem "Odszyfruj" przy wybranym wierszu poniżej (patrz sekcja "Klucz odszyfrowania"), albo niezależnie z pliku BET_TEST_X.json poniżej.

| Czas | Użytkownik | IV (base64) | Ciphertext (base64) |
|---|---|---|---|
| 2026-06-20T14:40:28.497857 | admin | `hEQoKmlrJ1aWbFx6GM7LwA==` | `8fX65+vHgb1PraAJVALYRfkAU2b2arIYDE0Gd50EeM/nK0UfP1Ce91IjoZXVZEWHKAxSDAUK8Goq1ZXWMiOx2+iLOkLVijMsgYNZSKa5w2k=` |
