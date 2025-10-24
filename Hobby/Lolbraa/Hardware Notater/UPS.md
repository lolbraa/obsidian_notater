# BlueWalker PowerWalker VI 650 LCD (650VA 360W)
Kjøpt nytt batteri: 

| Dato       | Hendelse           | Notat                                                                                                                                                            |
| ---------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 02.10.2023 | Kjøpt nytt batteri | [BlueWalker PW PWB12-7](https://www.komplett.no/product/893783/datautstyr/pc-tilbehoer/ups-overspenningsvern/ups-og-ups-batteri/bluewalker-pw-pwb12-7) for 314kr |
| 23.04.2024 | Testet batteritid  | Last på ca 100W (LolbraaNAS og ruter).<br>Varte ca 30 minutter.                                                                                                  |

## Tips
[Komplett-anmeldelse](https://www.komplett.no/product/893766/datautstyr/pc-tilbehoer/ups-overspenningsvern/ups-og-ups-batteri/bluewalker-pw-ups-vi-2200-shl?channable=008081696400383933373636dd&gad_source=1&gclsrc=aw.ds#technical-details)
> Mye kapasitet for pengene, gir et kurant display for hva som skjer og hvilket modus den er i. Fungerer i Linux med medfølgende programvare eller enda bedre NUT med "usbhid-ups" driver. For de som vil programmere denne i NUT, så er dette følgende konfigurasjon i ups.conf: **[ups] driver = usbhid-ups port = auto vendorid = "06da" productid = "ffff" desc = "BlueWalker PW VI 2200 LCD"** Trekker to stjerner siden USB-kortet i denne er av elendig type og at tilkoblingen mister forbindelsen til maskinen hele tiden. Og det eneste man kan gjøre for å få den opp igjen er å manuelt koble til og fra kabelen. Mange har rapportert om denne feilen, og det gjelder ikke bare denne typen UPS. Problemet med dette er at UPS-en ikke kan kjøre en kontrollert shutdown av maskiner ved lengre strømstans. Dog finnes det løsninger for dette også, som jeg vurderer å prøve selv. Dette innebærer i å skaffe en USB-hub med portstrømstyring. Da kan man enkelt resette USB-pluggen med en kommando automagisk når det oppdages at kommunkasjonen er borte. Det mest irriterende med denne feilen, er at consolevinduet på linuxboksen blir spammet med broadcastmeldinger om "Connection lost" og "UPS unavailable" En serielport hadde kanskje ikke vært så dumt.


# Eaton Ellipse MAX 850
| Dato       | Hendelse               | Notat                                                                                          |
| ---------- | ---------------------- | ---------------------------------------------------------------------------------------------- |
| 20.05.2024 | Kjøpt to nye batterier | [AGM-batteri 12 V \| Clas Ohlson](https://www.clasohlson.com/no/p/36-5460) 329,90 \*2 = 659,80 |

[AGM-batteri 12 V | Clas Ohlson](https://www.clasohlson.com/no/p/36-5460) ?
[Bruksanvisning Eaton Ellipse MAX 850 USBS DIN (40 sider)](https://www.bruksanvisningpdf.no/eaton/ellipse-max-850-usbs-din/bruksanvisning)
![[Eaton Ellipse MAX.png]]
```
Ellipse MAX 850 USBS DIN
Serial No: ADGK4204D
Art .: FUE-510822
NT:06

10A MAX
50/60Hz
220-240V~10
3.70A MAX
550W/850VA PF=0.65
6.30A **MAX**
```