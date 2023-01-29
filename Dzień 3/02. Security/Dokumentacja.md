# Skanowanie luk w zabezpieczeniach obrazów

Polecenie `docker scan` umożliwia skanowanie istniejących obrazów platformy Docker przy użyciu nazwy obrazu lub identyfikatora. Na przykład uruchom następujące polecenie, aby przeskanować obraz hello-world:
```bash
docker scan hello-world
```
Możesz uzyskać szczegółowy raport ze skanowania obrazu Dockera, dostarczając plik Dockerfile użyty do utworzenia obrazu. Składnia jest
```bash
docker scan --file Dockerfile <nazwa_obrazu>
```

Aby uzyskać więcej darmowych możliwości skanowania zarejestruj się poprzez użycie:

```bash
docker scan --file Dockerfile docker-scan:e2e
```

Więcej informacji na temat docker scan znajdziesz w dokumentacji - https://docs.docker.com/engine/scan/. 

Jeżeli posiadasz konto docker z planem conajmniej pro który oferuje aktualnie 300 skanów, to takie skany możesz przeprwoadzać bezpośrednio w aplikacji `docker desktop` oraz na przykład w swoim repozytorium