# Prototype
Jeg har laget en prototype ved bruk av Claude til å spore lastebilene. Sporingen skjer gjennom en mobilnetttilkoblet iPad montert i lastebilen. På denne appen kan man laste pakker inn i lastebilen, og spore pakker. Jeg har brukt Next.js, PostgreSQL (via NEON), Prisma (som ORM Løsning) og Leaflet.js for kart funksjonen. 

### Admin Dashboard
Gjennom Admin dashboarden får man oversikt over alle aktive kjøretøy, siste hendelser, og hvordan APIen fungerer. 

### Sjåførapp
På dette grensesnittet kan man laste pakker i bulk, oppdatere GPS på kjøretøyet og håndtere pakker manuelt som fallback.

### Kundeportal
Her kan kunder skrive inn et pakkenjummer og se hvor pakken befinner seg bassert på lastebilens siste GPS posisjon.

### GPS Tracking
For å oppdatere lastebilen sin posisjon sender man en post til /api/vehicles/gps. En request ser sånn ut ![[Pasted image 20260611111319.png]]
Man trenger riktig API key for bilen, jeg har også valgt å sende hastighetsdata sånn at man kan teoretisk estimere lastebilens posisjon basert på hastigheten til den forrige GPS pingen.

Akuratt nå så må sjåføren sende GPS posisjon manuelt ved å trykke en knapp på Sjåførappen. Men det går ann å koble APIen direkte opp mot en app som Dawarich.

### Uthenting av pakke posisjon
![[Screenshot 2026-06-11 at 11.19.05.png]]
Appen bruker denne koden til å finne posisjonen til en pakke. Først tar koden å sjekker at Pakken finnes i databasen, deretter finner den lastebilen (eller varehuset) pakken har en pointer til. Deretter henter den siste lokasjonen til denne lastebilen eller varehusets fastsatt posisjon. 

# Testing av Lastebilstatus
For å teste tilkoblingstatusen ville jeg ha laget en program som henter ut siste innsente possisjon til hver lastebil, og deretter gi brukeren en liste over alle lastebilene, og hvor lenge det har vært siden siste lokasjonsrapport.


![[lastebil_status_flytskjema.svg|484]]

Det som skjer når brukeren laster in nettsiden:
1. Programmet henter alle registrerte lastebilen fra Databasen
2. Henter den nyeste GPS-pinger for hver lastebil ID
3. Beregner differansen mellom siste GPS-ping og Nåtid
4. Basert på terskeler kan vi tildele hver lastebil en "Logisk Status" (f.eks. < 5 min = online, < 30 min = forsinket, > 30 min = frakoblet)
5. Dataen vises på siden i en liste som kan sorteres etter lastebil ID, eller tid siden sist ping.