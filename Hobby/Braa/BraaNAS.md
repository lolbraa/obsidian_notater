10
	BraaNAS (ny)
	Hostname: BraaNAS
	OS: Unraid
	Specs:
		CPU: Intel Pentium G3250 3.2 GHz
		RAM: 2x 
		Hovedkort: ASUS BB5M-G3250
			6 SATA: 4 SATA3 og 2 SATA2
			1 PCIEx16
			2 PCIEx1
		PSU: Silver Power SP-SS850 fra gamle Martins PC
	Disker:
		12TB...

16.04.2025

Måtte bytte CMOS-batteri?



## Minnepenner
1. Død i januar 2025
2. Billig 2GB greie - Død ca. 17. mars 2025
	Denne? 
	Flash Vendor:
	    CBM
	Flash Product:
	    Flash_Disk 
	Flash GUID:
	    1E3D-6025-2117-0101BA332000  
	- Fungerer fortsatt (15.04.2025)
	- Sluttet å fungere, tror jeg (22.04.2025)
3. Kingston 64GB - tatt i bruk 22.04.2025
	- 0951-1666-74CC-E811F9BC05F4
	- DataTraveler_3.0 - 61.9 GB (sda)
9.2025, Ny død, stuck på boot? Unraid Connect hadde ikke sluttet å fungere, ingen backup i sky. Vurderer å sende en fresh minnepenn til Martin.
4. Kingston 64GB - tatt i bruk 16.10.2025
	- 0951-1666-73CD-18C1F9DB06C5
	- DataTraveler_3.0 - 62 GB (sda)
   


### DIsk-oversikt

| Plassering | Koblet til          | Disk                      | SN                                                                |     |
| ---------- | ------------------- | ------------------------- | ----------------------------------------------------------------- | --- |
|            | Hovedkort - SATA6G1 | 12TB Disk 5 - PARITY      | Recertified ZRT1EV1Y, ST12000NM000J-2TY103_ZRT1EV1Y - 12 TB (sdd) |     |
|            | Hovedkort - SATA6G2 | 12TB Disk 6 - Arraydisk 1 | Recertified ZRT1CT56, ST12000NM000J-2TY103_ZRT1CT56 - 12 TB (sde) |     |
|            | Hovedkort - SATA6G3 | SSD - Cache 1             | SanDisk_X110_2.5_7MM_128GB_141817402705 - 128 GB (sdc)            |     |
|            | Hovedkort - SATA6G4 | SSD - Cache 2             | SAMSUNG_MZ7LF128HCHP-000L1_S2G8NXAH325317 - 128 GB (sdb)          |     |
|            | Hovedkort - SATA3G  |                           | WD RED fra FamBraaNAS,                                            |     |
|            | Hovedkort - SATA3G  |                           | WD RED fra FamBraaNAS                                             |     |
|            |                     |                           |                                                                   |     |

## UPS
> [!NOTE]- NUT Device Scanner
> ```
> -----------------------------------------------------
> INFO: The NUT Scanner is also available from the terminal with more advanced settings.
> INFO: You can use 'nut-scanner -h' to see all available options for searching UPS devices.
> -----------------------------------------------------
> 
> Reading the system network configuration...
> Also scanning for SNMP devices on detected IP range: 192.168.1.1 - 192.168.1.255 ...
> 
> NUT Scanner is now searching for UPS devices...
> #####################################################
> 
> [nutdev-usb1]
> driver = "nutdrv_qx" # alternately: blazer_usb
> port = "auto"
> vendorid = "0665"
> productid = "5161"
> product = "USB to Serial"
> vendor = "INNO TECH"
> # bus = "003"
> # device = "002"
> # busport = "003"
> 
> #####################################################
> HOW TO INTERPRET THESE RESULTS:
> 
> Please select the UPS Driver, reported as 'driver' here, for your UPS inside the NUT Settings.
> It is usually best to leave the UPS Driver Port on 'auto' instead of using what is reported as 'port' here.
> 
> In case UPS Driver Port on 'auto' does not work, you can try using the 'port' information reported here instead.
> Beware that this might make the UPS Driver blind to any other physical ports than the one that is currently used.
> 
> Any additional settings reported here (apart from 'driver' and 'port') can be ignored in most cases.
> They could however prove very helpful in cases where your UPS Driver is not able to connect to your UPS.
> You can then put these extra settings in UPS.CONF using the GUI configuration editor (beware GUI reserved lines).
> 
> In case of a detected SNMP device, select all the displayed SNMP settings from inside the GUI (including the 'port').
> Alternatively, you can use 'Auto Config' to apply the entire displayed configuration without needing to set up the GUI.
> 
> NOTE: 'apc_modbus' requires for MODBUS protocol to be enabled on the UPS - otherwise use 'usbhid-ups'.
> ```


# Scripts / jobber

## Synkronisere BraaNAS Fotobank -> LolbraaNAS/Immich
rsync pull fra LolbraaNAS, for da har LolbraaNAS SSH-nøkkelen til BraaNAS (Braa Systemnokkel). Da gjør den diff-checking ([ Rsync (over SSH) performance - Push or Pull? ](https://www.reddit.com/r/selfhosted/comments/14gwmyb/rsync_over_ssh_performance_push_or_pull/))
```sh
rsync --archive --delete --progress --partial --verbose --human-readable --log-file="/mnt/user/appdata/.logs/rsync_sync_fotobank_fra_braanas/log_forste_manuelle_overskrive_gammel_fambraanas.txt" root@100.72.76.11:"/mnt/user/felles/Fotobank/" "/mnt/user/BraaNAS/felles/Fotobank"
```

### Churne gjennom Immich filer
> [!NOTE]-
> ```log
> immich_server            | [Nest] 7  - 01/14/2025, 8:23:50 AM   ERROR [Microservices:JobService] Unable to run job handler (thumbnailGeneration/generate-thumbnails): Error: VipsJpeg: ./lib/jpegli/decode_scan.cc:535: Incomplete scan detected.
> immich_server            | VipsJpeg: ./lib/jpegli/decode_marker.cc:448: Duplicate SOI marker
> immich_server            | [Nest] 7  - 01/14/2025, 8:23:50 AM   ERROR [Microservices:JobService] Error: VipsJpeg: ./lib/jpegli/decode_scan.cc:535: Incomplete scan detected.
> immich_server            | VipsJpeg: ./lib/jpegli/decode_marker.cc:448: Duplicate SOI marker
> immich_server            |     at Sharp.toBuffer (/usr/src/app/node_modules/sharp/lib/output.js:163:17)
> immich_server            |     at MediaRepository.decodeImage (/usr/src/app/dist/repositories/media.repository.js:57:68)
> immich_server            |     at MediaService.generateImageThumbnails (/usr/src/app/dist/services/media.service.js:161:63)
> immich_server            |     at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
> immich_server            |     at async MediaService.handleGenerateThumbnails (/usr/src/app/dist/services/media.service.js:111:25)
> immich_server            |     at async JobService.onJobStart (/usr/src/app/dist/services/job.service.js:148:28)
> immich_server            |     at async EventRepository.onEvent (/usr/src/app/dist/repositories/event.repository.js:134:13)
> immich_server            |     at async Worker.processJob (/usr/src/app/node_modules/bullmq/dist/cjs/classes/worker.js:394:28)
> immich_server            |     at async Worker.retryIfFailed (/usr/src/app/node_modules/bullmq/dist/cjs/classes/worker.js:581:24)
> immich_server            | [Nest] 7  - 01/14/2025, 8:23:50 AM   ERROR [Microservices:JobService] Object:
> immich_server            | {
> immich_server            |   "id": "471436cd-dc6f-424c-94dd-69a4011e80d9"
> immich_server            | }
> immich_server            | 
> immich_server            | [Nest] 7  - 01/14/2025, 8:24:08 AM   ERROR [Microservices:JobService] Unable to run job handler (thumbnailGeneration/generate-thumbnails): Error: Unknown error
> immich_server            | [Nest] 7  - 01/14/2025, 8:24:08 AM   ERROR [Microservices:JobService] Error: Unknown error
> immich_server            |     at Sharp.toBuffer (/usr/src/app/node_modules/sharp/lib/output.js:163:17)
> immich_server            |     at MediaRepository.decodeImage (/usr/src/app/dist/repositories/media.repository.js:57:68)
> immich_server            |     at MediaService.generateImageThumbnails (/usr/src/app/dist/services/media.service.js:161:63)
> immich_server            |     at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
> immich_server            |     at async MediaService.handleGenerateThumbnails (/usr/src/app/dist/services/media.service.js:111:25)
> immich_server            |     at async JobService.onJobStart (/usr/src/app/dist/services/job.service.js:148:28)
> immich_server            |     at async EventRepository.onEvent (/usr/src/app/dist/repositories/event.repository.js:134:13)
> immich_server            |     at async Worker.processJob (/usr/src/app/node_modules/bullmq/dist/cjs/classes/worker.js:394:28)
> immich_server            |     at async Worker.retryIfFailed (/usr/src/app/node_modules/bullmq/dist/cjs/classes/worker.js:581:24)
> immich_server            | [Nest] 7  - 01/14/2025, 8:24:08 AM   ERROR [Microservices:JobService] Object:
> immich_server            | {
> immich_server            |   "id": "b783c95a-efa5-4edc-9891-836f5325bc74"
> immich_server            | }
> immich_server            | 
> immich_server            | [Nest] 7  - 01/14/2025, 8:24:18 AM   ERROR [Microservices:JobService] Unable to run job handler (thumbnailGeneration/generate-thumbnails): Error: VipsJpeg: ./lib/jpegli/decode_scan.cc:539: Failed to decode DCT block
> immich_server            | [Nest] 7  - 01/14/2025, 8:24:18 AM   ERROR [Microservices:JobService] Error: VipsJpeg: ./lib/jpegli/decode_scan.cc:539: Failed to decode DCT block
> immich_server            |     at Sharp.toBuffer (/usr/src/app/node_modules/sharp/lib/output.js:163:17)
> immich_server            |     at MediaRepository.decodeImage (/usr/src/app/dist/repositories/media.repository.js:57:68)
> immich_server            |     at MediaService.generateImageThumbnails (/usr/src/app/dist/services/media.service.js:161:63)
> immich_server            |     at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
> immich_server            |     at async MediaService.handleGenerateThumbnails (/usr/src/app/dist/services/media.service.js:111:25)
> immich_server            |     at async JobService.onJobStart (/usr/src/app/dist/services/job.service.js:148:28)
> immich_server            |     at async EventRepository.onEvent (/usr/src/app/dist/repositories/event.repository.js:134:13)
> immich_server            |     at async Worker.processJob (/usr/src/app/node_modules/bullmq/dist/cjs/classes/worker.js:394:28)
> immich_server            |     at async Worker.retryIfFailed (/usr/src/app/node_modules/bullmq/dist/cjs/classes/worker.js:581:24)
> immich_server            | [Nest] 7  - 01/14/2025, 8:24:18 AM   ERROR [Microservices:JobService] Object:
> immich_server            | {
> immich_server            |   "id": "81d4478e-c9af-42d2-aa68-1f5ab8d2d4ce"
> immich_server            | }
> immich_server            | 
> ```
> 
> En kjøring av rsync for BraaNAS:/felles/Fotobank. Tar over 12 minutter å sjekke at den IKKE trenger å overføre filer.
> ```
> root@LolbraaNAS:/mnt/user# time rsync --archive --delete --progress --partial -v --stats --human-readable root@100.72.76.11:"/mnt/user/felles/Fotobank/" "/mnt/user/BraaNAS/felles/Fotobank" | tee $logFile -a
> hostfile_replace_entries: link /root/.ssh/known_hosts to /root/.ssh/known_hosts.old: Operation not permitted
> update_known_hosts: hostfile_replace_entries failed for /root/.ssh/known_hosts: Operation not permitted
> receiving incremental file list
> ./
> Annet/fotball/
> Annet/fotball/Vear G97/
> Annet/fotball/Vear G97/07.02.03 Vearcup/
> Person_Inger/
> Person_Martin_Andre/
> Usorterte/Ny mappe (2)/
> Usorterte/Privat/0007/
> Usorterte/Privat/06.03.25/
> Usorterte/Privat/06.06.30/
> Usorterte/Privat/08.fotobok/
> Usorterte/Privat/2010 mars2/
> 
> Number of files: 374,710 (reg: 373,251, dir: 1,459)
> Number of created files: 0
> Number of deleted files: 0
> Number of regular files transferred: 0
> Total file size: 1.69T bytes
> Total transferred file size: 0 bytes
> Literal data: 0 bytes
> Matched data: 0 bytes
> File list size: 930.01K
> File list generation time: 0.034 seconds
> File list transfer time: 0.000 seconds
> Total bytes sent: 2.92K
> Total bytes received: 8.13M
> 
> sent 2.92K bytes  received 8.13M bytes  10.85K bytes/sec
> total size is 1.69T  speedup is 208,107.06
> 
> real    12m28.488s
> user    0m3.099s
> sys     0m36.604s
> ```
> 


## Automatisk opplasting av bilder fra Nikon kamera til NAS og videre sortering i Fotobank
Bruker Nikon sin FTP funksjon til SFTPGo-docker på BraaNAS.
- Egen bruker, nikon
- Lagrer seg på /mnt/user/felles/Fotobank/!NIKON/

phockup-docker (docker compose, dockge) flytter og sorterer filene i riktig mappe
- [GitHub - ivandokov/phockup: Media sorting tool to organize photos and videos from your camera in folders by year, month and day.](https://github.com/ivandokov/phockup)
```
  phockup:
    volumes:
      - /mnt/user/felles/Fotobank/!NIKON:/mnt/input
      - /mnt/user/felles/Fotobank/2020-2029:/mnt/output
    environment:
      - CRON=* * * * *
      - OPTIONS=--move -d YYYY/YYYY.MM.DD --original-names
        --log="/mnt/input/Automatisk_sortering_av_bilder.log.txt"
    image: ivandokov/phockup:latest
```

# Synkronisering av Backups fra LolbraaNAS:/eksterndisk til BraaNAS:/lolbraa
Første synkronisering:
- Prøvde først å kjøre Duplicacy copy-kommando med et nytt repository på BraaNAS gjennom SMB-mount. Det tok evigheter, og ble avbrutt flere ganger.
- Valgte å integrere BraaNAS i Teliasky-skriptet.
	- Total chunk size is 5616G in 1187211 chunks


# Error arraydisk 3
WDC_WD30EFRX-68EUZN0_WD-WCC4N5KCFEZ0 - 3 TB (sdg)
```
Apr 27 18:06:08 BraaNAS kernel: ata6: SATA max UDMA/133 abar m2048@0xf7d1a000 port 0xf7d1a380 irq 28
Apr 27 18:06:08 BraaNAS kernel: ata6: SATA link up 3.0 Gbps (SStatus 123 SControl 300)
Apr 27 18:06:08 BraaNAS kernel: ata6.00: ATA-9: WDC WD30EFRX-68EUZN0, 82.00A82, max UDMA/133
Apr 27 18:06:08 BraaNAS kernel: ata6.00: 5860533168 sectors, multi 16: LBA48 NCQ (depth 32), AA
Apr 27 18:06:08 BraaNAS kernel: ata6.00: configured for UDMA/133
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] 5860533168 512-byte logical blocks: (3.00 TB/2.73 TiB)
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] 4096-byte physical blocks
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] Write Protect is off
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] Mode Sense: 00 3a 00 00
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] Write cache: enabled, read cache: enabled, doesn't support DPO or FUA
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] Preferred minimum I/O size 4096 bytes
Apr 27 18:06:08 BraaNAS kernel: sdg: sdg1
Apr 27 18:06:08 BraaNAS kernel: sd 6:0:0:0: [sdg] Attached SCSI disk
Apr 27 18:06:56 BraaNAS emhttpd: WDC_WD30EFRX-68EUZN0_WD-WCC4N5KCFEZ0 (sdg) 512 5860533168
Apr 27 18:06:56 BraaNAS kernel: mdcmd (4): import 3 sdg 64 2930266532 0 WDC_WD30EFRX-68EUZN0_WD-WCC4N5KCFEZ0
Apr 27 18:06:56 BraaNAS kernel: md: import disk3: (sdg) WDC_WD30EFRX-68EUZN0_WD-WCC4N5KCFEZ0 size: 2930266532 
Apr 27 18:06:56 BraaNAS emhttpd: read SMART /dev/sdg
Apr 27 22:34:15 BraaNAS emhttpd: spinning down /dev/sdg
Apr 28 08:46:02 BraaNAS emhttpd: read SMART /dev/sdg
Apr 28 15:00:09 BraaNAS emhttpd: spinning down /dev/sdg
May  1 00:00:02 BraaNAS emhttpd: read SMART /dev/sdg
May  1 00:01:36 BraaNAS kernel: ata6.00: exception Emask 0x0 SAct 0xc3e SErr 0x0 action 0x0
May  1 00:01:36 BraaNAS kernel: ata6.00: irq_stat 0x40000008
May  1 00:01:36 BraaNAS kernel: ata6.00: failed command: READ FPDMA QUEUED
May  1 00:01:36 BraaNAS kernel: ata6.00: cmd 60/40:08:a0:96:c5/05:00:00:00:00/40 tag 1 ncq dma 688128 in
May  1 00:01:36 BraaNAS kernel: ata6.00: status: { DRDY ERR }
May  1 00:01:36 BraaNAS kernel: ata6.00: error: { UNC }
May  1 00:01:36 BraaNAS kernel: ata6.00: configured for UDMA/133
May  1 00:01:36 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#1 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=4s
May  1 00:01:36 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#1 Sense Key : 0x3 [current] 
May  1 00:01:36 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#1 ASC=0x11 ASCQ=0x4 
May  1 00:01:36 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#1 CDB: opcode=0x88 88 00 00 00 00 00 00 c5 96 a0 00 00 05 40 00 00
May  1 00:01:36 BraaNAS kernel: I/O error, dev sdg, sector 12949888 op 0x0:(READ) flags 0x0 phys_seg 76 prio class 0
May  1 00:01:36 BraaNAS kernel: ata6: EH complete
May  1 00:01:40 BraaNAS kernel: ata6.00: exception Emask 0x0 SAct 0x787000 SErr 0x0 action 0x0
May  1 00:01:40 BraaNAS kernel: ata6.00: irq_stat 0x40000008
May  1 00:01:40 BraaNAS kernel: ata6.00: failed command: READ FPDMA QUEUED
May  1 00:01:40 BraaNAS kernel: ata6.00: cmd 60/40:70:e0:a6:c5/05:00:00:00:00/40 tag 14 ncq dma 688128 in
May  1 00:01:40 BraaNAS kernel: ata6.00: status: { DRDY ERR }
May  1 00:01:40 BraaNAS kernel: ata6.00: error: { UNC }
May  1 00:01:40 BraaNAS kernel: ata6.00: configured for UDMA/133
May  1 00:01:40 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#14 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=8s
May  1 00:01:40 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#14 Sense Key : 0x3 [current] 
May  1 00:01:40 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#14 ASC=0x11 ASCQ=0x4 
May  1 00:01:40 BraaNAS kernel: sd 6:0:0:0: [sdg] tag#14 CDB: opcode=0x88 88 00 00 00 00 00 00 c5 a6 e0 00 00 05 40 00 00
May  1 00:01:40 BraaNAS kernel: I/O error, dev sdg, sector 12953544 op 0x0:(READ) flags 0x0 phys_seg 139 prio class 0
May  1 00:01:40 BraaNAS kernel: ata6: EH complete
May  1 10:22:11 BraaNAS emhttpd: spinning down /dev/sdg
May 10 13:30:14 BraaNAS emhttpd: read SMART /dev/sdg

```


# Diagnostics: September, plutselig nede for telling
![[BraaNAS-1758302846182.webp|500x552]]
greit ved reboot
