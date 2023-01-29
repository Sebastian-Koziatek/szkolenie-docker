# Secrets

`Secrets` to obiekt zawierający niewielką ilość poufnych danych, takich jak hasło, token lub klucz. Użycie klucza tajnego oznacza, że ​​nie musisz zawierać poufnych danych w kodzie aplikacji.

Ponieważ `Secrets` mogą być tworzone niezależnie od Podów które ich używają, istnieje mniejsze ryzyko ujawnienia `Secrets` (i jego danych) podczas tworzena, przeglądania i edytowania Podów. Kubernetes i aplikacje działające w klastrze mogą również stosować dodatkowe środki ostrożności w przypadku obiektów tajnych, na przykład unikając zapisywania tajnych danych w magazynie nieulotnym.

```yaml
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file, it will be
# reopened with the relevant failures.
#
apiVersion: v1
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
kind: Secret
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: { ... }
  creationTimestamp: 2020-01-22T18:41:56Z
  name: mysecret
  namespace: default
  resourceVersion: "164619"
  uid: cfee02d6-c137-11e5-8d73-42010af00002
type: Opaque
```