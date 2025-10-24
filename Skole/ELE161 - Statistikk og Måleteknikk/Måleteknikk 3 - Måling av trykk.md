# Trykk
$$
p = \frac{F}{A}
$$
## Enheter
- Pascal (Pa) 
- Bar (bar) 
- Millibar (mbar) 
- Atmosfære (atm) 
- Millimeter kvikksølv (mmHg) 
- Pounds per square inch (psi) 
	- 1 Pa = 1 N/m²
	- 100 kPa = 100000 Pa
	- 0.001 bar = 100 Pa
	- 1 bar = 100 kPa
	- 0,1333 kPa (1 atm ≈ 760 mmHg)
	- 101,325 kPa = 1,01325 bar
	- 6,894757 kPa (1 bar ≈ 14.5 psi)

## "Typer" trykk
### Absolutt trykk
- Trykk relativt til vakuum

Anvendelser (eksempler):
- Strømningsberegninger
- Prosessoptimalisering i industrien

Enheten **bar kan bli referert til som bara**.
### Overtrykk (gauge pressure)
- Absolutt trykk minus atmosfærisk trykk

Anvendelser (eksempler):
- Styrkeberegninger i rør og tanker
- I bildekk
- Å sikre riktig strømningsretning ut av en skorstein

Enheten **bar kan bli referert til som barg**.
### Differensialtrykk (trykkforskjell)
- Forskjell mellom trykket to steder

Anvendelser (eksempler):
- Strømningsmåling
- Nivåmåling
- Å sikre riktig strømningsretning


![[Måleteknikk 3 - Måling av trykk-1758699261798.webp|500x240]]


# Målinger
## Væskekolonne
![[Måleteknikk 3 - Måling av trykk-1758699292859.webp|500x350]]![[Måleteknikk 3 - Måling av trykk-1758699314907.webp|200x350]]


## Mekanisk trykkmåling
med fjær




## Elektronisk trykkmåling
### Målecellen
Målecelle for trykkforskjellsmåling.
- Består av to kammer adskilt av en membran.
- Membranen kan være en tynn metallplate, keramikkskive, plastskive eller annet…
![[Måleteknikk 3 - Måling av trykk-1758699462125.webp|500x239]]

Målecelle for overtrykk
- En side av målecellen er åpen til luft 
- Det betyr at det er atmosfærisk trykk på den siden 
- Membranen må være sterkere enn for trykkforskjells-celler siden trykkforskjellen mellom de to kamrene nå er større.

Målecelle for absolutt trykk
- Vakum på den ene siden


### Målemetoder
Flere måter, for eksempel:
- Strekklapp
- Piezoresistivt element
- Potensiometer
- Kapasitivt element
- Induktivt – Linear Variable Differential Transformer (LVDT)
- Magnetisk – Hall sensor
- Piezoelektrisk
- Optisk

$$
R = R_{0} \left(  1 + G \frac{\Delta l}{l_{0}} \right)
$$

### Strekklapp
![[Måleteknikk 3 - Måling av trykk-1758699613218.webp|500x264]]
![[Måleteknikk 3 - Måling av trykk-1758699630000.webp|500x241]]

Typiske data
- $R_{0}$ rundt 120 ohm
- G ca 2
- $\Delta l/l_{0}$ mellom -0.01 og 0.02 (kan også klemmes sammen)

### Piezoresistive materialer
$$
R = R_{0} \left(  1 + G \frac{\Delta l}{l_{0}} \right)
$$
- Består av et p- eller n-dopet halvledermateriale (silikonbasert)
	- For p-dopet materiale: 𝐺 kan typisk være mellom 100 og 175
	- For n-dopet materiale: 𝐺 kan typisk være mellom -100 og -140
- Kan lage svært små enheter som mer effektivt måler forskyvningen enn det strekklapper kan gjøre
- Basis for MEMS – teknologi (MicroElectrical Mechanical Systems)
- Disse kan festes på membranen i en målecelle for trykk, for å måle forskyvningen …eller membranen er laget av et slikt stoff…