
# Instalacja
Docker compose wystarczy pobrać ze strony - https://docs.docker.com/compose/install/ 
W przypadku systemu linux (nie WSL) zalecane jest używanie reposytorium do pobrania. Jeżeli jest skonfigurowane repozytorium zgodnie z dokumentacja to wystarczy

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
Dokumentacja:
- docker compose <a href="https://docs.docker.com/compose/compose-file/compose-file-v2/" title="docker-compose version 2"> Version:2</a></td> i <a href="https://docs.docker.com/compose/compose-file/compose-file-v3/" title="docker-compose version 3">Version:3 </a>
- <a href="https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html"> Yaml </a> na podstawie ansible 

# Czym jest docker compose? 

to narzędzie, które zostało opracowane w celu pomocy w definiowaniu i udostępnianiu aplikacji wielokontenerowych. Dzięki Compose możemy utworzyć plik YAML w celu zdefiniowania usług i za pomocą jednego polecenia możemy wszystko rozpisać w jednym pliku.
Dzięki docker-compose zarządzanie cała infrastrukturą kotnenerów jest znacznie prostsza. 

# Najważniejsze komendy:<br>

- `docker-compose build` - wykonuje zbudowanie pliku `docker-compose.yml`.
- `docker-compose images` - listuje wszystkie zbudowane obrazy uzywane przez `docker-compose`.
- `docker-compose stop` - zatrzymuje wskazany kontener.
- `docker-compose run` - komenda podobna do `docker run`, stworzy kontener z obrazu określonego w pliku `docker-compose.yml`.
- `docker-compose up` - to połączenie komend `docker-compose build` i `docker-compose run`. Zbuduje obrazy jeżeli nie są zbudowane i uruchomi kontener. 
- `docker-compose ps` - listuje wszystkie kontenery uruchomione przez `docker-compose`
- `docker-compose down` - komenda podobna do `docker system prune`. Zastopuje serwisy w kontenerze, zamknie kontener, usuniego, usunie konfiguracje sieci oraz obrazy.
___
### Przykładowa struktura pliku

```yaml
version: "3.7"
services:
  ...
volumes:
  ...
networks:
  ...
```
W tym przykładowym pliku

W części pierwszej dekalrujemy serwisy które będziem konteneryzować.

```yaml
services:
  frontend:
    image: my-vue-app
    ...
  backend:
    image: my-springboot-app
    ...
  db:
    image: postgres
    ...
  ```

W części drugiej deklarujemy odpowiednio wszysktie montowane volumeny, lub przekazane zasoby.
W częsci trzeciej konfigurujemy sieć.

Przykładowy plik docker-compose

```yaml
services:
  network-example-service:
    image: karthequian/helloworld:latest
    ports:
      - "80:80"
    ...
  my-custom-app:
    image: myapp:latest
    ports:
      - "8080:3000"
    ...
  my-custom-app-replica:
    image: myapp:latest
    ports:
      - "8081:3000"
    ...
```