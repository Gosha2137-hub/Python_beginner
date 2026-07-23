# Statistics
python in use
Let's focus on method from pandas called: **.describe()**  
Służy ono do **autoamtycznego generowania zestawu podstawowych statystyk opisowych** dla każdej numerycznej kolumny w DataFrame.  

## Parametry
Output zawiera następujące parametry:  
1. ***count*** (Liczebność) : Informuje, ile prawidłowych(niepustych) pomiarów znajduje się w kolumnie.
2. ***mean*** (Średnia arytmetyczna)
3. ***std*** (Odchylenie Standardowe) : Miernik rozrzutut danych wokół średniej. Mówi o stabilności rozkładu badanej zmiennej.
4. ***min*** (Wartość Minimalna)
5. ***25%*** (Pierwszy kawartyl - $Q_1$) : wartość, powyżej której znajduje się 25% wszytkich pomiarów.
6. ***50%*** (Drugi kwartyl/ Mediana - $Q_2$) : Środkowa wartość w uporządkowanym zbiorze danych. Jeśli mediana mocno różni się od średniej, to znak, że rozkład stężenia radonu jest asymetryczny.
7. ***75%*** (Trzeci kwartyl - $Q_3$) : Wartość, poniżej której znajduje się 75% pomiarów.
8. ***max*** (Wartość maksymalna)

Kolejna parametry opisujące ***Kształt rozkładu***:  
* ***Skośność (Skewness)*** : Asymetria rozkładu, czyli czy dane są rozłożone symetrycznie wokół średniej, czy też rozkład "pochyla się" w którąś stronę, tworząc długi ogon.
  * Interpretacja:
    * Skośność = 0 : Rozkład symetryczny
    * Skośność > 0 : Skośność prawostronna - Wykres ma długi ogon po prawej stronie. Oznacza to, że większość pomiarów jest niska, ale pojawiają się nieliczne bardzo wysokie wartości. Średnia jest większa od mediany.
    * Skośność < 0 : Skośność lewostronna - Wykres na długi ogon po lewej stronie. Oznacza to, że większość wartości jest wysoka, a nieliczne są bardzo niskie. Średnia jest mniejsza od mediany.
* ***Kurtoza(Kurtosis)*** : Skupienie i "grubość ogonów", czyli jak bardzo wartości są skoncentrowane wokół średniej oraz jak "ciężkie" lub "grube" są ogony rozkładu (czyli jak duże jest prawdopodobieństwo wystąpienia wartości skrajnych).
  * Interpretacja:
    * Kurtoza = 0 : Rozkład mezokurtyczny , odpowiada idealnemu rozkładowi normalnemu.
    * Kurtoza > 0 : Rozkład leptokurtyczny - "smukły", Wykres jest bardzo strzelisty w centrum, a jego ogony są grube. Oznacza to, że dane są mocno skupione wokół średniej, ale jednocześnie ryzyko pojawienia się nagłych, akstremalnych wartosci jest wyższe niż w standardowym rozkładzie normalnym.
    * Kurtoza < 0 : Rozkład platokurtyczny - "spłaszczony", Wykres jest bardziej płaski, przypomina rozjechany pagórek. Dane są bardziej rozproszone, a wartości skrajne wystepują rzadko.
   
 ## Wizualizacja Danych

  Tutaj skupimy się na dwóch ważnych metodach przedstawia danych.
  * **Histogram**
    * Pokazuje kształt i gęstość rozkładu, dzieli cały zakres danych na równe przedziały, a wysokość słupka pokazuje, jak wiele pomiarów wpadło do danego przedziału.
  * **Boxplot**
    * Pudełko (Kwartyle) : Dolna krawędz to $Q_1$, górna to $Q_3$, a linia w środku to Mediana. Szerokość pudełka pokazuje, w jakim zakresie mieści się połowa nabardziej typowych pomiarów.
    * Wąsy (Whiskers) : Pokazują statystyczny zasięg "normalnych" danych.
    * Outliery (Kropki poza wąsami) : Anomalie
## Współczynniki Korelacji  
### Współczynnik korelacji Pearsona (r)  
Mierzy liniową zależność między dwiema zmiennymi ciągłymi.Sprawdza, czy punkty na wykresie układają się wzdłuż prostej linii.  
* Stosujemy gdy dane są ciągłe, nie mają silnych wartości odstających i wykazują prostoliniowy trend.
* Współczynnik ten bada czy wraz ze wzrostem zmienne X zmienna Y rośnie/spada w stałym proporcjonalnym tempie.
* Jest bardzo wrażliwy na wartości odstające.
### Współczynnik korelacji Spearmana ($\rho$ lub $r_s$)  
MIerzy monotoniczną zależność na podstawie rang (kolejności) danych, a nie bezpośrednich wartości numerycznych.  
* Stosujemy gdy zależność jest nieliniowa, dane są porządkowe lub występują wartości odstające.
* Współczynnik ten bada czy wraz ze wzrostem zmiennej X zmienna Y ma tendencję do wzrostu/spadku, niezależnie od tego, czy tempo tej zmiany jest stałe.
* Jest odporny na pojedyńcze wartości odstające,ponieważ przelicza dane na ich pozycje w szeregu(rangi).
### Interpretacja Wartości Współczynników  
Oba współczynniki przyjmują wartości z przedziału [-1,1]. Znak mówi o kierunku, a wartość bezwzględne o sile relacji.  
* Dla **Wartości dodatniej** : Korelacja dodatnia, zależność rosnąca.
* Dla **Warości ujemnej** : Korelacja ujemna, zależność malejąca.
* Dla **Wartości bliskiej zero** : Brak zależności, zmienne są od siebie niezależne.
Z kolei dla wartości bezwzględnych z przedziałów:
* 0.0-0.2 : Brak lub bardzo słaba zależność
* 0.2-0.4 : Słaba korelacja
* 0.4-0.7 : Umiarkowana/średnia korelacja
* 0.7-0.9 : Silna korelacja
* 0.9-1.0 : Bardzo silna korelacja

**Zapamiętaj : Korelacja nie oznacza przyczynowości**  
Wysoki współczynnik korelacji mówi jedynie o tym, że zmienne zmieniają się razem, ale nie dowodzi sam w sobie, że jedna jest bezpośrednią przyczyną drugiej.
