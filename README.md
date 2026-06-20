# Dowód uczciwości typów

Ten dokument wyjaśnia — bez żargonu programistycznego — jak działa mechanizm, który ma
udowodnić, że nikt (włącznie z administratorem aplikacji) nie mógł po cichu zmienić Twojego
typu na mecz po tym, jak zobaczył wynik. Jeśli nie interesuje Cię "jak", a tylko "czy mogę
zaufać", przejdź do sekcji [W skrócie: dlaczego można temu wierzyć](#w-skrócie-dlaczego-można-temu-wierzyć).

## Jaki problem to rozwiązuje

W zwykłej aplikacji do obstawiania Twój typ jest jednym wierszem w bazie danych. Administrator
tej bazy — teoretycznie — mógłby po zakończeniu meczu zmienić ten wiersz tak, żeby wyglądało,
jakbyś obstawiał inaczej niż w rzeczywistości (np. żeby kogoś uprzywilejować albo zaszkodzić).
Nikt z zewnątrz by tego nie zauważył, bo baza danych nie pamięta swojej własnej historii — wie
tylko, jaki jest stan *teraz*.

Mechanizm opisany w tym dokumencie eliminuje potrzebę takiego zaufania. Nie musisz wierzyć
administratorowi na słowo — możesz to **samodzielnie sprawdzić**, w każdej chwili, nawet nie
mając konta w tej aplikacji.

## Analogia: zapieczętowana koperta

Najprościej wyobrazić to sobie tak, jak działają zapieczętowane koperty w teleturniejach:

1. **Wpisujesz typ.** Aplikacja od razu zamyka go w "zapieczętowanej kopercie" — w
   rzeczywistości to szyfrowanie, ale efekt jest identyczny: treść jest nieczytelna dla
   kogokolwiek, kto nie ma klucza, włącznie z administratorem aplikacji.
2. **Koperta trafia na publiczną tablicę.** Zaszyfrowana treść jest wysyłana na zewnętrzny,
   publiczny serwis (GitHub) —a niezależny od tej aplikacji. Widać tam dokładnie, **kiedy**
   koperta się pojawiła i **kto** ją podpisał (Twój pseudonim), ale nie da się jej jeszcze
   otworzyć.
3. **Klucz zostaje schowany do startu meczu.** Dopóki zakłady na dany mecz są otwarte, klucz do
   odszyfrowania nie istnieje nigdzie publicznie — jest trzymany wyłącznie w bazie danych
   aplikacji.
4. **Mecz się zaczyna → klucz zostaje ujawniony.** W momencie startu meczu (czyli już po
   zamknięciu zakładów — nikt nie może już niczego zmienić) klucz zostaje dopisany do *tego
   samego* publicznego pliku.
5. **Każdy może otworzyć kopertę i porównać.** Od tej chwili każdy — Ty, inny uczestnik, osoba
   z zewnątrz — może odszyfrować zapisaną treść i sprawdzić, czy zgadza się z tym, co aplikacja
   pokazuje jako Twój typ.

Kluczowa właściwość tego schematu: **koperta (zaszyfrowana treść) trafia na widok publiczny,
zanim ktokolwiek pozna klucz.** Dlatego nikt — nawet administrator — nie może podmienić treści
koperty *po fakcie* bez pozostawienia widocznego dowodu (więcej w sekcji [Dlaczego nie da się
tego oszukać](#dlaczego-nie-da-się-tego-oszukać)).

## Co dokładnie się dzieje, krok po kroku

| Krok | Co się dzieje |
|---|---|
| 1. Dodajesz lub edytujesz typ | Aplikacja natychmiast szyfruje wynik, datę, godzinę i Twój pseudonim algorytmem AES-256 (standard używany m.in. przez banki) |
| 2. Wysyłka na GitHub | Zaszyfrowana treść trafia do publicznego, dedykowanego repozytorium GitHub — w ciągu kilku sekund od zapisania typu |
| 3. Zakłady wciąż otwarte | Plik na GitHubie rośnie (nowy wiersz przy każdym typie/edycji), ale klucza odszyfrowania nigdzie nie widać |
| 4. Mecz startuje | Klucz odszyfrowania zostaje dopisany jako **ostatni** wpis w tym samym pliku |
| 5. Weryfikacja | Każdy może teraz odszyfrować wszystkie wpisy i zobaczyć rzeczywiste typy wraz z czasem ich dodania |

Każda **edycja** typu dopisuje **nowy** zaszyfrowany wiersz — stary nigdy nie jest usuwany ani
nadpisywany. Dzięki temu widoczna jest cała historia: jeśli ktoś zmienił typ trzy razy przed
startem meczu, wszystkie trzy wersje (i ich godziny) zostają w pliku.

## Co zawiera zaszyfrowany wpis

Każdy wiersz w pliku na repozytorium zawiera:

- **Czas** dodania/edycji typu (czas warszawski),
- **Pseudonim** osoby, która typowała,
- **Zaszyfrowaną treść** (nieczytelną bez klucza) — w tym sam wynik, ale też ponownie datę,
  godzinę i pseudonim *wewnątrz* szyfrogramu. Dzięki temu odszyfrowanie pojedynczego wiersza —
  nawet wyrwanego z kontekstu — od razu mówi, kto, co i kiedy obstawił, bez potrzeby ufania
  jawnym danym leżącym obok.

Plik nazywa się np. `20260620_1500_NED_SWE.md` — data i godzina meczu jako pierwsze, żeby pliki
w repozytorium ułożyły się chronologicznie przy przeglądaniu alfabetycznym.

## Jak samodzielnie zweryfikować swój typ (bez wiedzy technicznej)

Nie trzeba rozumieć kryptografii, żeby to sprawdzić:

1. Na karcie meczu kliknij **"Zobacz typy uczestników"** → zakładkę **"Repozytorium"**.
   Zobaczysz listę: kto i kiedy dodał/edytował typ, z linkiem do konkretnego zapisu (commita)
   na GitHubie.
2. Kliknij **"Odszyfruj dane z repozytorium"** — aplikacja sama pobiera plik z GitHuba i
   odszyfrowuje go w Twojej przeglądarce (nic nie przechodzi przez serwer aplikacji). Jeśli
   mecz się jeszcze nie zaczął, zobaczysz informację, że klucz nie jest jeszcze ujawniony —
   to oczekiwane.
3. Przy każdym odszyfrowanym wierszu jest link **"Odszyfruj →"** — otwiera wyszukiwanie Google
   z gotowym zapytaniem zawierającym klucz, dane i prośbę o odszyfrowanie AES-256-CBC. To
   **niezależna, druga weryfikacja** tego samego wyniku, bez polegania na kodzie tej aplikacji.
4. Najbardziej nieufni mogą otworzyć link do pliku na GitHubie wprost (przycisk "Plik dowodowy
   na repozytorium") i samodzielnie skopiować klucz/dane do dowolnego narzędzia
   AES-256-CBC albo zapytać o to dowolny czat AI — wynik zawsze powinien się zgadzać.

## Dlaczego nie da się tego oszukać

**Klucz nie istnieje "z góry".** Dla każdego meczu generowany jest osobny, losowy klucz —
dopiero gdy ktoś pierwszy postawi typ. Klucz nigdy nie jest wysyłany do przeglądarki, nie
pojawia się w żadnym publicznym API ani odpowiedzi serwera — aż do startu meczu.

**Zaszyfrowana treść jest publiczna od razu, klucz dopiero później.** To jest istota
zabezpieczenia: gdyby ktoś chciał podstawić "lepszy" typ po zobaczeniu wyniku, musiałby zrobić
to *przed* ujawnieniem klucza — czyli zanim mecz się zacznie. Ale w tym momencie wynik meczu
jeszcze nie jest znany, więc nie ma czego "poprawiać".

**Po starcie meczu nic nie da się już zmienić bez śladu.** GitHub zapisuje pełną historię
zmian (commitów) pliku — każda zmiana ma datę, autora i dokładną treść różnicy. Nawet osoba z
dostępem administracyjnym do repozytorium nie może po cichu nadpisać starego wpisu — taka
zmiana zostałaby zarejestrowana jako nowy, widoczny commit, z innym czasem niż oryginalny.
Można samodzielnie przejrzeć całą historię commitów pliku na GitHubie.

**Repozytorium jest publiczne i niezależne.** Nie trzeba mieć konta — ani w aplikacji, ani na
GitHubie — żeby zobaczyć plik, jego historię commitów, i samodzielnie odszyfrować dane. To
nie jest "zaufaj nam" — to "zweryfikuj sam".

## Czego ten mechanizm NIE chroni (uczciwie o ograniczeniach)

Żeby nie obiecywać więcej, niż mechanizm faktycznie daje:

- **Nie chroni przed tym, że administrator widzi Twój typ na żywo.** Typ jest jawnie widoczny
  w bazie danych aplikacji od momentu dodania — tak działa każda aplikacja tego typu. Ten
  mechanizm chroni przed **późniejszą, niezauważoną zmianą** typu po fakcie, nie przed
  podglądaniem w czasie rzeczywistym.
- **Nie ma dodatkowej "plomby" wykrywającej manipulację samego szyfrogramu** (w żargonie:
  brak MAC/HMAC). W praktyce oznacza to, że osoba mająca pisemny dostęp do repozytorium
  (czyli wyłącznie administrator z odpowiednim tokenem) mogłaby teoretycznie podmienić
  zaszyfrowane bajty *przed* ujawnieniem klucza — ale i tak nie wiedziałaby, na co je podmienić
  bez znania wyniku, a próba pozostawiłaby nowy commit w historii repozytorium. Po ujawnieniu
  klucza każda taka manipulacja staje się natychmiast widoczna: odszyfrowanie zwróci czytelny
  błąd ("nie można odszyfrować — możliwa manipulacja") zamiast poprawnego wyniku.
- **Dotyczy tylko klasycznych typów wyniku** ("Moje typy"), nie kuponów bukmacherskich.
- **Nie chroni przed błędnie wpisanym wynikiem meczu** — to osobna kwestia, niezależnie
  weryfikowalna przez wyniki live (ESPN) widoczne w aplikacji.

## Najczęstsze pytania

**Co jeśli GitHub akurat nie działa, gdy dodaję typ?**
Nic się nie gubi. Wpis czeka w kolejce po stronie aplikacji i zostaje wysłany automatycznie,
gdy GitHub znów odpowiada — najdalej przy najbliższym sprawdzeniu (domyślnie co 2 minuty).

**Co jeśli administrator zmieni godzinę meczu?**
Nazwa pliku na repozytorium zawiera godzinę startu, więc zmiana godziny zmienia nazwę pliku.
Aplikacja sama wykrywa to i odtwarza plik pod nową nazwą z pełną historią wpisów — nic nie
ginie.

**Czy muszę ufać tej aplikacji, że poprawnie wszystko zaszyfrowała?**
Nie musisz — to jest właśnie sens przycisku "Odszyfruj →" przy każdym wpisie: otwiera on
zapytanie do Google/AI z gotowymi danymi, więc możesz odszyfrować dany wpis **całkowicie
niezależnym narzędziem**, bez polegania na kodzie tej aplikacji.

**Czy widzę typy innych graczy zanim mecz się zacznie?**
To zależy od ustawienia "Ukryj typy przed meczem" w panelu administracyjnym. Niezależnie od
tego ustawienia, zakładka "Repozytorium" jest zawsze dostępna i pozwala śledzić, że typy są
faktycznie dodawane — bez ujawniania ich treści przed czasem.

## W skrócie: dlaczego można temu wierzyć

- Typ jest szyfrowany **natychmiast** po dodaniu i wysyłany na **publiczne, niezależne**
  repozytorium — w ciągu kilku sekund.
- Klucz do odszyfrowania jest ujawniany **dopiero po starcie meczu**, gdy nikt nie może już
  nic zmienić.
- Każda zmiana typu to **nowy wpis**, nigdy nadpisanie starego — cała historia jest widoczna.
- Cały mechanizm działa na **GitHubie**, czyli poza kontrolą tej aplikacji — historię commitów
  może przejrzeć każdy, bez konta.
- Weryfikację możesz wykonać **samodzielnie i niezależnie** od aplikacji — przyciskiem
  "Odszyfruj" prowadzącym do zewnętrznego wyszukiwania, albo wprost w dowolnym narzędziu
  AES-256-CBC.
