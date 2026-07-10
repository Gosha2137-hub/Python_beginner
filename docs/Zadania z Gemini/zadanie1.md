```python
import pandas as pd
import numpy as np
print("Wszystko działa!")
```

    Wszystko działa!
    

# Zadanie 1  

## Wstępne przetwarzanie i synchronizacja danych z czujników 
  * W laboratorium zostanie rozmieszczona sieć czujników radonu i parametrów środowiskowych. Dane z różnych urządzeń mogą mieć różne kroki czasowe lub brakujące wartości.
      1. Wygeneruj za pomocą **numpy** dwa sztuczne pliki CSV: pierwszy z pomiarami radonu (co 10 minut), drugi z pomiarami temperatury i wilgotności (co 15 minut).
      2. Wczytaj oba pliki za pomocą **pandas**, przekształć kolumny z czasem na format **datetime** i ustaw je jako indeks (**DatetimeIndex**).
      3. Połącz oba zbiory danych w jeden obiekt DataFrame tak, aby miały wspólny krok czasowy (np. co 10 minut). Wykorzystaj metodę **merge_asof** lub **resample()** ze strategią interpolacji liniowej dla brakujących danych środowiskowych.
      4. Oczyść dane: zidentyfikuj i usuń ewentualne wartości odstające (np. ujemne stężenia radonu będące błędem czujnika).

## Krok 1: generowanie sztucznych danych


```python
import pandas as pd
import numpy as np

np.random.seed(42) # Ustawienie ziarna losowości

#Generowanie zakresu dat na 3 dni
czas_radon = pd.date_range(start="2026-01-01 00:00", end="2026-01-04 00:00", freq="10min")
czas_pogoda = pd.date_range(start="2026-01-01 00:00", end="2026-01-04 00:00", freq="15min")

radon_values = np.random.normal(loc=40, scale=10, size=len(czas_radon))

radon_values[15]=-999.0
radon_values[120]=-5.0

df_radon = pd.DataFrame({"Data_Czas":czas_radon,"Radon_Bq_m3": radon_values})

#Tworzenie danych pogodowych
temp_values=np.random.normal(loc=18, scale=2,size=len(czas_pogoda))
wilg_values=np.random.normal(loc=50,scale=5, size=len(czas_pogoda))

df_pogoda=pd.DataFrame({
    "Data_Czas":czas_pogoda,
    "Temperatura_C":temp_values,
    "Wilgotnosc_proc":wilg_values
})

#Zapis do plików CSV
df_radon.to_csv("czujnik_radon.csv", index=False)
df_pogoda.to_csv("czujnik_pogoda.csv", index=False)

print("Plik CSV zostały wygenerowane pomyślnie!")
```

    Plik CSV zostały wygenerowane pomyślnie!
    

## Ziarnostość  
podając konkretną liczbę jako seed, algorytm zawsze wystartuje z tego samego miejsca i wypluje **dokładnie taką samą sekwencję liczb**  
W przypadku braku konkretnego **seed**, Python wybierze stronę startową na podstawie aktualnego czasu systemowego, więc za każdym razem trafimy w inne miejsce i wyniki będą wyglądać na całkowicie losowe  
**Zatem głównym celem seed jest odtwarzalność eksperymentów**

## Zapamiętaj Funkcje:  

**pd.date_range(start="...", end="...",freq="...")**  
* generowanie stałych sekwencji dat, z następującymi parametrami  
    * start
    * end
    * periods - liczba okresów (generowanych dat), które chcesz uzyskać
    *freq - częstotliwość, z jaką daty mają być generowane, wyróżniamy  
        * "D" - dzień kalendarzowy
        * "B" - dzień roboczy (bez weekendów)
        * "H" - godzina
        * "T" lub "min" - minuta
        * "W" - Tydzień
        * "M" - ostatni dzień miesiąca
        * "MS" - Pierwszy dzień miesiąca
        * "YS" - Pierwszy dzień roku


**np.random.normal(loc= ,scale= ,size= )**  
* loc - wartość oczekiwana rozkładu normalnego
* scale - Odchylenie standardowe
* size - Określa, ile liczb chcesz wygenerować i w jakiej strukturze(wymiarze), możemy podawać w postaci krotki (liczba wygenerowanych danych - wierszy, na ile kolumn)


**.to_csv(index= ,sep= ,encoding= ,columns= ,na_rep= )**  
* index - Domyślnie Pandas zapisuje do pliku pierwszą kolumnę z indeksami. Aby to wyłączyć uwzględniamy **index=False**
* sep - separator, domyśnie kolumny rodzielone przecinkie
* encoding - Jeśli w pliku mamy polskie znaki to należy uwzględnić **encoding='utf-8'**
* columns - można wyróżnić kolumny które chcemy zapisać w pliku, podajemy je w postaci listy **columns=['kolumna1', 'kolumna2']**
* na_rep - Decyduje, jak mają zostać zapisane brakujące dane (NaN). Domyślnie zostawia puste pola, ale można ustawić np. **na_rep='Brak'**

## Krok 2: Wczytanie danych i ustawienie indeksu datetime


```python
#Wczytanie Plików
df_r = pd.read_csv("czujnik_radon.csv")
df_p = pd.read_csv("czujnik_pogoda.csv")

#Konwersja kolumny tekstowej na format Datetime
df_r["Data_Czas"] = pd.to_datetime(df_r["Data_Czas"])
df_p["Data_Czas"] = pd.to_datetime(df_p["Data_Czas"])

#Ustawienie czasu jako indeksu tabeli
df_r.set_index("Data_Czas", inplace=True)
df_p.set_index("Data_Czas",inplace=True)

print("Dane wczytane. Indeks ustawiony na format Datetime.")
print("\nPierwsze wiersze danych radonu:")
print(df_r.head(3))
```

    Dane wczytane. Indeks ustawiony na format Datetime.
    
    Pierwsze wiersze danych radonu:
                         Radon_Bq_m3
    Data_Czas                       
    2026-01-01 00:00:00    44.967142
    2026-01-01 00:10:00    38.617357
    2026-01-01 00:20:00    46.476885
    

### Zapamiętaj Funkcje!

**pd.read_csv()**

**pd.to_datetime()**  
* Gdy Pandas wczytuje plik CSV, kolumnę z datą i godziną domyślnie traktuje jak zwykły tekst (string). to_datetime() bierze tektową kolumnę (tutaj df_r["Data_Czas"]), analizuje zapisane tam znaki i zamienia je na specjalne obiekty typu **datetime64**

**.set_index()**  
* parametr inplace=True - zmian dokonujemy na oryginela

## Krok 3 : Czyszczenie Danych - Usuwanie wartości odstających


```python
bledy = df_r[df_r["Radon_Bq_m3"]<0]
print(f"Znaleziono błędy pomiarów: {len(bledy)}")

df_r.loc[df_r["Radon_Bq_m3"]<0,"Radon_Bq_m3"] = np.nan

df_r["Radon_Bq_m3"] = df_r["Radon_Bq_m3"].interpolate(method="linear")

print("Czyszczenie zakończone. Błędy zostały poprawione poprzez interpolację")
```

    Znaleziono błędy pomiarów: 0
    Czyszczenie zakończone. Błędy zostały poprawione poprzez interpolację
    

### Zapamiętaj Funkcje

**nazwa_pliku.loc[warunek na wiersze, 'nazwa kolumny']**  
* loc to metoda służąca do wybierania wierszy i kolumn na podstawie etykiet lub warunków logicznych.
* Idealnie nadaje się do filtrowania i masowego nadpisywania danych **nazwapliku.loc[warunek,nazwa kolumn]=np.nan** - Tutaj dla wszystkich wierszy w których warunek został spełniony dotychczasowa wartość zostaje zamieniona na wartość NaN


**df_r["Radon_Bq_m3"]=df_r["Radon_Bq_m3"].interpolate(method="linear")**  
* Uzupełniamy barakujące dane (wiersze z NaN) za pomocą interpolacji liniowej

## Krok 4: Synchronizacja i łączenie danych


```python
df_p_10min = df_p.resample("10min").interpolate(method="linear")

df_final= pd.merge(df_r, df_p_10min, left_index=True, right_index=True, how="inner")

print("Połączenie udane! Oto podgląd zsynchronizowanej tabeli:")
print(df_final.head(10))

df_final.to_csv("jurlab_czyste_dane.csv")
```

    Połączenie udane! Oto podgląd zsynchronizowanej tabeli:
                         Radon_Bq_m3  Temperatura_C  Wilgotnosc_proc
    Data_Czas                                                       
    2026-01-01 00:00:00    44.967142      19.435085        43.259073
    2026-01-01 00:10:00    38.617357      19.006120        45.790824
    2026-01-01 00:20:00    46.476885      18.577155        48.322576
    2026-01-01 00:30:00    55.230299      18.148190        50.854327
    2026-01-01 00:40:00    37.658466      17.178725        50.600275
    2026-01-01 00:50:00    37.658630      16.209261        50.346222
    2026-01-01 01:00:00    55.792128      15.239797        50.092170
    2026-01-01 01:10:00    47.674347      16.122833        49.161847
    2026-01-01 01:20:00    35.305256      17.005869        48.231524
    2026-01-01 01:30:00    45.425600      17.888905        47.301202
    

### Zapamiętaj Funkcje

**df_p.resample()**  
* Metoda w Pandas służy do zmiany częstotliwości (próbkowania) danych czasowych. Jest stworzona specjalnie dla obiektów z indeksem typu *DatetimeIndex*  
* W naszym przykłądzie z pomiarów co 15 minut chcemy stworzyć pomiary co 10 minut  
* W połączeniu: *.resample().interpolate(method="linear")* zmienia nam częstotliwość próbkowania z jednoczesnym zapełnianiem pustych miejsc przy użyciu interpolacji 

**pd.merge(tabela1, tabela2, left_index, right_index,how)**  
* polecenie merge służy do łączenia dwóch różnych tabel w jedną na podstawie wspólnego klucza.  
    * u nas łączymy dane z czujnika radonu z danymi pogodowymi  
* left_index = True - w lewej tabeli użyj indeksu jako punktu wspólnego  
* right_index = True - w prawej tabeli również użyj indeksu do dopasowania wierszy  
    * tzn. że tabele będą łączone po dacie i czasie  
* how ="inner" - parametr how decyduje o strategii łączenia, gdyby w którejś tabeli brakowało konkretnych dat. Wartość "inner" czyli część wspólna, działa w taki sposób że,  
    * do nowej tabeli trafiają tylko te daty i godziny, które istneiją jednocześnie w obu tabelach
