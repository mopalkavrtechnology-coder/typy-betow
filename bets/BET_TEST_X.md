# Plik testowy — demonstracja mechanizmu dowodu uczciwości typów

- To plik **demonstracyjny** (dane fikcyjne) — nie odpowiada żadnemu prawdziwemu meczowi.
- Każdy wpis (typ każdego użytkownika, ujawnienie klucza, sekcja odszyfrowana) został zrobiony jako OSOBNY commit, żeby historia commitów tego pliku sama demonstrowała działanie mechanizmu.
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał (np. przyciskiem "Odszyfruj dane z repozytorium" w aplikacji, albo niezależnie z pliku BET_TEST_X.json poniżej).

```ndjson
{"ts":"2026-06-20T04:17:01.418285","user":"admin","nonce":"4SSVXICdrn3K+ZmihyLstw==","ciphertext":"CPnfTHrbUHPWKwchkFBzujSodRLvIHHZED5Fgz7lwp0="}
{"ts":"2026-06-20T05:24:01.418285","user":"user1","nonce":"WKhELnbgAFXJ4OUhier8zw==","ciphertext":"KjDNXCLnkQA7J/dxCnmKJdQREHSxFS9dhAvl0KHkjZs="}
{"ts":"2026-06-20T06:31:01.418285","user":"admin2","nonce":"GJw+U0YzYaMU70Sj9MuX3A==","ciphertext":"xpeZxaStC72+hAf1ukwKDLaPRwnMzLlxKcntU0Rd+W4="}
```
