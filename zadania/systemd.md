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
ExecStart=/usr/local/bin/node_exporter --web.systemd-socket $OPTIONS

[Install]
WantedBy=multi-user.target
```
Wykonaj przeładowanie konfiguracji daemonów przy pomocy systemctl daemon-reload

Następnie wykorzystując polecenie systemctl uruchom usługę node_exportera Sprawdź status uruchomionej usługi oraz czy usługa będzie uruchomiona przy restarcie systemu

Określ PID uruchomionego procesu

Zabij określony proces

Zweryfikuj czy proces przestał działać, sprawdź również status usługi

Zrestartuj usługę z poziomu komendy systemctl i zweryfikuj status jej aktywności
