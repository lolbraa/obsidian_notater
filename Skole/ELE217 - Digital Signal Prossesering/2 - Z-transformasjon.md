```table-of-contents
```

# Definisjon av Z
![[2 - Z-transformasjon-2025.01.16 10.23.19.jpg|550]]

## Z-tabell
![[2 - Z-transformasjon-2025.01.24 10.07.32.jpg|550]]

## Unit Step
Long division/polynomdivisjon
![[2 - Z-transformasjon-2025.01.16 09.47.49.jpg|550]]

![[2 - Z-transformasjon-2025.01.16 10.18.49.jpg|550]]

![[2 - Z-transformasjon-2025.01.24 10.14.19.jpg|550]]

Hvordan gjøre det i matlab?

# Transferfunksjon i Z-domenet
![[2 - Z-transformasjon-2025.01.16 10.23.20.jpg|550]]
![[2 - Z-transformasjon-2025.01.16 10.24.38.jpg|550]]



## IIR og FIR
![[2 - Z-transformasjon - IRR og FIR.jpeg|500]]
![[2 - Z-transformasjon - reminder.jpeg|450]]


Regne på funksjoner i Z-domenet, husk:
- En transferfunksjon som har et ledd UTEN z, husk at det er z⁰. 
  Hvis $T(z) = 3 + z^{-1}$, blir $Y(z) = T(z) * X(z) = (3 * z^0 + z^{-1}) * X(z)$.
- I en transferfunksjon er Y-leddet nederst og X-leddet øverst.
- Skal man finne utgangene fra en transferfunksjon, burde man som regel ta en long division av transferfunksjonen hvis den er rasjonell.

## Løse utsignal basert på transferfunksjon
### Eksempel 2.7
![[2 - Z-transformasjon-2025.01.24 12.03.29.jpg|550]]![[2 - Z-transformasjon-2025.01.24 12.04.03.jpg|550]]![[2 - Z-transformasjon-2025.01.24 12.04.22.jpg|550]]
## Eksempler Transferfunksjon i Z-domenet
### Eksempel 1
![[2 - Z-transformasjon-2025.01.16 10.01.29.jpg|550]]![[2 - Z-transformasjon-2025.01.16 10.01.42.jpg|550]]


### Eksempel 2
![[2 - Z-transformasjon-2025.01.16 10.01.58.jpg|550]]![[2 - Z-transformasjon-2025.01.16 10.02.11.jpg|550]]


### Eksempel 3
![[2 - Z-transformasjon-2025.01.16 11.02.46.jpg|550]]![[ELE217 Drawing 2025-01-16 10.33.21.excalidraw]]![[2 - Z-transformasjon-2025.01.16 11.02.55.jpg]]


### Eksempel 4
![[2 - Z-transformasjon 2025-01-21 13.36.02.excalidraw]]


---

# Løse i Matlab
## Syntaks
```matlab
% Arrays/sekvenser
x = [2 2 1]

% Sette opp en transferfunksjon, rasjonal funksjon med Z
numz = [1 2 -1]
denz = [1 0 0]

% Putte på stimuli og visualisere
dstep(numz, denz)
axis([0 5 0 4]) % Overstyre lengdene på aksene

dlsim(numz, denz, x)


% Polynomdividere
partfrac()
```

## Eksempler Matlab
![[2 - Z-transformasjon-2025.01.16 10.02.36.jpg|550]]

![[2 - Z-transformasjon-2025.01.16 10.02.50.jpg|550]]

