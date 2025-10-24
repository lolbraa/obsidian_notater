# Oversikt
## Brukere
- root 	/	{1PASSWORD} 	(for SSH, WebUI og lokal)
- kristoffer / 	{1PASSWORD} 	(share)
- lolandbraa 	/ 	standard	(share)
## Shares
- /Lolbraa Backup - Et slags arkiv. Lett tilgjengelig backup av enheter, prosesser, osv.
	- /LolbraaNAS - Interne backups
- /Lolbraa Bilder - Personlige bilder og videoer.
- /Lolbraa Media - Alt av media, feks serier.
- /nextcloud
- /public - Viktig, lett tilgjengelig informasjon. Enkel destinasjon for opplastning
- /storj
- /ncgoffsite

# Backuprutiner
## Duplicacy
- Backup til: `/mnt/disks/eksterndisk/duplicacy-backup`
	- Userscript `Backup: Sync LolbraaNAS [Duplicacy/NextCloud-Borg] -> Telia sky & BraaNAS` laster videre opp til Telia Sky med rsync
	- Duplicacy kopierer til BraaNAS offsite gjennom SMB mount (via Unassigned Devices-plugin).
		- BraaNAS kjører egen Duplicacy web edition som utfører check og prune.
- `/mnt/user/appdata/Duplicacy
`
Backup av
* /Lolbraa Backup
* /Lolbraa Bilder
* /public
* /immich

Bilder:
- [[LolbraaNAS-2025.02.10 13.28.04.jpg|DASHBOARD]]
- [[LolbraaNAS-2025.02.10 13.27.38.jpg|STORAGE]]
- [[LolbraaNAS-2025.02.10 13.27.13.jpg|BACKUP]]
- [[LolbraaNAS-2025.02.10 13.26.24.jpg|SCHEDULE]]
### Restore
- For å få tilgang til Telia Sky, sjekk usersript "backup_rclone_serve" for SFTP-tilgang. Denne legges til som storage i Duplicacy med user: lolbraa og pass: Wmds2Foe. Storage-password er i 1pass. Da kan restore under.
- For å restore gå i GUI, velg kilde, revisjon, plassering og i options:
```
-key /config/private.pem -key-passphrase iyfYosfmVsoq2NDAH*DY8uRFTMC-gG
```
- _The storage password is used to encrypt the config file only, not chunks. Chunks are encrypted by a secret key stored in the config file._

### Kommandolinje
[CLI commands with Web Edition - Support - Duplicacy Forum](https://forum.duplicacy.com/t/cli-commands-with-web-edition/4194)
	For the GUI version there are some options, but not the CLI version commands. If you want to use the CLI version with the repositories and storages configured in the GUI version, you must cd to the repository folder you want (C:\Users\<username>\.duplicacy-web\repositories\localhost\xx) and call the CLI version (which is under C:\Users\<username>\.duplicacy-web\bin) from there.
```
docker exec -it Duplicacy sh
duplicacy list --files -r revision | grep "path/to/dir/" > list1

/home/duplicacy/.duplicacy-web/bin/duplicacy_linux_x64_3.2.3 %%%%KOMMANDO%%%%


```

## NextCloud Borg
- Borg-løsningen er innebygd i AIO-løsningen. 
- Lagres til `/mnt/disks/eksterndisk/NC`, og blir videre lastet opp til Telia Sky.
- Passord: 3d4e496b9590bc4d2cef324e7bbd485a9a831ce9ac42b6cb
- https://github.com/nextcloud/all-in-one#pro-tip-backup-archives-access
### Restore
- Følg instruksene her [GitHub - nextcloud/all-in-one: 📦 The official Nextcloud installation method. Provides easy deployment and maintenance with most features included in this one Nextcloud instance.](https://github.com/nextcloud/all-in-one?tab=readme-ov-file#backup-solution)
	- Hvis dockers fortsatt eksisterer/det ikke er en fresh install, følg [how to change backup directory path once submitted? · nextcloud/all-in-one · Discussion #596 · GitHub](https://github.com/nextcloud/all-in-one/discussions/596).
	- [How to properly reset the instance?](https://github.com/nextcloud/all-in-one#how-to-properly-reset-the-instance).

## ImmichDB 
Backup med en docker-container bestemt i Docker Compose.
Før restore, les om instruksene er oppdatert her [Backup and Restore | Immich](https://immich.app/docs/administration/backup-and-restore/)
### Automated Restore
```
cd "/mnt/user/Lolbraa Backup/LolbraaNAS/immichdb"

gunzip < last/immich-latest.sql.gz \
| sed "s/SELECT pg_catalog.set_config('search_path', '', false);/SELECT pg_catalog.set_config('search_path', 'public, pg_catalog', true);/g" \
| docker exec -i immich_postgres psql --username=postgres
```
Sist gjort
```sh
docker compose down -v  # CAUTION! Deletes all Immich data to start from scratch
## Uncomment the next line and replace DB_DATA_LOCATION with your Postgres path to permanently reset the Postgres database
# rm -rf DB_DATA_LOCATION # CAUTION! Deletes all Immich data to start from scratch
docker compose pull             # Update to latest version of Immich (if desired)
docker compose create           # Create Docker containers for Immich apps without running them
docker start immich_postgres    # Start Postgres server
sleep 10                        # Wait for Postgres server to start up
# Check the database user if you deviated from the default
gunzip < "/mnt/user/immich/library/backups/immich-db-backup-1735434000008.sql.gz" \
| sed "s/SELECT pg_catalog.set_config('search_path', '', false);/SELECT pg_catalog.set_config('search_path', 'public, pg_catalog', true);/g" \
| docker exec -i immich_postgres psql --username=postgres  # Restore Backup
docker compose up -d            # Start remainder of Immich apps
```
## ZFS Snapshots

## Appdata og minnepenn backup
- "Backup/restore Appdata"-plugin
- `/mnt/user/Lolbraa Backup/LolbraaNAS/Appdata- og minnepenn-backup/`, og blir backet videre opp av Duplicacy

# Nettverk
## Reverse proxy
Offentlig gjennom Nginx Reverse Proxy
Implementere Tailscale iht. [denne](https://www.reddit.com/r/unRAID/comments/10xdx5g/how_to_share_services_with_a_custom_domain_no/)?
## VPN
### WireGuard
- LolbraaNAS (endpoint: vpn.lolandbraa.no)
	- Tunnel wg0
		- Local tunnel pool: 10.253.132.0/24
	- Tunnel wg1
		- Local tunnel pool: 10.201.132.0/24
- BraaVPN RPI på Tolvsrød (endpoint: braavpn.lolandbraa.no)
	- Tunnel 1: eth0

### Tailscale

## DDNS


---

# Viktig instrukser
## Disk dør:
- Forstå SMART https://docs.unraid.net/legacy/FAQ/understanding-smart-reports/
	- Se også [[SMART-rapporter]]
- https://docs.unraid.net/legacy/FAQ/replacing-a-data-drive/

---

# Pools
## Unraid Parity-Protected Array

## Diverse

## Cache (ZFS)
No compression
~~Compression - default (ref [Unraid | ZFS, Unraid Array, or Hybrid? Choosing the Right Storage Solution for Your Needs](https://unraid.net/blog/zfs-guide))~~

Etter 31.01.2024:
Måtte bytte Kingston 960GB pga. SMART CRC error, se [[Workshop Troubleshooting HDD]]. Kjøpte to 1TB HDD av samme type.
![[LolbraaNAS-2025.01.31 19.38.02.jpg|400]]
![[PXL_20250131_192116719.jpg]]

> [!NOTE]- Frem til 31.01.2024
> Gjrot om til 
> ![[LolbraaNAS-20240521144548502.jpg|400]]

> [!NOTE]- Alternativer til utvidelse
> 3x 1TB til 500kr + 2x 2TB til 750kr
> ![[LolbraaNAS-2.png|400]] og ![[LolbraaNAS-3.png|400]]
> 
> 6x 1TB til 500kr
> ![[LolbraaNAS-4.png|400]]
> 


## Unassigned Devices
### eksterndisk
*Tidligere 12TB-disk "Data" formatert NTFS (brukt til å blant annet frakte data fra Tbg til Bergen)*
Brukes til å lagre backups av data NextCloud og Duplicacy, og lastes herifra opp til skyen. Se [[#Backuprutiner]].
Formatert til ZFS encrypted med pool name "eksterndisk". Passord i 1pass.



---

# Hardware
- Hovedkort: [ASUS P8Z77-V LK, Socket-1155](https://www.komplett.no/product/771425?noredirect=true "‌") ([support](https://www.asus.com/us/supportonly/p8z77-v%20lk/helpdesk_knowledge/), oppdatert BIOS 08.03.2024) ([spec](https://www.techpowerup.com/review/asus-p8z77-v/))
	- [[E8534_P8Z77-V_LK 1.pdf]]
		- Hovedkortet støtter ikke PCIe x8-slot samtidig som x16. Kjører GPU og HBA i x8.
- CPU: [Intel Core i5-3570K Processor](https://www.komplett.no/product/660227?noredirect=true "‌")!
	- [intel.com Intel® Core™ i5-3570K Processor](https://www.intel.com/content/www/us/en/products/sku/65520/intel-core-i53570k-processor-6m-cache-up-to-3-80-ghz/specifications.html)
- GPU: Se [[#GPU]]
- Minne: [HX316C10FBK2/16](https://www.kingston.com/dataSheets/HX316C10FBK2_16.pdf) (2X16GB)
	- Max 32GB
	- Supplert med HyperX FURY Memory Black - 16GB Kit*(2x8GB) - Part Number: HX316C10FBK2/16 Specs: DDR3 1600MT/s Non-ECC Unbuffered DIMM CL10 2RX8 1.5V 240-pin 4Gbit Memory Profile: 1600MT/s 10-10-10 1.5V
- PSU: Corsair CX600M
- [Lite-On DVD±RW Writer, iHAS124](https://www.komplett.no/product/768359?noredirect=true "‌")
- [NZXT Phantom Big Tower Sort](https://www.komplett.no/product/605768?noredirect=true "‌")
    - 2015: [HyperX Cloud II Gaming Headset Rød](https://www.komplett.no/product/835972?noredirect=true "‌")
- HBA: LSI 9207-8i IT Mode med to stk SAS-4SATA
	- [[LSISAS9207-8i_UG_v2-2.pdf]]
	- Se [[#HBA]]
- Raid-kort
    - ~~StarTech: 2x SATA~~
    - ~~Ubrukt: StarTech 4port SATA III 6gbps [PEXSAT34RH](https://www.startech.com/en-us/cards-adapters/pexsat34rh)~~
    - ~~Ubrukt: MicroConnect ASM1061 [2-ports SATA3 (6Gbps)/eSATA PCIe 2.0 x1](https://www.multicom.no/microconnect-diskkontroller-sata-6gb-s-esata/cat-p/c/p8778076)~~
- Backplane: [CMR-2131 SAS](https://www.chieftec.eu/products-detail/336/CMR-2131SAS), 2x 5,25" bays for 3x SATA/SAS HDDs/SSDs (3,5"/2,5") with 80cm Fan,2xMolex-3xSATA

## Hovedkort
BIOS-innstillinger
- Virtualisering
- Fast boot off
	- Sliter med at etter POST så står den i sort skjerm. Dette er forhåpentligvis en fiks
- PCIe 8x mode for PCIe 1 og 2
- ROM Options
	- For å kunne få opp LSI-BIOS
- CSM
	- Skrudd av for skjermkort, men fungerer på enabled?

## Disker
Sjekk garantien og andre ting på [[SSD og HDD Specs]].
#### HDD
- 2stk Seagate Ironwolf Pro 18TB i array til array
    - *ST18000NE000-2YY101_ZR5DB5WM (sdb) Until 6 March 2028
    - *ST18000NE000-2YY101_ZR5EMZM1 (sdc) Until 22 December 2027
    - 7.5W
- 1stk Seagate Ironwolf Pro 12TB utenom array til backup
    - *ST12000VN0008-2YS101_ZV70923Z (sdd) Until 28 June 2026
- 1stk Seagate Barracuda  1TB
	- *ST1000DM003-1ER162_Z4Y1TKG7 - 1 TB (sdj)
- 1stk Seagate Exox X16 14TB
	- *ST14000NM000J-2TX103_ZRS00LZW (sdh)

#### SSD
Se [[SSD og HDD Specs]] for mer generell informasjon.
- 4stk [1000GB PNY CS900](https://www.elkjop.no/product/pc-datautstyr-og-kontor/lagring/intern-ssd/pny-cs900-25-1000-gb-serial-ata-iii-3d-tlc/519630?utm_source=prisjakt&utm_medium=pricecomparison&utm_campaign=prisjakt-listing-5 "‌") SSD til Cache ([SSD-specs](https://www.techpowerup.com/ssd-specs/#PNY%20CS900 "‌"))
	1. *PNY_CS900_1TB_SSD_PNY23402310040101482 (sde)
	2. *PNY_CS900_1TB_SSD_PNY23402310040101485 (sdf)
- 2stk Samsung 850 EVO 250GB
	1. *Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E (sdg)
	2. *Samsung_SSD_850_EVO_250GB_S21PNSAG319056D (sdh)
- ~~1stk Kingston A400 960GB  [SA400S37/960G](https://www.kingston.com/en/ssd/a400-solid-state-drive?partnum=sa400s37%2F960g)~~
	- ~~*KINGSTON_SA400S37960G_50026B7785459723 - 960 GB (sdl)~~
Ikke i bruk:
- 2stk 2TB [PM863a Series Enterprise SSD MZ-7LM1T9N](https://www.samsung.com/us/business/support/owners/product/pm863a-series-1-92tb/) 
	- Power Consumption (W): Read: 3W, Write: 4W
	- TBW: 3 Years/2,773TBW

### DIsk-oversikt

| Plassering      | Koblet til          | Disk                                                                                  | SN                                                       |                                                     |
| --------------- | ------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------- | --------------------------------------------------- |
| Backplane 2 - 3 | Hovedkort - SATA3G1 | 12TB ARRAYDISK 4 (tidligere Data)                                                     | ST12000VN0008-2YS101_ZV70923Z (sdf)                      |                                                     |
| Backplane 2 - 2 | Hovedkort - SATA3G2 | 1TB ARRAYDISK 3                                                                       | ST1000DM003-1ER162_Z4Y1TKG7 - 1 TB (sdj)                 |                                                     |
| Backplane 2 - 1 | HBA - 2 - P4        | 14TB eksterndisk (tatt over for Data)                                                 | ST14000NM000J-2TX103_ZRS00LZW (sdh)                      |                                                     |
| Backplane 1 - 3 | HBA - 2 - P3        | 18TB ARRAYDISK 2 - NCGOFFSITE                                                         | ST18000NM000J-2TV103_WR50A85F - 18 TB (sdi)              |                                                     |
| Backplane 1 - 2 | HBA - 2 - P2        | 18TB ARRAYDISK 1                                                                      | ST18000NE000-2YY101_ZR5EMZM1 - 18 TB (sdg)               |                                                     |
| Backplane 1 - 1 | HBA - 2 - P1        | 18TB PARITY 1                                                                         | ST18000NE000-2YY101_ZR5DB5WM - 18 TB (sde)               |                                                     |
| Løst            | HBA - 1 - P1        | 1TB Cache SSD 1                   PNY_CS900_1TB_SSD_PNY23402310040101482 - 1 TB (sdm) |                                                          |                                                     |
| Løst            | HBA - 1 - P2        | 1TB Cache SSD 2                                                                       | PNY_CS900_1TB_SSD_PNY23402310040101485 - 1 TB (sdl)      | PNY_CS900_1TB_SSD_PNY23402310040101482 - 1 TB (sdm) |
| Løst            | HBA - 1 - P2        | 1TB Cache SSD 2                                                                       | PNY_CS900_1TB_SSD_PNY23402310040101485 - 1 TB (sdl)      |                                                     |
| Løst            | HBA - 1 - P3        | 1TB Cache SSD 3                                                                       | PNY_1TB_SATA_SSD_PNA3924102934AT07516 (sdk)              |                                                     |
| Løst            | HBA - 1 - P4        | 1TB Cache SSD 4                                                                       | PNY_1TB_SATA_SSD_PNA3924102934AT06325 (sdn)              |                                                     |
| På PSU          | Hovedkort - SATA6G1 | 250GB Diverse SSD 1                                                                   | Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E - 250 GB (sdd) |                                                     |
| På PSU          | Hovedkort - SATA6G2 | 250GB Diverse SSD 2                                                                   | Samsung_SSD_850_EVO_250GB_S21PNSAG319056D - 250 GB (sdc) |                                                     |
|                 |                     |                                                                                       |                                                          |                                                     |
|                 |                     |                                                                                       |                                                          |                                                     |


### HBA
En SATA-port fungerer ikke. P1 fra SAS-konnektor nærmest PCIe-konnektoren. To kondensatorer er borte. Fikk en ny en, som nå er i NASen.
> [!NOTE]- Melding til selger
> Nå testet jeg å bytte plass på break-out kablene. Problemet fulgte ikke kabel, men SAS-kontaktene. Det er første SATA-port, P1, som ikke fungerer når de er tilkoblet SAS-kontakten nærmest PCIe-kontakten, altså J6. Jeg tok en visuell inspeksjon rundt kontakten, og kontakten i seg selv så bra ut. Men når jeg snudde den rundt og lokaliserte undersiden, er det klart at et par komponenter er revet av. Etter hva jeg klarer å tyde så er det to kondensatorer, av en rekke hvor hver SATA-port har to kondensatorer hver. Altså er begge kondensatorene for P1-lanen revet av. Det var vel flaks i uflaksen at det ikke berørte to ulike lanes, hehe. Jeg vet ikke helt hva vi skal gjøre med dette. Helt ærlig er det ingen deal breaker for meg, og jeg forstår jo at hvis du gjør dette i stor skala, at du ikke har kontroll på alle komponentene dine. Men igjen så er det litt surt. Hva tenker du?
> ![[LolbraaNAS-20240914201840140.jpg|500]]
```SH
root@LolbraaNAS:~# lspci | grep LSI
02:00.0 Serial Attached SCSI controller: Broadcom / LSI SAS2308 PCI-Express Fusion-MPT SAS-2 (rev 05)
```


## GPU
Se [[Hardwaretranscoding]].
Se [[Annen hardware#LolbraaKVM]].
- [NVIDIA Quadro P400 Specs | TechPowerUp GPU Database](https://www.techpowerup.com/gpu-specs/quadro-p400.c2934)
- [\[Plugin\] Nvidia-Driver - Plugin Support - Unraid](https://forums.unraid.net/topic/98978-plugin-nvidia-driver/)
Bilde av driver: [[LolbraaNAS-1.png]]


---

# Changelog

| Dato          | Pris                                                                                         | Endring                                                                                                                                                                                                                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Oktober? 2023 |                                                                                              | Endret formål på Gaming PC til NAS. Installert Unraid. Kjøpte 2x 18tb + 1x 12tb disker.                                                                                                                                                                                                                          |
| 9.10.2023     | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=306350124) 150kr               | [2-ports SATA3 (6Gbps)/eSATA PCIe 2.0 x1-kort fra MicroConnect ASM1061](https://www.multicom.no/microconnect-diskkontroller-sata-6gb-s-esata/cat-p/c/p8778076)                                                                                                                                                   |
| 17.11.2023    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=328972104) 150kr               | StarTech 4port SATA III 6gbps [PEXSAT34RH](https://www.startech.com/en-us/cards-adapters/pexsat34rh)                                                                                                                                                                                                             |
| Desember 2023 |                                                                                              | Kjøpte 2x PNY 1tb SSDer for cache. Har også kjøpt nye raid-kort.                                                                                                                                                                                                                                                 |
| 13.03.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=283936213) 90kr (ink frakt)    | 3stk Molex til 2stk Sata Splitter                                                                                                                                                                                                                                                                                |
| 13.03.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=343165026) 234kr (ink. frakt)  | HyperX FURY Memory Black - 16GB Kit*(2x8GB) - DDR3 1600MT/s CL10 DIMM for å supplere eksisterende                                                                                                                                                                                                                |
| 15.03.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=343611823) 835kr (ink. frakt)  | [Chieftec Backplane CMR-2131](https://www.chieftec.eu/products-detail/336/CMR-2131SAS)<br>                                                                                                                                                                                                                       |
| 27.03.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=345816444) 596kr (ink. frakt)  | Kingston a400 960gb 2,5" SSD SATA 3.0, 2.5", TLC, up to 500/450/s read/write, 7mm [SA400S37/960G](https://www.kingston.com/en/ssd/a400-solid-state-drive?partnum=sa400s37%2F960g)                                                                                                                                |
| 31.03.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=346259825) 1651kr (ink. frakt) | ~~2stk 1TB Intel®SSD 540s Series (SSDSC2KW010X8)~~ + 2stk 2TB [PM863a Series Enterprise SSD MZ-7LM1T9N](https://www.samsung.com/us/business/support/owners/product/pm863a-series-1-92tb/) + ~~1stk 1TB Kingston [KC400 (SKC400S37)]()~~. <br>Solgt igjen.                                                        |
| 02.04.2024    | Kjøpt [Finn]() 1500                                                                          |                                                                                                                                                                                                                                                                                                                  |
| 26.04.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=349175090) 590 kr              | # Nvidia Quadro P400 2GB GDDR5 grafikkort, CUDA Cores 256 GPU Memory 2 GB GDDR5 Memory Bandwidth 32 GB/Sec Memory Interface 64-Bit PCI Express 3.0 x16                                                                                                                                                           |
| 08.09.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=369531826) 438 kr              | LSI 9207-8i IT Mode med to stk SAS-4SATA                                                                                                                                                                                                                                                                         |
| 08.09.2024    | Kjøpt [Finn](https://www.finn.no/bap/forsale/ad.html?finnkode=369321206) 1400 kr             | Seagate Exos X16 - 14TB - Harddisk - ST14000NM001G                                                                                                                                                                                                                                                               |
| 13.09.2024    | Montert HBA og ny disk                                                                       | Hovedkortet støtter ikke PCIe x8-slot samtidig som x16. Kjører GPU og HBA i x8.<br>Gjort om kabling; se [[#DIsk-oversikt]].<br>Startet pre-clear på disk. Tok 54 timer.                                                                                                                                          |
| 17.09.2024    | Implementert ny disk                                                                         | Formatert til ZFS encrypted med pool name "eksterndisk", Data. Passord i 1pass.<br>Flyttet ekstern-backup-endepunkt fra Data til eksterndisk med kommando [[Workshop kommandoer#Migrere eksterndisk]]                                                                                                            |
| 23.11.2024    | Lagt gammel eksterndisk (Data) til array                                                     | Flyttet korrupte bilder/videoer fra Data-disken (original backup tatt i tønsberg) til en egen mappe i Roars nextcloud.<br>Formatert og lagt til i array. Formatert som ZFS Encrypted                                                                                                                             |
| 24.01.2025    | Kjøpt 2 stk 1TB SSD                                                                          | For å bytte ut Kingston som gir masse CRC-errors.                                                                                                                                                                                                                                                                |
| 31.01.2025    | Byttet inn 1TB diskene                                                                       | Formatert til ZFS RAID Z1. Se [[#Cache (ZFS)]]. Flyttet alle filer med Unbalanced til array, foruten Immich sin encoded-video. Tror det er mange unødvendig filer der, så ønsker å generere alt på nytt. Per 31.01.2024 talte 21389 filer med `find . -type f -path "./immich/library/encoded-video/*" \| wc -l` |

## Upgrade path
- Nye disker
	- Array
		1. Trenger en cold spare.
		- Fortsette med 18TB disker. Kan ha en spinnende konstant, og når den er full, putte inn en ny.
		- [Prisjakt HDDs](https://www.prisjakt.no/c/interne-harddisker?direction=asc&sort=property.64014)
		- [What Hard Drive should I buy for my DIY NAS? - YouTube](https://www.youtube.com/watch?v=09PTfJWF7T8)
	- Cache
		1. Flere SSDer for rask tilgang til Immich og NextCloud.
		- [x] ZFS-cache-pool 
			- formatert btrfs raid 1. IKKE stabilt med raid5, så hvordan gjøre ekspansjon? Omformatere til ZFS?
			- Kan da ha en ZFS-disk i array for snapshot-backups.
			- [btrfs-kalkulator](https://carfax.org.uk/btrfs-usage/?c=1&slo=1&shi=100&p=1&dg=1&d=1000&d=1000&d=1000)
			- [Unraid RAID-management-docs](https://docs.unraid.net/unraid-os/manual/storage-management/#change-pool-raid-levels)
- [x] Flere SATA-porter
	- [Recommended controllers for Unraid - Storage Devices and Controllers - Unraid](https://forums.unraid.net/topic/102010-recommended-controllers-for-unraid/)
	- HDD trenger ikke SATA3 (6GB/s)
	- Ikke anbefalt med RAID/HBA-kort generelt, helst rett til hovedkort.
		- Men HBA-kort er mer stabile enn RAID-kort (dårlig drivere og annet)  Sjekk ut linken for mye nyttig info: [Don't use PCIe SATA cards with Unraid, use a cheap HBA](https://unraid-guides.com/2020/12/07/dont-ever-use-cheap-pci-e-sata-expansion-cards-with-unraid/)
		- LSI SAS 9300-8i HBA (SAS3008) and LSI SAS 9201-8i HBA (SAS2008).
			- Trenger aktiv kjøling rett på kontrolleren! 
				- [Installation of LSI SAS 9207-8i - General Support - Unraid](https://forums.unraid.net/topic/81530-installation-of-lsi-sas-9207-8i/)
				- [Reddit - kommentarer](https://www.reddit.com/r/unRAID/comments/p6fmed/just_moved_to_a_lsi_92078i_controller_why_did_i/)
			- [Tips til boot, sjekk av IT-mode, osv. - Reddit](https://www.reddit.com/r/unRAID/comments/le6o4c/how_to_check_if_my_lsi_92078i_is_flashed_to_it/)
		- ServeRAID-kort er anbefalt (må være flashet)
			- [ServeRAID M1015 -key for sale | eBay](https://www.ebay.com/sch/i.html?_nkw=ServeRAID+M1015+-key)
		- Hovedkortet støtter ikke PCIe x8-slot samtidig som x16 
- [ ] Bedre PSU
	- Ligger på 60-90W, så helst ikke for stor effekt.
	- Viktigere med bedre kvalitet enn mer kapasitet. Ofte er best utnyttelse ved 50-80% (?). Sjekk datablad.
	- Sjekk hva LTT Labs anbefaler når det kommer på banen?
	- [Reduce power consumption with powertop - User Customizations - Unraid](https://forums.unraid.net/topic/98070-reduce-power-consumption-with-powertop/)
	- [Proper Power Supply Sizing Guidance | TrueNAS Community](https://www.truenas.com/community/threads/proper-power-supply-sizing-guidance.38811/)
	- [PSU Tier List rev. 17.0g - Cultists Network](https://cultists.network/140/psu-tier-list/)
		- [Seasonic Prime Fanless PX](https://seasonic.com/prime-fanless-px#specification)
- [x] GPU for transcoding
	- Evt ny prosessor med Intel QuickSync. 7. generasjon?
		- [# latest recommendations for GPU for transcoding?](https://www.reddit.com/r/unRAID/comments/pyr9vi/latest_recommendations_for_gpu_for_transcoding/)
	- [Nvidia NVENC generasjoner](https://en.wikipedia.org/wiki/Nvidia_NVENC)
	- [Nvidia GPU generasjoner](https://en.wikipedia.org/wiki/List_of_Nvidia_graphics_processing_units)
	- Intel Arc 310 er bra bang for buck virker det som, men den tar PCIe 4x, noe hovedkortet ikke har
		- [Best pris på ASRock Intel Arc A310 Low Profile HDMI DP 4GB Skjermkort - Sammenlign priser hos Prisjakt](https://www.prisjakt.no/product.php?p=12819104)
		- [ASUS P8Z77-V Intel Z77 Express LGA 1155 Review | TechPowerUp](https://www.techpowerup.com/review/asus-p8z77-v/)
	- [x] Nvidia Quadro P400 (GP107)
		- [NVIDIA Quadro P400 Specs | TechPowerUp GPU Database](https://www.techpowerup.com/gpu-specs/quadro-p400.c2934)
		- [Nvidia Quadro P400 2GB GDDR5 grafikkort | FINN torget](https://www.finn.no/bap/forsale/ad.html?finnkode=349175090)
		- [nVidia Hardware Transcoding Calculator for Plex Estimates](https://www.elpamsoft.com/?p=Plex-Hardware-Transcoding)
		- [Reddit - Dive into anything](https://www.reddit.com/r/jellyfin/comments/109edwj/expected_transcoding_performance_quadro_p400/)
		- [NVIDIA GPU | Jellyfin](https://jellyfin.org/docs/general/administration/hardware-acceleration/nvidia/)
		- kun 30w TDP, men støtter ikke nyeste formater (AV1, mest spenstige HEVC osv)
- [x] HDD Backplane
	- [Finn-søk](https://www.finn.no/bap/forsale/search.html?price_to=1500&q=backplane+or+hotswap&stored-id=69969077&sub_category=1.93.3215)
	- [CHIEFTEC Backplane CMR-2131 SAS 2x 5,25" bays for 3x SATA/SAS HDDs](https://store.euro-tec.no/chieftec-backplane-cmr-2131-sas-2x/cat-p/c/p9652920)
	- [CMR-2131SAS-Chieftec](https://www.chieftec.eu/products-detail/336/CMR-2131SAS)


---

# Benchmarks
## HDD Preclear
HDD 18TB ST18000NM000J-2TV103_WR50A85F (sdg) Feb 18 15:33:26 preclear_disk_WR50A85F_32354: Preclear: total elapsed time: 71:49:27
HDD 14TB ST14000NM000J-2TX103_ZRS00LZW (sdh) Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: Cycle: elapsed time: 54:27:59 
> [!NOTE]- Preclear-logg 14.09.2024
> ```logg
> Sep 14 20:21:46 preclear_disk_ZRS00LZW_18186: Pause (sync command issued) Sep 14 20:21:46 preclear_disk_ZRS00LZW_18186: Paused Sep 14 20:22:21 preclear_disk_ZRS00LZW_18186: Resumed Sep 15 00:41:13 preclear_disk_ZRS00LZW_18186: Zeroing: progress - 75% zeroed @ 193 MB/s Sep 15 06:43:20 preclear_disk_ZRS00LZW_18186: Zeroing: progress - 100% zeroed @ 39 MB/s Sep 15 06:43:22 preclear_disk_ZRS00LZW_18186: Zeroing: zeroing the disk completed! Sep 15 06:43:22 preclear_disk_ZRS00LZW_18186: Signature: writing signature... Sep 15 06:43:23 preclear_disk_ZRS00LZW_18186: Signature: verifying Unraid's signature on the MBR ... Sep 15 06:43:24 preclear_disk_ZRS00LZW_18186: Signature: Unraid preclear signature is valid! Sep 15 06:43:24 preclear_disk_ZRS00LZW_18186: Post-Read: post-read verification started 1 of 5 retries... Sep 15 06:43:24 preclear_disk_ZRS00LZW_18186: Post-Read: verifying the beginning of the disk. Sep 15 06:43:24 preclear_disk_ZRS00LZW_18186: Post-Read: verifying the rest of the disk. Sep 15 10:22:16 preclear_disk_ZRS00LZW_18186: Post-Read: progress - 25% verified @ 260 MB/s Sep 15 14:18:23 preclear_disk_ZRS00LZW_18186: Post-Read: progress - 50% verified @ 233 MB/s Sep 15 18:48:32 preclear_disk_ZRS00LZW_18186: Post-Read: progress - 75% verified @ 196 MB/s Sep 16 00:50:07 preclear_disk_ZRS00LZW_18186: Post-Read: elapsed time - 18:06:40 Sep 16 00:50:07 preclear_disk_ZRS00LZW_18186: Post-Read: post-read verification completed! Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Cycle 1 Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: ATTRIBUTE               INITIAL NOW   STATUS Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Reallocated_Sector_Ct   0       0     - Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Power_On_Hours          11831   11859 Up 28 Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Reported_Uncorrect      0       0     - Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Airflow_Temperature_Cel 33      42    Up 9 Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Current_Pending_Sector  0       0     - Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: Offline_Uncorrectable   0       0     - Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.: UDMA_CRC_Error_Count    0       0     - Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: S.M.A.R.T.:  Sep 16 00:50:09 preclear_disk_ZRS00LZW_18186: Cycle: elapsed time: 54:27:59 Sep 16 00:50:10 preclear_disk_ZRS00LZW_18186: Preclear: total elapsed time: 54:28:02
> ```

## HDD [DiskSpeed](http://192.168.0.10:18888)
egen mappe i obsidian

## Effektforbruk

|            | av [W]    | tomgang [W] | full last [W] | GPU    | HDDs | SSDs | notater                                                                       |
| ---------- | --------- | ----------- | ------------- | ------ | ---- | ---- | ----------------------------------------------------------------------------- |
| høst 2023  | 0.75-0.81 | 61.8        | -             | GTX760 | 3    | 4    |                                                                               |
| høst 2023  | -         | 61.8        | 110           | iGPU   | 3    | 4    | full last med 100% CPU transcoding                                            |
| 01.03.2024 | -         | ~110        | ~135          | GTX760 | 4    | 4    |                                                                               |
| 08.03.2024 | -         | 78-80       | 126           | iGPU   | 4    | 4    | Etter auto powertop-optimalisering.                                           |
| 01.05.2024 | -         | 110-120     | 150-60        | P400   | 5    | 5    | Ny Standard: Powertop-optimaliseringer ved boot og endret BIOS-innstillinger. |
| 04.06.2024 | -         | 90-110      | 135           | iGPU   | 5    | 5    | Fjernet GPU og byttet fra 4xSATA til 2stk 2xSATA-kort                         |
[# Running an Energy Efficient Unraid Server](https://unraid.net/blog/energy-efficient-server)
[# Reduce power consumption with powertop](https://forums.unraid.net/topic/98070-reduce-power-consumption-with-powertop/)

## Parity Operation History

| Action       | Date                             | Size  | Duration                     | Speed       | Status   | Errors |
| ------------ | -------------------------------- | ----- | ---------------------------- | ----------- | -------- | ------ |
|              |                                  |       |                              |             |          |        |
| Parity-Check | 2024-09-03, 01:23:18 (Tuesday)   | 18 TB | 1 day, 1 hr, 23 min, 17 sec  | 196.9 MB/s  | OK       | 0      |
| Parity-Check | 2024-08-02, 04:38:15 (Friday)    | 18 TB | 1 day, 13 hr, 44 min, 3 sec  | 132.5 MB/s  | OK       | 5      |
| Parity-Check | 2024-07-02, 01:20:19 (Tuesday)   | 18 TB | 1 day, 1 hr, 32 min, 10 sec  | 195.8 MB/s  | OK       | 5      |
| Parity-Check | 2024-06-03, 13:34:42 (Monday)    | 18 TB | 1 day, 13 hr, 34 min, 41 sec | 133.1 MB/s  | OK       | 0      |
| Disk-Clear   | 2024-05-25, 23:21:44 (Saturday)  | 1 TB  | 1 hr, 37 min, 15 sec         | 171.4 MB/s  | OK       | 0      |
| Parity-Check | 2024-05-04, 06:04:27 (Saturday)  | 18 TB | 1 day, 7 hr, 48 min, 9 sec   | 157.2 MB/s  | OK       | 0      |
| Parity-Check | 2024-05-02, 20:28:12 (Thursday)  | 18 TB | 20 hr, 28 min, 11 sec        | Unavailable | Canceled | 0      |
| Parity-Check | 2024-04-03, 03:49:52 (Wednesday) | 18 TB | 1 day, 3 hr, 49 min, 50 sec  | 179.7 MB/s  | OK       | 0      |
| Parity-Check | 2024-03-08, 17:21:00 (Friday)    | 18 TB | 27 sec                       | Unavailable | Canceled | 0      |
| Parity-Check | 2024-03-05, 22:13:40 (Tuesday)   | 18 TB | 1 day, 6 hr, 38 min, 43 sec  | 163.2 MB/s  | OK       | 0      |
| Parity-Check | 2024-03-03, 19:00:54 (Sunday)    | 18 TB | 15 hr, 43 min, 8 sec         | Unavailable | Canceled | 0      |
| Parity-Check | 2024-03-02, 15:28:05 (Saturday)  | 18 TB | 15 hr, 28 min, 3 sec         | Unavailable | Canceled | 0      |
| Parity-Check | 2024-02-23, 07:16:53 (Friday)    | 18 TB | 2 day, 13 hr, 2 min, 18 sec  | 81.9 MB/s   | OK       | 0      |
| Parity-Check | 2024-02-17, 01:47:56 (Saturday)  | 18 TB | 1 day, 10 hr, 5 min, 24 sec  | 146.7 MB/s  | OK       | 0      |
| Parity-Check | 2024-02-03, 00:15:02 (Saturday)  | 18 TB | 1 day, 15 min, 1 sec         | 206.2 MB/s  | OK       | 0      |
| Parity-Check | 2024-01-23, 16:39:01 (Tuesday)   | 18 TB | 23 hr, 23 min, 37 sec        | 213.7 MB/s  | OK       | 0      |
| Parity-Check | 2024-01-14, 16:11:18 (Sunday)    | 18 TB | 23 hr, 37 min, 23 sec        | 211.7 MB/s  | OK       | 0      |
| Parity-Check | 2024-01-13, 16:48:58 (Saturday)  | 18 TB | 9 min, 57 sec                | Unavailable | Canceled | 0      |
| Parity-Check | 2024-01-02, 23:20:48 (Tuesday)   | 18 TB | 23 hr, 20 min, 41 sec        | 214.2 MB/s  | OK       | 0      |
| Parity-Check | 2023-12-03, 13:30:43 (Sunday)    | 18 TB | 1 day, 18 min, 48 sec        | 205.7 MB/s  | OK       | 0      |
| Parity-Check | 2023-11-24, 17:48:47 (Friday)    | 18 TB | 23 hr, 58 min, 28 sec        | 208.6 MB/s  | OK       | 0      |
| Parity-Check | 2023-11-07, 19:43:16 (Tuesday)   | 18 TB | 40 sec                       | Unavailable | Canceled | 0      |
| Parity-Check | 2023-11-02, 14:40:39 (Thursday)  | 18 TB | 14 hr, 49 min, 59 sec        | 337.1 MB/s  | OK       | 0      |
| Parity-Check | 2023-10-16, 21:29:24 (Monday)    | 18 TB | 1 day, 7 min, 38 sec         | 207.2 MB/s  | OK       | 1      |
| Parity-Check | 2023-10-02, 22:08:49 (Monday)    | 18 TB | 22 hr, 53 min, 45 sec        | 218.4 MB/s  | OK       | 0      |
| Parity-Sync  | 2023-09-25, 03:51:43 (Monday)    | 18 TB | 1 day, 21 min, 42 sec        | 205.2 MB/s  | OK       | 0      |
| Parity-Sync  | 2023-09-24, 00:41:11 (Sunday)    | 18 TB | 5 min, 13 sec                | Unavailable | Canceled | 0      |
| Parity-Sync  | 2023-09-23, 20:46:46 (Saturday)  | 18 TB | 1 hr, 21 min, 11 sec         | Unavailable | Canceled | 0      |
| Parity-Sync  | 2023-09-23, 08:50:57 (Saturday)  | 18 TB | 1 min, 45 sec                | Unavailable | Canceled | 0      |



