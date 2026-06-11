## Mål
For jeg ville ha startet på å lage en brukerveiledning må vi avklare hvilke mål vi har. Jeg refererer herved til denne brukerveiledningen/onepager filen som "Produktet"

Hovedmålet er å fikse nett problemene så fort som mulig, men jeg synes at det er svært viktig å ta med oss følgende sekundærmål:
1. Produktet skal ikke ta fokus vekk fra veien. Vi må presisere at sjåføren skal parkere før de begynner med veilederen.
2. Produktet skal være så visuelt som mulig, vi vil unngå å ha for mye tekst i dokumentet
3. Enklere hjelp fra IT Avdelingen. Hvis problemet ikke kan løses av produketet, skal det stå en liste over informasjon man skal hente ut til IT avdelingen. Dermed får man hjelp mye fortere. 
	1. Dette kan fks være informasjon som Serienummer på iPad, får man kontakt med andre nettsider osv.

## Stuktur
Jeg ville ha laget en flowchart med konkrete handlinger som brukeren kan følge. Alt sjåføren trenger å gjøre, er finne onepageren som heter "Nett problemer nettbrett/scanner" og starte på toppen av arket. Med å ha en flowchart reduserer vi terskelen av IT kompetanse som kreves for å løse problemet. De trenger kun å følge stegene, og trenger ikke å tenke på mye annet. 
## Pedagogiske Virkemidler
Det er viktig å huske at sjåfører er ikke IT-Personell og de leser ofte veiledningen under mye stress. Stress blir enda verre når man ikke forstår teknologien, man har sikkert opplevd dette når man hjelper foreldrene med IT, de blir fort irritert og gir opp. 

Ved å bruke en flowchart med konkrete handlinger og Ja/Nei svar kan vi redusere stress nivået.
### Ikoner:
Bruk ikoner til å gjøre feilsøkingsprosessen så enkelt som mulig. Eksempel:

**IKKE Gjør dette:** "Sjekk hvis Cloudflare ikonet lyser grønt og er aktiv" Vi kan ikke forvente at brukeren vet hva cloudflare er, der er ikke jobben deres å vite. 

**Gjør dette:** "Se etter dette ikonet på øveste venstre hjørnet på iPaden (Sett inn bilde av ikonet). Er skyen grønn?"
### Farger:
Det kan være fint å bruke farger for å understreke hvis en av feilsøkingstegene trenger ekstra fokus. For eksempel hvis en av stegene kreves avinstallering av et program er det viktig å presisere at brukeren må være sikker på at de sletter riktig app.

## Feilmeldingskjema
Det er en veldig god ide å inkludere informasjon som sjåføren skal samle inn før de ringer. Her er et eksempel fra Claude om informasjonen som vi kan be sjåføren sende inn med sin ticket.

![[Screenshot 2026-06-11 at 12.25.22.png]]
Her unngår vi å gå gjennom flere steg som sjåføren allerede har prøvd.

## IT-Avdelingen
IT avdelingen bør bruke informasjonen de får tillsent av sjåføren til å utarbeide en plan på hvordan de ønsker å løse saken. 

Siden dette er et problem som er alvorlig nokk til at sjåføren må stanse lastebilen ville jeg definere saken som kritisk. Hovedfokuset skal altid være å få lastebilen tilbake på ruten sin, så fort og sikkert som mulig. Dette bør avdelingen gjøre gjennom en SLA plan, et eksemepel av en sånn plan er:
	IT avdelingen skal prøve å løse problemet med nettet så fort som mulig, hvis avdelingen ikke klarer å fikse problemet innen (fks. 30 minutter) skal de ta en vurdering om hvis lastebilen kan forsette å kjøre uten systemet. 
Da bør IT Avdelingen allerede ha en standardisert rutine for "Kjøring uten iPad med Nett" som de kan tilsende sjåføren. 

IT Avdelingen bør sammenligne med andre saker for å identifisere om de har noe til felles, eller hvis der er et problem som oppstår flere ganger. Derfor er det viktig å dokumentere saken i et ticket system.