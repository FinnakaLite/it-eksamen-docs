## VLAN 10 - Enhets Administrasjon 
#### Subnett: 172.31.254.0/24
Administrasjonsnettverket vil kun bli brukt til at AP-er, svitsjer og annen infrastruktur skal kommunisere med hverandre. Ingen brukere vil være til stede på dette nettverket. Brannmurregler vil bli satt opp for å forhindre kommunikasjon med dette nettverket på noen måte.

## VLAN 11 - Felles ressurser (Lokalt):
#### Subnett: 10.1.11.0/24
Dette nettverket skal inneholde ressurser som brukes av alle teamene. Dette inneholder printere, smartboards, møterom etc. Alle portene som står åpne på dette VLAN-et skal bruke Port Security. Dette betyr at bare én enhet, med riktig MAC-adresse, får lov til å koble seg opp til den porten. Dette nettet inkluderer ikke ressurser som servere, og det er ikke mulig å koble seg til dette nettet fra eksterne enheter slik som Cloudflare One-enheter.

## VLAN 12 - Felles ressurser (Globalt):
#### Subnett: 10.1.12.0/24
Dette nettet skal inneholde ressurser som man skal få tilgang til fra hvor som helst via Cloudflare One. Dette inkluderer lokale servere, kasseadministrasjonssystemer etc. Servere som ligger i skyen skal få en direkte kobling opp mot dette nettet. Grunnen til at vi ikke setter printere på dette nettet er fordi det er unødvendig — printere brukes kun lokalt og trenger ikke ekstern tilgjengelighet.

## VLAN 20 - Administrative Ansatte:
#### Subnett: 10.1.20.0/23
Dette nettet brukes til alle ansatte som driver med kontorarbeid. Full tilgang til lokale og globale felles ressurser. 

## VLAN 30 - Feltarbeidere:
#### Subnett: 10.1.30.0/23
Dette nettet brukes til feltarbeidere, vanligvis bare håndterminaler og iPad-er til sjåfører. Dette nettet har tilgang til globale felles ressurser, men på lokale fellesressurser har de kun tilgang til printere. Feltarbeidere trenger ikke tilgang til møteromsressurser, dette er en unødvendig sikkerhetsrisiko.

## VLAN 111 - Gjestenett
#### Subnett: 10.111.0.0/19
Gjestenettverket vil være isolert fra alle andre VLAN-er, og alle enheter på nettverket vil være isolert fra hverandre. Dette betyr at enheter på gjestenettverket bare vil kunne kommunisere med ruteren. Gjester og alle personlige enheter som telefoner og smartklokker vil være på dette nettverket, ettersom disse ikke trenger lokal nettverkstilgang. Ingen multicast-trafikk er tillatt på dette nettet, derfor er det ikke et problem at subnettet er så stort.

## VLAN 15 - Cloudflare Uplink
#### Subnett: 10.1.15.0/30
Spesielt nettverk for enheten som kjører Cloudflared-connectoren. Dette nettet bruker en /30-adresse siden det kun trenger to brukbare IP-er: én til ruteren og én til Cloudflare-hosten. Grunnen til at vi har dette nettet er for å sende trafikk til Cloudflare. Dette nettet har full tilgang til alle VLAN-er bortsett fra Enhetsadministrasjon og Gjestenettet. Firewall policies konfigureres i Cloudflare.

## Cloudflare VPC
### Les mer om Cloudflare her: [[Cloudflare Configuration]]
Enheter koblet til Cloudflare One får en IP-adresse tildelt av Cloudflare-serverne. Vi bruker 10.8.0.0/16 som overordnet range for å identifisere IP-er i Cloudflare-nettet. Dette er ikke et VLAN, men et eksternt nett som rutes via Cloudflare Uplink-enheten.

### IP-ranges i Cloudflare-nettet:
#### Ressurser (Servere, Osv.): 10.8.12.0/23
Range for normal use: 10.8.12.10-10.8.12.254 (Rest of IPs are reserved for possible expansion later) x.x.12 used to identify devices as a global resource
#### Håndterminaler: 10.8.16.0/20
Range for normal use: 10.8.16.10-10.8.19.254 (Rest of IPs are reserved for possible expansion later)
#### Kjøretøyklienter: 10.8.32.0/20
Range for normal use: 10.8.32.10-10.8.35.254 (Rest of IPs are reserved for possible expansion later)
#### Administrative ansatte remote: 10.8.64.0/20
Range for normal use: 10.8.64.10-10.8.67.254 (Rest of IPs are reserved for possible expansion later)
## Brannmur – VLAN-tilgangsoversikt (Lokalt)

Tabellen viser hvilken tilgang hvert VLAN har til de andre. Regler håndheves på ruteren (Dream Machine Pro). "Ja" betyr tillatt, "Nei" betyr blokkert. Cloudflare-spesifikke regler håndteres separat i Cloudflare Zero Trust.

| Fra \ Til             | VLAN 10 Admin | VLAN 11 Lokale res. | VLAN 12 Globale res. | VLAN 15 CF Uplink | VLAN 111 Gjest |
| --------------------- | :-----------: | :-----------------: | :------------------: | :---------------: | :------------: |
| VLAN 10 Admin         |       —       |         Nei         |         Nei          |        Nei        |      Nei       |
| VLAN 11 Lokale res.   |      Nei      |          —          |         Nei          |        Nei        |      Nei       |
| VLAN 12 Globale res.  |      Nei      |         Nei         |          —           |        Nei        |      Nei       |
| VLAN 20 Admin ansatte |      Nei      |         Ja          |          Ja          |        Nei        |      Nei       |
| VLAN 30 Feltarbeidere |      Nei      |    Kun printere     |          Ja          |        Nei        |      Nei       |
| VLAN 15 CF Uplink     |      Nei      |         Ja          |          Ja          |         —         |      Nei       |
| VLAN 111 Gjest        |      Nei      |         Nei         |         Nei          |        Nei        |       —        |
>[!info] Det er viktig å merke at ingen VLANS har **DIREKTE** tilgang til CF Uplink nettet, de sender dataen til ruteren, som deretter videresender dataen til Cloudflared Serveren. Klienten ser ikke at cloudflare nettverket ligger i skyen.

