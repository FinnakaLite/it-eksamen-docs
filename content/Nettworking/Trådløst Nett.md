# Ansatt Nett:
Ansatte logger inn på det trådløse nettverket med Entra-brukeren sin via 802.1X-autentisering. Aksesspunktet sender autentiseringsforespørselen til en RADIUS-server, som verifiserer brukeren mot Entra ID. RADIUS tildeler automatisk riktig VLAN basert på hvilken Entra-gruppe brukeren tilhører. Les mer om [[Entra ID]]

Grunnen til at jeg gjør dette fremfor et delt nettverkspassord (PSK) er at når en ansatt slutter, mister de umiddelbart tilgang bare ved å deaktivere Entra-kontoen — ingen endring av passord på alle enheter nødvendig. Det gir også full logging over hvem som er koblet til.


# Gjestenett:
Gjestenettet står åpent, og hvem som helst kan koble seg til dette nettet. Alle enheter på nettet er isolert fra hverandre. Siden nettet ikke har et passord betyr dette ofte at dataen som sendes mellom enheten og APen er Ukryptert. Dette løser vi med bruk av OWE (Opportunistic Wireless Encryption). OWE bruker nøkkeler på hver ende som krypterer dataen når enheten støtter dette. 

