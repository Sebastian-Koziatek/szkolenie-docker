## Docker sock 

> Po pierwsze należy zrozumiec czym jest docker.sock. Jest to domyślny socket systemu unix który odpowiada za komunikację pomiędzy proecasami na hoście. Docker deamon domyślnie nasłuchuje docker.sock, jeżeli jesteś na systemie Linux/Unix to możesz użyć /var/run/docker.sock do zarządzania kontenerami. 

Możemy sobie podejrzeć te sockety:

```
curl --unix-socket /var/run/docker.sock http://localhost/version
```
> Reasumując jeżli kontenerowi dockera umożliwimy komunikację z socketem demona dockera to możemy uruchomić dockera w dockerze np tak:

```
docker run -v /var/run/docker.sock:/var/run/docker.sock \
           -ti docker
```

> UWAGA! - jeżeli przekażesz kontenerowi docker.sock to pamiętaj że kontener będzie miał więcej uprawnień nad demonem dockera na twoim hoście. Więc kiedy chcesz tego użyć w celach produkcyjnych to miej to na uwadze `(ale lepiej unikaj)`!

### Dla testu się zabawmy

1.  Uruchom docker container w interaktywnym trybie z zamontowaniem docker.sock jako volumenu. Dla bezpiczeńśtwa użyjemy domyślnego docker image

```
docker run -v /var/run/docker.sock:/var/run/docker.sock -ti docker
```
2. Kiedy jesteś już w kontenerze możesz zaoberwować że masz tu wszystko to co u siebie na hośćie, spradź odpowiednio uruchomione kontenery i obrazy. 
3. Pobierz obraz ubuntu z dockerhub i sprawdź czy się pobrał
```
docker pull ubuntu
docker images
```
4. Wewnątrz kontenera stwórz sobie plik dockerfile - skorzystajmy z pobranego obrazu ubuntu:

```
FROM ubuntu:18.04
RUN apt-get update && \
    apt-get -qy full-upgrade && \
    apt-get install -qy curl && \
    apt-get install -qy curl && \
    curl -sSL https://get.docker.com/ | sh
```
```
docker build -t test-image .
```