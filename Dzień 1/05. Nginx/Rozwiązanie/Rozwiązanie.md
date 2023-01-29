# TASK

1. Zbuduj przygotowany obraz nginx'a z głównego folderu.
```sh
docker image build -t my-nginx nginx/
```

2. Uruchom kontener ze zbudowanego obrazu
3. Uruchom kontener w tle
```
docker run -d my-nginx
``` 

4. Wejdz do shella zbudowanego kontenera, pobierz pakiet `curl` i spradź działanie `nginx` w kontenerze.
```
docker ps -a
docker exec -it <id> sh
apk add curl
curl localhost
```

5. W folderze nginix dodaj plik o nazwie "password" i wprowadź w nim dowolną wartość.
6. Zbuduj obraz jeszcze raz 
```sh
docker image build -t my-nginx:2 nginx/
```
>`-t` nada `tag` po `:` dla naszego obrazu 

7. Uruchom konterner z nowego obrazu
```sh
docker container run -d my-nginx:2
```
8. Z racji że mamy już swoje dwa działające kontenery to wejdzmy do do my-nginix i sprawdźmy czy jest tam plik password 
```sh
docker container exec -ti <container_id> sh
ls
```
9. Jak widać pliku password nie ma, spradźmy teraz obraz `my-nginix:2` który zbudowaliśmy po dodaniu pliku
```
docker container exec -ti <container_id> sh
ls
```
<i> Plik znajduje się w katalogu zbudowanym na obraznie po jego dodaniu </i>


# Docker ignore.

1. Stwórzmy sobie plik .dockerignore w katalogu nginx i dopiszmy do niego stworzony przez nas plik password

```.dockerignore
password
```

1. Zbudujmy obraz my-nginx ponownie:

```sh
docker image build -t my-nginx:3 nginx/
```
3. Uruchom pnownie kontener (pamiętaj o fladze -d)
4. Sprawdź czy plik password dalej się tam znajduje?
___

## Forward port

Upewnij się że nie masz żadnych uruchomionych kontenerów i skasuj nieużywane. 

```sh
docker container rm <id>
```

1. Uruchom konterner z obrazu my-nginix z nową flagą `-p` aby przekierować porty. Pamiętaj o uruchomieniu kontenera w tle.
   
```sh
docker container run --name my-nginx -p 8080:80 -d my-nginx
curl localhost:8080
```

><i>to przekierowuje port na moim komputerze (8080) na port kontenera (80)</i>
___
>W tym momencie wyczyść sobie dockera, skasuj wszystkie obrazy i kontenery które posiadasz.
```sh
docker ps -a
docker stop <container_id>
docker rm <container_id>
docker image ls
docker image rm <image_id>
```