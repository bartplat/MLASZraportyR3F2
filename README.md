![KL+RP+IBE+EFS](inst/Belka-Losy-absolwentow-Kolor-PL.png)

# MLASZraportyR3F2

Pakiet został opracowany w ramach projektu *Monitorowanie losów edukacyjno-zawodowych absolwentów i młodych dorosłych* (POWR.02.15.00-IP.02-00-004/16) prowadzonego w Instytucie Badań Edukacyjnych w ramach działania 2.15. Kształcenie i szkolenie zawodowe dostosowane do potrzeb zmieniającej się gospodarki II. osi priorytetowej Efektywne polityki publiczne dla rynku pracy, gospodarki i edukacji Programu Operacyjnego Wiedza, Edukacja, Rozwój.

Pakiet `MLASZraportyR3F2` zawiera szablon raportu oraz zbiór funkcji używanych w szablonach np. do generowania wykresów. Szablony służą do obliczania wskaźników dla 2. fali 3. rundy Monitoringu Losów Absolwentów. Runda ta została zrealizowana za pomocą badania sondażowego metodą CAWI. Pakiet `MLASZraportyR3F2` zawiera jedynie szablon napisany w języku `R Markdown` i używane przez niego funkcje, natomiast, żeby generować przy jego pomocy raporty wymagany jest drugi pakiet zawierający zbiór funkcji będących silnikiem raportowania - [`MLASZraporty`](https://github.com/bartplat/MLASZraporty). Zbiory danych ze wskaźnikami, których można użyć do generowania raportów pakietem `MLASZraportyR3F2` można stworzyć przy użyciu pakietu [`MLASZdaneR3F2`](https://github.com/bartplat/MLASZdaneR3F2).

# Instalacja / aktualizacja

Pakiet nie jest dostępny na CRAN, więc trzeba instalować go ze źródeł.

Instalację najprościej przeprowadzić wykorzystując pakiet *devtools*:

```r
install.packages('devtools') # potrzebne tylko, gdy nie jest jeszcze zainstalowany
devtools::install_github('bartplat/MLASZraportyR3F2', build_opts = c("--no-resave-data"))
```
Pakiet `MLASZraportyR3F2` jest zależny od pakietu `MLASZraporty`, ale nie ma potrzeby go dodatkowo instalować, ponieważ dzieje się to podczas instalacji pakietu `MLASZraportyR3F2`.

Dokładnie w ten sam sposób można przeprowadzić aktualizację pakietu do najnowszej wersji.

# Użycie

Do generowania raportów służy funkcja `generuj_raporty()` z pakietu `MLASZraporty`. Jej przykładowe wywołanie wygląda następująco:

```r
library(MLASZraportyR3F2)
generuj_raporty(
  pakiet = "MLASZraportyR3F2",
  szablon = "raport_szkola_r3f2.Rmd",
  wskazniki = szk,
  wskaznikiGrPor = woj,
  kolumnaNazwaPliku = nazwa_pliku,
  parametry = list(typDokumentu = "pdf",
                   progLiczebnosci = 10,
                   wyrownanieTabWykr = "center",
                   plikZObiektami = "../data/wskR3F2.RData",
                   obiektWskazniki = "szk",
                   obiektWskaznikiPorownanie = "woj")
)
```

Raporty zostaną utworzone w aktywnym folderze. Jeśli nie jesteś pewien, jaki to folder, użyj funkcji `getwd()` i ew. funkcji `setwd()`, aby go zmienić.

Zbiór wskaźników, oprócz kolumn wygenerowanych za pomocą pakietu `MLASZdaneR3F2`, powinien zawierać także kolumnę z nazwą każdego z generowanych raportów - argument `kolumnaNazwaPliku` w funkcji `generuj_raporty()`. Nie jest ona tworzona w wyniku działania funkcji pakietu `MLASZdaneR3F2`, więc trzeba ją dodać samemu. Przykładowe nazwy plików składające się z ID RSPO szkoły oraz dopisku "raport_v1" można stworzyć w następujący sposób:

```r
szk = szk %>% 
  mutate(nazwa_pliku = paste0(id_rspo, "raport_v1"))
```
