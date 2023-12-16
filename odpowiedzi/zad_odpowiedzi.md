# Wprowadzenie

Przejdź do katalogu domowego, następnie do katalogu nadrzędnego i katalogu głównego. Wykorzystaj odpowiednie parametry. Na koniec wróć do katalogu domowego. 
```shell 
cd ~ 
cd .. 
cd / 
cd ~ 
```
Utwórz katalog o nazwie TwojeImie, następnie stwórz trzy podkatalogi nazwie katalogA, katalogB i katalogC za pomocą jednej komendy. 
```shell 
mkdir -p TwojeImie/{katalogA,katalogB,katalogC}
#lub
mkdir -p TwojeImie/katalogA/katalogB/katalogC
``` 

Zmień nazwę katalogC na KatalogDoUsuniecia, a następnie go usuń.
```shell
mv TwojeImie/katalogC TwojeImie/KatalogDoUsuniecia 
rm -r TwojeImie/KatalogDoUsuniecia
```

W katalogB utwórz pliki o nazwie plikA, plikB, plikC.
```shell
touch TwojeImie/katalogB/{plikA,plikB,plikC}
```

Przenieś zawartość katalogB do katalogA, a następnie skopiuj plikA z katalogA do katalogB, zmieniając jego nazwę na plikTymaczasowy.
```shell
mv TwojeImie/katalogB/* TwojeImie/katalogA/ 
cp TwojeImie/katalogA/plikA TwojeImie/katalogB/plikTymaczasowy
```

Utwórz, wpisując kilka dowolnych linijek tekstu, w katalogB plik tekstowy o nazwie plikDoDowiazania. Utwórz dowiązanie twarde o nazwie plikDowiazany do pliku plikDoDowiazania. Sprawdź zawartość pliku plikDowiazany. Zmień plik w edytorze tekstowym i sprawdź, czy zawartość uległa zmianie. 
```shell
echo "Tekst do pliku" > TwojeImie/katalogB/plikDoDowiazania 
ln TwojeImie/katalogB/plikDoDowiazania TwojeImie/katalogB/plikDowiazany 
cat TwojeImie/katalogB/plikDowiazany 
vi TwojeImie/katalogB/plikDowiazany 
cat TwojeImie/katalogB/plikDowiazany
```

Usuń plik o nazwie plikDoDowiazania. Czy plikDowiazany nadal istnieje i wyświetla jakąś zawartość? 
```shell
rm TwojeImie/katalogB/plikDoDowiazania 
ls TwojeImie/katalogB/plikDowiazany 
cat TwojeImie/katalogB/plikDowiazany
```

Utwórz dowiązanie symboliczne o nazwie plikDowiazany2 do plikDowiazany i wykonaj operacje jak przy dowiązaniu twardym. Sprawdź różnice między dowiązaniami.
```shell
ln -s TwojeImie/katalogB/plikDowiazany TwojeImie/katalogB/plikDowiazany2 
ls -li TwojeImie/katalogB
```

Usuń katalogB. 
```shell
rm -r TwojeImie/katalogB
```

# Operacje na plikach

Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym zaczynające się od kropki.

```shell
ls -ld .*
# lub
find . -maxdepth 1 -name '\.*' -print
```

Wyszukaj wszystkie pliki lub katalogi w swoim katalogu domowym kończące się tyldą (~).
```shell
find ~ -name '*~'
```

Wyszukaj wszystkie katalogi w swoim katalogu domowym kończące się tyldą (~) lub rozpoczynające się od kropki.
```shell
find ~ -type d \( -name '*~' -o -name '.*' \)
# jezeli pliki ORAZ katalogi i przy uzyciu regexa
ls -la | egrep "\..*|.*~$"
```

Wyszukaj wszystkie pliki tekstowe o nazwie kończącej się rc i wyświetl ich zawartość za pomocą edytora tekstowego.
```shell
find ~ -type f -name '*rc' -exec cat {} \;
```

Przejdź do katalogu /tmp/. Utwórz katalog /tmp/test/ i utwórz w nim pliki asia, basia, casia, dasia, easia, fasia. Za pomocą komendy find usuń wszystkie pliki z katalogu /tmp/test/, których nazwy składają się z napisu asia poprzedzonego dowolną literą.

```shell
cd /tmp/ 
mkdir test 
touch test/{a,b,c,d,e,f}asia 
find test -name '?asia' -delete
```

Utwórz pliki i katalogi jak powyżej. Usuń wszystkie pliki z katalogu /tmp/test/, których nazwy składają się z napisu asia poprzedzonego dowolną literą. Niech przed usunięciem pliku komenda find zażąda potwierdzenia od użytkownika.

```shell
cd /tmp/ 
mkdir test 
touch test/{a,b,c,d,e,f}asia 
find test -name '?asia' -ok rm {} \;
```

Znajdź największy katalog w katalogu /etc.

```shell
du -hs /etc/* | sort -rh | head -1
```

# Procesy

Uruchom nieskończony ping na stronę www.wp.pl i przekieruj output komendy do pliku diagnostyka.txt. Polecenie uruchom w trybie deamona.
```shell
nohup ping www.wp.pl > diagnostyka.txt &
```

Znajdz powyzszy daemon i go zakończ
```shell
# skorzystaj z albo wyświetlonego ID procesu albo:
ps | grep ping
kill TUWPISZID
```

Wyświetl 5 procesów najbardziej obciążających pamięć RAM procesów z przestrzeni wszystkich procesów (nie tylko obecnego użytkownika) zachowując strukturę: PID: 1234 Nazwa: x/y/z Zużycie pamięci: 2137
```shell
ps -Ao pid,comm,%mem --sort=-%mem | head -n 6
# lub
top -bn 1 -o %MEM | grep "^ " | awk '{ printf("%-8s  %-8s  %-8s\n", $1, $10, $12); }' | head -n 6
```

Wyświetl wszystkie procesy związane z protokołem ssh, a następnie wyświetl je w następującym formacie (pomiń proces grepa). Nazwa procesu nie powinna zawierać dwukropka na końcu
```shell
ps aux | grep ssh | grep -v grep
```

https://github.com/navdeep-G/samplemod
Wyświetl wszystkie pliki pythona, jakie znajdują się w folderze ~/repo. Ze wspomnianych plików, wyświetl łączną liczbę ich linijek
```shell
find ~/repo -name '*.py' -exec wc -l {} \;
```

Wypisz wszystkie procesy wykonujace komendę bash
```shell
ps aux | grep bash
```


# systemd
Pobierz poniższy plik binarny node_exportera. 

dla ubuntu: `cd /tmp && curl -OL https://github.com/prometheus/node_exporter/releases/download/v1.2.2/node_exporter-1.2.2.linux-amd64.tar.gz` 

dla macOS: `curl -OL https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-arm64.tar.gz`

dla ubuntu: `cd /tmp && tar -xvf /tmp/node_exporter-1.2.2.linux-amd64.tar.gz` 

dla macOS: `cd /tmp && tar -xvf /tmp/node_exporter-1.7.0.linux-arm64.tar.gz`


Utwórz użytkownika o nazwie node_exporter z katalogiem domowym
```shell
# utworzy rowniez grupe i przypisze do grupy
sudo useradd -m node_exporter
```

Przenieś pobraną binarkę do katalogu /user/local/bin oraz dodaj prawa własności użytkownika i grupy na node_exporter
```shell
sudo mv node_exporter /usr/local/bin 
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
```

W katalogu /etc/systemd/system utwórz plik usługi node_exportera o nazwie node_exporter.service
```shell
vi /etc/systemd/system/node_exporter.service
```

W utworzonym katalogu wklej poniższą konfigurację
```text
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

Wykonaj przeładowanie konfiguracji daemonów przy pomocy systemctl daemon-reload
```shell
sudo systemctl daemon-reload
```

Następnie wykorzystując polecenie systemctl uruchom usługę node_exportera Sprawdź status uruchomionej usługi oraz czy usługa będzie uruchomiona przy restarcie systemu
```shell
sudo systemctl start node_exporter
sudo systemctl status node_exporter 
sudo systemctl is-enabled node_exporter
```

Określ PID uruchomionego procesu
```shell
ps -ef | grep node_exporter
```

Zabij określony proces
```shell
sudo kill PID
```

Zweryfikuj czy proces przestał działać, sprawdź również status usługi
```shell
ps -ef | grep node_exporter 
sudo systemctl status node_exporter
```

Zrestartuj usługę z poziomu komendy systemctl i zweryfikuj status jej aktywności
```shell
sudo systemctl restart node_exporter 
sudo systemctl status node_exporter
```

# Skrypty

Napisz skrypt, który będzie wyświetlał zawartość katalogu, który zostanie przekazany do skryptu jako argument wywołania.
```shell
dir=$1 
ls $dir
```

```shell
show_directory_content() {
    dir=$1
    ls $dir
}

show_directory_content /path/to/directory
```

Napisz skrypt, który poprosi użytkownika o podanie dwóch liczb, a następnie wyświetli ich sumę, różnicę, iloczyn i iloraz.
```shell
echo "Podaj pierwszą liczbę: " 
read num1 
echo "Podaj drugą liczbę: " 
read num2 
echo "Suma: $((num1 + num2))" 
echo "Różnica: $((num1 - num2))" 
echo "Iloczyn: $((num1 * num2))" 
echo "Iloraz: $((num1 / num2))"
```

Napisz skrypt, zliczający liczbę linii w syslogu (/var/log/syslog).
```shell
wc -l /var/log/syslog
```

Napisz skrypt zliczający liczbę plików o podanym rozszerzeniu w zadanym katalogu. Typ rozszerzenia ma być podawany do pliku jako zewnętrzny argument. Do tego możesz wykorzystać repozytorium pobrane w ćwiczeniu dotyczącym przetwarzania strumieni danych
```shell
count_files_by_extension() {
    dir=$1
    extension=$2
    ls $dir/*.$extension 2> /dev/null | wc -l
}

count_files_by_extension /path/to/directory txt
```

Zaimplementuj dziecięcą grę FizzBuzz Wypisz wszystkie liczby od 1 do 100, jednak jeżeli liczba jest podzielna przez poniższe liczby wygeneruj obok odpowiedni napis:

* 3 – wypisz „Fizz”
* 5– wypisz „Buzz”
* 3 i 5 wypisz „FizzBuzz”.

Zaimplementuj powyższy kod z wykorzystaniem funkcji. Do funkcji fizzbuzz przekazywany jest parametr – maksymalna liczba generacji liczb

```shell
fizzbuzz() {
    for i in $(seq 1 $1)
    do
        if (( i%3 == 0 )) && (( i%5 == 0 ))
        then
            echo "FizzBuzz"
        elif (( i%3 == 0 ))
        then
            echo "Fizz"
        elif (( i%5 == 0 ))
        then
            echo "Buzz"
        else
            echo "$i"
        fi
    done
}

fizzbuzz 100
```
