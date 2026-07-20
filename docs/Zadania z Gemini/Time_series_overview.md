# Time Series
Notes based on lecture Dr. Jarosław Kotwicz , Szeregi Czasowe - część I Instytut Informatyki Uniwersytet w Białymstoku

## Dane Statystyczne
Ogólna Klasyfikacja:  
1. **Dane przekrojowe** (cross sectional data) :  wiele jednostek obserwowanych w jednej jednostce czasu.
2. **Szeregi czasowe** (time series data) : jedna jednostka obserwowana w wielu jednostkach czasu.
3. **Dane panelowe** (panel data, cross sectional time series data) : wiele jednostek obserwowanych w wielu jednostkach czasu.

## Szeregi Czasowe
### Definicja
* Szeregiem czasowym nazywamy zbiór wartości badanej cechy, zaobserwowaneych w różnych momentach (przedziałach) czasu. Jest on uporządkowany chronologicznie.
  * W rachunku prawdopodobieństwa odpowiednikiem szeregu czasowego jest ciąg zmiennych losowych, będący szczególnym przypadkiem procesu stochastycznego.
  * Niech t = 1,...,n będą momentami czasu, natomiast $y_t$ wynikami obserwacji pewnego zjawiska w danych momentach lub okresach czasu. Wtedy szereg czasowy jest zbiorem : { $y_t$ : t=1,..,n} = {(t,$y_t$) : t=1,...,n}
  * Równiedobrze {$Y_t$ : t=1,...,n} będzie ciągiem zmiennych losowych, zaś {$y_t$ : t =1,...,n} konkretną realizają tego ciągu. Wtedy szereg czasowy jest ciągiem zmiennych losowych {(t, $Y_t$) : t = 1,...,n} o określonym rozkłądzie łącznym.

 ### Składowe szeregu czasowego  
 1. **Tendencja rozwojowa - trend** : Własność szeregu ujawniająca się poprzez systematyczne, jednokierunkowe zmiany (wzrost lub spadek) poziomu badanego zjawiska w długim okresie czasu. *W wypadku trendu na zjawisko oddziaływuje stale pewnien zbiór wyników nazywany przyczynami głównymi*
 2. **Wahania cykliczne/koniunkturalne - skłądowa cykliczna** : Długookresowe, falowe inaczej rytmiczne wahania wokół tendencji rozwojowej. Obserwowane są one w dłuższych od roku okresach i ich analiza wymaga długoletnich obserwacji.
 3. **Wahania okresowe/sezonowe - składowa sezonowa** : Rytmiczne wahania wokół jego tendencji rozwojowej o określonym cyklu i okresie nie przekraczającym jednego roku. Rekrezentują efekty powtarzające się z pewną prawidłowością, co roku w tych samych okresach. Występują one często pod wpływem czynników przyrodnicznych lub kalendarza.
 4. **Wahania przypadkowe** : nazywana składową przypadkową, co sugeruje zawieranie przypadkowych wahań szeregu wokół części systematycznej, które trudno jest zdefiniować.
### Kryterium porównawcze
Składowe szeregu czasowego połączone mogą być związkami  
* **addytywnym** , wtedy dla sezonowości addytywnej mamy do czynienia z efektami sezonowymi polegajacymi na zaniżeniu lub zawyżeniu wartości zjawiska w okresach tego samego typu. *Wskaźnik addytywny jest dodawany do wartości trendu.*
*  **multiplikatywnym** , wtedy dla sezonowości multiplikatywnej efekty sezonowe są w przybliżeniu stałe w ujęciu procentowym. *Wskaźnik multiplikatywny jest przemnażany przez wartość trendu*

## Analiza Szeregów Czasowych  
Celem analizy szeregó czasowych jest zbudowanie modelu pewnego zjawiska/procesu w oparciu o obserwowane zmiany w czasie pewnych mierzalnych wielkości opisujących ten proces.  
Analiza szeregów czasowych obejmuje następujące zagadnienia:  
1. **Analiza opisowa szeregu czasowego** : wyznaczanie średniej arytmetycznej, wariancji, odchylenia standardowego idt.
2. **Porównanie poziomów zjawiska w czasie** : analiza dynakimi zjawisk z wykorzystaniem miar dynamiki
3. **Dekompozycja szeregu czasowego** :
 * **Wyodrębienie trendu** : ilustrującego działanie przyczyn głównych
 *  **Wyodrębnienie wahań sezonowych** : polega na wyznaczaniu wskaźników sezonowości zwanych również wskaźnikami okresowości lub wskaźnikami wahań sezonowych.
 *   **Wyodrębnienie wahań przypadkowych** : ilustrujących działania przyczyn przypadkowych, efekt ich odziaływania wyraża się za pomocą odchylenia standardowego reszt.  

