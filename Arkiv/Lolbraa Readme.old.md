Nettverksinfrastruktur
-----------------
192.168
.100.1 // Telia Ruter/modem default-profil EMG3525-T50B
.101.1 // Telia Ruter bridge-profil EMG3525-T50B
.0.1 // TP-link ruter
	- Archer C3200
.0.100-199 // DHCP-pool
.0.254 // Cisco switch 1
	- https://community.cisco.com/kxiwq67737/attachments/kxiwq67737/5976-discussions-small-business--witches/20243/1/Cisco%20SLM2008AG%20Smart%20Switch.pdf




Nettverksenheter - Statisk IP-tabell
-----------------
192.168.0
.5 // LolbraaRPI (Hostname: lolbraarpi)
	- Raspberry PI 1B
	Users:
	- lolandbraa	/	{1PASSWORD}
	Cases:
	- Pi-hole (standard installasjon)
		- DNS over HTTPS med Cloudflared (https://docs.pi-hole.net/guides/dns/cloudflared/)
			- Fjernet støtte for RPI 1B, så måtte oppgradere. 
		- http://192.168.0.5/admin/
	Synkroniseres med https://github.com/mattwebbio/orbital-sync ???


.10 // LolbraaNAS [80 WebUi] (Hostname: lolbraanas.local)
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
	
	

.11 //LolbraaNAS Pi-hole [80 WebUi] (Hostname: pihole.local)
	- Docker-bilde: Pi-Hole DoT DoH
	- DNS-server med sikret DNS-upstream gjennom Cloudflared og Google-greier
	- Vurderte Gravity Sync mellom Pihole-installasjonene, men den krever standard Docker.
	- Orbital sync synkroniserer piholes


		
	



Ekstern IP, DNS, osv.
---------------------
Nginx Proxy Manager (NPM)
- Port 80 og 443 er forwarded til 180 og 1443 på 192.168.0.10

WireGuard
- LolbraaNAS (endpoint: vpn.lolandbraa.no)
	- Tunnel wg0
		- Local tunnel pool: 10.253.132.0/24
	- Tunnel wg1
		- Local tunnel pool: 10.201.132.0/24
- BraaVPN RPI på Tolvsrød (endpoint: braavpn.lolandbraa.no)
	- Tunnel 1: eth0
		

DDNS
- Docker



	- -----Dynamic DNS gjennom duckdns.org.
		- Token: 0bf938cd-cb85-4f52-903d-1db171e9f46c
		- Domain: lolandbraa.duckdns.org
		- https://www.duckdns.org/update?domains={lolandbraa}&token={0bf938cd-cb85-4f52-903d-1db171e9f46c}

Nginx Proxy Manager
- cloud.lolandbraa.no
- immich.lolandbraa.no
- jellyfin.lolandbraa.no
	- https://www.reddit.com/r/jellyfin/comments/d7a16g/jellyfin_behind_nginx_proxy_manager/



Viktig instrukser
-----------------
Unraid USB ID:

Disk dør:
- Forstå SMART https://docs.unraid.net/legacy/FAQ/understanding-smart-reports/
- https://docs.unraid.net/legacy/FAQ/replacing-a-data-drive/

Hovedbackup

-keep 0:1800 -keep 180:360 -keep 30:180 -keep 7:30 -keep 1:3 -a
Completed


Nextcloud backup
- /mnt/disks/Data/NC
- https://github.com/nextcloud/all-in-one#pro-tip-backup-archives-access
- Passord: 3d4e496b9590bc4d2cef324e7bbd485a9a831ce9ac42b6cb

Appdata og minnepenn backup
- "Backup/restore Appdata"-plugin

Immich - laget med Docker-Compose
- Oppdatering etter instrukser nederst https://immich.app/docs/install/unraid
- Backup etter instrukser https://immich.app/docs/administration/backup-and-restore
	- Automatisert med instruksene som står der med bildet https://github.com/prodrigestivill/docker-postgres-backup-local
	- Backup-dir: /mnt/user/Lolbraa Backup/Homelab Backups/Immich_Backup/
	- FORELØPIG KUN DATABASE, IKKE ORIGINAL-filer
		- Restore: gunzip < db_dumps/last/immich-latest.sql.gz | docker exec -i immich_postgres psql -U postgres -d immich
- Import av Google Takeout
	- Betalt løsning https://metadatafixer.com/pricing
	- Immich-go (brukt 10.2023 for hele katalogen. Gikk for det meste bra)
	- For å bytte ut Google Photos:
		- Immich (evt Google Memories) må være mer stabilt (alle alternativene er ganske ferske)
		- Bedre og lettere hardware acceleration
		- Bedre instrukser for hvilke transcoding-innstillinger
		- Bedre import-verktøy fra Google-Photos 
			- Immich-go ga noen rar datoer og la ikke automatisk filer i arkivet
			
			
			


Tidspunkter
-----------
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
-
- Immich
	- Backup av database 00.00 (@daily)
	
- NextCloud
	- Backup 22.00



Hovedbackup:
- /mnt/disks/Data/borg_backup/
- Backup til ekstern hdd med Borgmatic-docker -> overføring til Telia Sky med Rclone
- basert på https://forums.unraid.net/topic/99218-support-borgmatic/?do=findComment&comment=915587
- Borgmatic: En enklere versjon av Borg Backup.
- Rclone: Klarer å jobbe med Jottacloud og sørger for sikker overføring
- Healthcheck.io
- encryption_passphrase i 1pass

Hovedbackup Duplicati:
- Docker kjører med Linuxserver-bilde.
- Eget script (i docker /custom-cont-init.d; på host /appdata) kjøres på start og installerer rclone + kopierer rclone.conf
	- Hvis det ødelegges kan man mounte /boot/config/plugins/rclone og spesifisere det i Duplicati
- Repo kobles til rclone etter https://duplicati.readthedocs.io/en/latest/05-storage-providers/#rclone
- Kommando

- Backups Duplicati til Telia Sky
	- Lolbraa Bilder: daglig 20.00
	- Lolbraa Media: ukentlig tirsdag 10.00
	- Lolbraa Backup: hver 3. dag 08.00
	- nextcloud: 
- Backups filer Borgmatic + rClone
	- Prune, compact og create av rep: hver dag 11.00 og 23.00 (0 13,23 * * *)
	- Check av backup: ukentlig onsdag 02.00 (0 2 * * 3)
	- Rclone-sync med en gang? Foreløpig hver dag 05.00 (0 5 * * *)
	
	
Spin-down
- Ønsker å spinne ned diskene? 
Hvis nyopplastede filer forblir i Cache lenge 
(feks at mover ikke blir engasjert før den er 50% full), 
trenger ikke Array å starte heller.
Backups blir tatt fra Cache, og den er sikret med Raid.
Tilgang til filer er stort sett sporadisk, og ikke lenge om gangen.
Den eneste jevnlige tilgangen er vel bilder/immich? Ha det på cache?

