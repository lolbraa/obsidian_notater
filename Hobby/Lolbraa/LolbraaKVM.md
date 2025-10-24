PiKVM Raspberry Pi 4 - 1GB ram med [PiKVM](https://docs.pikvm.org/v3/) V3 HAT- Fantoft
- 2.519,25 NOK for både RPI og PiKVM
- [PiKVM HAT v3 PCI Mount](https://www.printables.com/model/763141-pikvm-hat-v3-pci-mount)
- Med Nvidia P400 måtte jeg skru av CSM (Computer Support Module...?) for å få riktig output

Dokumentasjon [PiKVM Handbook](https://docs.pikvm.org/)

Serial
# Update
[update os - PiKVM Handbook](https://docs.pikvm.org/_update_os/?h=updat)
```
pikvm-update
```

# Installere pakker
[FAQ & Troubleshooting - PiKVM Handbook](https://docs.pikvm.org/faq/#first-steps)
PiKVM OS is based on Arch Linux ARM and uses the [pacman](https://wiki.archlinux.org/title/Pacman) package manager.
- Ensure the date is correct: `date`. Otherwise you may get the error `SSL certificate problem: certificate is not yet valid`
- It is recommended to update the OS before installing new packages (see the tip upper ^^^).
- Switch filesystem to RW-mode: `rw`.
- Find some packages (`emacs` for example): `pacman -Ss emacs`.
- Install it: `pacman -Syy` to update local packages list and `pacman -Su emacs` to install.
- Remove it: `pacman -R emacs`.
- Switch filesystem to RO-mode: `ro`.

# Informasjon
## Serial
Se [[Serial#LolbraaKVM]]
## Oversikt
![[LolbraaKVM-20240908154330575.jpg|500]]
1. [**ATX controller** interface](https://docs.pikvm.org/atx_board/) (power on/off, reboot control, PWR and HDD ACT LEDs).
2. **HDMI reset** jumper. Connects GPIO 17 and RESET pin to HDMI capture chip. Currently not used, don't touch it.
3. **SPI and GPIO** for the custom extension boards.
4. **Audio capture** jumpers. Connects I2S pins 18, 19, 20 to HDMI capture chip.
5. **UART access** jumpers. Connects GPIO 14 and 15 to the RJ-45 and USB console ports.
6. **Serial console port** (default: /dev/ttyAMA0, RS232 input, outputs +6V/-6V, for the Raspberry Pi or server console access, use the [Cisco/Mikrotik-style](https://wiki.mikrotik.com/wiki/File:Rj45-pinout.gif.png) cable).
7. **USB-C console port** (shared with #6 above, takes priority over RJ45).
8. **Power** and **activity LEDs**. On the left of the LEDs the watchdog jumper is located. Don't touch it.
9. **USB-C power input**.
10. **I2C display connector**.
11. **Alternate +5V power input/output** header pins.
12. **RTC clock** supercapacitor (rechargeable).
13. **FAN connector** - PWM controlled.
14. **CSI-2 interface** and **HDMI backpowering** jumper, see [Step 9 of the Basic Setup](https://docs.pikvm.org/v3/#basic-setup). Open: (jumper removed) diode will stop current from HDMI input (backpower will be fixed), closed: (jumper connected to both pins) will allow current from HDMI device.
15. Built-in **power splitter** port.
16. **HDMI capture port** (max 1080p @ 50Hz) with **sound capture** support.
17. **USB emulation pins** for alternative access.
18. **USB-C emulation port** - this port is doing the emulation of a USB keyboard, mouse, Virtual CD-ROM or USB Flash Drive, USB-Ethernet, USB-Serial port and a lot of other Linux-supported features.
19. **1-Wire** & **Neo-pixel** interface (under, advanced user feature).

## Customize panelet
[Discord](https://discord.com/channels/580094191938437144/880066200959328328/1280293598360768624)
	The PiKVM's html pages are generated from pug files included in KVMD. The HTML itself is a result of the pug files. So I'd say the best way is to modify the pug files and store them in a separate repo so you can regenerate html later. My PiKVM-IDE has an F1->tasks script to recompile the pug files. [https://github.com/adamoutler/PiKVM-IDE](https://github.com/adamoutler/PiKVM-IDE "https://github.com/adamoutler/PiKVM-IDE")



# 26.09.2025 Problemer med DNS
Kunne ikke oppdatere eller pinge google.com, feil med DNS
```sh
journalctl -u systemd-resolved -f

Sep 26 08:19:03 lolbraakvm systemd-resolved[258]: Using degraded feature set TCP instead of UDP for DNS server 100.100.100.100.
Sep 26 08:19:13 lolbraakvm systemd-resolved[258]: Using degraded feature set UDP instead of 
TCP for DNS server 100.100.100.100

tailscale set --accept-dns=false
```

