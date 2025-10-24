```table-of-contents
```

Det er flere metoder for å gjøre et "analog" filter (det vil si en transferfunksjon i s-domenet) om til et digitalt filter i z-domenet. De har ulike styrker, ulemper og vanskelighetsgrader. Right tool for the job.
I de fleste metodene må du kompensere på ulike vis, feks. ved å justere gain ved en frekvens.

Se [[Skole/ELE217 - Digital Signal Prossesering/Oblig 4|Oblig 4]] for eksempler på alle ulike metoder, mange løst i Matlab.


OBS: For hvordan man endrer lavpass til høypass, se siste avsnitt.

IIR: Infinite Impulse Response Filtertypen har tilbakekobling og vil derfor kunne gi et signal
på utgangen for alltid selv om inngangssignalet bare er en impuls. Filter-typen kan lages
veldig kompakt, men med risiko for ustabilitet. Filter-typen har ulineær fase.


# Direkte design





# Bilinear transform
![[4 - Design av IIR-filtre-2025.02.11 12.37.27.jpg|550]]

T = 1 / f_s
1. Må undersøke om det må prewarpes!
	1. wc' må være mindre enn 1% forskjellig fra wc, se s. 82.
2. Prewarpe ved å endre wc i T(s) til wc'.
3. Utfør bilinear transform ved å bytte s til uttrykket med Z.

## Warping
![[4 - Design av IIR-filtre-2025.02.11 12.38.05.jpg]]

Man kan unngå prewarping ved å la samplingsfrekvensen være større enn ca 18.14.
![[4 - Design av IIR-filtre-2025.02.11 12.39.04.jpg|550]]![[4 - Design av IIR-filtre-2025.02.11 12.39.12.jpg|550]]

## Prewarping
Kompansere warpingen som skjer under sampling ved å "prewarpe", tommelfingelregel 1%.


![[4 - Design av IIR-filtre-2025.02.11 12.46.57.jpg|550]]
![[4 - Design av IIR-filtre-2025.02.11 12.47.10.jpg|550]]![[4 - Design av IIR-filtre-2025.02.11 12.47.17.jpg|550]]

## Eksempler
![[4 - Design av IIR-filtre-2025.02.11 12.48.02.jpg|550]]

![[4 - Design av IIR-filtre-2025.02.11 12.48.20.jpg|550]]


---

# Impulse-invariant method
1. Invers-laplacetransformer fra S- til tidsdomenet, og så laplacetransformer til z-domenet.
2. T = 1 / f_s
3. Undersøk om det må skaleres: Er det et lavpass, hva er gain i Z = 1?


![[4 - Design av IIR-filtre-2025.02.11 12.49.36.jpg]]
![[4 - Design av IIR-filtre-2025.02.11 12.49.44.jpg|550]]![[4 - Design av IIR-filtre-2025.02.11 12.50.00.jpg|550]]![[4 - Design av IIR-filtre-2025.02.11 12.50.06.jpg|450]]

![[4 - Design av IIR-filtre-2025.02.11 12.51.39.jpg|550]]


![[4 - Design av IIR-filtre-2025.02.11 12.51.50.jpg|550]]
![[4 - Design av IIR-filtre-2025.02.11 12.52.06.jpg|550]]![[4 - Design av IIR-filtre-2025.02.11 12.52.51.jpg|350]]



## Matlab
```matlab
%Butterworth
wc=70;
wcsq=70^2;
b=wc*2^0.5;
d=[1 b wcsq];
fs=100;
T=1/fs;

n=[wcsq];     %Lavpass
c2dm(n,d,T,'matched')
%[a,b]=c2dm(n,d,T,'matched')

n=[1 0 0];    %Høypass
c2dm(n,d,T,'matched')

n=[b 0];      %Båndpass
c2dm(n,d,T,'matched')

n=[1 0 wcsq];  %Båndstopp
c2dm(n,d,T,'matched')

```




![[4 - Design av IIR-filtre-2025.03.26 12.44.07.png|550]]


---

# Pole-Zero Map
S. 89-90 i boka
1. Bytte $z = e^{sT}$
	1. hvor s er frekvensen for knekkfrekvensen (hva s er i knekkfrekvensen, feks s = -10)
	2. hvor T = 1 / f_s
2. $T(z) = k * \frac{1}{(z - resultatet)}$, trenger å finne gainen k
	1. Løser k for en viss frekvens, feks DC-gainen ved lavpass
3. Legger til et nullpunk i Z = -1, altså (z +1)


# Fra lavpass til høypass
s. 94 i boka

## I s-domenet
![[4 - Design av IIR-filtre-2025.03.26 20.32.56.png|550]]

![[4 - Design av IIR-filtre-2025.03.26 20.34.15.png|550]]



## I z-domenet
![[4 - Design av IIR-filtre-2025.03.26 20.35.51.png|550]]
![[4 - Design av IIR-filtre-2025.03.26 20.36.18.png|550]]




