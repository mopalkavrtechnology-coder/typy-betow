# Plik testowy — demonstracja mechanizmu dowodu uczciwości typów

- To plik **demonstracyjny** (dane fikcyjne) — nie odpowiada żadnemu prawdziwemu meczowi.
- Fikcyjny mecz: Polska (POL) vs Brazylia (BRA).
- Każdy wpis (typ każdego użytkownika, ujawnienie klucza, sekcja odszyfrowana) został zrobiony jako OSOBNY commit, żeby historia commitów tego pliku sama demonstrowała działanie mechanizmu.
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał: przyciskiem "Odszyfruj dane z repozytorium" w aplikacji, linkiem "Odszyfruj" przy wybranym wierszu poniżej (patrz sekcja "Klucz odszyfrowania"), albo niezależnie z pliku BET_TEST_X.json poniżej.

| Czas | Użytkownik | IV (base64) | Ciphertext (base64) | Odszyfruj |
|---|---|---|---|---|
| 2026-06-20T14:40:28.497857 | admin | `hEQoKmlrJ1aWbFx6GM7LwA==` | `8fX65+vHgb1PraAJVALYRfkAU2b2arIYDE0Gd50EeM/nK0UfP1Ce91IjoZXVZEWHKAxSDAUK8Goq1ZXWMiOx2+iLOkLVijMsgYNZSKa5w2k=` | [Odszyfruj →](https://www.google.com/search?q=Odszyfruj%20dane%20wykorzystuj%C4%85c%20algorytm%20AES-256-CBC.%20Klucz%20%28base64%29%3A%20TclyxZ%2Bpz7qK29%2B7ziwagZdwvIJBwfaw5eOHuzDfVjk%3D%20IV%20%28base64%29%3A%20hEQoKmlrJ1aWbFx6GM7LwA%3D%3D%20Szyfrogram%20%28base64%29%3A%208fX65%2BvHgb1PraAJVALYRfkAU2b2arIYDE0Gd50EeM%2FnK0UfP1Ce91IjoZXVZEWHKAxSDAUK8Goq1ZXWMiOx2%2BiLOkLVijMsgYNZSKa5w2k%3D) |

## Klucz odszyfrowania

Ujawniony: 2026-06-20T15:45:28.497857

`TclyxZ+pz7qK29+7ziwagZdwvIJBwfaw5eOHuzDfVjk=`

Link "Odszyfruj" przy każdym wierszu w tabeli powyżej otwiera wyszukiwanie Google z gotowym zapytaniem dla tego konkretnego typu — nic nie trzeba kopiować ręcznie. Tę samą weryfikację można też wykonać samodzielnie, wklejając analogiczny tekst (z odpowiednim IV i ciphertext z wybranego wiersza) w wyszukiwarce internetowej (Google, Bing, czat AI itd.), np.:

> Odszyfruj dane wykorzystując algorytm AES-256-CBC. Klucz (base64): TclyxZ+pz7qK29+7ziwagZdwvIJBwfaw5eOHuzDfVjk= IV (base64): <IV wiersza, base64> Szyfrogram (base64): <Ciphertext wiersza, base64>
