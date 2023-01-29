## `Service`
`Service` Kubernetes to logiczna abstrakcja dla wdrożonej grupy `POD` w klastrze (które pełnią tę samą funkcję).

Ponieważ pody są efemeryczne, usługa umożliwia grupie podów, które zapewniają określone funkcje (usługi sieciowe, przetwarzanie obrazów itp.) przypisanie nazwy i unikalnego adresu IP (clusterIP). Dopóki usługa działa pod tym adresem IP, nie zmieni się. Usługi określają również zasady ich dostępu.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: service-python
spec:
  ports:
  - port: 3000
    protocol: TCP
    targetPort: 443
  selector:
    run: pod-python
  type: ClusterIP
```

`kubectl get svc` - pokaże nam aktywne service zdefniowane na klustrze