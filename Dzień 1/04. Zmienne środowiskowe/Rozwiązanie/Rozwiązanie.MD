# Zmienne środowiskowe zadania

### Zmienne za pomocą ARG

1. Wejdz do katalogu `Przykłady` i zapoznaj się oboma plikami `Dockerfile`
2. Używając pliku `Dockerfile-ARG` stwórz dwa obrazy z dwiema róznymi wersjami ubuntu, dla zachowania porządku nadaj obrazom tag odpowiedni dla wersji systemu który został użyty do budowania obrazu.

```bash
docker build -t zmienna-arg:latest -f Dockerfile-ARG --build-arg UBUNTU_VERSION=latest .
docker build -t zmienna-arg:16.04 -f Dockerfile-ARG --build-arg UBUNTU_VERSION=16.04 .
```

3. Uruchom dwa terminale. Na jednym uruchom obraz z jedną wersją systemu a na drugim z drugą. 
```bash
docker run -it zmienna-arg:latest sh
docker run -it zmienna-arg:16.04 sh
```
4. Wejdz w obu terminalach do katalogu `/etc/` i podejrzyj plik z informacja o wersji sytemy `lsb-release`
```
cd /etc
cat lsb-release
```
5. Czy wersje się różnią? 

### Zmienne za pomocą ENV
1. Wejdz do katalogu `Przykłady` i zapoznaj się oboma plikami `Dockerfile`
2. Używając pliku `Dockerfile-ENV` zbuduj obraz z użyciem parametru `--build-arg` po którym zdefniuj imie.

```bash
docker build -t imie -f Dockerfile-ENV --build-arg name=Pawel .
```
3. Wystartuj kontener ze zabudowanego obrazu. Jakie imie się wyświetliło?

```bash   
docker run imie
```

4. Wystartuj kontener i dokonaj zmiany imienia uzywając przełącznika `-e` i odwołując się do zadeklarowanej zminnej przy startowaniu kontenera. 

```bash
docker run -e env_name=Anna imie
```

5. Stwórz kilka kontenerów z róznymi imionami używając zmiennej. 

```bash
docker run -e env_name=Marek imie
docker run -e env_name=Witold imie
docker run -e env_name=Anna imie
```