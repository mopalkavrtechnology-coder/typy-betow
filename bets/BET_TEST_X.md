# Plik testowy — demonstracja mechanizmu dowodu uczciwości typów

- To plik **demonstracyjny** (dane fikcyjne) — nie odpowiada żadnemu prawdziwemu meczowi.
- Każdy wpis (typ każdego użytkownika, ujawnienie klucza, sekcja odszyfrowana) został zrobiony jako OSOBNY commit, żeby historia commitów tego pliku sama demonstrowała działanie mechanizmu.
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał, np. za pomocą decrypt.html.

```ndjson
{"ts":"2026-06-19T23:48:11.021110","user":"admin","nonce":"fyDZ7T+9Wk8fjuJzIRnuow==","ciphertext":"jMLTY3ZfwL5GfSWPOsDmaE128KX6S78AfIRPAX8Nk5k="}
{"ts":"2026-06-20T00:55:11.021110","user":"user1","nonce":"v5m9gt7hekL1P5gqm8NJeQ==","ciphertext":"dS+Mig7bue7IwBinSHzg57SxUG6MXCMW6aENojk5pWA="}
{"ts":"2026-06-20T02:02:11.021110","user":"admin2","nonce":"6U9jaxt04lRrf+kZQU2jLQ==","ciphertext":"LnCVcf0MXoFZE2cqC4lXRlJO+ppLTm4potK5Kay40aE="}
```
