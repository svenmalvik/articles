# Hva er Service Discovery og når er det viktig?

https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/

Spørsmålet er hvor tjenesten vi skal kalle kjører.

Måten vi har løst det tidligere var å definere lokasjonen i en konfig fil. I skyen er det ikke mulig lenger fordi tjenester deployes dynamisk hvor som helst pga autoskalering, failovers og oppgraderinger.

## Client‑side discovery
Klienten selv er ansfarlig for å finne riktig netverk adresse av tilgjengelige instanser og lastbalansere requestene mellom de. Klienten bruker en servce registry for det.

The client queries a service registry, which is a database of available service instances. The client then uses a load‑balancing algorithm to select one of the available service instances and makes a request.

## Server‑side discovery
