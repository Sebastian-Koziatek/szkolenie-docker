1. Stwórz nowy katalog w `06. Docker compose` w którym stwórzysz jeden plik `docker-compose.yml` który stwórzy trzy kontenery w oparciu o wskazane aplikacje i ich konfigurację. Posiłkuj się danymi z dockerhub. 

- Kontener z aplikacją `plex`:
- -  Nadaj nazwe kontenera: `plex-szkolenie`
- -  Wskaż dowolne miejsce mapowania folderów.
- - zdefniuj port `32400` dla kontenera i przekieruj go na port `32400` na localhost
- - zdefniuj aby kontener restartował sie zawsze, chyga że zostanie zatrzymany
- Kontener z aplikacją deluge:
- - Nadaj nazwe kontnera: `deluge-szkolenie`
- - Ustaw strefę czasową na `Europe/Warsaw`
- - Przekieruj porty `8112:8112` / `6881:6881` / `6881:6881/udp`
- - zdefniuj aby kontener restartował się zawsze gdy napotka błąd
- Kontener z aplikacja `pihole`
- - Nadaj nazwe kontenera: `pihole-szkolenie`
- - Przekieruj porty zgodnie z dokumentacja
- - Ustaw strefę czasową na `Europe/Warsaw`
- - Ustaw hasło do portalu webowego
  > Zgodnie z tym co omwialiśmy takie wprowadzenie hasła w samym docker-compose.yml jest to sprzeczne z zasadami poprawnego budowania plików konfiguracjnych. Dokumentacja dopuszcza takie użycie, ale to oczywisty błąd. Zastanów się w jaki inny sposób - poprawny powinno się takie hasło dostarczyć? Na potrzeby tego zadania pozostaw hasło zgodnie z dokumentacją. 
- - Wskaż dowolne miejsce mapowania folderów.
- - zdefniuj aby kontener restartował sie zawsze, chyba że zostanie zatrzymany

___

