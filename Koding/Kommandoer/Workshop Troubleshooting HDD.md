# LolbraaNAS
## Diverse2 - Samsung: Disk-error: Uncorrectable 
### Feilmeldinger:
Fåttt noen av disse, kun en gang?
Uncorrectable error cnt på Samsung
```
17-01-2025 10:06	Unraid Diverse disk SMART health [187]	Warning [LOLBRAANAS] - uncorrectable error cnt is 8	Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E (sde)	warning	
17-01-2025 10:04	Unraid Diverse disk SMART health [187]	Warning [LOLBRAANAS] - uncorrectable error cnt is 2	Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E (sde)	warning	
16-01-2025 06:28	Unraid Diverse disk SMART health [5]	Warning [LOLBRAANAS] - reallocated sector ct is 1	Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E (sde)	warning
```


## Cache 3 Kingston (sdj): HDD-error: CRC-error
### Feiloppførsel:
- Ved store overføringer kommer mange feilmeldinger.

### Feilmeldinger:
Ulike feilmeldinger. Eks Syslog
```SYSLOG
```
Fra WebUI (etterfulgt like etter av "returned to normal")

> [!NOTE]-  30\. Januar: **DEGRADED**
> ```
>       pool: cache
>      state: DEGRADED
>     status: One or more devices are faulted in response to persistent errors.
>     	Sufficient replicas exist for the pool to continue functioning in a
>     	degraded state.
>     action: Replace the faulted device, or use 'zpool clear' to mark the device
>     	repaired.
>       scan: scrub repaired 0B in 00:59:09 with 0 errors on Sun Jan 26 00:59:10 2025
>     config:
> 
>     	NAME           STATE     READ WRITE CKSUM
>     	cache          DEGRADED     0     0     0
>     	  raidz1-0     DEGRADED     0     0     0
>     	    /dev/sdi1  ONLINE       0     0     0
>     	    /dev/sdl1  ONLINE       0     0     0
>     	    /dev/sdj1  FAULTED      7     4     0  too many errors
> 
>     errors: No known data errors
> ```
> SYSLOG
> ```
> Jan 30 03:12:20 LolbraaNAS kernel: sd 3:0:4:0: attempting task abort!scmd(0x00000000e6e7404d), outstanding for 30424 ms & timeout 30000 ms
> Jan 30 03:12:20 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7153 CDB: opcode=0x28 28 00 46 d1 e9 e8 00 00 08 00
> Jan 30 03:12:20 LolbraaNAS kernel: scsi target3:0:4: handle(0x000d), sas_address(0x4433221105000000), phy(5)
> Jan 30 03:12:20 LolbraaNAS kernel: scsi target3:0:4: enclosure logical id(0x500605b005d926a0), slot(6) 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7129 UNKNOWN(0x2003) Result: hostbyte=0x0b driverbyte=DRIVER_OK cmd_age=23s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7121 UNKNOWN(0x2003) Result: hostbyte=0x0b driverbyte=DRIVER_OK cmd_age=4s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7121 CDB: opcode=0x28 28 00 69 37 98 f0 00 00 80 00
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7129 CDB: opcode=0x28 28 00 5d 3e 7c 10 00 00 08 00
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 1564376080 op 0x0:(READ) flags 0x700 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 1765251312 op 0x0:(READ) flags 0x700 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=800959504384 size=4096 flags=180880
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=903807623168 size=65536 flags=180880
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: task abort: SUCCESS scmd(0x00000000e6e7404d)
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7153 UNKNOWN(0x2003) Result: hostbyte=0x03 driverbyte=DRIVER_OK cmd_age=34s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7153 CDB: opcode=0x28 28 00 46 d1 e9 e8 00 00 08 00
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 1188162024 op 0x0:(READ) flags 0x700 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=608337907712 size=4096 flags=180880
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7143 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=2s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7143 Sense Key : 0x2 [current] 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7143 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7143 CDB: opcode=0x28 28 00 66 84 f2 80 00 00 08 00
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 1719988864 op 0x0:(READ) flags 0x700 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=880633249792 size=4096 flags=180880
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7146 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=0s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7146 Sense Key : 0x2 [current] 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7146 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7146 CDB: opcode=0x28 28 00 00 00 0a 10 00 00 10 00
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 2576 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=270336 size=8192 flags=b08c1
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7147 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=0s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7147 Sense Key : 0x2 [current] 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7147 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7147 CDB: opcode=0x28 28 00 6f c8 16 10 00 00 10 00
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 1875383824 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=960195469312 size=8192 flags=b08c1
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7148 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=0s
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7148 Sense Key : 0x2 [current] 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7148 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:23 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7148 CDB: opcode=0x28 28 00 6f c8 18 10 00 00 10 00
> Jan 30 03:12:23 LolbraaNAS kernel: I/O error, dev sdj, sector 1875384336 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 2
> Jan 30 03:12:23 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=960195731456 size=8192 flags=b08c1
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7133 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=0s
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7133 Sense Key : 0x2 [current] 
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7133 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7133 CDB: opcode=0x28 28 00 00 00 0a 10 00 00 10 00
> Jan 30 03:12:25 LolbraaNAS kernel: I/O error, dev sdj, sector 2576 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 2
> Jan 30 03:12:25 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=270336 size=8192 flags=b0ac1
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7134 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=0s
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7134 Sense Key : 0x2 [current] 
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7134 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7134 CDB: opcode=0x28 28 00 6f c8 16 10 00 00 10 00
> Jan 30 03:12:25 LolbraaNAS kernel: I/O error, dev sdj, sector 1875383824 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 2
> Jan 30 03:12:25 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=960195469312 size=8192 flags=b0ac1
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7135 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=0s
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7135 Sense Key : 0x2 [current] 
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7135 ASC=0x4 ASCQ=0x0 
> Jan 30 03:12:25 LolbraaNAS kernel: sd 3:0:4:0: [sdj] tag#7135 CDB: opcode=0x28 28 00 6f c8 18 10 00 00 10 00
> Jan 30 03:12:25 LolbraaNAS kernel: I/O error, dev sdj, sector 1875384336 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 2
> Jan 30 03:12:25 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=1 offset=960195731456 size=8192 flags=b0ac1
> ```

> [!NOTE]- Januar 2024
> ```
> 23-01-2025 09:00	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 524288	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:58	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:55	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:54	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:42	Unraid Cache 3 SMART message [199]	Notice [LOLBRAANAS] - sata crc error count returned to normal value	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	normal	
> 23-01-2025 08:40	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:38	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:35	Unraid Cache 3 SMART message [199]	Notice [LOLBRAANAS] - sata crc error count returned to normal value	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	normal	
> 23-01-2025 08:30	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 08:27	Unraid Cache 3 SMART message [199]	Notice [LOLBRAANAS] - sata crc error count returned to normal value	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	normal	
> 23-01-2025 07:52	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 524288	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:49	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 458752	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:45	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:42	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:41	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:40	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:30	Unraid Cache 3 SMART message [199]	Notice [LOLBRAANAS] - sata crc error count returned to normal value	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	normal	
> 23-01-2025 07:28	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 23-01-2025 07:24	Unraid Cache 3 SMART message [199]	Notice [LOLBRAANAS] - sata crc error count returned to normal value	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	normal
> ```

> [!NOTE]- Oktober 2024
> ```WARNING
> 01-10-2024 11:08	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 524293	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 09:22	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 524291	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 08:51	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 524290	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:22	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 524289	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:20	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:18	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:11	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:09	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:05	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 02:01	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:58	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:51	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:50	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:48	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:46	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:41	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:37	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:35	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:29	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:27	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:25	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:24	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:22	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:16	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:15	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:13	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:11	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:06	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:02	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 01:00	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:57	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:56	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:49	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:47	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:45	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:44	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:42	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:39	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:36	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 1	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:30	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:29	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:28	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:26	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:24	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:23	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:18	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:16	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:13	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:11	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:05	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:04	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:03	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:02	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 01-10-2024 00:00	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:58	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:58	Unraid Cache disk disk utilization	Warning [LOLBRAANAS] - Cache disk is high on usage (76%)	PNY_CS900_1TB_SSD_PNY23402310040101482 (sdi)	warning	
> 30-09-2024 23:54	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:53	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:48	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 393216	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:46	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 327680	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:45	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 262144	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:43	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:41	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:38	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 196608	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:37	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 65536	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:32	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 131072	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:30	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 1	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> 30-09-2024 23:26	Unraid Cache 3 SMART health [199]	Warning [LOLBRAANAS] - sata crc error count is 1	KINGSTON_SA400S37960G_50026B7785459723 (sdj)	warning	
> ```

### Årsak:
Kan være flere ulike årsaker
- Mange peker til dårlig SATA-kabel eller HBA.

### Fiks:
> [!NOTE]- Oktober 2024: ZFS-scrub i WebUI. 
> Konkluderer med at det ikke haster. 
> ```
>   pool: cache
>  state: ONLINE
>   scan: scrub in progress since Tue Oct  1 14:55:31 2024
> 	1.82T scanned at 0B/s, 32.2G issued at 767M/s, 1.82T total
> 	0B repaired, 1.73% done, 00:40:48 to go
> config:
> 
> 	NAME           STATE     READ WRITE CKSUM
> 	cache          ONLINE       0     0     0
> 	  raidz1-0     ONLINE       0     0     0
> 	    /dev/sdi1  ONLINE       0     0     0
> 	    /dev/sdl1  ONLINE       0     0     0
> 	    /dev/sdj1  ONLINE       0     0     0
> 
> errors: No known data errors
> 
> ```

31.01.2025:
Idet jeg skal til å bytte den ut pga. ZFS kaller den degraded, leser jeg at CRC-error er FEILTOLKET av Unraid. Det er altså ingen ting galt som skjer, men en vendor-specific SMART-datapunkt. Ref [Reddit - Dive into anything](https://www.reddit.com/r/unRAID/comments/1d5vran/sata_crc_error_count/).
```
...
 That being said, your initial query was regarding the value interpreted by the UNRAID software as standing for "SATA CRC Error". In fact, this is not the case and the reason for this false positive is because SMART diagnostic applications for SATA SSDs are not standardised as opposed to M.2 NVMe SSDs. This means that certain values can be incorrectly interpreted by different software applications depending on where these values are located.

For the SA400S37, value 199 is in fact vendor specific and by that we mean it can and does vary from one SA400S37/480G SSD controller to another. One uses the value to report raw data, the other SSD does not utilise the value at all.  
```


---



## HDD-error
### Feiloppførsel:

**SCSI Devices**

|            |                                                           |
| ---------- | --------------------------------------------------------- |
| [0:0:0:0]  | cd/dvd  PiKVM    CD-ROM Drive     0606  /dev/sr0   1.07GB |
| [1:0:0:0]  | disk    Kingston DataTraveler 3.0       /dev/sda   15.4GB |
| [2:0:0:0]  | disk     USB      SanDisk 3.2Gen1 1.00  /dev/sdb   15.6GB |
| [3:0:0:0]  | disk    ATA      PNY CS900 1TB SS 0615  /dev/sdc   1.00TB |
| [4:0:0:0]  | disk    ATA      PNY CS900 1TB SS 0615  /dev/sdd   1.00TB |
| [5:0:0:0]  | disk    ATA      ST12000VN0008-2Y SC60  /dev/sde   12.0TB |
| [6:0:0:0]  | disk    ATA      ST18000NM000J-2T SN02  /dev/sdf   18.0TB |
| [7:0:0:0]  | disk    ATA      ST18000NE000-2YY EN01  /dev/sdg   18.0TB |
| [8:0:0:0]  | disk    ATA      ST1000DM003-1ER1 CC43  /dev/sdh   1.00TB |
| [9:0:0:0]  | disk    ATA      Samsung SSD 850  2B6Q  /dev/sdi    250GB |
| [10:0:0:0] | disk    ATA      Samsung SSD 850  2B6Q  /dev/sdj    250GB |
| [11:0:0:0] | disk    ATA      ST18000NE000-2YY EN01  /dev/sdk   18.0TB |
| [12:0:0:0] | disk    ATA      KINGSTON SA400S3 Z1.3  /dev/sdl    960GB |

### Feilmeldinger:

> [!NOTE]- logs
> 
> ```
> May 23 19:41:39 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x100000 SErr 0x0 action 0x6 frozen
> May 23 19:41:39 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 23 19:41:39 LolbraaNAS kernel: ata10: hard resetting link
> May 23 19:41:39 LolbraaNAS kernel: I/O error, dev sdj, sector 1875384624 op 0x1:(WRITE) flags 0x700 phys_seg 1 prio class 2
> May 23 19:41:39 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=2 offset=960195878912 size=4096 flags=180ac0
> May 23 19:42:01 LolbraaNAS nginx: 2024/05/23 19:42:01 [error] 20252#20252: *416078 connect() to unix:/var/run/syslog.sock failed (111: Connection refused) while connecting to upstream, client: 192.168.0.214, server: , request: "GET /webterminal/syslog/ws HTTP/1.1", upstream: "http://unix:/var/run/syslog.sock:/ws", host: "lolbraanas"
> May 23 19:42:04 LolbraaNAS nginx: 2024/05/23 19:42:04 [error] 20252#20252: *416118 connect() to unix:/var/run/syslog.sock failed (111: Connection refused) while connecting to upstream, client: 192.168.0.214, server: , request: "GET /webterminal/syslog/ws HTTP/1.1", upstream: "http://unix:/var/run/syslog.sock:/ws", host: "lolbraanas"
> 
> 
> May 23 19:52:29 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x1800000 SErr 0x0 action 0x6 frozen
> May 23 19:52:29 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 23 19:52:29 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 23 19:52:29 LolbraaNAS kernel: ata10: hard resetting link
> May 23 19:52:30 LolbraaNAS kernel: I/O error, dev sdj, sector 1875384184 op 0x1:(WRITE) flags 0x700 phys_seg 1 prio class 2
> May 23 19:52:30 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=2 offset=960195653632 size=4096 flags=180ac0
> May 23 19:52:30 LolbraaNAS kernel: I/O error, dev sdj, sector 1875384696 op 0x1:(WRITE) flags 0x700 phys_seg 1 prio class 2
> May 23 19:52:30 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=2 offset=960195915776 size=4096 flags=180ac0
> May 23 21:25:07 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x100000 SErr 0x0 action 0x6 frozen
> May 23 21:25:07 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 23 21:25:07 LolbraaNAS kernel: ata10: hard resetting link
> May 23 21:25:07 LolbraaNAS kernel: I/O error, dev sdj, sector 1875384680 op 0x1:(WRITE) flags 0x700 phys_seg 1 prio class 2
> May 23 21:25:07 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdj1 error=5 type=2 offset=960195907584 size=4096 flags=180ac0
> May 23 21:25:33 LolbraaNAS kernel: usb 1-1.2: device descriptor read/64, error -32
> May 23 21:25:33 LolbraaNAS kernel: usb 1-1.2: device descriptor read/64, error -32
> May 23 21:25:33 LolbraaNAS kernel: usb 1-1.2: device descriptor read/64, error -32
> ```
> 
> ZFS-pool-status
> ```
>   pool: cache
>  state: ONLINE
> status: One or more devices has experienced an unrecoverable error.  An
> 	attempt was made to correct the error.  Applications are unaffected.
> action: Determine if the device needs to be replaced, and clear the errors
> 	using 'zpool clear' or replace the device with 'zpool replace'.
>    see: https://openzfs.github.io/openzfs-docs/msg/ZFS-8000-9P
>   scan: scrub repaired 0B in 00:43:59 with 0 errors on Thu May 23 20:38:24 2024
> config:
> 
> 	NAME           STATE     READ WRITE CKSUM
> 	cache          ONLINE       0     0     0
> 	  raidz1-0     ONLINE       0     0     0
> 	    /dev/sdc1  ONLINE       0     0     0
> 	    /dev/sdd1  ONLINE       0     0     0
> 	    /dev/sdj1  ONLINE       0     7     0
> 
> errors: No known data errors
> ```
> 
> Annen dag:
> ```
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: exception Emask 0x0 SAct 0x1004000 SErr 0x0 action 0x6 frozen
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: cmd 61/08:70:18:7b:65/00:00:07:00:00/40 tag 14 ncq dma 4096 out
> May 25 21:53:36 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: cmd 61/08:c0:80:7f:65/00:00:07:00:00/40 tag 24 ncq dma 4096 out
> May 25 21:53:36 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 21:53:36 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 25 21:53:36 LolbraaNAS kernel: ata8: hard resetting link
> May 25 21:53:37 LolbraaNAS kernel: ata8: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 25 21:53:37 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 25 21:53:37 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 25 21:53:37 LolbraaNAS kernel: ata8.00: configured for UDMA/133
> May 25 21:53:37 LolbraaNAS kernel: ata8: EH complete
> May 25 21:53:40 LolbraaNAS root: Fix Common Problems: Warning: Blank TLD ** Ignored
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: exception Emask 0x0 SAct 0x40000020 SErr 0x0 action 0x6 frozen
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: cmd 61/10:28:48:59:20/00:00:0e:00:00/40 tag 5 ncq dma 8192 out
> May 25 21:55:00 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: cmd 61/08:f0:08:59:20/00:00:0e:00:00/40 tag 30 ncq dma 4096 out
> May 25 21:55:00 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 25 21:55:00 LolbraaNAS kernel: ata8: hard resetting link
> May 25 21:55:00 LolbraaNAS kernel: ata8: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 25 21:55:00 LolbraaNAS kernel: ata8.00: configured for UDMA/133
> May 25 21:55:00 LolbraaNAS kernel: ata8: EH complete
> May 25 21:56:48 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x10000 SErr 0x0 action 0x6 frozen
> May 25 21:56:48 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 25 21:56:48 LolbraaNAS kernel: ata10.00: cmd 61/08:80:20:5a:c9/00:00:06:00:00/40 tag 16 ncq dma 4096 out
> May 25 21:56:48 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 21:56:48 LolbraaNAS kernel: ata10.00: status: { DRDY }
> May 25 21:56:48 LolbraaNAS kernel: ata10: hard resetting link
> May 25 21:56:49 LolbraaNAS kernel: ata10: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 25 21:56:49 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 25 21:56:49 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 25 21:56:49 LolbraaNAS kernel: ata10.00: configured for UDMA/133
> May 25 21:56:49 LolbraaNAS kernel: ata10: EH complete
> May 25 21:57:30 LolbraaNAS kernel: ata8.00: exception Emask 0x0 SAct 0x1000 SErr 0x0 action 0x6 frozen
> May 25 21:57:30 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 25 21:57:30 LolbraaNAS kernel: ata8.00: cmd 61/08:60:20:ba:c8/00:00:06:00:00/40 tag 12 ncq dma 4096 out
> May 25 21:57:30 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 21:57:30 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 25 21:57:30 LolbraaNAS kernel: ata8: hard resetting link
> May 25 21:57:31 LolbraaNAS kernel: ata8: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 25 21:57:31 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 25 21:57:31 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 25 21:57:31 LolbraaNAS kernel: ata8.00: configured for UDMA/133
> May 25 21:57:31 LolbraaNAS kernel: ata8: EH complete
> 
> May 25 22:00:17 LolbraaNAS kernel: ata9.00: exception Emask 0x0 SAct 0x8 SErr 0x0 action 0x6 frozen
> May 25 22:00:17 LolbraaNAS kernel: ata9.00: failed command: WRITE FPDMA QUEUED
> May 25 22:00:17 LolbraaNAS kernel: ata9.00: cmd 61/08:18:b8:19:c8/00:00:6f:00:00/40 tag 3 ncq dma 4096 out
> May 25 22:00:17 LolbraaNAS kernel:         res 40/00:00:00:00:00/00:00:00:00:00/00 Emask 0x4 (timeout)
> May 25 22:00:17 LolbraaNAS kernel: ata9.00: status: { DRDY }
> May 25 22:00:17 LolbraaNAS kernel: ata9: hard resetting link
> May 25 22:00:18 LolbraaNAS kernel: ata9: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 25 22:00:18 LolbraaNAS kernel: ata9.00: configured for UDMA/133
> May 25 22:00:18 LolbraaNAS kernel: sd 11:0:0:0: [sdk] tag#3 UNKNOWN(0x2003) Result: hostbyte=0x00 driverbyte=DRIVER_OK cmd_age=30s
> May 25 22:00:18 LolbraaNAS kernel: sd 11:0:0:0: [sdk] tag#3 Sense Key : 0x5 [current] 
> May 25 22:00:18 LolbraaNAS kernel: sd 11:0:0:0: [sdk] tag#3 ASC=0x21 ASCQ=0x4 
> May 25 22:00:18 LolbraaNAS kernel: sd 11:0:0:0: [sdk] tag#3 CDB: opcode=0x2a 2a 00 6f c8 19 b8 00 00 08 00
> May 25 22:00:18 LolbraaNAS kernel: I/O error, dev sdk, sector 1875384760 op 0x1:(WRITE) flags 0x700 phys_seg 1 prio class 2
> May 25 22:00:18 LolbraaNAS kernel: zio pool=cache vdev=/dev/sdk1 error=5 type=2 offset=960195948544 size=4096 flags=180ac0
> May 25 22:00:18 LolbraaNAS kernel: ata9: EH complete
> ```
> SMART-data
> ```
> 25.05.2025 22.00
> |199|SATA CRC error count|0x0032|100|100|000|Old age|Always|Never|524380|
> ```
> 
> **En tredje dag**
> - Innlemmet fiksen med kernel-parameter og rebootet
> - Men får nå error-meldinger for Samsung-SSDene (ata10 og ata8, Diverse og Diverse 2).
> - Ser nå at jeg har antatt feil; de fleste feilmeldingene tidligere er fra disse diskene - men også ata9.
> - Mest sannsynlig en feil med kontrolleren, "88SE9230 PCIe 2.0 x2 4-port SATA 6 Gb/s RAID Controller Marvell Technology Group Ltd." (tatt fra DiskSpeed). 
> 
> Logs fra disk-loggen på /Main
> Diverse
> ```
> May 31 18:55:13 LolbraaNAS emhttpd: Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E (sdl) 512 488397168
> May 31 18:55:13 LolbraaNAS emhttpd: import 33 cache device: (sdl) Samsung_SSD_850_EVO_250GB_S2R6NXAH318808E
> May 31 18:55:14 LolbraaNAS emhttpd: read SMART /dev/sdl
> May 31 18:56:10 LolbraaNAS emhttpd: #011devid    1 size 232.88GiB used 123.03GiB path /dev/sdl1
> May 31 18:56:10 LolbraaNAS kernel: BTRFS info (device sdl1): first mount of filesystem 8f2e740d-d94b-4067-9580-37066ce7624a
> May 31 18:56:10 LolbraaNAS kernel: BTRFS info (device sdl1): using crc32c (crc32c-intel) checksum algorithm
> May 31 18:56:10 LolbraaNAS kernel: BTRFS info (device sdl1): using free space tree
> May 31 18:56:10 LolbraaNAS kernel: BTRFS info (device sdl1): enabling ssd optimizations
> May 31 18:56:10 LolbraaNAS kernel: BTRFS info (device sdl1: state M): turning on async discard
> May 31 19:13:33 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x8000000 SErr 0x0 action 0x6 frozen
> May 31 19:13:33 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 31 19:13:33 LolbraaNAS kernel: ata10.00: cmd 61/20:d8:80:19:04/00:00:19:00:00/40 tag 27 ncq dma 16384 out
> May 31 19:13:33 LolbraaNAS kernel: ata10.00: status: { DRDY }
> May 31 19:13:33 LolbraaNAS kernel: ata10: hard resetting link
> May 31 19:13:34 LolbraaNAS kernel: ata10: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:13:34 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:13:34 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:13:34 LolbraaNAS kernel: ata10.00: configured for UDMA/133
> May 31 19:13:34 LolbraaNAS kernel: ata10: EH complete
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x200000 SErr 0x0 action 0x6 frozen
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: cmd 61/20:a8:e0:b3:17/00:00:19:00:00/40 tag 21 ncq dma 16384 out
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: status: { DRDY }
> May 31 19:16:48 LolbraaNAS kernel: ata10: hard resetting link
> May 31 19:16:48 LolbraaNAS kernel: ata10: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:16:48 LolbraaNAS kernel: ata10.00: configured for UDMA/133
> May 31 19:16:48 LolbraaNAS kernel: ata10: EH complete
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x400 SErr 0x0 action 0x6 frozen
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: cmd 61/08:50:20:51:41/00:00:07:00:00/40 tag 10 ncq dma 4096 out
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: status: { DRDY }
> May 31 19:19:02 LolbraaNAS kernel: ata10: hard resetting link
> May 31 19:19:02 LolbraaNAS kernel: ata10: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:19:02 LolbraaNAS kernel: ata10.00: configured for UDMA/133
> May 31 19:19:02 LolbraaNAS kernel: ata10: EH complete
> May 31 19:19:19 LolbraaNAS kernel: BTRFS info (device sdl1): scrub: started on devid 2
> May 31 19:19:19 LolbraaNAS kernel: BTRFS info (device sdl1): scrub: started on devid 1
> May 31 19:25:36 LolbraaNAS kernel: ata10.00: exception Emask 0x0 SAct 0x400 SErr 0x0 action 0x6 frozen
> May 31 19:25:36 LolbraaNAS kernel: ata10.00: failed command: WRITE FPDMA QUEUED
> May 31 19:25:36 LolbraaNAS kernel: ata10.00: cmd 61/10:50:38:74:4d/00:00:07:00:00/40 tag 10 ncq dma 8192 out
> May 31 19:25:36 LolbraaNAS kernel: ata10.00: status: { DRDY }
> May 31 19:25:36 LolbraaNAS kernel: ata10: hard resetting link
> May 31 19:25:37 LolbraaNAS kernel: ata10: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:25:37 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:25:37 LolbraaNAS kernel: ata10.00: supports DRM functions and may not be fully accessible
> May 31 19:25:37 LolbraaNAS kernel: ata10.00: configured for UDMA/133
> May 31 19:25:37 LolbraaNAS kernel: ata10: EH complete
> ```
> Diverse 2
> ```
> May 31 18:55:13 LolbraaNAS emhttpd: Samsung_SSD_850_EVO_250GB_S21PNSAG319056D (sdj) 512 488397168
> May 31 18:55:13 LolbraaNAS emhttpd: import 34 cache device: (sdj) Samsung_SSD_850_EVO_250GB_S21PNSAG319056D
> May 31 18:55:14 LolbraaNAS emhttpd: read SMART /dev/sdj
> May 31 18:56:10 LolbraaNAS emhttpd: #011devid    2 size 232.88GiB used 123.03GiB path /dev/sdj1
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: exception Emask 0x0 SAct 0x200 SErr 0x0 action 0x6 frozen
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: cmd 61/08:48:10:2d:25/00:00:00:00:00/40 tag 9 ncq dma 4096 out
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 31 19:10:04 LolbraaNAS kernel: ata8: hard resetting link
> May 31 19:10:04 LolbraaNAS kernel: ata8: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 31 19:10:04 LolbraaNAS kernel: ata8.00: configured for UDMA/133
> May 31 19:10:04 LolbraaNAS kernel: ata8: EH complete
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: exception Emask 0x0 SAct 0x800000 SErr 0x0 action 0x6 frozen
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: cmd 61/20:b8:20:35:c8/00:00:05:00:00/40 tag 23 ncq dma 16384 out
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 31 19:10:59 LolbraaNAS kernel: ata8: hard resetting link
> May 31 19:10:59 LolbraaNAS kernel: ata8: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 31 19:10:59 LolbraaNAS kernel: ata8.00: configured for UDMA/133
> May 31 19:10:59 LolbraaNAS kernel: ata8: EH complete
> May 31 19:18:03 LolbraaNAS kernel: ata8.00: exception Emask 0x0 SAct 0x80 SErr 0x0 action 0x6 frozen
> May 31 19:18:03 LolbraaNAS kernel: ata8.00: failed command: WRITE FPDMA QUEUED
> May 31 19:18:03 LolbraaNAS kernel: ata8.00: cmd 61/08:38:48:8b:64/00:00:07:00:00/40 tag 7 ncq dma 4096 out
> May 31 19:18:03 LolbraaNAS kernel: ata8.00: status: { DRDY }
> May 31 19:18:03 LolbraaNAS kernel: ata8: hard resetting link
> May 31 19:18:04 LolbraaNAS kernel: ata8: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
> May 31 19:18:04 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 31 19:18:04 LolbraaNAS kernel: ata8.00: supports DRM functions and may not be fully accessible
> May 31 19:18:04 LolbraaNAS kernel: ata8.00: configured for UDMA/133
> May 31 19:18:04 LolbraaNAS kernel: ata8: EH complete
> ```

### Årsak:
- Strømforsyningsproblemer? [hard drive - Are these SATA errors dangerous? - Ask Ubuntu](https://askubuntu.com/questions/133946/are-these-sata-errors-dangerous/133960#133960)
- Dårlig tilkobling? [SATA exception Emask 0x10 SAct 0x0 SErr 0x4000000 action 0xe frozen - Thomas-Krenn-Wiki-en](https://www.thomas-krenn.com/en/wiki/SATA_exception_Emask_0x10_SAct_0x0_SErr_0x4000000_action_0xe_frozen)
- Ny firmware?
	- Forsøke oppdatering [KSM Firmware Update- Kingston Technology](https://www.kingston.com/en/support/technical/ksm-firmware-update) 
	- ny firmware-dokument [SA400\_GENERIC\_RN.pdf](https://media.kingston.com/support/downloads/SA400_GENERIC_RN.pdf)
- Skru av Powertop og alle andre strømoptimaliseringer?
	- [powertop - Unraid](https://forums.unraid.net/topic/98070-reduce-power-consumption-with-powertop/#:~:text=controllers%20have%20an%20incompatibility) nevner eksplisitt problemer med noen kontrollere.
- Endret fra x2 til x4 PCIe-lanes i BIOS?

### Fiks:
1. Forsøkt [M.2 SATA Adapter & "failed command: READ FPDMA QUEUED" error ](https://www.reddit.com/r/unRAID/comments/18v94ys/m2_sata_adapter_failed_command_read_fpdma_queued/?share_id=cLLc02Z8yrsSOPtSO-Npb&utm_content=1&utm_medium=android_app&utm_name=androidcss&utm_source=share&utm_term=2&rdt=44357) og lagt inn i kernel-parameters som vist her [\[Solved\] PCIE errors - General Support - Unraid](https://forums.unraid.net/topic/111161-solved-pcie-errors/#comment-1013378)
```
libata.force=noncqtrim
```

2. Skrevet om spare-kommandoene i go-filen (etter [powertop - Unraid](https://forums.unraid.net/topic/98070-reduce-power-consumption-with-powertop/#:~:text=controllers%20have%20an%20incompatibility) ) for å hoppe over host 10,11,12, altså kun ta 1-8 (tall valgt basert på tabellen nederst https://lolbraanas/Tools/SysDevs) og rebootet.
   Samtidig endret x4 til x2 i BIOS.

---