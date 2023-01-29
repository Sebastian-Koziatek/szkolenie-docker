# Wprowadzenie do dockera. Uruchom swój pierwszy kontener!

### Poniżej znajdują się podstawowe polecenia, wykonaj je w terminalu zastanawiając się co one robią i co oznaczają. 

1. Zacznij od ściągnięcia przykładowego `obrazu` (docker image):

```sh
docker image pull hello-world
```

2. Sprwadź czy `obraz` znajduje się w twoich lokalnych zasobach, wylistujemy posiadane obrazy:

```
docker image ls
```

3. A teraz stwórz `kontener` (docker container) z pobranego `obraz`

```sh
docker container run hello-world
```


4. Sprawdź czy ten `kontener` jest aktualnie uruchomiony?

```sh
docker container list
```
5. Skoro go nie ma to moze sprawdzimy czy jest wyłączony?

```sh
docker container list -a
```

6. Teraz dodajmy kilka parametrów do stworzenia kontenera. Stwórz i uruchom `kontener` z poniszymi parametrami:
```sh
docker container run --name <myname> --label=type=szkolenie hello-world
```
>Zastanów się jakie `parametry` dla `kontenera` zostały tutaj ustawione?

7. Listowanie `kontenerów`

```sh
docker container ls
docker container ls -a
docker container ls -a -f status=exited
docker container ls -a -f label=type=szkolenie
```

8. Zobacz logi `kontenera`

```sh
docker container logs <myname|id>
``` 

9. Skasuj `kontener`

```sh
docker container rm <myname>
```