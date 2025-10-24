```table-of-contents
```

IIR bedre på de fleste måter (som færre koeffisienter), men
- kan være ustabile
- har ulineær faseforskyvning

FIR-filtre kan designes med lineær faserespons.

FIR: Finite Impulse Response Filtertypen har ikke tilbakekobling og vil derfor ha en
utdøende respons på en impuls på inngangen. Fordelen FIR har over IIR er at det kan lages
med lineær fase. Ulempen er at det typisk blir mye større (mer komplekst) enn IIR.

Se [[Skole/OneNote Universitet/Universitet/ELE142 Felles/Oblig 5|Oblig 5]] for eksempler.

# Bakgrunn
Distortion/Påvirkning av faseulinearitet på rektangulær-respons (5.2) og impuls-respons (5.3)
![[5 - Design av FIR-filtre-2025.04.14 22.44.22.png|550]]

## En lineær faserespons skaper ikke distortion
It can be shown that only if a filter is such that the gradient of the plot of phase shift against frequency  is constant will there be no distortion  of the signal due  to the phase  response. This  is  because  the  effective  signal  delay  introduced  by  a  filter  is  given  by dr  where  ø is the phase  change.  It follows  that we  require  that  ø = kco, where k is a constant,  if the delay  is to be the same for all frequencies,  as then dø/dco = k. 


## FIR-filtre med lineær faserespons
Symmetri om den midterste koeffisienten.
![[5 - Design av FIR-filtre-2025.04.14 22.57.01.png|550]]

![[5 - Design av FIR-filtre-2025.04.14 22.55.24.png|200]]
![[5 - Design av FIR-filtre-2025.04.14 22.54.05.png|550]]

# Windowing / Fourier transform


1. Du får oppgitt antall koeffisienter N. $k = \frac{n-1}{2}$. k er faktor som skifter hele vinduet, og hva som speiles rundt
2. Sett opp formelen for C(n) vist nederst på bildet, sett inn verdier og forenkle. n = (n - k). 
3. Løs C(n) for halvparten av n-verdiene. n speiles rundt k, så feks. første og siste er like.
	1. Den midterste løses slik at brøken får null i nevner. Da må man utføre på annet vis. Se bilde fra presentasjon under, C(k).
		1. sin x / x -> 1, så derfor vil sin 3n / n -> 3. 
4. Unngå uønsket ripple i passbåndet? Kan bruke Hamming-vindu eller andre

![[5 - Design av FIR-filtre-2025.04.15 10.54.47.png|550]]
![[5 - Design av FIR-filtre-2025.05.20 09.01.06.png|550]]

![[5 - Design av FIR-filtre-2025.05.20 08.55.56.png|550]]



----

# Frequency Sampling method
![[5 - Design av FIR-filtre-2025.05.20 11.36.34.png|550]]

## Formler
![[5 - Design av FIR-filtre-2025.05.20 11.40.35.png|550]]
Alpha for partall er (N / 2) - 1 (ifølge Yngve). Partall skal også ha en mindre Z-koeeffisient.
![[5 - Design av FIR-filtre-2025.05.20 11.33.27.png|550]]

## Eksempler
![[5 - Design av FIR-filtre-2025.05.20 11.40.55.png|550]]
Oblig 5 oppg. 4
~~Yngve trolig gjort feil ved at det skal være to punkt med x\[3], og gå opp til z⁷????~~
![[5 - Design av FIR-filtre-2025.05.20 11.37.51.png|550]]