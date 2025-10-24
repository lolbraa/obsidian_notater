# Shannons informasjonsteori
Shannon var den første i informasjonsteori.
**Trenger å kjenne frekvensen** til ordene.

Informasjonsmengde $I_{k}$
Informasjonsinnhold $I$ hvor melding $M = 2^N$
Den totale informasjonen


$$
\text{Midlere kodelengde: }l = \sum_{k=1}^n l_{k}*p(m_{k})
$$


## Den gjennomsnittlige informasjonen - entropi - H
- Fjernet all overflødig informasjon; den minste størrelsen du trenger for å uttrykke et budskap
- Entropi er et mål på det absolutt optimale, og kan brukes til å måle komprimeringsmetoder.
	- Det absolutt optimale når alle meldinger er like sannsynlige (s. 301 Thorvaldsen), $H_{maks} = \log_{2}(M)$
- Det er også den gjennomsnittlige informasjon per meldingsintervall L
$$
\text{Entropi: }H = \sum_{k=1}^M p_{k}*\log_{2}\left( \frac{1}{p_{k}} \right)
$$
hvor 
- $p_{k}$ er sannsynligheten for hvert ord i sekvensen
- M er antall binære ord

*Eksamensoppgaver:*
> *Når en skal komprimere en data-mengde med binære ord, hvordan benyttes beregnet entropi av datamengden? Hvilket av ordene ¨Informasjonsmengde¨ eller ¨Usikkerhet¨ ville du brukt om entropien i dette tilfellet? Hvorfor?*
> Entropien blir et mål for hvor mye datamengden kan komprimeres. Her passer det å benytte ordet "Informasjonsmengde" for entropien, siden den sier hvor mye informasjon som finnes i datamengden.
> ![[8 - Datakomprimering og Kryptering-2025.05.19 10.28.01.png|550]]


## Redundans - $\eta$
$$
\text{Redundans: } \eta = \frac{l - H}{H}
$$
## Maksimum overførbar trafikk - C
$$
\text{Maksimum overførbar trafikk: } C = B * \log_{2}({1 + \frac{S}{N}) bit/s}
$$
hvor 
- B er frekvensbåndbredde
- S er energien i et bit
- N er total hvit støy innenfor B
- S/N er signal-støy forholdet

*Eksamensoppgaver*
> ![[8 - Datakomprimering og Kryptering-2025.05.19 10.16.47.png|550]]



## Shannon-Fanon-kode
It assigns a code to each symbol based on their probabilities of occurrence. 
It is a variable-length encoding scheme, that is, the codes assigned to the symbols will be of varying lengths.
Algoritmen er lossless.


Kode-tabellen lages med instruksjoner til mottaker om stopp:
- 11 betyr at det kommer mer informasjon.
- 00, 01, 10 betyr at symbolet er avsluttet.


### Eksempel
![[8 - Datakomprimering-2025.02.27 09.49.33.jpg|550]]


## Generelle eksamensoppgaver
![[8 - Datakomprimering og Kryptering-2025.05.19 10.32.39.png|550]]
$$
\text{Informasjonsmengde: } I_{k} = \log_{2}\left( \frac{1}{p_{k}} \right) \text{Kun for meldinger med lik sannsynlighet}???
$$
![[8 - Datakomprimering og Kryptering-2025.05.19 10.33.58.png|550]]
![[8 - Datakomprimering og Kryptering-2025.05.19 10.34.37.png|550]]

![[8 - Datakomprimering og Kryptering-2025.05.19 11.06.20.png|550]]


---


# Lempel-Ziv, ZIP-kode
Trenger ikke kjenne frekvensen til ordene før de kan komprimeres.
Nærmer seg entropien asymptotisk.
Beholder all informasjon

![[8 - Datakomprimering-2025.03.06 08.47.53.jpg|550]]

![[8 - Datakomprimering og Kryptering-2025.05.19 11.06.38.png|550]]



---



# Morsekode
![[8 - Datakomprimering-2025.03.06 08.48.41.jpg|550]]
![[8 - Datakomprimering-2025.03.06 08.49.17.jpg|550]]
![[8 - Datakomprimering-2025.03.06 08.47.01.jpg|550]]



# Huffmann-kode
En perfekt komprimeringsalgoritme, litt lik ZIP-kode.


# RSA
Første asymmetriske nøkkel, en offentlig og en privat nøkkel.
Bruker store primtall (større enn $10^{100}$)

RSA kan kun kryptere data lik størrelsen på nøkkelen, gjerne 256 bytes.

![[8 - Datakomprimering-2025.03.06 09.13.00.jpg|550]]

# AES
Bruker gjerne RSA for å overførere AES-nøkkelen.
- RSA kan kun kryptere lik størrelsen på RSA-nøkkelen, mens AES har ingen grense



