Pappa kjøpte en diagnotiserings-computer snakke med SL-motoren greie. Fulgte med en 256GB ssd med Windows to go og masse programmer. 
- Kunne boote over USB.
- Klonet disken til en lokal NVME på en laptop pappa hadde med CloneZilla.
- Tok etterpå backup av SSDen med CloneZilla til `braanas/mnt/user/backup/stig/`.

Kobler til diagnotisering med ethernet-kabel. Trenger USB-ethernet med denne laptopen.
- 15s-eq2025no, [https://support.hp.com/us-en/product/details/hp-15.6-inch-laptop-pc-15-e2000/model/2100376551?sku=4T3R7EA](https://support.hp.com/us-en/product/details/hp-15.6-inch-laptop-pc-15-e2000/model/2100376551?sku=4T3R7EA)
- Endret IP-addresse-konfigurasjon i Windows etter dette [How to Configure MB SD Connect C4 DoIP?](https://www.obdii365.com/service/configure-mb-sd-c4-doip-scanner.html?srsltid=AfmBOoqe9WMHMmfmob-VZoRho2a6ZlGG2h-hK5sdto9z4GMKFrkWkRXN)
	- IP address: **172.29.127.24**
	- Subnet mask: **255.255.0.0**
	- 5. Click on **Advanced**
	- 6. Click on **Add** to configure DoIP IP address
	- 7. Set DoIP IP address to **169.254.0.**** (i.e 169.254.0.45)

Bruksanvising:
1. 
