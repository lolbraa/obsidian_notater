[Reducing SD Card Wear on a Raspberry Pi or Armbian Device • Chris Dzombak](https://www.dzombak.com/blog/2021/11/reducing-sd-card-wear-on-a-raspberry-pi-or-armbian-device/#if-the-system-can%E2%80%99t-use-a-read-only-filesystem)
- tmpfs /tmp /var/spool/rsyslog
- log2ram
- disabled swap
- filsystem-sjekk på boot
- 
# Pi-hole 
[80 WebUi] (Hostname: pihole.local)
	- Docker-bilde: Pi-Hole DoT DoH
	- DNS-server med sikret DNS-upstream gjennom Cloudflared og Google-greier
	- Vurderte Gravity Sync mellom Pihole-installasjonene, men den krever standard Docker.
	- ~~Orbital sync synkroniserer piholes~~
	- DHCP-server
Oppdatere 
```
sudo PIHOLE_SKIP_OS_CHECK=true pihole -r # Må skippe pga Rasbian?
```

## DHCP
Bruker for DHCP-server
Se statiske designasjoner [[Hobby/Lolbraa/Nettverksinfrastruktur#DHCP-tabell|Nettverksinfrastruktur]].

## Gravity lists
[EasyList - Overview](https://easylist.to/)
- EasyList, Cookies List, Privacy og to Fanboys
# Syslog
https://pimylifeup.com/raspberry-pi-syslog-server/
"/media/lolandbraa/4646-0D35/LolbraaNASsyslog.log" (Clas Ohlsson usb-penn)

# Oppdatere
[Raspberry Pi Documentation - Raspberry Pi OS](https://www.raspberrypi.com/documentation/computers/os.html)
```
sudo apt update
sudo apt full-upgrade
```
# Statisk IP
eth0 192.168.0.5
wlan0 192.168.0.6
[3 Easy Ways To Set A Static IP Address On Raspberry Pi – RaspberryTips](https://raspberrytips.com/set-static-ip-address-raspberry-pi/)
```
sudo nmtui
```

# Backup
LolbraaNAS rsync-puller / til LolbraaNAS: 
[How To Backup Your Entire Linux System Using Rsync - OSTechNix](https://ostechnix.com/backup-entire-linux-system-using-rsync/)
```LolbraaRPI:/etc/sudoers 
# rsync backup til lolbraanas https://askubuntu.com/questions/719439/using-rsync-with-sudo-on-the-destination-machine
lolandbraaa ALL=NOPASSWD:/usr/bin/rsync
```
- Laget en ny nøkkel, med privat på LolbraaNAS, og offentlig lagt inn i LolbraaRPI:authorised_keys
- Spesefisert i kommando eller LolbraaNAS /root/.ssh/config [key authentication - Specifying an IdentityFile with SSH - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/494483/specifying-an-identityfile-with-ssh)
```
Host 192.168.0.5
IdentityFile /root/.ssh/id_lolbraarpi
```

[How to backup Raspberry Pi - Linux Tutorials - Learn Linux Configuration](https://linuxconfig.org/how-to-backup-raspberry-pi)## How to back up the full Raspberry Pi system
[rpi-clone | A shell script to clone a booted disk on a Raspberry Pi.](https://rpi-clone.jeffgeerling.com/)
har ikke satt opp

# Docker
Installert med [Getting Started With Docker On Raspberry Pi (Full Guide) – RaspberryTips](https://raspberrytips.com/docker-on-raspberry-pi/)

# Changelog
Kjøpt [Komplett](https://www.komplett.no/product/1133778/datautstyr/pc-komponenter/hovedkort/integrert-cpu/raspberry-pi-4-model-b-2gb-ram) for 639kr 20.01.2024
