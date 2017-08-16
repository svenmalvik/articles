# Hva er Service Discovery og når er det viktig?

https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/

Spørsmålet er hvor tjenesten vi skal kalle kjører.

Måten vi har løst det tidligere var å definere lokasjonen i en konfig fil. I skyen er det ikke mulig lenger fordi tjenester deployes dynamisk hvor som helst pga autoskalering, failovers og oppgraderinger.

## Client‑side discovery
Klienten selv er ansfarlig for å finne riktig netverk adresse av tilgjengelige tjeneste-instanser. Klienten slår informasjonen opp i Servce Registry-en. Klienten lastbalansere requestene mellom disse. 

## Server‑side discovery
Klienten kommuniserer kun med lastbalanseren som selv slår opp i Service Registry-en for å finne mulige netverk adresser til tjenester.

-Bilde
The client makes a request to a service via a load balancer. 
The load balancer queries the service registry and 
routes each request to an available service instance. 

AWS Elastic Load Balancer (ELB) er en server-sidige discovery ruter. ELB-en brukes vanlig til å lastbalansere ekstern trafikk fra internett, men kan også brukes for intern trafikk i virtual private cloud (VPC). 
EC2 instanser og ECS kontainere registreres i ELB.

HTTP servers og lastbalansere som NGINX Plus og NGINX kan også brukes som server-sidig discovery lastbalanser. 

I noen miljøer som i Kubernetes og Marathon kjører det en proxy på enhver host i et cluster. Proxy-en er i dette eksempelet en server-sidig discovery lastbalanser. Klienten ruter requesten via proxy-en med host’s IP address og service’s assigned port. Proxy-en videresender requesten til en tilgjengelig service instans som kjører på en eller annen node i klusteret.

Fordelen med server-sidig discovery er at den abstraherer detailjer vekk fra klienten. Klientene forholder seg enkelt og greit til lastbalanseren.

Ulempen er at det introduseres nok en kritisk system komponente.


## Service Registry
Service instances registreres og de-registreres i Service Registry-en.
