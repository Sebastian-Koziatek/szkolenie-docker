### Odpalamy Portainer w kontenerze

1. Tworzymy volumin dla kontenera
```
docker volume create portainer_data
```
2. Ściągamy i uruchamiamy obraz
```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:2.9.3
```
