23 000 TW (/h ?) from the sun every year

# Utvikling i ernergi-markedet 
## verden over
I 2013 bestod energibruken av 80,9% fossile brensler.
I 2023 bestod energibruken av 79,8% fossile brensler selv om man har bygd ut ca 13% mer produksjon!

## Norge
Solcelle-etableringen i Norge har sunket kraftig siste par årene, spesielt etter introduksjon av strømstøtte. Politikken bygger ikke opp mot bygginga v solcelleparker.
Vi trenger fortsatt solcelle-utbygging siden kraftbehovet vårt vokser så mye, og vi bygger ikke mer vannkraftverk.

I Norge har produksjonskapasitet gått fra 
- Ny innstallert effekt i 2025, 62 MW

# Myter
## Solar panels are not as effective in Norway
Basert på noen antakelser
- Dubai har "mest" sol energi i året (1700 kWh/kw/år).
- Munchen har ekstremt mye solinstallasjoner - men har like mye - 1040kWh/kw/år
- Bergen 689
- Sør-Norge har like stort potensial som Nord-Tyskland

Kaldere klima i Norge øker effektiviteten betraktelig.

Norge har godt utgangspunkt for solinnstallasjoner. 
- Genererer strøm også ved diffust lys/skyer
- produserer på ganske lik linje med fastlands Europa



# Theory
## Energy from the sun, photons
I sola er det fusjon

Placks 1 radiation law - funksjon for Spectral Irradiance
Kan snu den og derivere og få peak spectral irradiance som funksjon av temperatur:
$$
\lambda_{peak}(µm) = \frac{2900}{T}
$$
$$
\lambda \text{ er bølgelengde av lyset}
$$
$$
T \text{ er temperatur i kelvin?}
$$
Siden sola er sykt varm (6 000 ... grader) blir bølgelengdene i $nm$-skalaen (topp på 500 nm).

Energien i et photon. H er Plancks konstant og c lysets hastighet
$$
E = {h}*frekvens = konstant * \frac{c}{\lambda}
$$
Photon energy, in electronvolt
$$
1 eV = 1.602176634×10^{−19} J.
$$

## Semi-conductor
Electricity - the movement of charges, electrons
*conduction band and valence band, bandgap i mellom*
- Conductors has overlap between the conduction band and valence band
- Isolator har stor potensial/avstand mellom båndene
- Halvleder kan vi bestemme når skal lede eller ikke


Silikon er et av mange grunnstoff som kan fungere som halvledere
- Det andre mest tilgjengelige grunnstoffet i verden
- Doper det

Halvledere for PV
- Titanium Dioxide, nye typer
- ....


## Photovoltaics
Halvledere, to sider
1. Absorbering av lys, genererer enten elektron-hull eller excitons (?)
	1. Lys-energien gjør at elektronene hopper fra den ene siden til den andre
	2. Lys-energien, fotonene, er større enn band gap-energy
2. Seperation of charge carriers ....

### Important parameters; the amount of solar energy absorbed
- Utilization of band gap energy is important
- Spectral utilization
- Light management (?)

### Generation
- Photons - light or electromagnetic waves
- Phonons - energy from lattice vibrations, vibrations
- ...


### Grunnstoffene
GaAs har mye bedre absorpsjon-kurve enn silikon, så man bruker det i type satelitter - men det er dyrt.
![[3 - Photovoltaics-2025.09.09 11.25.08.webp|550]]

Silikonet man bruker i elektronikk må være 99% (med 9 desimaler) og er av monochrystaline struktur.


Silikon har indirect gap, trenger også **phonon** - trenger mer energi
Alpha
![[3 - Photovoltaics-2025.09.09 11.19.43.webp|550]]


### The trouble with homo-junction solar cells
Silikon absorberer fotoner opp til 1.1 eV, mens de andre kan absorbere høyere
![[3 - Photovoltaics-2025.09.09 11.21.13.webp|350]]

Den optimale energien i en foton er samme som band gap-energien. 
- Har fotonet lavere energi så vil ikke elektronet hoppe over, og all energi blir varme
- Har fotonet mer enn band gap, så blir differansen til varme
![[3 - Photovoltaics-2025.09.09 11.21.37.webp|450]]![[3 - Photovoltaics-2025.09.09 11.50.59.webp|350]]

Si må være tykkere for å få utnyttet all energien
![[3 - Photovoltaics-2025.09.09 11.44.54.webp|450]]

Si Maksimum teoretisk effektivitet er 33%, se tabell
![[3 - Photovoltaics-2025.09.09 11.22.22.webp|350]]![[3 - Photovoltaics-2025.09.09 11.51.47.webp|350]]


## Doping: Tre typer halvledere
- Intrinsic 
- n-type
- p-type

Silikon er i gruppe 4
- 4 valenselektroner, kan forme konvalensbånd med 4 andre silikon-atomer
- Rent silikon-materiale er helt stabilt

Kan dope
- med Fosfor fra gruppe 5 - gjør at strukturen har ett elektron til overs - n-type
- med Bor fra gruppe 3 - gjør at strukturen har elektronhull - p-type


### PN-junction
Kombinert P- og N-type mot hverandre. Får en depletion-zone i mellom seg
- Når den er saturated så er det et elektrisk felt 

I en PV-struktur lager man P-typen mindre, men mye kraftigere dopet. N-siden gjør man stor med lav konsentrasjon av doping.
- Det gjør at depletion-zone er mye større enn i en tradisjonell PN-junciton, og gir en større spenning, se under.




## Solar cell efficiency limits

$$
n = \frac{P_{out}}{P_{in}} = \frac{{I_{SC}*V_{OC}FF}}{P_{in}}
$$
1. Fill factor, determined by diode characteristic and series resistance
2. Short circuit current
	- increases as the bandgap decreases
	- For a given bandgap, determined by reflection, absorption, recombination
	- Lower Eg = more photons qualify → $I_{SC}$ øker
	- Høyere Eg = flere photoner har $E < Eg$ → $I_{SC}$ 
3. Open circuit voltage, increases as the bandgap increases. For a given bandgap, determined by recombination.

FYLL FRA PP
