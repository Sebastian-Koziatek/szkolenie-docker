W katalogu `my-maven-docker-project` znajduje się gotowa aplikacja w javie wyświetlająca prosty `Hello World`. Zbudujemy w oparciu o nią nasz kontener dockera.

### Budowanie aplikacji
1. Zbuduj przygotowaną aplikację używając `mavena`.

```
mvn clean install
```

Projekt zostanie stworzony w katalogu w którym jestes. Utworzony zostanie folder target w którym znajdować sie bedzie plik jar z aplikacją.

### Budowanie kontnera z aplikacja

2. W katalogu `my-maven-docker-project` stwórz dockerfile z ustwaieniami:

- Ma zostać zbudowany z obrazu openjdk:8
- Dodaj z folderu `target`  plik `my-maven-docker-project.jar`
- W `ENTRYPOINT` ustaw polecenie `java -jar my-maven-docker-project.jar`
- Wystaw port 8080

3. W repozytorium dockerhub (https://hub.docker.com/) stwórz nowe repozytorium, nazwij je np maven.

4. Zbuduj obraz aplikacji z dockerfile
   
```
docker build -t <nazwa_uzytkownika>/maven .
```

5. Prześlij zbudowany obraz do repozytorium dockerhub

```
docker push <nazwa_uzytkownika>/maven
```
6. Skaskuj obraz z lokalnych zasobów
7. Pobierz swój obraz ze swojego repozytorium na dockerhub
8. Uruchom go z użyciem portu 8080

```
docker run -d -p 8080:8080 <nazwa_uzytkownika>/maven
```

> sprawdź czy działa - http://localhost:8080/


