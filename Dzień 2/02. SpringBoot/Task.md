### Urchamianie aplikacji javy w kontenerze na przykładzie springboot

1. Zajrzyj na strone springboota. Pozwala on przyśpieszyc i ułątwić budowanie alikacji webowych i mikroserwisów we frameworku spring.   

`https://start.spring.io/`

Przygotuj aplikację którą będziemy konteneryzować. Wybierz podane opcje:

Project: Maven
Language: Java
Spring Boot: 3.0.0
Name: Szkolenie
Packging: Jar
Java: 17 
Dependencies - add dependencies: Spring Web

Wygeneruj i pobierz przygotowany projekt i wklej go to katalogu Aplikacja.

3. Podmień zawartość pliku Aplikacja/src/main/SzkolenieApplication.java 
danymi z pliku `dependencies.md`

4. Za pomocą mavena zbudujemy teraz ten projekt. W katalogu z aplikacja uruchom polecenie
```
mvn clean install
```
Utworzył nam sie folder `target` który zawiera naszą aplikację Javy - `spring-boot-docker-0.0.1-SNAPSHOT.jar`
5. Skoro mamy zbudowaną już aplikację to stwórzmy sobie dockerfile aby stworzyc dla niej kontener. <br>
Stwórz docker file który: </br>
- Zbuduje kontener z obrazu `FROM openjdk:19`
- Stworzy zmienną środowiskową `ARG` o wartości `JAR_FILE=target/*.jar`
- skopiuje naszą zbudowną aplikację `${JAR_FILE}` do kontenera i nazwie ją `app.jar`
- W entrypoint spwooduje jej uruchomienie `java -jar ./app.jar`


Nasz dockerfile powinien wyglądac tak:

```
FROM openjdk:19
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```
6. Zbudujmy obraz z dockerfile

```   
docker build -t springboot .
```

7. Sprawdźmy czy aplikacja urochomi. Uruchom kontener z obrazu w tle i na porcie 8080 (specjalnie brak -d)

```
docker run -p 8080:8080 springboot
```