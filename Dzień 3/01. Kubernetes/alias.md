Alias do podmiany komendy kubectl na komende używającą pliku yaml.

```
cd ~:/.
nano .bashrc
```

dopisz na końcu pliku

```
alias kubectl='kubectl --kubeconfig=/Volumes/Storage/k8s/k8s-1-24-4-do-0-lon1-1664810780234-kubeconfig.yaml'
```

Przeładuj powłokę poleceniem `bash`