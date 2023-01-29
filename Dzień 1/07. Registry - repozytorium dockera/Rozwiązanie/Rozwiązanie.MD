# Docker hub
1. Wejdz do katalogu 04. Nginix i przygotuj obraz który wyślesz na Docker Hub

```bash
docker image build -t <nazwa_użytkownika>/<nazwa_repozytorium>:tag nginx/
```

2. Wyślij go na docker hub

```bash
docker push <nazwa_użytkownika>/<nazwa_repozytorium>:tag
```

3. Zweryfikuj czy obraz jest widoczny
>Wejdz na swoje konto na https://hub.docker.com/ i sprawdź w repozytoriach.
4. Wyczyść obrazy posiadane lokalnie

```bash
docker images
docker images rm
```

5. Pobierz swój obraz z Docker Hub

```bash
docker pull <nazwa_użytkownika>/<nazwa_repozytorium>:tag
```

# Lokalne repozytorium

1. Stwórz kontener ze swoim repozytorium.

```bash
docker tag ubuntu:16.04 localhost:5000/my-ubuntu
```

2. Pobierz obraz np ubuntu:16.04 z docker hub.

```bash
docker pull ubuntu:16.04
```

3. Zmień nazwe oraz tak obrazu ubuntu:16.04 na taką by można było obraz przesłąć do lokalnego repozyorium.
 ```
 <host>:port/<nazwa_obrazu>
 ```
  ```
 docker tag ubuntu:16.04 localhost:5000/my-ubuntu
 ```
 4. Wyślij obraz do lokalnego repozytorium.
 
 ```bash
 docker push localhost:5000/my-ubuntu
 ```
 5. Skasuj wszystkie obrazy.

```bash
docker images
docker image rm
```

 6. Pobierz wysłany obraz z lokalnego regsitry. 

```bash
docker pull localhost:5000/my-ubuntu
```