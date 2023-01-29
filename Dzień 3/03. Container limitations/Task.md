# Limitacja zasobów kontenera w dockerze

Limity zasobów możemy ustawić bezpośrednio za pomocą polecenia docker run. To proste rozwiązanie. Limit będzie jednak dotyczył tylko jednego konkretnego wykonania obrazu.

## Memory

Aby ograniczyć pamięć, musimy użyć parametru `m`:
```docker
docker run -d -m 512m nginx
```
Możemy również ustawić miękki limit zwany rezerwacją.

Aktywuje się, gdy docker wykryje niski poziom pamięci na komputerze hosta:
```docker
docker run -d -m 512m --memory-reservation=256m nginx
```

Możecie to sprawdzić używając:

```docker
docker inspect <id> | grep -i mem 
```

## CPU
Domyślnie dostęp do mocy obliczeniowej maszyny hosta jest nieograniczony. Limit procesorów możemy ustawić za pomocą parametru cpus.
Ograniczmy nasz kontener do użycia co najwyżej dwóch procesorów:
```docker
docker run -d --cpus=2 nginx
```
Możemy również określić priorytet alokacji procesora.

Wartość domyślna to `1024`, a wyższe liczby mają wyższy priorytet:


```docker
docker run -d --cpus=2 --cpu-shares=2000 nginx
```

Weyfikacja: 

```
docker inspect <id> | grep -i cpu
```
> Przy ograniczeniu do liczby procesorów limtacja zostanie włączona dopiero kiedy kontener będzie się chciał odwołać do większej ilości zasobów, dlatego będzie to do tego czasu nie widoczne w `inspect`. 

### Ustawianie limitu pamięci za pomocą pliku `docker-compose`
>UWAGA! Aktualnie aby wykorzystać opcje lmitacji zasobów kontenera wymagane jest użycie dockercompose w wersji `3.0` lub wyższej.

1. Zbuduj obrazy i pokolei sprawdź poleceniem inspect ich limtacje w kontenerze

- ograniczenie limitu pamięci 
```yaml
version: '3.9'

services:
  app:
    image: nginx
    mem_limit: 300m 
```

`docker inspect <id> | grep -i mem`

- rezerwacja pamieci `ram` dla kontenera
```yaml
version: '3.9'

services:
  app:
    image: nginx
    mem_limit: 300m
```

- limitacja `cpu`

```yaml
version: '3.9'

services:
  app:
    image: nginx
    mem_limit: 300m
      cpus: 0.5
```
`docker inspect <id> | grep -i cpu`
> Tu informacje otrzymamy dopiero jak cpu będzie chcial wysycić większą ilośc zasobu i zostanie odcięty.
