# Deployment 

Kubernetes `Deployment` informuje Kubernetes, jak tworzyć lub modyfikować wystąpienia podów, które przechowują aplikację kontenerową. Wdrożenia mogą pomóc w efektywnym skalowaniu liczby `ReplicaSet`, umożliwieniu wdrożenia zaktualizowanego kodu w kontrolowany sposób lub przywróceniu w razie potrzeby wcześniejszej wersji wdrożenia. Wdrożenia Kubernetes są wykonywane przy użyciu kubectl, narzędzia wiersza polecenia, które można zainstalować na różnych platformach, w tym Linux, macOS i Windows.

>Można by określić to jako pewnego rodzaju nadzorce dla `replicaSet`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```