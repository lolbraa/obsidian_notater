Volume control laws: Hvordan volum skal oppføre seg

## Uike typer logaritmiske potmetere:
*Pot law identification letters*
*ALPS Code letter, Pot characteristics*
A    Logarithmic 
B    Linear 
C    Anti-logarithmic 
RD  Reverse-log 
# Loaded-linear pots
![[13 - Volumkontroll-2025.03.11 10.48.50.jpg|250]]![[13 - Volumkontroll-2025.03.11 10.48.38.jpg|250]]


# Passiv volumkontroll
Si at du har en signalkilde og et potensiometer, hvor potensiometeret er koblet til en forsterker og høyttaler. Hvis lydnivået ut ved full guffe 100dB SPL er:
- Vil halvparten av et lineært potensiometeret være 100dB - 6dB = 94dB SPL. Det er ikke ønskelig.
- Vi ønsker et potensiometer som oppfører seg på et vis logaritmisk
## Ulike konfigurasjoner av forsterkerkretser
Potmeter før en forsterker: 
- Ikke bra ift. støy

Potmeter mellom forsterker og buffer:
- Bra ift. støy
- Stor fare for klipping siden forsterkeren er på full guffe.

# Aktiv volumkontroll

Problemet med logaritmiske potmetere er at de ikke er lett å få lage like identiske potmetere; de varierer mer fra hverandre enn lineære. Det er et problem for stereo og liknende

![[13 - Volumkontroll-2025.03.11 10.50.34.jpg|550]]


## Baxandall active volume stage
- Ønsker tilnærmet logaritmisk karakteristikk selv om en bruker lineært potensiometer.
- Ønsker bedre SNR ved lavt volum enn det passiv kontroll gir.

![[13 - Volumkontroll-2025.03.11 10.55.23.jpg|550]]

Bufferet gjør at man ikke belaster potmeteret, selv om R3 belaster litt.

Kondensatorene gjør at man ikke kan få DC-strømmer i kretsen (gjennom potmeteret og ut til høyttaler). Små DC-strømmer fører til skrapelyder når man justerer på potmeteret.

Man kan bruke flere opamps for å minske støyen



### Gjennomgang på tavla
![[13 - Volumkontroll-2025.03.17 11.50.21.jpg|300]]

![[13 - Volumkontroll-2025.03.17 11.52.01.jpg|550]]
![[13 - Volumkontroll-2025.03.17 11.52.09.jpg|550]]

Ganske perfekt logaritmisk i midtre parti (dB)
![[13 - Volumkontroll-2025.03.17 12.30.30.jpg|550]]


## Støyanalyse: Passiv vs. Baxandall

Passiv krets
![[13 - Volumkontroll-2025.03.17 12.34.06.jpg|550]]

Baxandall krets
![[13 - Volumkontroll-2025.03.17 12.33.58.jpg|550]]


Tester ulike X-nivåer
VED X = 1
Passiv
![[13 - Volumkontroll-2025.03.17 12.33.45.jpg|550]]
Baxandall
![[13 - Volumkontroll-2025.03.17 12.36.21.jpg|550]]
På fullt volum er den passive bedre enn aktive!

Resultat
![[13 - Volumkontroll-2025.03.17 12.50.52.jpg|550]]

Begge får dårligere SNR ved lavere volum, men den passive blir betraktelig dårligere.



# Finne kondensator-verdier basert på nedre grensefrekvens
C1
![[13 - Volumkontroll-2025.05.05 11.52.37.png|550]]

C2 og siste stykket
![[13 - Volumkontroll-2025.05.05 11.53.32.png|550]]

Boka har valgt mye høyere kondensatorverdier for å ikke skape forvrengning.