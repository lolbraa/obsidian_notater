 Oversikt
---
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
---
Duplicacy
Backup av
* /Lolbraa Backup
* /Lolbraa Bilder
* /public
# Nettverk
---
# Reverse proxy
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



# Hardware
---
 [ASUS P8Z77-V LK, Socket-1155](https://www.komplett.no/product/771425?noredirect=true "‌")
- [Intel Core i5-3570K Processor](https://www.komplett.no/product/660227?noredirect=true "‌")
- Minne: HX316C10FBK2/16 (2X16GB)
- PSU: Corsair CX600M
- [Lite-On DVD±RW Writer, iHAS124](https://www.komplett.no/product/768359?noredirect=true "‌")
- [NZXT Phantom Big Tower Sort](https://www.komplett.no/product/605768?noredirect=true "‌")
    - 2015: [HyperX Cloud II Gaming Headset Rød](https://www.komplett.no/product/835972?noredirect=true "‌")
- Raid-kort
    - StarTech: 2x SATA
    - StarTech 4port SATA III 6gbps
    - annet 2x SATA (og eSATA)
## Disker
HDD
- 2stk Seagate Ironwolf Pro 18TB i array til array
    - ST18000NE000-2YY101_ZR5DB5WM (sdb) Until 6 March 2028
    - ST18000NE000-2YY101_ZR5EMZM1 (sdc) Until 22 December 2027
- 1stk Seagate Ironwolf Pro 12TB utenom array til backup
    - ST12000VN0008-2YS101_ZV70923Z (sdd) Until 28 June 2026
[Sjekk garanti på Seagate](https://www.seagate.com/gb/en/support/warranty-and-replacements/)

SSD
- 2stk [1000GB PNY CS900](https://www.elkjop.no/product/pc-datautstyr-og-kontor/lagring/intern-ssd/pny-cs900-25-1000-gb-serial-ata-iii-3d-tlc/519630?utm_source=prisjakt&utm_medium=pricecomparison&utm_campaign=prisjakt-listing-5 "‌") SSD til Cache ([SSD-specs](https://www.techpowerup.com/ssd-specs/#PNY%20CS900 "‌"))
	- PNY_CS900_1TB_SSD_PNY23402310040101482 (sde)
	- PNY_CS900_1TB_SSD_PNY23402310040101485 (sdf)
- 2stk Samsung 850 EVO 250GB
	- Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E (sdg)
	- Samsung_SSD_850_EVO_250GB_S21PNSAG319056D (sdh)****

---
# Changelog

| Dato           | Endring                                                                                 |
| -------------- | --------------------------------------------------------------------------------------- |
| Oktober? 2023 | Endret formål på Gaming PC til NAS. Installert Unraid. Kjøpte 2x 18tb + 1x 12tb disker. |
| Desember 2023  | Kjøpte 2x PNY 1tb SSDer for cache. Har også kjøpt nye raid-kort.                        |
|                |                                                                                         |

## HDD Preclear
HDD 18TB ST18000NM000J-2TV103_WR50A85F (sdg) Feb 18 15:33:26 preclear_disk_WR50A85F_32354: Preclear: total elapsed time: 71:49:27

---
# Arkiv
Effektforbruk:

- AV: 0.75-0.81 W
- IDLE (med GTX760): 88-100 W
- IDLE (kun iCPU): 61.8 W
- MAX (100% CPU transcoding + ripping): 110 W

Upgrade path:

- Cold spare 18TB HDD
    - Når NCGNAS trenger mer storage, gi den mine 18tb-disker i bytte mot x antall 12tb disker? Billigere og mer hensiktsmessig utvidelser for meg.
    - [
        
        ](https://www.prisjakt.no/c/interne-harddisker?direction=asc&sort=property.64014)

- [
    
    ](https://www.prisjakt.no/c/interne-harddisker?brand=1281&direction=asc&sort=property.64014)
- GPU for transcoding Jellyfin, Immich og NextCloud Memories - og Folding At Home?
- Flere 1tb SSD-er for lav responstid, spesielt for Immich/NextCloud. Bruke RAID 5?[
    
    ](https://carfax.org.uk/btrfs-usage/?c=1&slo=1&shi=100&p=1&dg=1&d=1000&d=1000&d=1000)
[

](https://docs.unraid.net/unraid-os/manual/storage-management/#change-pool-raid-levels)

Gammel stasjonær PC (originalt kjøpt/bygget 04.04.2013)

- Alt annet enn det som er blitt NAS
- [ASUS GeForce GTX 660Ti 2GB PhysX CUDA](https://www.komplett.no/product/759240?noredirect=true "‌")
- [Cooler Master GX 750W PSU](https://www.komplett.no/product/593204?noredirect=true "‌")
- [Kingston DDR3 HyperX 1600 MHz 16GB Black](https://www.komplett.no/product/776634?noredirect=true "‌")
- [ASUS Xonar DX Lydkort](https://www.komplett.no/product/347274?noredirect=true "‌")
- [BenQ 24" LED RL2450HT](https://www.komplett.no/product/657567?noredirect=true "‌")
- [ROCCAT Sota Mousepad Black](https://www.komplett.no/product/498331?noredirect=true "‌")
- [WD Desktop Green 2TB](https://www.komplett.no/product/760514?noredirect=true "‌")
- [Logitech Gaming Keyboard G105](https://www.komplett.no/product/649474?noredirect=true "‌")
- [Logitech G35 Gaming headset](https://www.komplett.no/product/435893?noredirect=true "‌")