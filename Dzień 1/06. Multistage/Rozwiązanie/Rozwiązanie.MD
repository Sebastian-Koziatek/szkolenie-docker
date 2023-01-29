# Zadania Multistage buid

1. Zbuduj obraz z pliku `Dockerfile`
``bash
docker build -t java:1 .
```
1. Zbuduj obraz z pliku `Dockerfile2`
```bash
docker build -t java:2 -f Dockerfile.multi .
```
2. Porównaj rozmiar obu obrazów.
```bash
docker images ls
```
3. Sciągnij obraz który w pliku `Dockerfile2` służy do budowy aplikacji.
```
docker pull gradle
```
4. Ściagnij obraz który w pliku `Dockerfile2` służy do uruchamiania przygotowanej aplikacji.
```
docker pull openjdk:11-jre-slim
```
5. Porównaj rozmiar obu obrazów.
```
docker images
```
6. Zastanów się jaka jest róznica pomiędzy `COPPY` a `ADD`. <br>
Coppy: obejmuje wskazany plik źródło i miejsce docelowe do którego się odnosi. Pozwala na kopiowanie tylko z zasobów lokalnych (na ogól hosta lub kontenera).<br>
ADD robi to samo, ale dodatkowo obsługuje 2 inne źródła.
- Adres URL zamiast lokalnego pliku/katalogu.
- Ma możliwość rozpakowywania skompresowanych plików.