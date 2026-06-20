# Plik testowy — demonstracja mechanizmu dowodu uczciwości typów

- To plik **demonstracyjny** (dane fikcyjne) — nie odpowiada żadnemu prawdziwemu meczowi.
- Każdy wpis (typ każdego użytkownika, ujawnienie klucza, sekcja odszyfrowana) został zrobiony jako OSOBNY commit, żeby historia commitów tego pliku sama demonstrowała działanie mechanizmu.
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał (np. przyciskiem "Odszyfruj dane z repozytorium" w aplikacji, albo niezależnie z pliku BET_TEST_X.json poniżej).

```ndjson
{"ts":"2026-06-20T04:22:24.397855","user":"admin","nonce":"0Gr+v+C1ZRAIHjfPTTyEyQ==","ciphertext":"ygsOnKi27NMAqe1PTRLaGUHHks5bW2bjOFAW8l6Ni4I="}
{"ts":"2026-06-20T05:29:24.397855","user":"user1","nonce":"FjHxANkl/a4sYCD87BnLFw==","ciphertext":"cJ4anBx0Mc0qxJWhQN42qYM0Q85xvUYFGAmrCIelFSk="}
{"ts":"2026-06-20T06:36:24.397855","user":"admin2","nonce":"g0tsAqD9tFGUYqocaxSgKA==","ciphertext":"EJOD6pNuZ3rzDr7DB8tij4vgRzrBhNiEe7bS9AvwL8c="}
{"ts":"2026-06-20T07:43:24.397855","user":"admin3","nonce":"9ryq9YKtAE9PC27Y4/trng==","ciphertext":"agpL1Qgg2aZM03YHfa/xCvTeuZKISfgybrLOrKxEAn8="}
{"ts":"2026-06-20T08:50:24.397855","user":"pokea","nonce":"NxCVbpVo1DmGnHCC+0KrnA==","ciphertext":"6eyrjAsqzRgwrQyKfzmcELNB9WrONxu0dPjbNE0dvPk="}
{"ts":"2026-06-20T09:57:24.397855","user":"Kura","nonce":"sJuJhx3VTND1QQDGqs9/Ww==","ciphertext":"MfZc+XVyWm59FxQvMp9G9/ygmTGQouLo9zKccTcXDnI="}
{"ts":"2026-06-20T11:04:24.397855","user":"q","nonce":"lUBfzOhpumTofE6fhDW11A==","ciphertext":"8DpFlKoaBlVeVK+qvkOYk7ZyiaWOSldDuZH232T7XBM="}
{"ts":"2026-06-20T12:11:24.397855","user":"qwe","nonce":"0xxHMeQr5WJlKGYRCPO3Og==","ciphertext":"K29DE+40G0HHBzVbftb/hjd/rXRNRqymHim9Fa9GX9s="}
{"ts":"2026-06-20T13:18:24.397855","user":"alice99","nonce":"aPirjIXjqR52QOMRKUGALw==","ciphertext":"UN0T5dyAlu9mF2Yewu062OFSK6v5BpE6hczU20Wiok8="}
```
