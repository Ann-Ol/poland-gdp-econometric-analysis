[README.md](https://github.com/user-attachments/files/32299300/README.md)
# Analiza ekonometryczna PKB Polski

## Opis projektu

Projekt przedstawia analizę ekonometryczną zależności pomiędzy **realnym PKB Polski** a wybranymi zmiennymi makroekonomicznymi na podstawie danych rocznych z lat **1998–2025**.

Celem projektu jest budowa, weryfikacja i interpretacja modelu regresji liniowej opisującego poziom realnego PKB Polski. Dobór zmiennych nie został oparty wyłącznie na księgowej tożsamości PKB, lecz na wieloetapowej procedurze ekonometrycznej.

Analiza obejmuje:

- kontrolę jakości i przygotowanie danych,
- przeliczenie zmiennych nominalnych na ceny stałe 2025 r.,
- analizę zmienności i eliminację zmiennych quasi-stałych,
- analizę korelacji,
- dobór zmiennych metodą Hellwiga,
- porównanie alternatywnych specyfikacji modeli,
- ocenę istotności parametrów i współliniowości VIF,
- wybór modelu z wykorzystaniem AIC i BIC,
- estymację modelu metodą najmniejszych kwadratów,
- diagnostykę reszt,
- interpretację ekonomiczną,
- przygotowanie orientacyjnego scenariusza trendowego do 2030 r.

## Dane

Analiza wykorzystuje roczne dane dla Polski z lat **1998–2025**, zapisane w pliku `Dane_PKB.xlsx`.

Zmienną objaśnianą jest realny PKB Polski. Wśród zmiennych kandydujących do modelu znajdują się m.in.:

- spożycie prywatne,
- kurs USD/PLN,
- import,
- eksport,
- wynagrodzenie brutto,
- CPI,
- stopa bezrobocia,
- akumulacja brutto,
- stopy procentowe,
- spożycie publiczne.

Zmienne pieniężne zostały przeliczone z wartości nominalnych na **ceny stałe 2025 r.** przy wykorzystaniu indeksu cen wyznaczonego na podstawie CPI.

Indeks cen i deflator pełnią funkcję pomocniczą i nie są zmiennymi objaśniającymi w modelu.

## Przygotowanie danych

Przed rozpoczęciem modelowania wykonano kontrolę:

- braków danych,
- duplikatów lat,
- ciągłości szeregu czasowego,
- poprawności struktury danych.

Zbiór wykorzystany w analizie zawiera **28 obserwacji rocznych** i nie zawiera braków danych ani zduplikowanych lat.

## Dobór zmiennych

Dobór zmiennych przeprowadzono wieloetapowo.

### 1. Eliminacja zmiennych quasi-stałych

Dla zmiennych objaśniających obliczono współczynnik zmienności. Zmienne o bardzo małej zmienności zostały wyeliminowane z dalszej analizy.

W tej części analizy CPI zostało odrzucone jako zmienna quasi-stała.

### 2. Analiza korelacji

Sprawdzono siłę zależności liniowej pomiędzy realnym PKB a potencjalnymi zmiennymi objaśniającymi oraz relacje pomiędzy samymi zmiennymi.

### 3. Metoda Hellwiga

Metodę Hellwiga wykorzystano jako jeden z etapów selekcji zmiennych, uwzględniający jednocześnie:

- związek zmiennych z PKB,
- zależności pomiędzy zmiennymi objaśniającymi.

### 4. Porównanie modeli

Przetestowano alternatywne kombinacje zmiennych objaśniających. Przy wyborze modelu uwzględniono:

- istotność statystyczną parametrów,
- współczynnik VIF,
- skorygowany współczynnik determinacji,
- kryterium AIC,
- kryterium BIC.

Finalnie wybrano model o najniższym AIC spośród modeli spełniających przyjęte ograniczenia dotyczące istotności parametrów i współliniowości.

## Model finalny

W modelu finalnym znalazły się trzy zmienne:

- `spozycie_prywatne_real`,
- `akumulacja_brutto_real`,
- `stopy_procentowe`.

Oszacowana postać modelu:

```text
PKB_real =
-501538,39
+ 1,84421 × spozycie_prywatne_real
+ 0,34763 × akumulacja_brutto_real
+ 4667,67 × stopy_procentowe
```

Najsilniejszą statystycznie zależność z realnym PKB wykazuje **realne spożycie prywatne**.

Parametry przy akumulacji brutto i stopach procentowych spełniają przyjęte w projekcie kryterium istotności na poziomie 10%, ale nie na poziomie 5%, dlatego ich interpretacja wymaga większej ostrożności.

## Dopasowanie modelu

Model charakteryzuje się bardzo wysokim dopasowaniem do danych:

| Miara | Wartość |
|---|---:|
| R² | 0,9965 |
| Skorygowane R² | 0,9961 |
| Liczba obserwacji | 28 |

Wysokie R² nie powinno być interpretowane jako dowód zależności przyczynowej. Część zmiennych objaśniających, w szczególności spożycie prywatne i akumulacja brutto, jest związana z wydatkowym ujęciem PKB.

## Diagnostyka modelu

W projekcie przeprowadzono zestaw testów diagnostycznych obejmujący m.in.:

- test serii,
- test Shapiro-Wilka,
- test Breuscha-Pagana,
- test Durbina-Watsona,
- test Ljunga-Boxa,
- test RESET.

### Autokorelacja reszt

Test Durbina-Watsona:

```text
DW = 1,3331
p-value = 0,008449
```

Wynik wskazuje na **dodatnią autokorelację reszt**, dlatego klasyczne błędy standardowe oraz wnioski dotyczące istotności parametrów należy interpretować ostrożnie.

### Postać funkcyjna

Test RESET:

```text
RESET = 3,72
p-value = 0,04058
```

Wynik sugeruje, że liniowa postać modelu może nie opisywać w pełni wszystkich zależności występujących w danych. Możliwymi przyczynami są m.in. nieliniowość, pominięte zmienne lub bardziej złożona dynamika czasowa.

## Scenariusz trendowy do 2030 r.

Na podstawie wybranego modelu przygotowano prosty scenariusz dla lat **2026–2030**.

Wartości zmiennych objaśniających zostały wyznaczone przez liniową ekstrapolację ich historycznych trendów, a następnie wykorzystane do obliczenia scenariuszowych wartości realnego PKB.

Ta część projektu ma charakter **orientacyjny** i nie stanowi pełnej prognozy makroekonomicznej. Mechaniczne przedłużenie trendów może prowadzić do wartości ekonomicznie mało realistycznych, dlatego wyniki powinny być interpretowane przede wszystkim jako demonstracja zastosowania oszacowanego modelu.

## Interpretacja wyników

Wyniki wskazują na silną współzmienność realnego PKB przede wszystkim z realnym spożyciem prywatnym, a w mniejszym stopniu również z akumulacją brutto i stopami procentowymi.

Oszacowanych parametrów nie należy interpretować jako czystych efektów przyczynowych. Projekt opisuje zależności występujące w danych historycznych.

Model należy traktować przede wszystkim jako narzędzie **opisowe i analityczne**, a nie kompletny model strukturalny polskiej gospodarki.

## Możliwe kierunki dalszego rozwoju

Naturalnym rozszerzeniem projektu byłoby:

- zbadanie stacjonarności szeregów czasowych,
- analiza kointegracji,
- zastosowanie transformacji logarytmicznych lub przyrostów,
- wykorzystanie odpornych błędów standardowych,
- porównanie modeli o alternatywnej postaci funkcyjnej,
- uwzględnienie opóźnień i dynamiki zmiennych w czasie.

## Technologie i biblioteki

Projekt został wykonany w **R / R Markdown** z wykorzystaniem pakietów:

- `readxl`,
- `dplyr`,
- `tidyr`,
- `ggplot2`,
- `scales`,
- `car`,
- `lmtest`,
- `tseries`.

## Struktura repozytorium

```text
.
├── README.md
├── Analiza_PKB.Rmd
├── Analiza_PKB.html
└── Dane_PKB.xlsx
```

Plik `Analiza_PKB.html` zawiera wyrenderowany raport wraz z kodem, wynikami, tabelami i wykresami.

Plik `Dane_PKB.xlsx` powinien znajdować się w tym samym katalogu co dokument `.Rmd`, ponieważ jest bezpośrednio wczytywany przez kod.

## Jak uruchomić projekt

1. Pobierz lub sklonuj repozytorium.
2. Upewnij się, że `Dane_PKB.xlsx` znajduje się w tym samym katalogu co `Analiza_PKB.Rmd`.
3. Otwórz plik `Analiza_PKB.Rmd` w RStudio.
4. W razie potrzeby zainstaluj wymagane pakiety R.
5. Wybierz **Knit → Knit to HTML**.

## Ograniczenia

Najważniejsze ograniczenia analizy:

- niewielka liczba obserwacji wynikająca z rocznej częstotliwości danych,
- część zmiennych jest bezpośrednio związana z rachunkową konstrukcją PKB,
- występuje dodatnia autokorelacja reszt,
- test RESET wskazuje na możliwą niedoskonałość liniowej postaci modelu,
- wysoki poziom dopasowania nie oznacza związku przyczynowego,
- scenariusz do 2030 r. opiera się na prostej ekstrapolacji trendów,
- projekt nie analizuje jeszcze pełnych właściwości szeregów czasowych, takich jak stacjonarność i kointegracja.

## Autorzy

**Bartosz Kawalec**  
**Anna Oleszko**  
**Kacper Saj**

Projekt został wykonany wspólnie.
