# Wzorzec Projektowy Strategia - przykład Kuchcika

Jest to implementacja przykładu z Wyzwania Projektowego odbywającego się w lutym 2021.<br/>
Kod dla Strategii znajduje się w pakiecie `strategy`.<br/>

## Jaki problem rozwiązuje Strategia?
Jak skoponować klasy, gdy jest więcej niż jeden sposó zrobienia czegoś. <br/>
Na przykład - jest więcej niż jeden sposób wyrabiania ciasta (mikserem lub recznie)<br/>
i kucharz może skorzystać z obu. Strategia doradza, jakie klasy utworzyć i jak je ze sobą połączy
ć.<br/>
Całość opiera się na interfejsie `SposóbWyrabiania` oraz jego dwóch implementacjach (ręcznym lub
 mikserem).<br/>
 Kuchcik ma w sobie pole sposobu wyrabiania i może wyrabiać ciasto używając metody z tego pola
 , korzystając z polimorfizmu.

## Jak wygląda Strategia tutaj?
Całość jest do zobaczenia tutaj:
![Alt text](pictures/KuchcikStrategia.jpg?raw=true "Gdzie Strategia?")

Jednak tutaj wszystkie klasy są nazwane po angielsku: <br/>
1. `Kuchcik` w projekcie nazywa się `Cook`
2. `SposóbWyrabiania` - `DoughKneadWay`
3. `RęczneWyrabianie` - `ManualKneadWay`
4. `WyrabianieMikserem` - `AutomatedKneadWay`
5. `Ciasto` - `Dough` <br/>
<br/>
`Runner` to `Runner` i w nim jest zawarta metoda `main`.<br/>
Tutaj jeszcze są zapisane wyjątki oraz testy. 

# Wzorzec Projektowy Budowniczy - przykład Pacjenta

Jest to implementacja wzorca Budowniczego z Wyzwania Projektowego odbywającego się w lutym 2021
.<br/>
Kod dla Budowniczego znajduje się w pakiecie `builder`.<br/>

## Jaki problem rozwiązuje Budowniczy?
Jak stworzyć obiekt, który składa się z dużej ilości pól.<br/>
Oczywiście, możnaby stworzyć jeden wielki konstruktor, jednak programista szybko by się pogubi
ł, który parametr w konstrkutorze to które pole.<br/>
Inną opcją byłoby wywoływanie setterów dla pól... i poniekąd czymś podobnym jest właśnie
 Budowniczy.<br/>
 <br/>
 Całość opiera się na stworzeniu nowej statycznej klasy, która będzie budować klasę Pacjenta. <br/>
 W naszym przykładzie Pacjent potrzebuje aż siedmiu danych i chcemy uniknąć robienia siedmio
 -parametrowego konstruktora.<br/>
 W `Pacjencie` konstruktor musi byc prywatny - nie chcemy umożliwiać korzystania z niego innym <br/>
 oraz powinien przyjmować jako parametr `PacjentBuilder`. I brać po kolei z niego pola i ustawia
 ć ich wartość swoim polom.
 W nowej statycznej klasie trzeba skopiować wszystkie pola z Pacjenta oraz<br/>
 dodać dla każdego pola metody ustawiające pole w Builderze i zwracające obiekt budujący.<br/>
 Oraz specjalną metodę `build()`, która ostatecznie wywoła prywatny konstruktor `Pacjenta` i jako
  parametr przekaże siebie (this).
  
  ## Jak wygląda Budowniczy tutaj?
  Całość jest do zobaczenia tutaj:
  ![Alt text](pictures/Builder.png?raw=true "Gdzie Budowniczy?")
  
# Wzorzec Projektowy Adapter - przykład Ladowarki

Jest to implementacja wzorca Adapter z Wyzwania Projektowego odbywającego się w lutym 2021
.<br/>
Kod dla Adaptera znajduje się w pakiecie `adapter`.<br/>

## Jaki problem rozwiązuje Adapter?
Adapter pomaga zaadaptować jedną klasę na potrzeby innej. <br/>
Przykładem, którym się tu posługuję, jest adaptacja prądu 220V na 19V. I tak, wiem, że w <br/>
rzeczywistości jest jeszcze kwestia prądu zmiennego i stałego, ale trochę <br/>
sobie uprośćmy - i ustalmy, że jest tylko adaptacja `220` na `19` :) <br/>
<br/>
Laptop potrzebuje zasilania `19V`, a w gniazdku elektrycznym w ścianie mamy `220V`. <br/> 
*Co teraz?* <br/>
Całość rozwiązania tak na prawdę sprowadza się do podzielenia prądu `220V` (tego z gniazdka
 elektrycznego) przez`11.5` tak, aby uzyskać prąd `19V` (tyle potrzeba laptopowi). <Br/>
 Dzieje się to w klasie `SocketAdapter
 ` (jak sama nazwa wskazuje). <br/>
<br/>
Kod składa się z następujących klas:
* `Laptop` - klasa reprezentująca laptopa, który posiada w sobie pole klasy
* `Charger` - czyli ładowarki. Jest to interfejs z metodą `give19V`
* `Socket` - gniazdko elektryczne wraz z metodą `give220V` zwracającą prąd 220V
* `SocketAdapter` - nasz adapter prądu z gniazdka (posiadający takie pole) na prąd 19V
<br/>
<br/>
Tak jak wspomniane w definicji wzorców, niezawsze wzorce to skomplikowany układ klas.<br/>
Tak będąc całkiem przyziemnym, tutaj wzorcem jest raptem działanie matematyczne (dzielenie)<br/>
i mądre ułożenie klas tak, aby można było użyć tego dzielenia w ogóle.

  
  ## Jak wygląda Adapter tutaj?
  Całość jest do zobaczenia tutaj:
  ![Alt text](pictures/Adapter.png?raw=true "Gdzie Adapter?")
  
# Wzorzec MVC - Model View Controller (Model Widok Kontroler)

Ten wzorzec nie znajduje się w książce `Wzorce Projektowe` Gang of Four, ale jest bardzo często
 stosowany w projektach z graficznym interfejsem użytkownika. *Graficzny interfejs użytkownika
 * to nic innego, jak wszystko to, co widzisz w programie - przyciski, kolory, coś się wyświetla
 , coś możesz kliknąć.<br/>
`MVC` to wzorzec architektoniczny - pomaga porozdzielać odpowiedzialności klas w przypadku
 projektu z GUI (graficznym interfejsem użytownika).<br/>
 Niektórzy patrzą na `MVC` jako zbiór kilku podstawowych wzorców - Strategii, Kompozytu
 , Obserwatora. Inni rozszerzają tą listę jeszcze bardziej. <Br/>
 W tym przykładzie jednak jest to bardzo uproszczone.
 
 # Jaki problem rozwiązuje?
 W aplikacjach z GUI pomaga podzielić system na części:
 * część Widoku - czyli wszystko to, co widzi użytkownik, w co może kliknąć...
 * część Kontrolerów - czyli to, co przyjmie zachowania użytkownika i co umie wyzwolić inną akcj
 ę po wciśnięciu przycisku przez użytkownika
 * część Modelu - czyli punkt główny programu, odzwierciedlenie całości problemu w kodzie. Model
  może zmieniać swój stan (i ta zmiana może być potem odwzorowana w widoku). Modelu nie "wida
  ć".
  
 `MVC` można porównać do działania człowieka: `View` to nasza skóra (tylko to widzimy
 ), `Controller` to mięśnie (mięśnie pod wpływem dotknięcia gorącej kuchenki przez skórę si
 ę kurczą), a `Model` to mózg, który wszystkim zawiadamia. Jeśli się poparzymy, mózg będzie mia
 ł zmieniony stan (uszkodzenie części systemu) i również i widok się zmieni (skóra zaczerwieni).
 
 # Wykres i ogólna zasada działania
 Ogólna zasada brzmi tak: użytkownik widzi widok. Jedno akcje odbierane są przez kontroler
 . Kontroler zleca zmianę stanu modelowi. Model informuje widok, że zmienił się mu stan, a widok
  się odświeża.
  ![Alt text](pictures/MVC-ogolne.jpg?raw=true "Ogólna zasada?")
  
  
  
 <br/>
 
# Przykład z kodu
Przykład zawarty w pakiecie `mvc` przedstawiaj bardzo prostą aplikację pokazującą Słońce i jego
 moc grzewczą, ustawianą przez użytkownika aż do podania przez niego wartości mniejszej od 0.<br/>
 Jest to oparte na trzech klasach, tak aby w prosty sposob pokazać MVC:
 * `WeatherController` - kontroler, który wie, co ma zrobić, gdy użytkownik poda liczbę. Posiada
  jako pole `WeatherModel` i zmienia mu stan (moc grzewczą), gdy zachodzi potrzeba
 * `WeatherModel` - tak na prawdę to nasze Słońce. Posiada moc grzewczą oraz możliwo
 ść informowania obserwujących go klas o zmianie w swoim stanie (czyli informuje `WeatherView` w
  metodzie `notifyObservers`)
 * `WeatherView` - klasa, która wyświetla Słońce z jego mocą grzewczą podaną prez użytkownika
 . Posiada jako pole `WeatherController` - i używa jej, gdy czas dla użytkownika podać liczb
 ę, oraz `WeatherModel` - bo to z niego wyciąga stan (moc grzewczą).
 
![Alt text](pictures/mvc-diagram.png?raw=true "Jak wyglądają klasy?")
  <br/>

 A tak wygląda działania MVC w przykładzie:

![Alt text](pictures/mvc-example.png?raw=true "MVC w praktyce")
 
 