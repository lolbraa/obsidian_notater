> [!caution] This page contained a drawing which was not converted.   

Tallområde for n antall bit er 2 n

# Convert Decimal to Binary

## Repeated Division-by-2 Method

LSB: Least Significant Bit (Minst signifikant først)

1. Divider tall på 2 med heltalls divisjon.
2. Rest er del av binørt resultat, minst signifikant bit ut først
3. Repeter divisjon til svar er 0

## Reapeted Multiplication by 2

MSB: Most Significant Bit (mest signifikant først)

# Logiske porter + binære tall

## AND-port: multiplikasjon og carrybit i addisjon

|   |   |   |
|---|---|---|
|A|B|X|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|
 
Brukes i addisjon og multiplikasjon
 
## XOR (Exclusive OR-port): addisjon

|   |   |   |
|---|---|---|
|A|B|X|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

## Binær addisjon

Mente = carry

## Binær subtraksjon

Brukes ikke i praksis  
Krever realisering av både addisjon- og subtraksjonslogikk  
Erstattet av 2's komplement og addisjon

## Binær multiplikasjon

Multiplikasjon av 2 bit

## Negative tall - signed numbers - ikke i bruk

Historisk brukte man noen ganger en bit av en byte til å definere pluss (0) eller minus (1). Av en byte på 8 bits ble muligheten til å representere tall redusert fra 256 til 128.
 
## 1's komplement - ikke i bruk

Positive tall representeres som de er  
Negative tall representeres ved å invertere ale bit
 
|   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|
|+7|0|0|0|0|0|1|1|1|
|-7|1|1|1|1|1|0|0|0|
 
## 2's komplement

Positive tall representeres som de er  
Negative tall representeres ved å invertere ale bit og addere inn 1.  
Du kan også ta 2 n   − ( d e t ⁡ n e g a t i v e   t a l l e t ) .
 
|   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|
|+7|0|0|0|0|0|1|1|1|
|-7|1|1|1|1|1|0|0|0|
||||||||||
   

En byte på 8 bit kan representere 256 tall. Med 2's kompliment deles dette på positive, 0 og negative tall. Gir:

- Postitivt mellom 0 og 127
- Negative tall mellom -1 og -128

Er du utenfor dette området blir det overflow.  
MSB (7.bit) er alltid 1 hvis tallet er negativt.
 
Regler fra læreren:  
1) Positive tall representeres direkte ved sin binære verdi, mest signifikante bit er 0. OBS: tall må  
være innen tallområdet gitt av antall bit N.  
2) Negative tall representeres på 2’s komplements form, mest signifikante bit blir automatisk 1 ved  
konvertering. OBS: tall må være innen tallområdet gitt av antall bit N.  
3) Addisjon og subtraksjon utføres ved binær addisjon.  
4) Mente fra mest signifikante posisjon strykes/ignoreres.  
5) Addisjon av et positivt tall og et negativt tall går alltid bra. (forutsatt at de begge er innen  
tallområdet gitt av antall bit N) Det er ikke nødvendig å sjekke for «overflow»  
6) Ved addisjon av to positive tall eller to negative tall så kan «overflow opptre». Dette oppdages  
ved å sjekke fortegn til resultat ved å se på mest signifikante bit  
• resultatet av en addisjon av 2 positive tall blir et negativt tall => overflow  
• resultatet av en addisjon av to negative tall blir et positivt tall => overflow  
7) Når «overflow» opptrer så er resultatet ikke riktig. **«**Overflow» må ikke forveksles med at det  
genereres mente fra mest signifikante bit som alltid skal ignoreres
 
## Addisjon/subtraksjon med 2's komplement

9-6 = 9 + (-6). Gjør den ene til 2's komplement

![[Binary Numbers R2.xlsx]]