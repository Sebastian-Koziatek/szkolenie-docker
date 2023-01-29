# Manualne tworzenie volumenów

Volumeny tworzone na potrzeby kontenera możemy traktować tak jak wirtualne dyski w przypadku wirtualizacji. Możeny tworzyć je manualnie za pomocą dockera.

```bash
docker volume create my-volume
```

Wszystkie wytworzone przez dockera volumeny możemy podejrzeć odpowiednim poleceniem:

```bash
docker volume ls
```

Możemy podejrzeć informacje o tym volumienie

```bash
docker volume inspect my-volume
```

# Montowanie zasobów hosta w kontenerze 

Aby stworzony przez nas volumen był widoczny w kontenerze musimy go zamontować. Służy do tego polecenie:

```bash
docker run -d \
-v nazwa_volumenu:/app \
nginx:latest
```

W tak utworzonym kontenerze zróbmy na utworzonym volumenie folder testowy 

```bash
docker exec -it <nazwa_contenera> sh 
```

Wejdzmy do naszego volumenu zamontowanego w /app, stwórzmy tam folder a w nim plik

```bash
cd app
mkdir testowy
cd testowy
echo . > plik_szkolenia
ls
```

Sprawdźmy teraz czy jak zamontujemy volumen w innym kontenerze czy jego zasób będzie widoczny.

```bash
docker run -d -v my-volume:/app alpine tail -f /dev/null
docker exec -it <nazwa_contenera> sh 
cd app
ls
```
Nasze pliki powinny się tu znajdować. <br>
Skoro jestesmy już w tym katalogu to stwórzmy folder `testowy2` i sprawdźmy czy pojawi się na obrazie z nginx.</br>
```bash
docker ps -a
docker -it <nazwa_kontenera_nginx> sh
cd app
ls
```</p>
Folder `testowy2` powinien sie tu znajdować

# Zasoby współdzielone z hostem

Dzięki temu że kontenery używaja systemu plików UnionFS mamy możliwośc przekazywania zasobów hosta wprost do kontenera. Kontener może w czasie rzeczywistym odczytywać i wprowadzać zmiany do wydzielonych zasobów.

Dla przykładu, jeżeli stworzymy sobie prosty kontener wyświetlający dane zawarte w pliku `index.html` który będzie się znajdował lokalnie na naszym hoście a zostanie uruchomiony przez serwer www w kontenerze to dokunując modyfikacji naszego pliku z poziomu hosta, dane powinny się zmieniać w czasie rzeczywistym. 

Składnia polecenia montującego do kontenera wskazany zasób:

```bash
docker run -v [zasób systemu plików gospodarza]:[punkt montowania w kontenerze] [nazwa obrazu]
```

Stwórzmy kontener na podstawie obrazu python:3.5-slim, który:
>  - Montuje katalog ~/docker w punkcie /shared_volume. <br>
>  - Uruchamia serwer HTTP działający na porcie 8000. <br>
>  - Udostępnia port 8000 w systemie gospodarza.</br>

```bash
docker run -d -v ~/docker:/shared_volume -p 8000:8000 python:3.5-slim /bin/bash -c "cd /shared_volume && python -m http.server 8000"
```

Dla przykładu na dysku D:\ posiadam folder szkolenie.

```bash
cd /mnt/d/Szkolenie
echo "Szkolenie docker!" >> index.hmtl

docker run -d -v /mnt/d/Szkolenie:/shared_volume -p 8000:8000 python:3.5-slim /bin/bash -c "cd /shared_volume && python -m http.server 8000"
```
Na adresie http://127.0.0.1:8000/ powinniśmy zobaczyć napis „Szkolenie docker!”. Każda modyfikacja pliku index.html powinna być widoczna po odświeżeniu przeglądarki.