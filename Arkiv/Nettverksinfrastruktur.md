# Nettverksenheter - IP-tabell
## Infrastruktur

192.168.100.1 // Telia Ruter/modem default-profil EMG3525-T50B
192.168.101.1 // Telia Ruter bridge-profil EMG3525-T50B

10.10.0.
	.1 // [[LolbraaSense]] på APU2...

192.168.0
	.1 // TP-link ruter Archer C3200
	.100-199 // DHCP-pool
	.254 // Cisco switch [Manual](https://community.cisco.com/kxiwq67737/attachments/kxiwq67737/5976-discussions-small-business--witches/20243/1/Cisco%20SLM2008AG%20Smart%20Switch.pdf)

---
## *Raspberry PIs*

192.168.0
.5 // [[LolbraaRPI]] (Hostname: lolbraarpi)
	- Raspberry PI 1B
	Users:
	- lolandbraa	/	{1PASSWORD}
	Cases:
	- Pi-hole (standard installasjon)
		- DHCP-server
		- DNS over HTTPS med Cloudflared [guide](https://docs.pi-hole.net/guides/dns/cloudflared/)
			- Fjernet støtte for RPI 1B, så måtte oppgradere. 
		- http://192.168.0.5/admin/
	Synkroniseres med https://github.com/mattwebbio/orbital-sync ???
.6 // LolbraaRPI wlan0

.9 // [[Annen hardware#LolbraaKVM|LolbraaKVM]]
- 

---
## *LolbraaNAS med Dockers og VMs*

192.168.0
.10 // [[Hobby/Lolbraa/LolbraaNAS|LolbraaNAS]] [80 WebUi] (Hostname: lolbraanas.local)
	- Tidligere krissgamingpc
	
	Users:
	- root 		/	{1PASSWORD} 	(for SSH, WebUI og lokal)
	- kristoffer 	/ 	{1PASSWORD} 	(share)
	- lolandbraa 	/ 	standard	(share)
	
	Shares:
	- /Lolbraa Backup - Et slags arkiv. Lett tilgjengelig backup av enheter, prosesser, osv.
	- /Lolbraa Bilder - Personlige bilder og videoer.
	- /Lolbraa Media - Alt av media, feks serier.
	- /nextcloud
	- /public - Viktig, lett tilgjengelig informasjon. Enkel destinasjon for opplastning
	
	Dockers:
	- Pi-hole -> .11
	- Nginx Proxy Manager - reverse proxy [180, 81 WebUi, 1443]
		- Port 80 og 443 er forwarded til 180 og 1443
		- Docker måtte være på "Bridge"/.10 for å kunne snakke med andre Dockers
		- Domener: cloud. immich.
	- Dynamic DNS gjennom Cloudflare DNS og domenet: nas.lolandbraa.no.
		- Docker-bilde: "Cloudflare-DDNS-config"
		- --Email: krissernbraa@hotmail.com
		- Token: Gp7m1AoG8DCJWEJ6ZteI1wJfODp7A8_DC-DpBaba
		- Zone: lolandbraa.no
		- Subdomain: *.
	- Jellyfin - Mediaserver [8096 WebUi, 8920 HTTPS WebUi, 7359, 1900 DNLA] (NPM: jellyfin.lolandbraa.no)
	- Immich - Fototjeneste [2283, 8082 Healthcheck] (NPM: immich.lolandbraa.no)
	- NextCloud [8080 admin, 11000 apache/direkte] (NPM: cloud.lolandbraa.no)
		- /mnt/user/NextCloud/data (spesielle permissions)
	- 
	
	
~~.11 // LolbraaNAS Pi-hole [80 WebUi] (Hostname: pihole.local)~~
	~~- Docker-bilde: Pi-Hole DoT DoH~~
	~~- DNS-server med sikret DNS-upstream gjennom Cloudflared og Google-greier~~
	~~- Vurderte Gravity Sync mellom Pihole-installasjonene, men den krever standard Docker.~~
	~~- Orbital sync synkroniserer piholes~~
- Dekommisjonert da LolbraaRPI fungerer som DHCP-server og derfor uansett må være oppe for at nettverket skal fungere.


.12 // vpnvm
- [[VPN#VM-løsningen]]
- 52:54:00:73:7E:B9

.13 // Homeassistant (hostname: homeassistant.local)
- [Home Assistant](http://hass.lolbraa.no)
- 52:54:00:C0:47:7C


---
## *Personlige enheter*

192.168.0
.20 // [[KrisStasjoner]]


.21 // [[KrisStasjoner]]POP
- hostname: krisstasjonerpop
- F0:2F:74:CB:47:93


.22 // [[KrissLaptop]]
- Hostname: KrissLaptop
- C8:34:8E:0B:FE:B2




---
## *LolbraaPVE med VMs og Containers*
[[Annen hardware#Ekstrasystem fra NCG]]
[[Annen hardware#Gammel Kriss Laptop fra VGS]]

192.168.0
.30 // LolbraaPVE
- Hostname: pve.lolbraa


---
## *IoT*

192.168.0
.40 // SW1
- Static DHCP
- Hostname: tasmota-BC4411-1041
- MAC: 4C:EB:D6:BC:44:11
- [Getting Started with our Tasmota Products | LocalBytes Blog](https://blog.mylocalbytes.com/kb/2022-10-01/getting-started-with-tasmota#connecting-the-devices)
- [Commands - Tasmota](https://tasmota.github.io/docs/Commands/#control)

.41 // SW2
- Static DHCP
- Hostname: tasmota-BC471F-1823
- MAC: 4C:EB:D6:BC:47:1F

.42 // PrusaLink WiFi
- satt statisk dhcp i PiHole
- prusalink.lan ???
- BC:FF:4D:2B:B9:0D

.43 // PrusaLink Eth
- 10:9C:70:0E:22:C3
- http://prusamini.lan/
- 

---

# Domener
Har to domener: lolandbraa.no og lolbraa.no.
1. **Lolandbraa.no er for utadvendte tjenester** som mail, nettsider, Immich, Jellyfin, osv.
   - *\*.lolandbraa.no peker til hjemmenettet (se [[#DDNS]]) hvor NPM proxyer domenene.* 
2. **Lolbraa.no er kun for intern bruk.** 
- *\*.lolbraa.no peker til 192.168.0.10 hvor NPM proxyer domenene.* 
 - *Andre domener settes **lokalt** i DNS-serveren (PiHole)*

*Det er flere grunner til at alle mye brukte tjenester går bak et domene:*
1. *Det gjør det mye lettere å huske/skrive inn i addressefeltet. Feks `pihole.lolbraa.no` istedet for `192.168.0.9`.*
2. *Man slipper porter som `glances.lolbraa.no` istedet for `192.168.0.10:61208/`.*
3. *Alt kan være over HTTPS - noe som gjør blant annet klipp og lim kompatibelt.*
4. *Det gjør at man kan velge hvilke 1pass-elementer som skal komme opp, så det faktisk er brukbart (1 mulighet på `unraid.lolbraa.no`, i stedet for 30 på `192.168.0.10`). Man må velge som vist på [[Nettverksinfrastruktur-20240806201452841.jpg|dette bildet]].*

## Cloudflare
Cloudflare brukes for:
1. Upstream DNS-navnetjener
2. [[Nettverkssikkerhet#Proxy|Proxy]]
3. [[Nettverkssikkerhet#WAF / brannmur|WAF / brannmur]]
4. [[Nettverkssikkerhet#Access|Access / login-tjeneste]]
5. 
## DDNS
- Docker: timothyjmiller/cloudflare-ddns:latest
- Oppdaterer hvert 5. minutt.
- Endrer lolandbraa.no (proxied) og nas.lolandbraa.no (ikke proxied).

## Nginx Proxy Manager (NPM)
Ruteren retter all trafikk på port 80 og 443 til LolbraaNAS.
NPM tar over port 80 og 443 på LolbraaNAS for videre proxying. *LolbraaNAS er tilgjengelig på 192.168.0.10:180 og :1443.*

Se [[Nettverkssikkerhet#Nginx Proxy Manager (NPM)]] for sikkerhetstiltak som Access Lists og Crowdsec.

## LOLANDBRAA.no
### Upstream DNS Records på Cloudflare
| Domain                | Destinasjon       | Proxied | Record | [[#DDNS]]  |
| --------------------- | ----------------- | ------- | ------ | ---------- |
| braavpn.lolandbraa.no | Tolsvrød          | Nei     | A      | BraaRPI    |
| lolandbraa.no         | Hjemmenettet      | Ja      | A      | LolbraaNAS |
| nas.lolandbraa.no     | Hjemmenettet      | Nei     | A      | LolbraaNAS |
| cloud.lolandbraa.no   | nas.lolandbraa.no | Nei     | CNAME  |            |
| immich.lolandbraa.no  | nas.lolandbraa.no | Nei     | CNAME  |            |
| \*.lolandbraa.no      | lolandbraa.no     | Ja      | CNAME  |            |
*Cloud og Immich er fordi disse tjenestene krever mulighet for å laste opp filer større enn 100MB. Se [[Nettverkssikkerhet#OBS Limitations ved pakkestørrelse]]. De må også defineres i lokalt DNS-register for NAT-loopback*

### Local DNS Records i Pihole

| Domain               | IP           |     |
| -------------------- | ------------ | --- |
| cloud.lolandbraa.no  | 192.168.0.10 |     |
| immich.lolandbraa.no | 192.168.0.10 |     |

### Proxied domener i NPM

| Domain                        | IP:PORT            | Informasjon |
| ----------------------------- | ------------------ | ----------- |
| https://immich.lolandbraa.no/ | 192.168.0.10:2283  | [[Immich]]  |
| http://status.lolandbraa.no/  |                    |             |
| https://stream.lolandbraa.no/ |                    | [[Media]]   |
| https://cloud.lolandbraa.no/  | 192.168.0.10:11000 |             |
*OBS: **www**.lolandbraa.no leder til en Cloudflare Pages-side med en static landingpage. NPM er satt opp til å redirigere alle subdomener til denne (\*.lolandbraa.no og \*.lolbraa.no).


## LOLBRAA.no
### Upstream DNS Records på Cloudflare
| Domain        | Destinasjon  | Proxied | Record |
| ------------- | ------------ | ------- | ------ |
| \*.lolbraa.no | 192.168.0.10 | Nei     | A      |


### Local DNS Records (A/AAAA) i Pihole

| Domain                          | IP           | Originalt hostname           |
| ------------------------------- | ------------ | ---------------------------- |
| http://pihole.lolbraa.no/admin/ | 192.168.0.5  | http://lolbraarpi.lan/admin/ |
| https://kvm.lolbraa.no/         | 192.168.0.9  | https://lolbraakvm.lan/      |
| http://hass.lolbraa.no          | 192.168.0.13 | http://homeassistant.local/  |

### Proxied domener i NPM

| Domain                         | IP:PORT            | Informasjon                              |               |
| ------------------------------ | ------------------ | ---------------------------------------- | ------------- |
| https://pve.lolbraa.no/        | 192.168.0.30:8006  |                                          |               |
| https://unraid.lolbraa.no/     | 192.168.0.10:1443  | [[Hobby/Lolbraa/LolbraaNAS\|LolbraaNAS]] |               |
| https://npm.lolbraa.no/        | 192.168.0.10:81    |                                          |               |
| https://unbalanced.lolbraa.no/ | 192.168.0.10:7090  |                                          |               |
| http://glances.lolbraa.no/     | 192.168.0.10:61208 |                                          |               |
| https://link.lolbraa.no/       | 192.168.0.10:3456  |                                          |               |
| https://dup.lolbraa.no/        | 192.168.0.10:3875  |                                          |               |
| https://prowlarr.lolbraa.no/   | media:9696         | [[Media]]                                |               |
| https://qbit.lolbraa.no/       | media:6880         | [[Media]]                                | FUNGERER IKKE |
| https://bazarr.lolbraa.no/     | media:6767         | [[Media]]                                |               |
| https://sonarr.lolbraa.no/     | media:8989         | [[Media]]                                |               |
| https://radarr.lolbraa.no/     | media:7878         | [[Media]]                                |               |
| https://manyfold.lolbraa.no    | 192.168.0.10:3214  |                                          |               |
| paperless.lolbraa.no           | 192.168.0.10:8999  |                                          |               |
|                                |                    |                                          |               |
|                                |                    |                                          |               |
|                                |                    |                                          |               |


---
# Tidspunkter
LolbraaRPI
- Cloudflared: ukentlig (/cron.weekly)


LolbraaNAS
- System
	- Mover: daglig 01.00
	- Trim: daglig 10.00
	- Parity check: månedlig 1. dag 00.00 - 07.00, over flere dager
- Backup Appdata og minnepenn
	- Backup: ukentlig torsdag 2230
- Backups hoved Duplicacy + rClone
	- Backup, check og prune: hver dag 23.00 (0 23 * * *)
	- Rclone-sync til TeliaSky hver dag 01.00 (0 1 * * *)
- Immich
	- Backup av database 00.00 (@daily)
- NextCloud
	- Backup 22.00



~~Hovedbackup:~~
- ~~/mnt/disks/Data/borg_backup/~~
- ~~Backup til ekstern hdd med Borgmatic-docker -> overføring til Telia Sky med Rclone~~
- ~~basert på https://forums.unraid.net/topic/99218-support-borgmatic/?do=findComment&comment=915587~~
- ~~Borgmatic: En enklere versjon av Borg Backup.~~
- ~~Rclone: Klarer å jobbe med Jottacloud og sørger for sikker overføring~~
- ~~Healthcheck.io~~
- ~~encryption_passphrase i 1pass~~

~~Hovedbackup Duplicati:~~
- ~~Docker kjører med Linuxserver-bilde.~~
- ~~Eget script (i docker /custom-cont-init.d; på host /appdata) kjøres på start og installerer rclone + kopierer rclone.conf~~
	- ~~Hvis det ødelegges kan man mounte /boot/config/plugins/rclone og spesifisere det i Duplicati~~
- ~~Repo kobles til rclone etter https://duplicati.readthedocs.io/en/latest/05-storage-providers/#rclone~~
- ~~Kommando~~

- ~~Backups Duplicati til Telia Sky~~
	- ~~Lolbraa Bilder: daglig 20.00~~
	- ~~Lolbraa Media: ukentlig tirsdag 10.00~~
	- ~~Lolbraa Backup: hver 3. dag 08.00~~
	- ~~nextcloud:~~ 
- ~~Backups filer Borgmatic + rClone~~
	- ~~Prune, compact og create av rep: hver dag 11.00 og 23.00 (0 13,23 * * *)~~
	- ~~Check av backup: ukentlig onsdag 02.00 (0 2 * * 3)~~
	- ~~Rclone-sync med en gang? Foreløpig hver dag 05.00 (0 5 * * *)~~


~~Spin-down~~
- ~~Ønsker å spinne ned diskene?~~ 
~~Hvis nyopplastede filer forblir i Cache lenge~~ 
~~(feks at mover ikke blir engasjert før den er 50% full),~~ 
~~trenger ikke Array å starte heller.~~
~~Backups blir tatt fra Cache, og den er sikret med Raid.~~
~~Tilgang til filer er stort sett sporadisk, og ikke lenge om gangen.~~
~~Den eneste jevnlige tilgangen er vel bilder/immich? Ha det på cache?~~

