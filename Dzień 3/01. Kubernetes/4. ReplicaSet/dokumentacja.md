# ReplicaSet

Celem `ReplicaSet` jest utrzymanie stabilnego zestawu replik podów działających w dowolnym momencie. Jako taki jest często używany do zagwarantowania dostępności określonej liczby identycznych Podów.

### Jak działa `ReplicaSet`?
ReplicaSet jest zdefiniowana za pomocą pól, w tym selektora, który określa, jak zidentyfikować pody, które może pozyskać, liczby replik wskazujących, ile podów powinien być utrzymywany, oraz szablonu poda określającego dane nowych podów, które należy utworzyć, aby spełnić tę liczbę kryteriów replik. ReplicaSet następnie spełnia swój cel, tworząc i usuwając pody w razie potrzeby, aby osiągnąć żądaną liczbę. Gdy ReplicaSet musi utworzyć nowe pody, używa swojego szablonu podów.

> Jest to w pewnym sensie zarządca skalowania kontenerów pokazanego w lekcji o `docker-compose`. Na k8s jest mocno rozbudowany i może być konfigurowany za pomcą pliku yaml lub w konfiguracji samego k8s.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  # modify replicas according to your case
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: php-redis
        image: gcr.io/google_samples/gb-frontend:v3
```