# Budujemy swój kontener z aplikacja nginx. 

1. Zbuduj przygotowany obraz nginx'a z głównego folderu.
2. Uruchom kontener ze zbudowanego obrazu
3. Uruchom kontener w tle
4. Wejdz do shella zbudowanego kontenera, pobierz pakiet `curl` i spradź działanie `nginx` w kontenerze.
5. W folderze nginix dodaj plik o nazwie "password" i wprowadź w nim dowolną wartość.
6. Zbuduj obraz jeszcze raz 
7. Uruchom konterner z nowego obrazu
8. Z racji że mamy już swoje dwa działające kontenery to wejdzmy do do my-nginix i sprawdź czy jest tam plik password 
9. Jak widać pliku password nie ma, spradźmy teraz obraz `my-nginix:2` który zbudowaliśmy po dodaniu pliku
Plik znajduje się w katalogu zbudowanym na obraznie po jego dodaniu


# Docker ignore.

1. Stwórzmy sobie plik .dockerignore w katalogu nginx i dopiszmy do niego stworzony przez nas plik password
2. Zbudujmy obraz my-nginx ponownie:
3. Uruchom nowy kontener (pamiętaj o fladze -d)
4. Sprawdź czy plik password dalej się tam znajduje?


# Przekierowywanie portów

Upewnij się że nie masz żadnych uruchomionych kontenerów i skasuj nieużywane. 


1. Uruchom konterner z obrazu my-nginix z nową flagą `-p` aby przekierować porty. Pamiętaj o uruchomieniu kontenera w tle.

___
>W tym momencie wyczyść sobie dockera, skasuj wszystkie obrazy i kontenery które posiadasz.
```sh
docker ps -a
docker stop <container_id>
docker rm <container_id>
docker image ls
docker image rm <image_id>
```