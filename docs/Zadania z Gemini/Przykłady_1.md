# Zadanie 1
## Wstępne przetwarzanie i synchronizacja danych z czujników 
  * W laboratorium zostanie rozmieszczona sieć czujników radonu i parametrów środowiskowych. Dane z różnych urządzeń mogą mieć różne kroki czasowe lub brakujące wartości.
      1. Wygeneruj za pomocą **numpy** dwa sztuczne pliki CSV: pierwszy z pomiarami radonu (co 10 minut), drugi z pomiarami temperatury i wilgotności (co 15 minut).
      2. Wczytaj oba pliki za pomocą **pandas**, przekształć kolumny z czasem na format **datetime** i ustaw je jako indeks (**DatetimeIndex**).
      3. Połącz oba zbiory danych w jeden obiekt DataFrame tak, aby miały wspólny krok czasowy (np. co 10 minut). Wykorzystaj metodę **merge_asof** lub **resample()** ze strategią interpolacji liniowej dla brakujących danych środowiskowych.
      4. Oczyść dane: zidentyfikuj i usuń ewentualne wartości odstające (np. ujemne stężenia radonu będące błędem czujnika).
