# Zmienne środowiskowe zadania

### Zmienne za pomocą ARG

1. Wejdz do katalogu `Przykłady` i zapoznaj się oboma plikami `Dockerfile`
2. Używając pliku `Dockerfile-ARG` stwórz dwa obrazy z dwiema róznymi wersjami ubuntu, dla zachowania porządku nadaj obrazom tag odpowiedni dla wersji systemu który został użyty do budowania obrazu.
3. Uruchom dwa terminale. Na jednym uruchom obraz z jedną wersją systemu a na drugim z drugą. 
4. Wejdz w obu terminalach do katalogu `/etc/` i podejrzyj plik z informacja o wersji sytemy `lsb-release`
5. Czy wersje się różnią? 


### Zmienne za pomocą ENV
1. Wejdz do katalogu `Przykłady` i zapoznaj się oboma plikami `Dockerfile`
2. Używając pliku `Dockerfile-ENV` zbuduj obraz z użyciem parametru `--build-arg` po którym zdefniuj dowolne imie. 
3. Wystartuj kontener ze zabudowanego obrazu i dokonaj zmiany imienia uzywając przełącznika `-e` i odwołując się do zadeklarowanej zminnej przy startowaniu kontenera. 
4. Stwórz kilka kontenerów z róznymi imionami używając zmiennej. 