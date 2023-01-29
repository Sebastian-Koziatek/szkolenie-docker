# Volumes

Pliki na dysku w kontenerze są efemeryczne, co stwarza pewne problemy w przypadku nietrywialnych aplikacji działających w kontenerach. Jednym z problemów jest utrata plików w przypadku awarii kontenera. Kubelet ponownie uruchamia kontener, ale z czystym stanem. Drugi problem występuje podczas udostępniania plików między kontenerami działającymi razem w pode. Abstrakcja woluminu Kubernetes rozwiązuje oba te problemy.

Przykład volumenu używanego w AWS EBS

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-ebs
spec:
  containers:
  - image: registry.k8s.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /test-ebs
      name: test-volume
  volumes:
  - name: test-volume
    # This AWS EBS volume must already exist.
    awsElasticBlockStore:
      volumeID: "<volume id>"
      fsType: ext4
```