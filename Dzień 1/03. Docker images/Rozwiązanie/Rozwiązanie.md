# Lekcja 03 - Rozwiązanie

1. W folderze znajduje się przygotowany plik Dockerfile. Stwórz teraz obraz z tego pliku o nazwie "my-hello-world".
```sh
docker image build -t my-hello-world .
```

2. Po zbudowaniu obrazu sprawdź czy obraz jest dostępny w zasobach dockera.

```sh
docker image ls 
```

3. Odszukaj swój obraz przy użyciu `etykiety (labela)` zadeklarowanego w pliku Dockerfile.

```sh
docker image ls -f label=imagetype=szkolenie
```
4. Skasuj stworzony przez siebie obraz.
```
docker image ls
docker image rm my-hello-world
```

5. Z obrazu `Dockerfile2` zbuduj ponownie obraz z tagiem `my-hello-world2`. 

```sh
docker image build -t my-hello-world2 -f Dockerfile2 .
```
6. Uruchom kontener i wywołaj swoje imie jako argument dla kontenera

```
docker run my-hello-world2 Jan
```

7. Przejrzyj logi kontenera przy użyciu jego ID.

```  
docker container logs <id>
```` 
8. Skaskuj stworzone kontenery. 
```
docker ps -a
docker rm <id>
```