The Solar Resource, presented by Andrés Olivares

# Geografien bak Sol intensitet 
[SunCalc - sunrise, sunset, shadow length, solar eclipse, sun position, sun phase, sun height, sun calculator, sun movement, map, sunlight phases, elevation, Photovoltaic system, Photovoltaic](https://www.suncalc.org/)
Jorda er tiltet ca. 23grader ift. sola.
- Ekvator er ikke varmeste, det er tropebåndene - 23 grader nord og sør for ekvator
![[2 - Solar radiation-2025.08.26 14.49.00.webp|550]]![[2 - Solar radiation-2025.08.26 14.49.10.webp|550]]

## Beregning av utnyttet effekt
[JRC Photovoltaic Geographical Information System (PVGIS) - European Commission](https://re.jrc.ec.europa.eu/pvg_tools/en/#MR)
[Maps gigafactory](https://earth.google.com/web/search/Tesla+Gigafactory+Nevada,+Electric+Avenue,+Sparks,+NV,+USA/@39.5408722,-119.4398906,1447.46938833a,633.93828954d,35y,0h,0t,0r/data=CqkBGnsSdQolMHg4MDk5MWZjMjQwYmEzMGI5OjB4N2U2NmIwZmE0ZmU1NWNkOBlkKN1MO8VDQCFXNOcqJ9xdwCo6VGVzbGEgR2lnYWZhY3RvcnkgTmV2YWRhLCBFbGVjdHJpYyBBdmVudWUsIFNwYXJrcywgTlYsIFVTQRgCIAEiJgokCdFmPegCRURAETunTfJUZkNAGS03VtGJjl3AISszKafZ4l3AQgIIAToDCgEwQgIIAEoNCP___________wEQAA?authuser=0)

Gigafactory Nevada solar roof
$$
A_{total} = 90000 m^2, 
A_{\text{per panel}} = 2,5 m^2, 
\phi = 0,23, 
Power = 610 W_{peak}
$$
Peak Power tested under Standard Test Conditions (STC) under 1000 W/m²
Solar Radiation on location, $G = 2055 \frac{kWh}{m^2}$ per year.
$$
E = 2000 \frac{kWh}{m^2} * 90 000 m^2 * 0,23 = 41,4 * 10^6 kWh= 41,4 GWh
$$

# Grunnleggende
Atmosfæren absorrberer mye av solenergien totalt sett
- Solceller kan kun absorbere en del av spektrumet - 23 %
- Et legeme, feks sort metall, kan absorbere hele spektrumet og derfor bedre effektivitet
![[2 - Solar radiation-2025.08.26 13.28.37.webp|550]]


## Begrensningene for solceller
Utnytter at atomene blir excited; at elektronene hopper opp på "energinivåer" i Bohrs atommodell
- Hoppingen skjer når elektronet blir truffet av fotoner
- Når et materiale består av mange atomer er det ikke lenger energinivå, men **energibånd**
- Energibånd og conduction band
	- I et metall er det ingen sperre/spenningsskille mellom valensbåndet og conduction band; elektronene flyter godt
	- Isolasjon er motsatt; stort spenningsnivå mellom båndene
	- Halvledere er midt i mellom, kan manipulere
		- Utnytter spenningsskillet til å høste energien i sola
![[2 - Solar radiation-2025.08.26 13.35.34.webp|700]]
- Teoretisk topp effektivitet for Si er ca. 32%

Båndet til ulike materialer
![[2 - Solar radiation-2025.08.26 13.39.16.webp|550]]


## Geografiske begrensninger
Jordas og solas geometriske forhold byr på problemer
- Sol-intensiteten varierer ila. året, og er forskjellig ulike steder på jorden.
- Når solstråler kommer på skrå er det to problemer
	- Arealet som solstråler treffer er større (Lamberts Cosine Law)
	- Solstrålet må passere mer masse av atmosfæren
![[2 - Solar radiation-2025.08.26 14.48.19.webp|350]]![[2 - Solar radiation-2025.08.26 14.46.55.webp|400]]


## Solcelle-teknologier
PERC i 2010 med 21%
Top Con med 23 % - mye bruk i dag i store prosjekter
BC (back contact) med 24% - snart i stor skala bruk


# Måling
## Metrologiske Målinger ved solcelleparker
Pyranometers
- På solcelleparker monterer man flere i ulike grader for å måle intensiteten (1) horisontalt for referansepunkt mot simulasjoner, og (2) retningen solcellene peker.

Vindmåling
- Tre tårn som sender ut ultralyd, og med doppler-effekten kan man beregne vindhastighet/retning

Regn

Temperatur
- Konveksjon for å dra luften over proben

## Solar Radiation
Deler opp i direkte/beam, diffust og reflektert. Sammen er "total radiation"
- Man bruker som regel bi-facial-paneler i parker for å innhøste reflektert energi; 20% mer energi ut
- Diffust kastes av skyer og atmosfæren
	- Blå himmel - nitrogen i atmosfæren
- Reflektert fra bakken osv.

Pyranometer måler **global solar radiation**
- Second class - Thermopile - dyr, presis, med glass, fragile
- Third class - Photodiode - billig, tåler mye, mer upresis
![[2 - Solar radiation-2025.08.26 14.52.55.webp|550]]

Albedometer - to pyranometer som opp og ned. Viktig for bi-facial paneler
![[2 - Solar radiation-2025.08.26 14.52.37.webp|200]]

Shadow device - Måle diffust lys
- En pyranometer hvor man blokkerer direkte sollys enten med en fast ring eller en motorisert skygge-bånd
![[2 - Solar radiation-2025.08.26 14.52.21.webp|550]]

Phyreliometer - Måler direkte lys
- En lang tube festet til en sol-tracker. Følger sola gjennom dagen. ![[2 - Solar radiation-2025.08.26 14.51.24.webp|550]]


# Annet
![[2 - Solar radiation-2025.08.26 14.54.11.webp|550]]

## Beregninger
Bruker mange programmer, SAM (fra NREL) er gratis. PVsyst er industristandard.

Perez-modell
![[2 - Solar radiation-2025.08.26 14.56.07.webp]]

Prosjekteringer: +-4% feil i kalkuleringer av effekt/energi for store prosjekt

![[2 - Solar radiation-2025.08.26 14.56.58.webp|550]]

