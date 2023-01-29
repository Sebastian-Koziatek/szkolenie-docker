# Skalowanie kontenerów 
1. Korzystając z pliku `docker-compose.yml` w folderze `Skalowanie kontenerów` zbuduj kontener.
2. Zwróc uwagę na zapis zakresu portów 
```docker
   ports: 
    - "6379-6385:6379"
```
3. Do skalowania kontenerów w oparciu o docker-compose użyj komendy 
```bash
docker-compose up --scale <nazwa_serwisu>=<wartość_skalowania> -d

np

docker-compose up --scale redis-master=3 -d
```
4. Zbuduj teraz 3 kontenery w przypadku dockerfile z redis-masterem
5. Używając docker-compose2.yml zeskaluj kontenery nginxa do 5

```bash
docker-compose -f docker-compose2.yml up --scale web=3 -d
```