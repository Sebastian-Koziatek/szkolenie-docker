

#  POD


















## Uruchamiamy poda i wystawiamy go na świat. 
____

W katalogu POD znajduje się przygotowany prosty plik yaml z nginx.

1. Upewnijmy się że `kubectl` poprawnie widzi `nod`. Wykonaj polecenie

```
kubectl get nodes
```
2. Jeżeli wszystko jest ok to z pliku mynginix-pod.yaml utwórz pierwszego `PODA`
```
kubectl create -f nginx-pod.yaml 
```
3. Sprawdź czy POD jest widoczny w klustrze.

```
kubectl get pod 
```
4. W kubernetesie mamy pełną mozliwośc podejrznia tekiego poda w ramach namespacu. Wykonaj poniższe polecenie i zapoznaj się z outputem.

```
kubectl describe pod nginx
```

5. Skasuj `POD`
   
```
kubectl delete pod nginx
```

# Uruchomienie poda i wystawienie go na świat na przykłądzie kubernetesa z 2 nodami i publicznym adresem IP.

1. Skorzystami z gotowego kontenera który zawiera skrypt loudbalancera.

```
kubectl apply -f https://k8s.io/examples/service/load-balancer-example.yaml
```

2. Sciągniemy teraz gotowy deplyomets zawierający prostą stronę `hello world`
   
```
kubectl get deployments hello-world
kubectl describe deployments hello-world

```

3. Pobierzemy informacje o `replicasets`

```
kubectl get replicasets
kubectl describe replicasets
```

> Uwaga! Zanim wykonasz nastepny krop upewnij się że zaden service nie jest już wystawiony na publiczny adres ip!
4. Stwórzym `service` który wystawi nam nasz deployments
   
```
kubectl expose deployment hello-world --type=LoadBalancer --name=my-service
```

5. Wyświetlmy informacje o tym `service`

```
kubectl get services my-service
```

Po wykonaniu tej komendy output pownien docelowo wyglądać tak:
```
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)          AGE
my-service   LoadBalancer   10.245.100.2   159.89.249.226   8080:31690/TCP   19m
```

> Zanim wartość `EXTERNAL-IP` się ustawi to może minąc do 20 min czasu. Wczesniej otrzymacie taki output

```
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
my-service   LoadBalancer   10.245.100.2   <pending>     8080:31690/TCP   72s
```

6. Na koniec prośba o posprzątaine:

```
kubectl delete service my-service
kubectl get replicasets
kubectl delete replicasets <name>
kubectl delete deploy hello-world
```
> Dzieki :). 