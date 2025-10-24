Disse to formlene/modellene muliggjør beskrivelse av lineære kretser i form av en topunktsmodell med en eller flere avhengige kilder.
# Den asymptotiske forsterkningformel
Topunktso,

![[5 Toterminalsmodeller-2025.02.18 09.49.53.jpg|550]]



Blokkdiagram av A_F
![[5 Toterminalsmodeller-2025.02.18 10.24.21.jpg|450]]


## OPAMP eksempel
![[5 Toterminalsmodeller-2025.02.18 09.33.50.jpg]]

Finner sløyfeforsterkning:
Setter den avhengige kilden U_b til en uavhengig kilde, og setter opp forsterkningsforhold $T = \frac{U_{id}}{U_{b}}$

![[5 Toterminalsmodeller-2025.02.18 09.34.42.jpg|550]]

Ser på forsterkningen av kilden, A_0
Finner 
![[5 Toterminalsmodeller-2025.02.18 09.42.35.jpg|550]]

Da blir den fullverdige forsterkningen i kretsen
![[5 Toterminalsmodeller-2025.02.18 09.42.51.jpg|550]]


# Blackmanns impedanseformel
Spør etter impedansen mellom to terminaler.
Måler sløyfeforsterkning ved to betingelser:
1. når man kortslutter terminalene.
2. når det er åpent mellom terminalene.

Obs: Som regel blir en av disse 0.
Velger ut en avhengig kilde i kretsen som gjør regnearbeidet enklest. Man gjør tre regnestykker som (oftest) er enklere enn å løse direkte.

## Forskjeller mellom de to
Dette er et spesialtilfelle av asymptotiske forsterkningformel der inn- og ut-terminaler er de SAMME. Altså er det både en strøm og spenning som varierer.
Man kan gjenbruke uttrykk fra asymptotiske forsterkningformel.

## Utførelse
![[5 Toterminalsmodeller-2025.02.18 09.47.42.jpg|550]]

$R'_{inn} = R'^0_{inn} * \frac{1+T_{K}}{1+T_{Å}}$

$T_K$ er sløyfeforsterkning når terminalene er kortsluttet, $U_{mn}$ = 0
$T_Å$ er sløyfeforsterkning når terminalene er åpne, I = 0.
$R_inn$ er impedansen når forsterkningen til den avhengige kilden er 0.
$R_ut$ er utgangsimpedansen med en normal krets, foruten selve strøm-/spenningsinngangskilden (dog skal resistansen R_s være med).


## OPAMP eksempel
En realisering med OPAMP negativt tilbakekoblet. Samme verdier som asymptotisk forsterkningsformel, og kan derfor gjenbruke verdier som T.

Merk at, for en negativ tilbakekoblet OPAMP, er
- $\frac{u_{o}}{u_{s}}$ er nøyaktig (så lenge T >> 1), mens 
- R_inn øker når T øker.
- R_ut minker når T øker.
Dette understreker at en ideell opamp har uendelig inngangsresistans og ingen utgangsresistans.
![[5 Toterminalsmodeller-2025.02.18 10.24.52.jpg|650]]


$R'⁰_{inn}$
![[5 Toterminalsmodeller-2025.02.18 10.32.01.jpg]]

$T_Å$
![[5 Toterminalsmodeller-2025.02.18 10.33.00.jpg|550]]

$R'_{inn} = R'^0_{inn} * \frac{1+T_{K}}{1+T_{Å}}$
![[5 Toterminalsmodeller-2025.02.18 10.40.45.jpg|350]]


Utgangsresistansen
$R'_{ut} = R'^0_{ut} * \frac{1+T_{K}}{1+T_{Å}}$
![[5 Toterminalsmodeller-2025.02.18 10.45.25.jpg|650]]




# Eksempler
![[5 Toterminalsmodeller-2025.02.18 10.59.27.jpg|550]]