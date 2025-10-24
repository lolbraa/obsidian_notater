# BraaRPI / BraaVPN
Raspberry Pi 3 B - Tønsberg
- VPN-server Tønsberg. Raspberry OS LITE. Brukernavn passord i 1pass. Headless. VPN med [https://pimylifeup.com/raspberry-pi-wireguard/](https://pimylifeup.com/raspberry-pi-wireguard/)
- [https://en.wikipedia.org/wiki/Raspberry_Pi#Model_B](https://en.wikipedia.org/wiki/Raspberry_Pi#Model_B)
- [https://www.etechnophiles.com/raspberry-pi-3-gpio-pinout-pin-diagram-and-specs-in-detail-model-b/](https://www.etechnophiles.com/raspberry-pi-3-gpio-pinout-pin-diagram-and-specs-in-detail-model-b/)

# BraaKVM
En av NanoKVMene jeg har kjøpt, se [[#NanoKVM]].
Statisk IP etter [Static IP - Sipeed Wiki](https://wiki.sipeed.com/hardware/en/kvm/NanoKVM/network/static_ip.html)
`/boot/eth.nodhcp`
```
192.168.1.11/24 192.168.1.1  # addr/netid gw
```

Etter å ha flyttet nettverk fra Fantoft til Tolvsrød slet den med å pinge WAN.
- Måtte fikse DNS i `/boot/resolv.conf`
- Måtte legge inn gateway (192.168.1.1) under route med `route add default gw 192.168.1.1`

Fikk ikke video-signal
-  Sjekket resolution med `echo "$(cat /kvmapp/kvm/width) * $(cat /kvmapp/kvm/height)"` (1080)
- Måtte bytte kabel

# LolbraaRPI
Raspberry Pi 4 B - 2GB ram - Fantoft
- PiVPN (WireGUard) og PiHole.
    - Overtatt for 1B da cloudflared mistet støtten.
[[LolbraaKVM]]

# Raspberry Pi 1 B - ubrukt
- ~~PiVPN (Wireguard) og PiHole på Fantoft~~
- ~~SysPI for NCG~~
- Gitt til Oscar

# NCG Adminlaptop
Gammel Nora laptop fra VGS

# Gammel Kriss Laptop fra VGS
[[LolbraaPVE]]


# [[Ebøker]]


# Mobil skjerm
[7 Inch LCD IPS Display HDMI-compatible Touch Screen With Case 1024x600 Resolution for Raspberry Pi 3 Pi4 PC Portable Monitor](https://www.aliexpress.com/item/1005005957866746.html?spm=a2g0o.order_list.order_list_main.76.794318021Z7s3S)
US $45.44 (med VOET skatt)

Plugg USB før HDMI. Noen ganger vil ikke HDMI fungere uten restart.

# NanoKVM
5 stk NanoKVM Lite for US $111.22 fra Aliexpress 18.01.2025
- trenger SD-kort
- 
[GitHub - sipeed/NanoKVM: NanoKVM: Affordable, Multifunctional, Nano RISC-V IP-KVM](https://github.com/sipeed/NanoKVM)
Sikkerhetsrisiko 
- [Response to concerns about NanoKVM security · Issue #301 · sipeed/NanoKVM · GitHub](https://github.com/sipeed/NanoKVM/issues/301)

# Ekstrasystem fra NCG
Prefabrikat av merke Medion
- Model: MT39
- Type: MED MT 8277N
- ML-110000
- MD 35024 (ERAZER Engineer P10)
- [MSN 10024023](https://www.medion.com/gb/service/international?int_country=no)
- Noe specs [Medion Erazer Engineer P10 MD35024 - Desktops - Coolblue](https://www.coolblue.nl/product/885876/medion-erazer-engineer-p10-md35024.html#product-specifications)

RAM: 2 x 16 GB (32GB) Micron DDR4 PV-2666 MHz
- MTA16ATF2G64AZ-2G6E1
- 16GB 2RXB PC4-2666V-UB1-11
CPU: i7-10700F SRH70 2.9GHZ, X043H589 (Comet Lake)
- [Intel.com](https://www.intel.com/content/www/us/en/products/sku/199318/intel-core-i710700f-processor-16m-cache-up-to-4-80-ghz/specifications.html)
- Ingen iGPU [Solved: How to I get into bios? Medion Erazer P10? - Page 2 - MEDION Community](https://community.medion.com/t5/Desktop-PC-All-In-One/How-to-I-get-into-bios-Medion-Erazer-P10/td-p/116152/page/2)
- PCI Express Configurations: Up to 1x16, 2x8, 1x8+2x4
- Max # of PCI Express Lanes: 16
- Sockets Supported: FCLGA1200
Hovedkort: 
- Specs: [FAQ: Specifications mainboard "ECS B460H6-EM". - MEDION Community](https://community.medion.com/t5/FAQs/FAQ-Specifications-mainboard-quot-ECS-B460H6-EM-quot/ta-p/157525) MSN 20067648
- Modell: ECS B460H6-EM
- Chipset: Mest sannsynlig Intel 
- 2 RAM-slots, DDR4?
	- Module: 	288-Pin DIMM
	- Type: 	SDRAM DDR4
	- Clock: 	2666 MHz
	- Voltage: 	1,2 V
	- Max: 32GB
- 4 SATA
- 2 M.2 SSD-slots (+1 for wlan)
	- SATA-breakout?
	- [Reddit - Dive into anything](https://www.reddit.com/r/DataHoarder/comments/xiqhik/m2_to_8xsata_adapter_anyone_tried_more_in_comments/)
	- [ECS07](https://www.silverstonetek.com/en/product/info/expansion-cards/ECS07/)
	- 
Which m.2 cards can be used:

| Slot | Connection   | Dimension  | Key(s) | Comment      |
| ---- | ------------ | ---------- | ------ | ------------ |
| 1    | SATA         | 2260, 2280 |        |              |
| 2    | PCIe x4 NVMe | 2260, 2280 | M key  | Optane ready |
| 3    |              | 2230       | E key  | only WLAN    |
The front PIN assignment can be seen in the illustration.![[Annen hardware-20240731104131970.jpg]]


## Changelog

| Dato        | Handling                                                                          | Beskrivelse                                                     |
| ----------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Sommer 2024 | Fått fra Martin                                                                   | Hovedkort, CPU, kabinett                                        |
| 07.08.2024  | Satt inn GPU                                                                      | P400 orig. for LolbraaNAS                                       |
| 07.08.2024  | Kjøpt RAM fra [Finnt](https://www.finn.no/bap/forsale/ad.html?finnkode=363190198) | 2 x 16 GB (32GB) DDR4 PV-2666. <br>Testet med Memtest i  timer. |
| 07.08.2024  |                                                                                   |                                                                 |