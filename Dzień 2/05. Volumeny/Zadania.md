# Zadania - docker volume

1. Stwórz volumin o nazwie `docker-szkolenie`
2. Wyświetl informacje o tym volumienie
3. Wylistuj wszystkie stworzone volumeny
4. Zamontuj volumin w kontenerze zbudowany na obrazie nginx, ustaw miejscie montowania na /app
5. Wejdz do kontenera i przejdz do katalogu zamontowango volumenu
6. Stwórz katalog testowy a w nim plik `plik_szkolenia` o dowolnej wartości.
7. Stwórz drugi kontener w oparciu o obraz alpine, uruchom go by działał w tle (dodaj parametr tail -f /dev/null) i zmontuj volumin `docker-szkolenie` do folderu `/app`.
8. W tym samym kontenerze na naszym volumenie stwórz folder `testowy2`
9. Wejdz ponownie do kontenera z nginix i sprawdz katalog /app, czy znajduje sie tam folder `testowy2`? 