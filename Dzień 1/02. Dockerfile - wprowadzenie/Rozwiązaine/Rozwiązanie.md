# Rozwiązanie zadań Dockerfile
1. Napisz plik docker file który:
- Powstanie z obrazu Linux Ubuntu
- Zaktualizuje repozytoria
- Zaktuatualizuje system
- Zainstaluje aplikacje curl
- Wykona polecenie `curl wttr.in`

> rozwiązanie znajduje się w pliku `Dockerfile` w folderze `Rozwiązanie`.
2. Zbuduj obraz z pliku dockerfile. Obraz nazwij `szkoleie`
```bash
docker build -t szkolenie .
```

3. Uruchom kontener ze zbudowanego obrazu i sprawdź co się wyświetliło.
   
```bash
docker run <image_id>
```