# Zadania - docker volume

1. Stwórz volumin o nazwie `docker-szkolenie`

```bash
docker volume create docker-szkolenie
```

2. Wyświetl informacje o tym volumienie
   
```bash
docker volume ls
```
3. Wylistuj wszystkie stworzone volumeny
   
```bash
docker volume inspect docker-szkolenie
```

4. Zamontuj volumin w kontenerze zbudowany na obrazie nginx, ustaw miejscie montowania na /app
```bash
docker run -d \
-v docker-szkolenie:/app \
nginx:latest
```

5. Wejdz do kontenera i przejdz do katalogu zamontowango volumenu
```bash
docker exec -it <nazwa_contenera> sh
cd /app
```
6. Stwórz katalog testowy a w nim plik `plik_szkolenia` o dowolnej wartości.
```bash
mkdir testowy
cd testowy
echo . > plik_szkolenia
ls
```
7. Stwórz drugi kontener w oparciu o obraz alpine, uruchom go by działał w tle (dodaj parametr tail -f /dev/null) i zmontuj volumin `docker-szkolenie` do folderu `/app`.
   
```bash
docker run -d -v my-volume:/app alpine tail -f /dev/null
docker exec -it <nazwa_contenera> sh 
cd app
ls
```
8. W tym samym kontenerze na naszym volumenie stwórz folder `testowy2`

```bash
mkdir testowy2
```

9.  Wejdz ponownie do kontenera z nginix i sprawdz katalog /app, czy znajduje sie tam folder `testowy2`? 

```bash
docker exec -it <nazwa_contenera> sh
cd /app
ls
```

