# team-project-smart-house

# Instalacja oraz konfiguracja brokera MQTT na Windows
## Instalacja brokera
  - pobranie brokera MQTT - [Mosquitto](https://mosquitto.org/download/),
  - domyślna instalacja oprogramowania,
  - przejście do folderu gdzie znajduje się zainstalowane Mosquitto,
  - skopiowanie ścieżki do folderu,
  - otworzenie Wiersza poleceń(cmd) - konieczne jest uruchomienie jako administrator,
  - przejście do folderu gdzie znajduje się zainstalowane Mosquitto:
     ```sh
     cd [scieżka do pliku]
     ```
  - sprawdzenie czy instalacja Mosquitto przebiegła pomyślnie:
     ```sh
     mosquitto install
     ```
  - jeśli operacja instalacji wcześniej nie przebiegła poprawnie teraz powinna się wykonać,
  - jeśli wykonała się poprawnie, powinien zostać wyrzucony błąd:
       ```sh
     Error: Określona usługa już istnieje.
     ```
  - broker uruchamia się przy pomocy polecenia:
     ```sh
     net start mosquitto
     ```
     co powinno skutkować odpowiedzią:
     ```sh
     Pomyślnie uruchomiono usługę Mosquitto Broker.
     ```
  - broker można wyłączyć pomocy polecenia:
     ```sh
     net stop mosquitto
     ```
     co powinno skutkować odpowiedzią:
     ```sh
     Usługa Mosquitto Broker jest właśnie zatrzymywana.
     Usługa Mosquitto Broker została zatrzymana pomyślnie.
     ```
## Konfiguracja brokera
  W celu poprawnego działania brokera konieczne jest otworzenie portu w systemie Windows(domyślnie: 1883) oraz dodanie komend w pliku konfiguracyjnym mosquitto.conf. 
  Otwieranie portu:
  - przyciśnij **Windows+R**,
  - otwórz **firewall.cpl**,
  - przejdź do **Ustawienia zaawansowane**,
  - wybierz **Reguły wbudowane** oraz stwórz nową regułę,
  - stwórz regułę rodzaju **Port**,
  - wybierz protokół **TCP** oraz konkretny port: **1883**,
  - zezwól na połączenia oraz wybierz zastosowania dla reguły,
  - nazwij regułę,
  - sprawdź czy reguła istnieje oraz jest uruchomiona w oknie **Reguły przychodzące**.
  
  Dodatkowo sprawdzenia czy port został otwarty można dokonać poprzez otwarcie Wiersza poleceń(cmd) oraz wywołanie  polecenia:
  ```sh
    netstat -a
  ```
  Pośród odpowiedzi powinien widnieć m.in.:
  ```sh
    TCP     [0.0.0.0:1883/127.0.0.1:1883]    [NAZWA KOMPUTERA]     LISTENING
  ```
  
  Konieczne jest również dokonanie zmiany w pliku konfiguracyjnym mosquitto.conf znajdującym się w folderze gdzie zainstalowane jest Mosquitto.
  Zmiany których trzeba dokonać:
  ```sh
      allow_anonymous true
      listener 1883
  ```
  Domyślnie parametr **allow_anonymous** ustawiony jest na **false** co oznacza, że wymagana jest autoryzacja użytkownika udostępniającego dane.
  Wartość parametru **listener** domyślnie nie jest zdefiniowana.
  
  W oryginalnym pliku konfiguracyjnym znak # oznacza komentarz. Trzeba pamiętać o odkomentowaniu dokonanych zmian.
## Popularne problemy
- Wiersz poleceń należy uruchamiać jako administrator,
- otwarcie portu w prawidłowy sposób(sprawdź czy port faktycznie jest otwarty, komenda powyżej),
- MQTT broker nie będzie działał jeśli na porcie 1883 jest uruchomiona już jakaś inna usługa,
- Firewall może blokować połączenie,
- konieczne może być umożliwienie pracy Mosquitto pomimo Firewalla,
- JAK RASOWY INFORMATYK POPROSTU ZRESTARTUJ.
