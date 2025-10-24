Kjøpt for 500kr [pfSense Router | FINN torget](https://www.finn.no/bap/forsale/ad.html?finnkode=368495987).

## DHCP
Subnet: 10.10.0.1/24

Import CSV
```csv
ip_address,hw_address,hostname,description
10.10.0.41,4C:EB:D6:BC:47:1F,tasmota-BC471F-1823
10.10.0.40,4C:EB:D6:BC:44:11,tasmota-BC4411-1041
10.10.0.21,F0:2F:74:CB:47:93,krisstasjonerpop
10.10.0.42,BC:FF:4D:2B:B9:0D,prusalink
10.10.0.43,10:9C:70:0E:22:C3,PrusaMINI
10.10.0.13,52:54:00:C0:47:7C,homeassistant
10.10.0.4,00:0D:B9:5A:E8:E5,LolbraaSense
```

## OpnSense
### Installasjon
Image type: Serial
Forsøker full, ikke embedded
- [Initial Installation & Configuration — OPNsense  documentation](https://docs.opnsense.org/manual/install.html#)
- [pcengines (produsent) sin how to OS install opnsense](http://pcengines.ch/howto.php#OS_installation)
- [Install OPNsense - High-End Security Made Easy™](https://opnsense.org/users/get-started/)
Feilet booting av live-environment til `mountroot>`. Byttet til annen USB. Noe med USB3?
- [Mounting failed with error 19 during installation](https://forum.opnsense.org/index.php?topic=10097.0)
### Initial konfigurering
Laget ny bruker for adminstrering, lolbraa
- Enabled SSH, sudo, ssh-access, osv.
SSH
- Kun nøkler, Lolbraa Systemnøkkel
- [How To Enable and Start SSH Server on OPNsense | ComputingForGeeks](https://computingforgeeks.com/how-to-enable-and-start-ssh-server-on-opnsense/)
git
- 

Tailscale
- [Using OPNsense with Tailscale · Tailscale Docs](https://tailscale.com/kb/1097/install-opnsense)
- [How to Install and Configure Tailscale on OPNsense? - zenarmor.com](https://www.zenarmor.com/docs/network-security-tutorials/how-to-install-and-configure-tailscale-on-opnsense)
- tailscale set --advertise-routes=10.10.0.0/24 

Todo:
- [OPNsense performance optimization](https://teklager.se/en/knowledge-base/opnsense-performance-optimization/)
- [Snapshots — OPNsense  documentation](https://docs.opnsense.org/manual/snapshots.html)
### Tips
Most files are written from the backend, the files are under /usr/local/etc/inc, DHCP configurations are written from services.inc.

### Oppdatere
#### Firmware
Instruks [APU bios upgrade](https://teklager.se/en/knowledge-base/apu-bios-upgrade/) (obs utdatert url i kommando)
Firmware lastes ned fra: [PC Engines - github pages](https://pcengines.github.io/) 
```sh
curl -o apu2_v4.19.0.1.rom https://dl.3mdeb.com/open-source-firmware/pcengines/apu2/apu2_v4.19.0.1.rom
sudo flashrom -w apu2_v4.19.0.1.rom -p internal:boardmismatch=force -c W25Q64BV/W25Q64CV/W25Q64FV
```
*Husk å oppdatere filnavn*


---

# Informasjon
## OS
Bra sammenligning (men litt utdatert) [pfSense vs OPNsense](https://teklager.se/en/pfsense-vs-opnsense/)
## Hardware
[PC Engines - github pages](https://pcengines.github.io/)
## Specs
**apu2e0** = 2 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (stripped down board)
```
Nätadapter för APU1 / APU2 / APU3
Router Kit: 1
power: EU
16GB mSATA SSD
Router Kit: 1
Wall Mount for APU chassis
Router Kit: 1
APU Chassi
chassis: black_2lan
Router Kit: 1
PC Engines APU2E0 - 2 LAN, GX-412TC quad core, 2GB RAM
wifi: no-wifi
ssembly: assemble
Router Kit: 1
operating_system: pfsense
```

[PC Engines apu2e0 product file](https://pcengines.ch/apu2e0.htm)

| apu2e0               | System board                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Status**           | Active                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Part numbers**     | **apu2e0** = 2 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (stripped down board)  <br>**apu2e2** = 3 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM  <br>**apu2e4** = 3 **i210AT** LAN / AMD GX-412TC CPU / 4 GB DRAM  <br>**apu2e5** = 3 **i211AT** LAN / AMD GX-412TC CPU / 4 GB DRAM  <br>**apu2d0** = 2 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (superseded)  <br>**apu2d2** = 3 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (superseded)  <br>**apu2d4** = 3 i210AT LAN / AMD GX-412TC CPU / 4 GB DRAM (superseded)  <br>**apu2c0** = 2 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (superseded)  <br>**apu2c2** = 3 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (superseded)  <br>**apu2c4** = 3 i210AT LAN / AMD GX-412TC CPU / 4 GB DRAM (superseded)  <br>**apu2b2** = 3 i211AT LAN / AMD GX-412TC CPU / 2 GB DRAM (superseded)  <br>**apu2b4** = 3 i210AT LAN / AMD GX-412TC CPU / 4 GB DRAM (superseded)                                                                         |
| **Use with**         | [case1d2u](https://pcengines.ch/case1d2u.htm) / [case1d2blku](https://pcengines.ch/case1d2blku.htm) / [case1d2redu](https://pcengines.ch/case1d2redu.htm) / [case1d2bluu](https://pcengines.ch/case1d2bluu.htm) enclosures (use 2 LAN enclosures for apu2c0)  <br>[ac12veur3](https://pcengines.ch/ac12veur3.htm) / [ac12vus2](https://pcengines.ch/ac12vus2.htm) / [ac12vuk](https://pcengines.ch/ac12vuk.htm) AC adapter  <br>[msata16f](https://pcengines.ch/msata16f.htm) / [msata16g](https://pcengines.ch/msata16g.htm) (and other sizes) mSATA SSD  <br>[sd4b](https://pcengines.ch/sd4b.htm) SD card  <br>[wle200nx](https://pcengines.ch/wle200nx.htm) / [wle600vx](https://pcengines.ch/wle600vx.htm) / [wle900vx](https://pcengines.ch/wle900vx.htm) miniPCI express wireless modules  <br>[spi1a](https://pcengines.ch/spi1a.htm) flash recovery module                                                                                                              |
| **Specification**    | - CPU: AMD Embedded G series GX-412TC, 1 GHz quad Jaguar core with 64 bit and AES-NI support, 32K data + 32K instruction cache per core, shared 2MB L2 cache.<br>- DRAM: 2 or 4 GB DDR3-1333 DRAM<br>- Storage: Boot from m-SATA SSD, SD card (internal sdhci controller), or external USB. 1 SATA + power connector.<br>- 12V DC, about 6 to 12W depending on CPU load. Jack = 2.5 mm, center positive<br>- Connectivity: 2 or 3 Gigabit Ethernet channels (Intel i211AT on apu2b2, i210AT on apu2b4)<br>- I/O: DB9 serial port, 2 USB 3.0 external + + 2 USB 2.0 internal, three front panel LEDs, pushbutton<br>- Expansion: 2 miniPCI express (one with SIM socket), LPC bus, GPIO header, I2C bus, COM2 (3.3V RXD / TXD)<br>- Board size: 6 x 6" (152.4 x 152.4 mm) - same as apu1d, alix2d13 and wrap1e.<br>- Firmware: [coreboot](https://pcengines.github.io/)<br>- Cooling: Conductive cooling from the CPU to the enclosure using a 3 mm alu heat spreader (included). |
| **Documentation**    | [user's manual](https://pcengines.ch/pdf/apu2.pdf), [[apu2.pdf]]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **Howto**            | [HowTo collection](http://pcengines.ch/howto.php#home)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Cooling assembly** | [apu cooling assembly instructions](https://pcengines.ch/apucool.htm)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **BIOS update**      | [Update 3/2017: various fixes, iPXE with setup  <br>](https://pcengines.ch/file/apu2_v4.0.7.rom.zip)[Update 3/11/2016: add iPXE payload (cannot disable in setup yet)  <br>](https://pcengines.ch/file/apu2_160311.zip)[Update 3/7/2016: add SD boot support](https://pcengines.ch/file/apu2_160307.zip)  <br>[Update 2/11/2016: fix some performance leaks](https://pcengines.ch/file/apu2_160211.zip)  <br>[Update 1/20/2016: fix miniPCIe IRQ assignments, wle200nx working](https://pcengines.ch/file/apu2_160120.zip)<br><br>Please see Howto collection for instructions on BIOS upgrade.                                                                                                                                                                                                                                                                                                                                                                                  |
| **Update apu2e:**    | Changed battery socket footprint to avoid contact problems. Add signal integrity resistor for core voltage control signal.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| **Update apu2d:**    | Reduce leakage current between V3 and V3A power rails (can cause problems with SD cards). Add options for better compatibility with LTE modem modules.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Update apu2c:**    | Integrate blue wire patches (EMI, power-up circuit) into PCB fab.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Schematic**        | [apu2b](https://pcengines.ch/schema/apu2b.pdf) / [apu2c](https://pcengines.ch/schema/apu2c.pdf) / [apu2d](https://pcengines.ch/schema/apu2d.pdf) schematics                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| **Manufacturer**     | PC Engines                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| **Origin**           | Taiwan                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |