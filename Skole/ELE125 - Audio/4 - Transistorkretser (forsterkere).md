# Oversikt forsterkere
Forskjellen mellom småsignal og storsignal, eller for og effektforsterker er gjerne
- 1 W transistorer
- Forforsterker forsterker spenning veldig, men gir ikke mye effekt/strøm.
	- Som regel 1-3 V ut
- Effektforsterker gir mye effekt.
	- Som regel 20-30 i gain
	- ca. 30 V RMS og 3.5 A RMS ut
	- Inngangsimpedans på 10 kOhm

Legge inn tekst fra notat 18
A/B 



# The three basic configurations
![[4 - Transistorkretser-2025.03.05 08.53.05.jpg|550]]

# Emitter Follower (EF), Common-Collector (CC)
The emitter follower (EF) is essentially a unity voltage gain amplifier that provides current gain. It is most often used as a buffer stage, permitting the high impedance output of a CE or LTP stage to drive a heavier load.

![[4 - Transistorkretser-2025.03.05 12.26.48.jpg]]


# Klasse A - Common-Emitter
![[4 - Transistorkretser-2025.03.05 12.21.43.jpg]]
![[4 - Transistorkretser-2025.03.05 12.22.35.jpg|550]]


![[4 - Transistorkretser-2025.01.26 21.37.32.jpg|550]]
- Inverterende
- Low distortion



## Problem
- Maks teoretisk effektivitet på 25%
	- Derfor oftest brukt for småsignal, som ikke krever mye effekt.
- Low distortion

## Tips:
Bruk $V_{CE} = \frac{1}{2} * V_{\mathbb{C}}$.
Kan bruke transformer på AC-ut for å få høyere effektoverføring, nærmere 50%

## Stabilisering av arbeidspunktet
Bruker thevenin-ekvivalent på base-resistansene.
[[Notat_05_Stabilisering_av_arbeidspunkt.pdf]]



# Felles Kollektor - Felles Emitter, FK-FE-trinn
## Notat
![[4 - Transistorkretser (forsterkere)-2025.03.11 09.51.10.jpg|450]]

Forenkles ned til regning som om det kun er en transistor!
# Kaskodekobling, FE-FB-trinn
## Notat
![[4 - Transistorkretser (forsterkere)-2025.03.11 09.51.41.jpg|450]]
Forenkles ned til regning som på en enkel transistor!

## Utledning tavla
![[4 - Transistorkretser (forsterkere)-2025.03.11 09.26.26.jpg|700]]
Forsterkningen likner veldig lik på et fellesemitter-trinn
$$
i_{c_{2}} = \alpha_{2}*i_{e_{2}}
$$
$$
R_{inn} = r_{\pi_{1}}
$$

# Darlingtonkobling
Q2 har lav kollektor strøm, derfor lav beta 
Q1 kan ikke skrus av raskt siden C_pi og R_pi har en utladning.
Kan koble motstand Q1_base/Q2_emitter mot Q1_emitter
- Større strøm i Q2 og utladningen av Q1 kan skje via resistoren
- Får kjøpt ferdige pakker med darlington-koblinger, men i audiosammenheng ønsker man full kontroll på dette

![[4 - Transistorkretser (forsterkere)-2025.04.08 09.32.04.png|300]]



# Klasse B 
![[4 - Transistorkretser-2025.01.26 21.44.01.jpg|550]]
- Bruker en NPN og en PNP-transistor
	- Signalet forsterkes gjennom en om gangen.
	- Må være biased til å skru av/på ved 0 V.
- Maksimal effektivitet er 78,5%

## Problem
"Crossover-distortion"
- Transistoren er blokkert frem til man når 0.7V på basen.
![[4 - Transistorkretser-2025.01.26 21.41.48.jpg]]



# Klasse AB
![[4 - Transistorkretser-2025.01.26 21.45.58.jpg|550]]
Putter inn to silikon-dioder istedet for R2 i klasse B.
Ettersom likestrømmen ikke kan gå gjennom kondensatorene til venstre, blir det et spenningsfall over diodene lik 1,2 - 1,4V. Det er mer enn det som trengs for diodene.


# Klasse C
![[4 - Transistorkretser-2025.01.26 21.52.31.jpg|550]]
- Effektivitet på 99%
- Annerledes fordi den er "tuned".
- Har en kondensator og spole i parallell.

## Problem
- Høy distortion
- Leder ikke for fulle 180 grader, bare positiv amplitude?
	- Ulike alternativer for å gjøre den bedre

## Alternativer



# Forsterkere med flere trinn
## Større forsterker
gode karakteristikker; jevn 40dB forsterkning opp til 50MHz (?)
![[4 - Transistorkretser-2025.02.28 10.46.57.jpg]]


## "Simple three-stage" power amplifier
![[4 - Transistorkretser-2025.03.05 11.39.51.jpg|550]]


I emitterfollower-trinnet (OPS) i push-pull (?) opererer Q6 og Q7 som AB-forsterkere, og det går ikke strøm kontinuerlig. Men Q4 og Q5 går det strøm i hele tiden
# Frekvensrespons