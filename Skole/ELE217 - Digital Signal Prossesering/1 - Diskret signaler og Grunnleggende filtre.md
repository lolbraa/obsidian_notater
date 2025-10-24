# Sampling
## Nyquist
Nyquist sier at vi må sample med 2x frekvensen av det analoge signalet inn.


## Forsinkelse
![[1 - Diskret signaler-2025.01.16 09.21.42.jpg|500]]


---

# Filtre
## Running average/transversal filter og FIR
Running average filter: Gjennomsnittet av nåværende verdi + n antall tidligere DATA_INN-verdier.
![[1 - Diskret signaler og Grunnleggende filtre-2025.01.23 14.16.53.jpg|550]]
A running average filter tends to smooth out any rapid changes in a signal and so is a form of **lowpass filter.**

FIR står for Finite Impulse Response, for ved en impuls vil filteret slutte å ha en verdi etter en viss tid har gått.

FIR-filtre bruker gjerne mange registre for å ta gj.s. av mange verdier.

## Feedback/recursive filters (IIR)
IIR benytter nåværende + tidligere DATA_UT-verdier.
![[1 - Diskret signaler og Grunnleggende filtre-2025.01.23 14.18.01.jpg|550]]
Etter en impuls på inngangen, vil IIR ha en verdi for all fremtid. Derfor Infinite Impulse Response.

IIR-filtre sparer som regel mange registre ift. FIR, men grunnet tilbakekoblingen kan den være ustabil.


---

# Oppgaver
![[1 - Diskret signaler-2025.01.16 09.31.42.jpg]]



