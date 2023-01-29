# Skalowanie aplikacji z docker-compose
1. Zbuduj z podanego `docker-compose.yml`  kontener
2. Wejdz na localhost:8080
3. Wejdz w sekcje load balancer - 
`HTTP Services > All status > Host('localhost') > whoami-skalowanieaplikacji@docker`
4. Sprawdż liczbę serwerów loadbalancerów dostepnych dla Traefika.
5. Za pomocą docker-compsoe zamknij kontener
6. Dodaj odpowiedni wpis do docker-compose tak aby dodać 5 loadbalancerów dla naszego kontenera z trafeikiem.
7. Zbuduj kontener ponownie
8.  Wejdz na localhost:8080 i sekcje load balancer - 
`HTTP Services > All status > Host('localhost') > whoami-skalowanieaplikacji@docker`
9. Sprawdź czy widzisz teraz 5 load balancerów 