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
