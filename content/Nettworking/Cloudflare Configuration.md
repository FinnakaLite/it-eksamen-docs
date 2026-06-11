Jeg bruker Cloudflare for å koble sammen nettverk på flere fysiske lokasjoner. Dette er mye enklere å bruke enn en "site-to-site VPN" siden den lager en mesh, dermed trenger ikke all trafikken å gå gjennom et knutepunkt. Vi bruker Entra ID som vår SSO løsning, bruker og enhets grupper i cloudflare blir delt ut automatisk bassert på sikkerhetsgrupper i Entra. Les mer om hvordan vi bruker [[Entra ID]]

![[Screenshot 2026-06-10 at 11.33.04.png]]

### Firewall Rules:
Jeg starter med å lage regler for å blokkere nesten all trafikk mellom nettverkene. Deretter åpner jeg opp for tilgang til ressursnettverkene. Klientene burde ikke trenge mer tilgang enn dette. Når det gjelder firewall-regler mellom lokale VLAN-er gjøres dette ikke på Cloudflare.
![[Screenshot 2026-06-10 at 11.55.30.png]]![[Screenshot 2026-06-10 at 11.55.47.png]]![[Screenshot 2026-06-10 at 11.56.02.png]]![[Screenshot 2026-06-10 at 11.56.13.png]]

# Hvordan virker det?
![[diagram-export-11-06-2026-11_47_48.svg]]