# Server Rommet (Core Components):
![[Pasted image 20260611104940.png|469]]

### Dream Machine Pro (Ruter)
Jeg bruker en UniFi Dream Machine Pro som min hovedruter. Denne modellen er sterk nok for det arbeidet vi skal gjøre, den kombineres med en til UDM Pro som oppererer i "Shadow Mode". Dette gir oss en failover løsning i tilfelle en ruter går ned. 

### Aggregation Switch:
Denne switchen bruker vi til å sende ut nettet til Edge Switches som er for langt vekk til å nå med kobberkabler, dermed bruker vi SFP med fiberkoblinger. 

### Switch Pro 24 PoE
Dette er en level 3-switch som vi bruker som vår core switch. Den har PoE++ som vi bruker til å gi strøm til Edge Switches og aksesspunktene. 

### Cloudflare Host
Dette er en Linux-maskin som kjører Cloudflared og hjelper med å koble opp mot vår Cloudflare VPC. Den ligger på sitt eget VLAN og kobles direkte inn i ruteren, deretter lager jeg routing-regler i ruteren som sender 10.8.x.x-trafikk via serveren. 

### Redundant Power
Dette er Ubiquiti sin versjon av en UPS. Den kan tilby ekstra strøm i tilfelle det blir et strømbrudd på lokalet. Dette er mer viktig hvis vi har sikkerhetskameraer på lokalet, men det er fint å ha likevel.

# Edge Switches
Logistikksentralen er veldig stor. Ved å bruke Edge Switches unngår vi å trekke kabler hele veien fra serverskapet ut til hver enhet. Jeg bruker to forskjellige typer switches: "Ultra 60W" og "Flex 2.5G PoE". 

Ultra 60W har 8 PoE+-porter og kan forsynes med strøm med PoE++. Dermed trenger vi ikke å finne en stikkontakt når en switch skal f.eks. monteres i taket. I de fleste tilfellene er Ultra 60W perfekt til det vi prøver å oppnå.

Et problem med Ultra 60W er at den kun har RJ45-porter. Dermed må vi bruke Flex 2.5G når en edge switch er for langt vekke. Flex 2.5G har en SFP+-port og kan dermed motta signaler via fiber. CAT-kabler kan oftest bare være 100 m lange, med fiber kan vi sende signaler i flere kilometer. Siden det ikke er mulig å sende strøm via fiber, trenger Flex 2.5G egen strømforsyning.

# Access Points
Jeg bruker 3 forskjellige aksesspunktmodeller, alle fra UniFi sin U7-serie. Forskjellige modeller tilbyr sine egne styrker, men for å sikre at de fungerer fint med hverandre er det ofte lurt å skaffe aksesspunkter fra samme leverandør og serie.

### U7 Long Range
Jeg bruker U7 Long Range når det kreves et aksesspunkt som skal dekke et stort areal. U7 LR koster mer enn andre U7-modeller, men sparer penger i det lange løp siden vi ikke trenger å montere så mange aksesspunkter. 

### U7 Mesh
Jeg bruker 2 U7 Mesh-aksesspunkter og monterer dem ute. U7 Mesh kan monteres utvendig på en stolpe på bygget. U7 Mesh tåler utendørsklimaforhold og er dermed perfekt for å ha på parkeringsplassen slik at lastebilsjåførene har tilgang til internett mens de venter på neste last. 

### U7 Lite
Dette er den billigste versjonen av U7-serien. Den tilbyr helt grei hastighet, men har mindre rekkevidde og klientkapasitet, derfor monterer jeg disse i områder med mindre fottrafikk der vi kan forvente at maks 10 enheter er påkoblet på en gang. 
