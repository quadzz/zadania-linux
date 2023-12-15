# Wprowadzenie

Przejdź do katalogu domowego, następnie do katalogu nadrzędnego i katalogu głównego. Wykorzystaj odpowiednie parametry. Na koniec wróć do katalogu domowego. 

Utwórz katalog o nazwie TwojeImie, następnie stwórz trzy podkatalogi nazwie katalogA, katalogB i katalogC za pomocą jednej komendy. 

Zmień nazwę katalogC na KatalogDoUsuniecia, a następnie go usuń.

W katalogB utwórz pliki o nazwie plikA, plikB, plikC.

Przenieś zawartość katalogB do katalogA, a następnie skopiuj plikA z katalogA do katalogB, zmieniając jego nazwę na plikTymaczasowy.

Utwórz, wpisując kilka dowolnych linijek tekstu, w katalogB plik tekstowy o nazwie plikDoDowiazania. Utwórz dowiązanie twarde o nazwie plikDowiazany do pliku plikDoDowiazania. Sprawdź zawartość pliku plikDowiazany. Zmień plik w edytorze tekstowym i sprawdź, czy zawartość uległa zmianie. 

Usuń plik o nazwie plikDoDowiazania. Czy plikDowiazany nadal istnieje i wyświetla jakąś zawartość? 

Utwórz dowiązanie symboliczne o nazwie plikDowiazany2 do plikDowiazany i wykonaj operacje jak przy dowiązaniu twardym. Sprawdź różnice między dowiązaniami.

Usuń katalogB. 

# Operacje na plikach

Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym zaczynające się od kropki.

Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym kończące się tyldą (~).

Wyszukaj wszystkie katalogi w swoim katalogu domowym kończące się tyldą (~) lub rozpoczynające się od kropki.

Wyszukaj wszystkie pliki tekstowe o nazwie kończącej się rc i wyświetl ich zawartość za pomocą edytora tekstowego.

Przejdź do katalogu /tmp/. Utwórz katalog /tmp/test/ i utwórz w nim pliki asia, basia, casia, dasia, easia, fasia. Za pomocą komendy find usuń wszystkie pliki z katalogu /tmp/test/, których nazwy składają się z napisu asia poprzedzonego dowolną literą.

Utwórz pliki i katalogi jak powyżej. Usuń wszystkie pliki z katalogu /tmp/test/, których nazwy składają się z napisu asia poprzedzonego dowolną literą. Niech przed usunięciem pliku komenda find zażąda potwierdzenia od użytkownika.

Znajdź największy katalog w katalogu /etc.

# Procesy

Uruchom nieskończony ping na stronę www.wp.pl i przekieruj output komendy do pliku diagnostyka.txt. Polecenie uruchom w trybie deamona.

Wyświetl 5 procesów najbardziej obciążających pamięć RAM procesów z przestrzeni wszystkich procesów (nie tylko obecnego użytkownika) zachowując strukturę: PID: 1234 Nazwa: x/y/z Zużycie pamięci: 2137

Wyświetl wszystkie procesy związane z protokołem ssh, a następnie wyświetl je w następującym formacie (pomiń proces grepa). Nazwa procesu nie powinna zawierać dwukropka na końcu

Pobierz repozytorium https://github.com/navdeep-G/samplemod<br/>
Wyświetl wszystkie pliki pythona, jakie znajdują się w repozytorium Ze wspomnianych plików, wyświetl łączną liczbę ich linijek

Wypisz wszystkie procesy wykonujace komendę bash

# systemd
Pobierz poniższy plik binarny node_exportera.
(`cd /tmp && curl -OL https://github.com/prometheus/node_exporter/releases/download/v1.2.2/node_exporter-1.2.2.linux-amd64.tar.gz`)
(cd /tmp && tar -xvf /tmp/node_exporter-1.2.2.linux-amd64.tar.gz)

Utwórz użytkownika o nazwie node_exporter z katalogiem domowym

Utwórz grupę o takiej samej nazwie

Dodaj użytkownika node_exporter do grupy node_exporter

Przenieś pobraną binarkę do katalogu /user/local/bin oraz dodaj prawa własności użytkownika i grupy na node_exporter

W katalogu /etc/systemd/system utwórz plik usługi node_exportera o nazwie node_exporter.service

W utworzonym katalogu wklej poniższą konfigurację
```text
[Unit]
Description=Node Exporter
Requires=node_exporter.socket

[Service]
User=node_exporter
EnvironmentFile=/etc/sysconfig/node_exporter
ExecStart=/usr/sbin/node_exporter --web.systemd-socket $OPTIONS

[Install]
WantedBy=multi-user.target
```
Wykonaj przeładowanie konfiguracji daemonów przy pomocy systemctl daemon-reload

Następnie wykorzystując polecenie systemctl uruchom usługę node_exportera Sprawdź status uruchomionej usługi oraz czy usługa będzie uruchomiona przy restarcie systemu

Określ PID uruchomionego procesu

Zabij określony proces

Zweryfikuj czy proces przestał działać, sprawdź również status usługi

Zrestartuj usługę z poziomu komendy systemctl i zweryfikuj status jej aktywności

# Skrypty

Napisz skrypt, który będzie wyświetlał zawartość katalogu, który zostanie przekazany do skryptu jako argument wywołania.

Napisz skrypt, który poprosi użytkownika o podanie dwóch liczb, a następnie wyświetli ich sumę, różnicę, iloczyn i iloraz.

Napisz skrypt, zliczający liczbę linii w syslogu (/var/log/syslog).

Napisz skrypt zliczający liczbę plików o podanym rozszerzeniu w zadanym katalogu. Typ rozszerzenia ma być podawany do pliku jako zewnętrzny argument. Do tego możesz wykorzystać repozytorium pobrane w ćwiczeniu dotyczącym przetwarzania strumieni danych

Zaimplementuj dziecięcą grę FizzBuzz Wypisz wszystkie liczby od 1 do 100, jednak jeżeli liczba jest podzielna przez poniższe liczby wygeneruj obok odpowiedni napis:
* 3 – wypisz „Fizz” 
* 5– wypisz „Buzz” 
* 3 i 5 wypisz „FizzBuzz”. 

Zaimplementuj powyższy kod z wykorzystaniem funkcji. Do funkcji fizzbuzz przekazywany jest parametr – maksymalna liczba generacji liczb
