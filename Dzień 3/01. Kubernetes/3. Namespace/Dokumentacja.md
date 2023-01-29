# Namespace

`Przestrzenie nazw` to sposób organizowania klastrów w wirtualne podklastry — mogą być przydatne, gdy różne zespoły lub projekty współdzielą klaster Kubernetes. W klastrze obsługiwana jest dowolna liczba przestrzeni nazw, z których każda jest logicznie oddzielona od innych, ale z możliwością komunikowania się ze sobą. Przestrzenie nazw nie mogą być zagnieżdżane w sobie.

Każdy zasób istniejący w Kubernetes istnieje w domyślnej przestrzeni nazw lub przestrzeni nazw utworzonej przez operatora klastra. Poza przestrzenią nazw istnieją tylko węzły i woluminy trwałej pamięci masowej; te zasoby niskiego poziomu są zawsze widoczne w każdej przestrzeni nazw w klastrze.

Namespacy mają dwie najważniejsze chechy w ramach kubernetesa:
- Namespace organizuja wszystkie zasoby w ramach budowy kubernetesa
- Mozna powiedziec że to virtual cluster w clustrze 

wykonaj komende 

```
kubectl get namespaces
```
Wyświetli nam ona zasoby naszego klastra kubernetes

```bash
NAME              STATUS   AGE
default           Active   7h45m
kube-node-lease   Active   7h45m
kube-public       Active   7h45m
kube-system       Active   7h45m
```

`kube-system` :
- system processes
- master i kubectl processes
> Uwaga, nie wykonuj żadnych operacji w ramach tego namespace.

`kube-public`:
- publicznie dostepne dane
- Configmap z informacją o klastrze 

```
kubectl cluster-info
```

`kube-node-lease`:
- przechowuje informacje `heartbeats` każdego noda 
- kazdy node posiada wygospdarowany fragment w tym namespace
- okresla dostepnosc noda

`default`
- to namespace wejscia dla tworzeina nowych namespacow

```
kubectl create namespace my-namespace
kubectl get namespace
```

Inną opcją tworzenia osobnego namespace jest opcja tworzenia go w ramach pliku konfiguracyjnego

```yml
apiVertsion :1
kind: ConfigMap
metadata:
  name: mysql-configmap
  namespace: my-namespace
data:
  db_url: mysql-service.database
```