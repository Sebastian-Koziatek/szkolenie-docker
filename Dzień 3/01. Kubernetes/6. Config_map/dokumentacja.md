# ConfigMap

`ConfigMap` to obiekt interfejsu API używany do przechowywania niepoufnych danych w parach klucz-wartość. Pody mogą wykorzystywać `ConfigMaps` jako zmienne środowiskowe, argumenty wiersza polecenia lub jako pliki konfiguracyjne w woluminie.

`ConfigMap` umożliwia oddzielenie konfiguracji specyficznej dla środowiska od obrazów kontenerów, dzięki czemu aplikacje można łatwo przenosić

### ConfigMaps i pody
Możesz napisać specyfikację poda, która odwołuje się do ConfigMap i konfiguruje kontenery w tym podzie na podstawie danych w ConfigMap. Pod i ConfigMap muszą znajdować się w tym samym `namespace`. 

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  creationTimestamp: 2016-02-18T18:52:05Z
  name: game-config
  namespace: default
  resourceVersion: "516"
  uid: b4952dc3-d670-11e5-8cd0-68f728db1985
data:
  game.properties: |
    enemies=aliens
    lives=3
    enemies.cheat=true
    enemies.cheat.level=noGoodRotten
    secret.code.passphrase=UUDDLRLRBABAS
    secret.code.allowed=true
    secret.code.lives=30    
  ui.properties: |
    color.good=purple
    color.bad=yellow
    allow.textmode=true
    how.nice.to.look=fairlyNice  
```

>Możesz przekazać argument --from-file wiele razy, aby utworzyć ConfigMap z wielu źródeł danych.

Można powiedzieć że config_map to zarządzca dla `secrets`

