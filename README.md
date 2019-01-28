# Elastic6-PurpleNectar2019

## Algemeen
Deze repo bevat een installatiehandleiding voor het installeren van een elasticsearch-omgeving t.b.v. een workshop Kibana op Purple Nectar 2019. De elasticsearch-omgeving wordt gevuld met een ritinformatie van taxi's in NYC.
Er is gekozen voor taxi-ritten omdat deze informatie goed begrijpelijk is voor een ieder met een IQ boven de 85.

Het idee is om uiteindelijk de data ingeladen en wel via Kibana te ontsluiten vanuit een docker contrainer.
Bij aanvang van de workshop kunnen de containers gestart worden zodat de uitgangspositie altijd gelijk is.

De oorspronkelijke dataset komt uit April 2015.
Er is gekozen voor deze dataset omdat in 2015 de New York Open Data voor Taxi's nog geo-locaties bevatten.
http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml

Op basis van een eenvoudige search and replace is het jaar 2015 vervangen door 2019.
Deze dataset bevat dus tijdens PN2019 data voor de gehele maand, inclusief de "last 15 minutes" (en de toekomst).
De aangepaste dataset is te vinden op:
https://www.dropbox.com/s/io0llunlr03qhze/green_tripdata_2019-04.csv?dl=0

De dataset bevat informatie van zogenaamde green taxi's/cabs.
Er is gekozen voor deze dataset omdat een volledige maand slecht 256MB groot is.
Dit komt omdat er aanzienlijk minder green cabs zijn t.o.v. yellow cabs.

bron: https://en.wikipedia.org/wiki/Boro_taxi -->
"Boro taxis (or boro cab) are taxicabs in New York City that are allowed to pick up passengers (street hails or calls) in outer boroughs (excluding John F. Kennedy International Airport and LaGuardia Airport unless arranged in advance) and in Manhattan above East 96th and West 110th Streets. **The color of boro taxis is apple green (bright green)** in contrast to the traditional yellow taxis in New York City." 

Bij het plotten van de pickup(geoip) in Kibana is duidelijk terug te zien dat er op Manhattan zeer weinig pickups zijn onder de bovengenoemde straten. Aan de deelnemers van de workshop kan dan ook gevraagd worden wat ze opvalt aan de visualisatie op de kaart. Tips boven de $100, levert ook leuke resultaten op.

### Pre-requirements
Om de omgeving te starten is het volgende benodigd (uitgaande van een Ubuntu 18.04 omgeving als user `root`):

1. Zorg dat [`docker`](https://docs.docker.com/install/linux/docker-ce/ubuntu/) is geinstalleerd
1. Zorg dat [`docker-compose`](https://docs.docker.com/compose/install/) is geinstalleerd:
```
curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### Data downloaden
1. Clone van deze repository:
```
git clone https://github.com/STROMANZ/Elastic6-PurpleNectar2019.git
```
2.  `cd` in de ge-clone-de directory en download de data:
```
cd Elastic6-PurpleNectar2019
./scripts/downloadData.sh
```

### Omgeving starten
Gebruik `docker-compose` om de stack te starten:
```
docker-compose up -d
```
