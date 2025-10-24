
**a. Hva er en default gateway? Hvorfor trenger vi denne?**
Default gateway er "gatewayen" mellom LAN og WAN, gjerne en ruter. Både IPv4- og IPv6-pakker som skal ut av intranettet sendes/hopper først til default gateway, som deretter tar seg av jobben med å rute pakkene videre. Når det kommer pakker fra WAN er det default gateway som igjen ruter pakkene så de kommer til riktig enhet.
Det er her man også gjerne har brannmuren for et nettverk.
For IPv4-pakker er det (som oftest) default gateway som har den offentlige IP-addressen for nettverket, og derfor denne ruteren som blir seende ut som avsender for en server (med mindre det er brukt CG-NAT eller annet addresse-besparende toplogier).
Vi trenger en default gateway for at alle enhetene på nettverket vet hvor de skal sende pakker ment for internettet; så det kun er en link mellom LAN og WAN. Det sparer også IPv4-addresser og gjør sikkerhet enklere.

**b. Gitt figuren nedenfor. Hvilken enhet/interface skal man bruke som default gateway for de merkede PCene? Begrunn valgene.**
Default gateway er neste hopp for pakker som skal oppstrøms, og i dette tilfellet er det ruterene.
H1 - R1 (G0/0)
K2 - R1 (G0/1)
Z3 - R3 (G0/0)

![[Oblig 5-1.png]]
**Gitt figuren nedenfor. Host A sender en pakke til Host C. Få med både source og destination address når du svarer på følgende:**
**c. Hvilke lag 2 og lag 3 adresser har pakken som sendes av Host A?**
Lag 3
Source IP: 172.16.10.100, Destination IP: 172.16.20.100
Lag 2:
Source MCA: 00-00-0c94-36-aa, Destination MAC: 00-00-0c94-36-ab


**d. Hvilke lag 2 og lag 3 adresser har pakken som mottas av Host C?**
Lag 3
Source IP: 172.16.10.100, Destination IP: 172.16.20.100
Lag 2:
Source MCA: 00-00-0c94-36-cd, Destination MAC: 00-00-0c94-36-cc
