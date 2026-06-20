# Plik testowy — demonstracja mechanizmu dowodu uczciwości typów

- To plik **demonstracyjny** (dane fikcyjne) — nie odpowiada żadnemu prawdziwemu meczowi.
- Każdy wpis (typ każdego użytkownika, ujawnienie klucza, sekcja odszyfrowana) został zrobiony jako OSOBNY commit, żeby historia commitów tego pliku sama demonstrowała działanie mechanizmu.
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał, np. za pomocą decrypt.html.

```ndjson
{"ts":"2026-06-19T23:48:11.021110","user":"admin","nonce":"fyDZ7T+9Wk8fjuJzIRnuow==","ciphertext":"jMLTY3ZfwL5GfSWPOsDmaE128KX6S78AfIRPAX8Nk5k="}
{"ts":"2026-06-20T00:55:11.021110","user":"user1","nonce":"v5m9gt7hekL1P5gqm8NJeQ==","ciphertext":"dS+Mig7bue7IwBinSHzg57SxUG6MXCMW6aENojk5pWA="}
{"ts":"2026-06-20T02:02:11.021110","user":"admin2","nonce":"6U9jaxt04lRrf+kZQU2jLQ==","ciphertext":"LnCVcf0MXoFZE2cqC4lXRlJO+ppLTm4potK5Kay40aE="}
{"ts":"2026-06-20T03:09:11.021110","user":"admin3","nonce":"WdbqIcW/SDF23Vedk7ifWw==","ciphertext":"rC8FrqrnB7WZz5+OqISHvhqZCRgMmtzNIhv7OCp2aI4="}
{"ts":"2026-06-20T04:16:11.021110","user":"pokea","nonce":"C9IHfi60nmwH9XhApf08/Q==","ciphertext":"iVvGvzkrQlir5naSoyxnuAPfSS2al1cUGolJ52hQyzI="}
{"ts":"2026-06-20T05:23:11.021110","user":"Kura","nonce":"VZ9rX1ek9DhojInDQacOBA==","ciphertext":"EBaWgwb+G2KNn4Ezf5oufeYdnHGfwF1H+PtaAOpwh+k="}
{"ts":"2026-06-20T06:30:11.021110","user":"q","nonce":"ZOKzcdtDwtsflMDaj4K5/Q==","ciphertext":"q1uoyAjiyXUQk7mMcdZlM7HWK9c7q3i67tR36XMmqOQ="}
{"ts":"2026-06-20T07:37:11.021110","user":"qwe","nonce":"kBb0orNPY6LOM+mIz82SmA==","ciphertext":"FcwycTkbDAyq9+w9BLAIPE6QZHuIcV10puo6pLHmrho="}
{"ts":"2026-06-20T08:44:11.021110","user":"alice99","nonce":"NNXIgl7nPSi5rmrancx1Wg==","ciphertext":"fO5uf5gCMHfxotjA9moJwbz+69Q2G2bFR/0BCrh1HVQ="}
{"ts":"2026-06-20T09:51:11.021110","user":"bobnowak","nonce":"g/jroj8RzlgMlLvCgr+gGw==","ciphertext":"1MQgSurjJ2AOwI59RrO2/CFF3QnV/DJy9+wxJsQYerc="}
{"ts":"2026-06-20T09:53:11.021110","event":"KEY_REVEAL","key":"Q3BcN+81JqsovGDwWLCcmkOSvjzul0JSUVw6IIG/Zn0="}
```

## Odszyfrowane dane (do weryfikacji ręcznej)

| Czas | Użytkownik | Typ |
|---|---|---|
| 2026-06-19T23:48:11.021110 | admin | 3 : 4 |
| 2026-06-20T00:55:11.021110 | user1 | 3 : 2 |
| 2026-06-20T02:02:11.021110 | admin2 | 1 : 4 |
| 2026-06-20T03:09:11.021110 | admin3 | 3 : 1 |
| 2026-06-20T04:16:11.021110 | pokea | 2 : 0 |
| 2026-06-20T05:23:11.021110 | Kura | 2 : 2 |
| 2026-06-20T06:30:11.021110 | q | 1 : 3 |
| 2026-06-20T07:37:11.021110 | qwe | 0 : 3 |
| 2026-06-20T08:44:11.021110 | alice99 | 2 : 4 |
| 2026-06-20T09:51:11.021110 | bobnowak | 1 : 2 |
