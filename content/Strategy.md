# Nettverk:
### Ved sentralen:
Det skal lages et nettverk for logistikksentralen med dekning over hele sentralen. Nettet skal deles inn i flere VLAN-er. I denne situasjonen bruker jeg et standard UniFi-oppsett, siden dette er enklere å visualisere. UniFi har blitt mye mer avansert enn det var før, og med moderne UniFi-produkter så klarer den alt vi trenger. 

### På håndterminaler:
Håndterminalene skal kobles til trådløst nett, men de skal også ha mobilnett. Mobilnettet skal kobles opp til Cloudflare One slik at de kan få sikker tilgang til ressursene som håndterminalene krever. 

### På kjøretøyklienter:
Dette gjøres i form av en iPad med mobilnett som er koblet opp til Cloudflare One. 

### Cloudflare One:
Vi kjører en liten klient i serverrommet som kobler det lokale nettet opp til Cloudflare via Cloudflare Routes. Grunnen til at jeg gjør dette er at det gjør det svært enkelt å koble til Azure eller andre ressurser som ikke er fysisk på samme lokasjon. Ved å bruke Cloudflare unngår vi å bruke en VPN, dette er mer sikkert og unngår at vi sender all trafikk gjennom en sentralisert VPN-server. 

