![[7 - OFDM-2025.04.10 11.46.17.png|550]]

# BPSK: Binary Phase Shift Keying
[Phase-shift keying - Wikipedia](https://en.wikipedia.org/wiki/Phase-shift_keying#Binary_phase-shift_keying_(BPSK))
[BPSK – Binary Phase Shift Keying \| GeeksforGeeks](https://www.geeksforgeeks.org/bpsk-binary-phase-shift-keying/)




# Orthogonal frequency-division multiplexing
Overfører en bitstrøm i "pakker" av et komplekst tidssignal hvor bitstrømmen er multiplekset som frekvenser. Bruker en grunnfrekvens som er høy så 

Robust mot fading, altså at når signaler blir sendt i et rom, vil signalet komme frem mange ganger på ulike tidspunkt pga. det går forskjellig veier gjennom rommet. Da vil signal som er delayed ødelegge med det ferskeste signalet ved interpolasjon. 
OFDM takler fading bra, for selv om tidssignalet blir påvirket, og dermed blir noen frekvenser dempet og andre forsterket, men det kan man enkelt justere på mottakeren, for man vet hva man forventer.

## Tid vs Frekvens oppbygning
Eksempel på to signaler: 
Å representere et bit ved å raskt skru av-på-av raskt (nederst til venstre), vil resultere i et "stort" frekvensrespons (øverst til venstre), for transientene ved raske endringer er ekstreme.
Frekvensresponsen av et "langt" step-response (nederst høyre) vil faktisk være bedre i frekvensdomenet (øverst høyre).
![[7 - OFDM-2025.02.25 14.40.29.jpg|550]]

## Frekvenser i OFDM
I OFDM tar man å folder det lange bittet over en høy frekvens for å flytte signalet opp i spektrumet.
Venstre er i tidsdomenet og høyre er i frekvensdomenet.
![[7 - OFDM-2025.02.25 14.48.08.jpg|550]]

I OFDM bruker man flere frekvenser til å parallelt overføre informasjon om flere bits.
Man velger et utgangspunkt for frekvensene, $f_{0}$, og alle bærefrekvenser er multiple av det.
Dette gjør at toppen for hver bit er perfekt avstand ift. interferens ved å være der nabofrekvensene krysser 0-aksen.
![[7 - OFDM-2025.02.25 14.51.44.jpg|550]]

![[7 - OFDM-2025.02.25 14.59.15.jpg|550]]

# OFDM-systemet
![[7 - OFDM-2025.02.25 15.03.29.jpg|550]]

## Koding
![[7 - OFDM-2025.02.25 15.03.13.jpg|550]]

Bruker ofte Harlem(?)-kode som kan detektere og **rette** en bit feil per "område".

## Interleaving
![[7 - OFDM-2025.02.25 15.03.46.jpg|550]]

## N-QAM og Gray-mapping
![[7 - OFDM-2025.02.25 15.04.13.jpg|550]]

N-QAM handler om å dele et komplekst plan opp i N antall bits.

Grey-mapping handler om hvilke bits som går hvor i planet, for å maksimere sjansen for at den feildetekterende koden kan fikse problemer. Hver bit sin nabo har kun en bits som er flippet.

Ut av N-QAM kommer det komplekse tall med amplitude OG fase, i en array. Dette brukes som "faser".


## IFFT
![[7 - OFDM-2025.02.25 15.06.57.jpg|550]]

Arrayen med komplekse tall mates inn i en fourier transform som gjør alle de "komplekse bittene" eller "fasene" om til en array av samples i tidsdomenet


## Guard-time
![[7 - OFDM-2025.02.25 15.12.53.jpg|550]]
Mellom hver "pakke" med en utlesning av en array, trenger man et tidsrom for å IKKE forstyrre neste signal, med tanke fading/forsinkelser av tidligere signal som går kronglete veier.


## Pilotkoder
![[7 - OFDM-2025.02.25 15.13.45.jpg|550]]
Man sender jevnlige pilotkoder som er forhåndsdefinert hos både sender og mottaker for å kalibrere forskyvninger i amplitude og fase!

## Peak to average power ratio
![[7 - OFDM-2025.02.25 15.15.30.jpg|550]]

## Totalt system
![[7 - OFDM-2025.02.25 15.14.28.jpg|550]]


![[7 - OFDM-2025.02.25 15.14.45.jpg|350]]

# Eksempel
![[7 - OFDM-2025.02.25 15.15.50.jpg|550]]

![[7 - OFDM-2025.02.25 15.15.51.jpg|550]]

![[7 - OFDM-2025.02.25 15.15.51-1.jpg|550]]

![[7 - OFDM-2025.02.25 15.15.51-2.jpg|550]]

![[7 - OFDM-2025.02.25 15.15.51-3.jpg|550]]

![[7 - OFDM-2025.02.25 15.15.52.jpg|550]]


![[7 - OFDM 2025-02-25 14.31.19.excalidraw]]