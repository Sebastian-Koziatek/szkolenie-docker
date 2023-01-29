# Zmienne środowiskowe 

Tworząc kontener możemy określić dostępne w nim zmienne środowiskowe. Ustawianie zmiennych środowiskowych jest istotnym elementem konfiguracji wielu kontenerów.

Do ustawiania zmiennych środowiskowych w kontenerze służy opcja -e w poleceniu docker run.

```bash
docker run -e [nazwa]:[wartość] [nazwa obrazu]
```


# Zmienne w dockerfile 

```bash
FROM openjdk:11

COPY target/app.jar /app/app.jar
COPY ./application.yml /app/config/application.yml

ENV SPRING_MONGO_HOST=localhost

WORKDIR /app

EXPOSE 8080
ENTRYPOINT java -jar app.jar
```

Przy uruchamianiu kontenera z tak zbduowanego obrazu możemy wprowadzi zadeklarowane zmienne np

```bash
docker run --env SPRING_MONGO_HOST=mongodb <image-name>
```

# ARG vs ENV

Parametr `ARG` nazywany jest zmienną czasu kompilacji, głównie dlatego że defniowanie i dostęp do zmiennych są dostępne tylko do czasu zbudowania obrazu, inaczej mówiąć są dostępne tylko od momentu ich „ogłoszenia” w Dockerfile do momentu zbudowania obrazu. Kontenery nie mają dostępu do wartości zmiennych ARG. Jeśli powiesz plikowi Dockerfile, aby oczekiwał różnych zmiennych ARG (bez wartości domyślnej), ale żadna nie zostanie podana podczas uruchamiania polecenia kompilacji, pojawi się komunikat o błędzie.

Wartości ARG można łatwo sprawdzić po zbudowaniu obrazu, przeglądając historię dokera obrazu. Dlatego są złym wyborem dla wrażliwych danych.

Zmienne `ENV` różnią się od `ARG` tym są również można je zdefniować w momencie uruchamiania kontenera rozpoczynające się od końcowego obrazu. Wartości ENV można nadpisać podczas uruchamiania kontenera.