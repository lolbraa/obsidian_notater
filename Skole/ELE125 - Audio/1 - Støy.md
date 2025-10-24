# Notasjon
Støy er helt tilfeldig og uforutsigbart, men kan beskrives statistisk.

![[1 - Støy-2025.01.17 11.31.39.jpg|550]]![[1 - Støy-2025.01.17 11.32.26.jpg|550]]


# Støykilder
## Termisk støy

## Shot noise

## 1/f, flicker noise

## Popcorn noise



# Støy i krets eksempel
Bildene beskriver/beviser at støyforholdet SNR blir dårligere når man har en spenningsdeling. Derfor burde man ikke attenuere signalet, for å så forsterke det.
![[1 - Støy-2025.01.20 09.56.04-1.jpg|550]]
![[1 - Støy-2025.01.20 09.56.04.jpg|550]]
![[1 - Støy-2025.01.20 09.56.02.jpg|550]]





# Triks

Opamps med FET inngangstrinn har mye mindre støytetthet enn BJT inngangstrinn.

## Ikke-inverterende forsterkning
Hvis vi gjør forsterkningen i første trinn veldig stor, blir støyen i andre trinn ubetydelig

Si at man skal forsterke signalet med 100, men pga. båndbreddehensyn til OPAMPene kan man ikke forsterke mer enn 50 på en opamp.
Da er det lurt å kjøre opp forsterkningen i 1. trinn så mye man kan!
Det er altså alltid lurt å sørge for at støyen bestemmer i 1. trinn, om det så er dioder, transistorer eller forsterkere

![[1 - Støy-2025.01.21 09.23.07.jpg|550]]![[1 - Støy-2025.01.21 09.23.18.jpg|550]]


## Kondensator for å minske støy
Denne kretsen er i utgangspunktet svært dårlig for støy
- Men putter man en kondensator på pluss-terminal. Kortslutter ved høyere frekvenser, og dess større kondensator, hvor mindre støy.


Trenger en motstand for å kansellere en bias-strøm? Putt en kondensator over, for det gir et behagelig resultat hvor størrelsen av kondensatoren gjør støyen mindre.
![[1 - Støy-2025.01.21 09.22.32.jpg]]


# Modeller
## Generell
![[1 - Støy-2025.01.21 10.19.10.jpg|550]]

## Transistor
Transistor
Felteffekttransistor: 
- Pøs på med strøm.
- gm er veldig lav.
- Strømstøyen i en felteffekttransistor er mye lavere.

Putte kondensator over Re (emitter) for å minske støy ut fra transistor.


![[1 - Støy-2025.01.21 10.19.37.jpg|550]]![[1 - Støy-2025.01.21 10.19.43.jpg|550]]

Ic optimal: Grafen har et "bredt" bunnpunkt, så havner man ikke på det absolutte minimumspunktet, så går det bra.


Minimal ekvivalent inngangstøytetthet er:
![[1 - Støy-2025.01.21 10.19.54.jpg|550]]
Lurt med transistor med høy verdi på beta.


rx er "aldri" oppgitt fordi den er så høy. Vanligvis mellom 100 og 200 ohm.


