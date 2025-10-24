[https://1drv.ms/w/c/abfe028a3358625f/EUy4FcmEbSNBoy\_tT\_ALYCMBnHKERAee\_GcFVZ0HSEnYsg?e=PYZNAn](https://1drv.ms/w/c/abfe028a3358625f/EUy4FcmEbSNBoy_tT_ALYCMBnHKERAee_GcFVZ0HSEnYsg?e=PYZNAn)
# Jukselapp
## Default gateway
## OSI-modell: lag 2 og 3
## Gangen i en forespørsel
1. Navnesøk
	1. DNS-protokollen
	2. DNS lokalt
	3. DNS-servere
2. MAC-søk
	5. ARP-forespørsel til default gateway
3. Sende forespørsel/pakke
	4. TCP-protokollen
	6. Default gateway
4. Motta pakker
	1. Brannmur

# 2021 vår kont
Oppgave 3 (bokmål)
**a. Forklart kort hva du trenger for å:**
**i. Kommunisere med en enhet på ditt lokale nettverk**
**ii. Kommunisere med en enhet på et annet nettverk**

> For å kommunisere lokalt må man ha tilgang til et fungerende media som for eksempel en kablet link, eller en trådløs forbindelse. Deretter må man vite MAC-adressen til motparten for å kunne sende trafikk dit. Dersom man har IP-adressen, kan man etterspørre MAC-adressen over nettverket eller omvendt.

> For å kommunisere eksternt er man avhengig av å vite IP-adressen man skal sende til, samt ha en fungerende default gateway på lag 3 man kan sende trafikk mot. Vet man ikke adressen til mottaker, kan den eventuelt slåes opp hos en DNS-server.

**b. Forklar forskjellen på båndbredde, throughput og goodput.**
> Båndbredde er den maksimale teoretiske hastigheten på et gitt medium med en gitt protokoll eller teknologi. Eksempelvis Ethernet med kobberkabel og en Gigabit link, da er båndbredden 1 Gbps.

> Throughput er den faktiske overføringsraten, og er vanligvis lavere enn båndbredden. Den påvirkes av mengden trafikk, type trafikk, og antall hopp fra kilde til destinasjon.

> Goodput er hvor mye nyttedata som er overført over en gitt tid, det vil si throughput minus trafikk overhead (etablere tilkoblinger, metadata, enkapsulering, retransmisjoner, osv.). Goodput er alltid lavere enn throughput.

**c. Forklar hvorfor vi har åpne standarder, og hva som er fordelene med dette.**
> Vi har åpne standarder for å sikre interoperabilitet, konkurranse og innovasjon. Vi unngår også monopoler. Dette gjør at vi kan kjøpe en smarttelefon fra en hvilken som helst produsent, og så lenge de følger standardene, så vil den kunne bruke både mobilnett og WiFi uavhengig av hvem som har produsert WiFi-ruteren eller radioene til mobilnettet. Små produsenter kan lettere komme seg ut på markedet, da de ikke blir låst ute så lenge de har åpne standarder å følge.

**d. Forklar hvorfor vi segmenterer IP-pakker.**
> Dette er litt det samme som fletting i biltrafikken. Hvis man ikke gjorde dette, kan det bli mye venting for å komme til. Store filer ville tatt opp hele linken i relativt lang tid. Hvis en del av infrastrukturen gikk ned under en stor filoverføring, måtte man ha begynt på nytt. Segmentering forhindrer dette ved å la oss multiplekse trafikken, og alle segmentene trenger ikke å reise samme vei. På denne måten kan vi utnytte flere linker til samme mål. Hvis et segment skulle gå tapt, trenger man bare sende det tapte segmentet på nytt.

e. Hva er det første en switch gjør når den mottar en «frame»? Beskriv prosessen fram til switchen videresender denne.
> Den sjekker source MAC adresse opp mot sin egen tabell. Hvis den ikke allerede ligger i tabellen, legges den til sammen med portnummeret den kom inn på. Hvis den eksisterer, oppdateres refresh timeren for den adressen (timer som sletter adressen etter X sekunder, typisk 5 min). Hvis adressen har byttet port, behandles det som en ny adresse og den gamle erstattes.

> Deretter sjekkes destinasjonsadressen. Hvis denne eksisterer i tabellen, sendes framen ut på tilhørende port. Hvis ikke, floodes den ut på alle porter med unntak av porten den kom inn på.

f. Hva er et broadcast domene? Forklar hvorfor vi prøver å begrense størrelsen på disse.
> Et broadcast domene er hvor langt man kan nå med broadcast trafikk. Da broadcast trafikk ikke videresendes av rutere, er dette typisk begrenset til det lokale nettverket med tilhørende switcher og enheter (PCer, mobiler, andre tilkoblede enheter).
> 
> Grunnen til at man vil begrense størrelsen på broadcast domener er at broadcast trafikk må behandles av alle enhetene som mottar den. Dette vil si at hver enhet må åpne og eventuelt videresende broadcast meldingen, samt sjekke om denne er relevant for seg. I mange tilfeller er den ikke det. Dette gjør at jo flere enheter man har i samme broadcast domene, jo mer unødvendig trafikk får man. Dette belaster både nettverket og enhetene. Nettverket går tregere, enhetene må bruke tid og ressurser på å lese meldingene, og enheter på batteri går fortere tom.

g. Dersom Host A sender en IP-pakke til Host B, hva blir destinasjonsadressene (lag 2 og 3) når pakken forlater Host A? Endres disse underveis? Skriv ned og begrunn kort.
> Destinasjonsadressene blir på lag 2 MAC-adressen til neste hopp. Dette er ruteren R2 med MAC BB:BB:BB:BB:BB:BB.
> 
> På lag 3 blir det endepunktadressen, det vil si Host B sin IP-adresse: 172.168.11.88
> 
> Lag 2 adressen endres ved hvert hopp, og vil hele tiden bruke MAC-adressen til neste enhet.
> 
> Lag 3 adressen endres ikke underveis.

# 2022 Høst
a. Hva er rollen til ”default gateway” (DGW) i et nettverk? Altså, hvordan brukes “default gateway” av enheter i et nettverk?
>Det er en nettverksenhet, for eksempel en ruter eller L3 switch, som kan rute trafikk til andre nettverk. Den trengs for å sende trafikk ut av det lokale nettverket. Hvis denne ikke finnes eller ikke kan nås, så kan man kun kommunisere internt på samme nettverk/subnett.

b. Beskriv fordeler og ulemper med trådløs kommunikasjon.
> Trådløs kommunikasjon gir brukerne økt mobilitet og fleksibilitet i og med at man ikke er låst til en bestemt plassering. Man er dog begrenset av rekkevidden på sender og mottaker, og kan bli påvirket av støy/interferens. I verste fall kan kommunikasjonen da bli upålitelig eller i praksis ubrukelig. Samtidig er trådløs kommunikasjon ofte avhengig av at frekvensen man sender på er ledig, ellers kan det oppstå kollisjoner. Da må man sende på nytt. Man må derfor ta hensyn til omgivelsene når man planlegger bruk av trådløs kommunikasjon, samt antall brukere i samme område. Trådløs kommunikasjon er i mange tilfeller half-duplex, slik at jo flere brukere i området, jo tregere blir systemet.

c. Rams opp noen spesielle krav som stilles til industrielle nettverk.
>Industrielle nettverk krever ofte kabler, plugger og enheter som tåler mer (fukt, støv, osv). I kommersielle nettverk sendes trafikk som standard etter best effort prinsippet, og kommer frem på litt tilfeldige tidspunkter avhengig av hvor mye trafikk som går på nettverket og andre faktorer. I industrielle nettverk er trafikken mer deterministisk, og enhetene vet når de skal sende og motta trafikk. Man er avhengig av at trafikk kommer i tide, og at den er pålitelig/intakt. Hvis ikke, kan det oppstå feil i produksjonsprosessen og medføre store problemer.

d. Hva er forskjellen på Broadcast-kommunikasjon, Unicast kommunikasjon og Multicastkommunikasjon?
>Unicast: informasjon overføres til en spesifikk enhet. Eksempler: filoverføring, nedlasting av webside, sende melding.
  Multicast: informasjon overføres til en eller flere mottakere. Eksempler: diverse rutingprotokoller, IPTV, andre livestreams som radio eller video.
  Broadcast: informasjon overføres til alle enheter på det lokale nettverket. Eksempler: rutingprotokoller, DHCP, ARP

![[eksamen22hnettverksoppgave.png]]

# 2022 Vår
a) (3%) Beskriv fordeler og ulemper med trådløs kommunikasjon.
> Trådløs kommunikasjon gir brukerne økt mobilitet og fleksibilitet i og med at man ikke er låst til en bestemt plassering. I tillegg slipper man å tenke på å ta med seg riktig eller lang nok kabel. Man er dog begrenset av rekkevidden på sender og mottaker, og kan bli påvirket av støy/interferens. I verste fall kan kommunikasjonen da bli upålitelig eller i praksis ubrukelig. Samtidig er trådløs kommunikasjon ofte avhengig av at frekvensen man sender på er ledig, ellers kan det oppstå kollisjoner. Da må man sende på nytt. Man må derfor ta hensyn til omgivelsene når man planlegger bruk av trådløs kommunikasjon, samt antall brukere i samme område. Trådløs kommunikasjon er i mange tilfeller half-duplex, slik at jo flere brukere i området, jo tregere blir systemet.

b) (3%) Hvorfor segmenterer vi data når vi eksempelvis skal sende en stor fil over internett? Hva ville skjedd dersom vi ikke segmenterte filen?
> Det er to fordeler med segmentering: økt hastighet og effektivitet. Dette da man kan sende større mengder data uten å binde opp en hel link (ved hjelp av multipleksing), samtidig som man kan unngå å sende hele filen på nytt hvis et segment skulle mangle. Da sender man bare det spesifikke segmentet om igjen.

c) (3%) Beskriv formålet med lag 2 i OSI-modellen (data link). Forklar hva som foregår på dette nivået når trafikk skal sendes over et medium.
> Formålet med lag 2 er å innkapsle pakken i riktig format for aktuelt media, eksempelvis Ethernet. Dette lar deg sende trafikk fra lagene over uavhengig av media/link type. I tillegg håndterer dette laget kommunikasjon mellom lag 2 hardware og lag 3 software, oppdeling/struktur internt i aktuell frame, adressering på lag 2 og feildeteksjon. På hvert hopp skjer følgende når det gjelder lag 2:
> 1. Enheten mottar en frame fra media
> 2. Fjerner innkapsling fra frame
> 3. Legger til ny innkapsling før eventuell videresending, tilpasset utgående link
> 4. Sender frame ut på aktuell link

d) (4%) Forklar hva en standard er for noe. Hva er fordelene med åpne standarder?
> En standard er et dokument som angir hvordan noe skal lages eller fungere. Dette kan for eksempel beskrive målene på bildekk, inngangsdører eller hva det skal være. Innenfor nettverk brukes dette gjerne til å beskrive protokoller som benyttes for å få tilgang til tjenester, kommunisere osv. Dette lar deg for eksempel koble til WLAN, laste ned en nettside og lese denne uavhengig av hvem som har produsert enheten din eller hvilket operativsystem/nettleser du bruker. Åpne standarder gir en del fordeler når det gjelder interopabilitet, konkurranse og innovasjon. Uten åpne standarder ville vi endt opp med en del monopol og utelåsing av mindre aktører, som ville motvirket innovasjon.

e) (7%) Forklar hva som skjer når PC1 forsøker å laste ned nettsiden «NRK.no» ut ifra figur 4. Få med hvordan den gjør bruk av lokal DNS og default gateway (DGW).
> 1. DNS request til DNS server 192.168.1.254 for NRK.no
> 2. Mottar DNS reply med 10.0.0.2
> 3. Sender ARP request for å få tak i MAC-adressen til DGW 192.168.1.1
> 4. Sender HTTP request til NRK.no på 10.0.0.2, via DGW sin MAC-adresse på L2
> 5. DGW bruker evt NAT og videresender http request til NRK.no via sin 200.0.0.2 adresse
> 6. NRK mottar denne og sender svaret til 200.0.0.2
> 7. «Home» videresender http reply til PC1