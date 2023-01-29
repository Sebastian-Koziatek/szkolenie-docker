# Debugowanie 

Debugowanie skonteneryzowanych aplikacji możemy podzielić na trzy warstwy:
1. Po pierwsze debugowanie i diagnostyka samego kontera za pomoca dockera, przeglądanie logów itd. 
2. Po drugie debugowanie i diagnostyka systemu na którym stoi w kontenerze nasz a aplikacja. 
3. Po trzecie to diagnostyka samej aplikacji, ale ta zależy od języka, technologii, zastosowanych rozwiązań itd. Powinna być wykonywana przez developera, tak samo jakby nie była w kontenerze. 

# Debugowanie kontenerów

1. Wiele programów loguje rzeczy do `stdout`*. Wszystko co daje sie zapisać do procesu `stouta` w konterze zostaje przechwycone do pliku historii na hoscie, gdzie mozną ja wyświetlić za pomocą polecenia logs.
> stdout - standardowy strumień komunikacji między komputerem a otoczeniem (zwykle terminalem). Występują w Uniksie i systemach uniksopodobnych, w środowisku uruchomieniowym C, C++ i ich pochodnych. Trzy podstawowe połączenia I/O noszą nazwy: standard input (stdin, standardowy strumień wejścia), standard output (stdout, standardowy strumień wyjścia) i standard error (stderr, standardowy strumień błędów). 
 
Żeby dobrze to zobrazować sciągnij sobie obraz jenkinsa i go wystartujemy.

```
docker run -d --name jenkins jenkins/jenkins:lts
```
Teraz mamy dostep do logów kontenera jenkins
```
docker logs jenkins
```
2. Docker stats - Jedną z rzeczy do weryfikacji poprawnego dzialania kontenera jest jego zaopatrznie w zasoby, do tego możemy użyc polecenia stats.  
```
docker stats <container_id>
```

3. `docker cp` to polecenie które pozwoli kopowiać wybrane pliki lub foldery z kontenera do naszej lokalnej ścieżki. Możemy dzięki temu np pobrać logi albo sprawdzić jakiś folder przy użyciu narzędzie których nie mamy na kontenerze.
   
```
docker cp <container_id>:/path/to/useful/file /local-path
```
skopiujmy z naszego obrazu my-nginix katalog /tmp w ktorym jest nginix
```
docker cp <container_id>:/tmp /tmp/data
```

4. To polecenie pozwala nam na zalogowanie się do powloki działającego kontenera. Dzieki temu można przeprowadzić pełną diagnostykę systemu. 
```
docker exec -it <container_id> /bin/bash
```
   
5. Nie możesz w ogóle uruchomić kontenera? eśli masz początkowe polecenie lub punkt wejścia, który natychmiast się zawiesza, Docker natychmiast go wyłączy. Może to uniemożliwić uruchomienie kontenera, więc nie będziesz mógł już więcej sprawdzić co się dzieję. Na szczęście istnieje obejście: zapisz bieżący stan zamykanego kontenera jako nowy obraz i uruchom go innym poleceniem, aby uniknąć istniejących awarii.

```
docker commit <container_id> moj-uszkodzony-kontener && docker run -it moj-uszkodzony-kontener /bin/bash
```

> To polecenie zapisze stan zmaykanego kontenera jao nowy obraz, uruchomi go oraz da nam możliwość wejścia do powłoki w celu diagnostyki.


# Debugowanie systemu 

1. Najczęściej używanym poleceniem do monitorowania kontera pod kontem diagnostyki systemu jest polecenie top. Jest dokładnie to samo co `docker stats`.

```bash
top
```
2. Tym poleceniem - vmstat, będziemy się posługiwać jeżeli będziemy potrzebowali dostainformacje co się dzieję w kwestii pamięci na systmie.

```bash
vmstat
vmstat -a
vmstat -s
```

3. Aby sprawdzić co jest uruchomione w danym momencie w naszym systemie wykonujemy to polecenie. Pozwala to nam na wylistowanie uruchomionych aplikacji ich PID.

```bash
ps
```

# Diagnostyka aplikacji

Diagnostyka aplikacji zależy od języka, technologii itd itp. Powinna być wykonywana przez developera, tak samo jakby nie była w kontenerze. 