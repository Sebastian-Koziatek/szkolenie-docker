## Izolacja kontnerów w praktyce

1.  Uruchom dwa terminale i kazżdym z nich uruchom kontener z obrazu busybox i wejdz do shella.

```   
docker run -it busybox sh
```

2. Na pierwszym `terminalu/kontenerze` stwórz plik szkolenie - `touch szkolenie`.
3. Sprawdź na drugim `temrinalu/konterze` czy plik istnieje - `ls`

# Izolacja kontnerów - izolacja sieci

1. Używając docker-compose.yml w głownym katalogu, stwórz kontenery na obrazie ubuntu.
2. Pobierz informacje na temat adresu IP z kontenera o nazwie `ubuntunet2`
3. Wejdz do shella kontenera `ubuntunet1` 
4. Zainstaluj pakiet potrzebny do wykonania polecenia `ping` (pakiet: iputils-ping)
5. Wykonaj ping poadając adres IP `ubuntunet2`
6. Czy kontenery da się pingować między soboą?
7. Zatrzymaj działające kontnery
8. Przyjżyj się plikowi `docker-compose2.yml` i zapoznaj się z konfiguracją sieci w tym ustawieniu
9. Zbuduj kontenery w oparciu o `docker-compose2.yml`
10. Pobierz informacje na temat adresu IP z kontenera o nazwie `ubuntunet2`
11. Wejdz do shella kontenera `ubuntunet1` 
12. Wykonaj ping poadając adres IP `ubuntunet2`
13. Czy teraz też kontenery da się pingować między soboą?