# Izolacja kontnerów - izolacja danych

1.  Uruchom dwa terminale i kazżdym z nich uruchom kontener z obrazu busybox i wejdz do shella.

```   
docker run -it busybox sh
```

2. Na pierwszym `terminalu/kontenerze` stwórz plik szkolenie - 
```bash
touch szkolenie
ls
```
3. Sprawdź na drugim `temrinalu/konterze` czy plik istnieje.
```bash
ls
```

# Izolacja kontnerów - izolacja sieci
1. Używając docker-compose.yml w głownym katalogu, stwórz kontenery na obrazie ubuntu.  
