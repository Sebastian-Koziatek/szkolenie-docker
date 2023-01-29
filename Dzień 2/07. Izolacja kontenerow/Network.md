# Sieci w dockerze - kontenery 

Docker podobnie jak wirtualne maszyny może tworzyć swoje wirtualne sieci. Domyślnie budując aplikacje webowe i uruchamiając je w kontenerze docker sam tworzy sobie sieć dla danego kontenera lub używa domyślnej konfiguracji. 

Możemy wyświetlić istniejące w dockerze sieci poleceniem

```bash
docker network ls 
```

docker-compose zawiera rozszerzoną konfiguracji sieci, można w nim defniować czy aplikacje/kontenery mają mieć możliwość działania w ramach jednej sieci czy wielu sieci i czy mają być izolowane czy nie. 

Szczegółów danej sieci możemy się dowiedzieć wykonująć polecenie.

```bash
docker network inspect networkname
```

Konfiguracja sieci dockera różni się w zależnośći od posiadanych kart sieciowych, skonfigurowanych połączeń, zainstalowanych VPN'ów oraz ogólnej konfiguracji systemu.

Informacje o danej konfiguracji sieci w danym kontenerze możemy uzusykać używająć polecenia

```bash
docker inspect <container_id>
```