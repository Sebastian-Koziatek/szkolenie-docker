# Zmienne środowiskowe w pliku .env - docker-compose

Istnieje możliwość stworzenia pliku o nazwie `.env`  Zawartość tego pliku może posłużyć do nadpisania wartości znajdujących się w pliku docker-compose.yml. 

Zawartość pliku .env defniujemy za pomocą schematu klucz=wartość

```docker
DB_PORT=5434
DB_USER=myuser
```

Przykład pliku docker-compose w którym uwzględniono zmienne środowiskowe. Zmienna ma zostać podstawiona, a odpowiada za to składnia ${DB_PORT} oraz ${DB_USER}

```yaml
version: '3.2'
​
services:
  postgres:
    image: postgres:9.6
    ports:
      - ${DB_PORT}:5432
    environment:
        POSTGRES_PASSWORD: secretpassword
        POSTGRES_USER: ${DB_USER}
```

Po wykonaniu polecenia
```bash
docker-compose up -d
```
docker zaciągnie wartości zmiennych z pliku `.env` i podstawi w odpowiednie miejsce. 

Całość można zweryfikować używając komendy

```bash
docker-compose config
```