# Dowód uczciwości typów: Holandia vs Szwecja

- Mecz ID: 33
- Planowany start: 2026-06-20T19:00:00
- Algorytm: AES-256-CBC (IV 16 bajtów, dopełnienie PKCS7, bez MAC), ciphertext i IV zakodowane w base64

Każdy wiersz poniżej to zaszyfrowany typ wpisany przed startem meczu. Klucz odszyfrowania zostanie dopisany jako **ostatni** wpis po rozpoczęciu meczu — od tego momentu każdy może zweryfikować, co kto wpisał (np. przyciskiem "Odszyfruj dane z repozytorium" w aplikacji, albo niezależnie z pliku match-{id}.json poniżej).

```ndjson
{"ts":"2026-06-20T09:00:57","user":"admin","nonce":"290pPuLKVjcwjgcKDDSD+Q==","ciphertext":"PE1N6BfXz6vUd2JkPrGRvGozWLlAKrsm26sjXk4lIgs="}
{"ts":"2026-06-20T12:13:34","user":"admin","nonce":"/o6V1Hk2Nk+oBSK5K2dxPw==","ciphertext":"cYZnBcqGIb+JmZoMDaempu8KPnXT7pBnI1A84FpkB4s="}
```
