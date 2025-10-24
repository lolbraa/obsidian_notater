# Selge
zeros med [killdisk](https://www.killdisk.com/eraser.html) 
[kilde Intel](https://www.intel.com/content/www/us/en/support/articles/000006198/memory-and-storage.html)
[Kilde Reddit](https://www.reddit.com/r/msp/comments/10peled/reliable_disk_wipe_utility_for_machines_that_will/)

# SMART-attributes
[Known smart-attributes - Wikipedia](https://en.wikipedia.org/wiki/Self-Monitoring,_Analysis_and_Reporting_Technology#Known_ATA_S.M.A.R.T._attributes)

Intel [Common SMART Attributes for Intel® Optane™ Technology...](https://www.intel.com/content/www/us/en/support/articles/000056596/memory-and-storage/client-ssds.html)
Seagate [How do I interpret SMART diagnostic utilities results? | Seagate UK](https://www.seagate.com/gb/en/support/kb/how-do-i-interpret-smart-diagnostic-utilities-results-203971en/?q=203971&l=en_US&fs=Search&pn=1)
- Fullstendig manual for seagate exos [[seagate-exos-manual-104425-19871593.pdf]]

# KrissStasjonær
## 4x Hoveddisker
[[SMART-data-20240802174814230.jpg]]

[[SMART-data-20240802174814286.jpg]]

[[SMART-data-20240802174814382.jpg]]

[[SMART-data-20240802174814512.jpg]]



## 2x SSD Kingston 240GB - Ekstradisker Linux
[[KrissStasjonær-20240802132717802-SMART.jpg]]
[[KrissStasjonær-20240802132648012-SMART.jpg]]



# Diverse
[[SSDer SMART-1.png]]
[[SSDer SMART-2.png]]
[[SSDer SMART-3.png]]




## 3x SSD Sandisk x110 120GB skal selges
[[SMART-data-20240802174746432.jpg]]

[[SMART-rapporter-20240802175650963.jpg]]

[[SMART-rapporter-20240802175810299.jpg]]


## 2x SSD 2TB feilkjøpt og solgt Finn
[[SSDer SMART-4.png]]
[[SSDer SMART-5.png]]


### Intel SSDs
[1.6 TB Intel SSD | FINN torget](https://www.finn.no/bap/forsale/ad.html?finnkode=369038277)
[Known smart-attributes - Wikipedia](https://en.wikipedia.org/wiki/Self-Monitoring,_Analysis_and_Reporting_Technology#Known_ATA_S.M.A.R.T._attributes)
[Common SMART Attributes for Intel® Optane™ Technology...](https://www.intel.com/content/www/us/en/support/articles/000056596/memory-and-storage/client-ssds.html)
SSD1: 
- Serie Nummer BTWA64440DR41P6KGN
- Kjørte timer: 52063
SSD2:
- Serie Nummer BTWA64440EJ31P6KGN
- Kjørte timer: 51936

| ID     | Attribute forklaring              |                                                                                                                                                            | SSD1 Hex     | Dec      | SSD2 Hex         | Dec       |
| ------ | --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | -------- | ---------------- | --------- |
| AD 173 | SSD Wear leveling count           | Counts the maximum worst erase count on any block.                                                                                                         | 0            |          | 0                |           |
| AF     | Power Loss Protection Failure     |                                                                                                                                                            | 012A001A2576 |          | 012D003231F6<br> |           |
| B4     | Unused Reserved Block Count Total | "Pre-Fail" attribute used at least in HP devices.<br><br>If the value drops to 0 the device may become read-only to allow the user to retrieve stored data | 0000030C80EF | 51151087 | 000002FEDF3F     | 50257727₁ |
