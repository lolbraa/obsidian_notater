```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

# Oversikt
FEC (Forward Error Correction) - kode er en kode som endrer/koder informasjons-ordet som skal sendes til et større ord (kodeordet). 
Dette gjør at flere bit må sendes, men at en klarer å detektere og rette feil som har oppstått under overføringen til mottaker etter at ordet er mottatt.
![[9 - Error Correction-2025.03.25 12.22.58.png|550]]



## Blokk-koder
- Har ikke minne
![[9 - Error Correction-2025.03.25 12.21.25.png|550]]

### Sykliske koder
Sykliske permutasjoner på av hverandre, på rekke. 
- Leser og løser kontinuerlig, gjerne i et skiftregister - derfor lett å realisere i HW.
- 

## Konvolusjonskoder
- Har minne



---

# Paritetsbit
Kan detektere en feil, men ikke korrigere.

![[9 - Error Correction-2025.03.13 08.52.41.jpg]]





# Hammingkode
## Spec
av 256 bit er 9 bit redundansbit, kan detektere to feil

Bruker XOR som en kalkulasjon lik modulo. Blir paritetsbit, men flere bits samme.
- Kan detektere 2 feil
- Kan korrigere 1 feil
- Bruker PARTALLSPARITET (hvor paritetsbittet OGSÅ teller)

Ser på fire databits av gangen, og så tre paritetsbit
- derfor fra 4 til 7 dimensjoner
- Posisjonen av paritetsbittene er i "powers of two".


![[8 - Datakomprimering-2025.03.13 08.37.47.jpg|550]]

Et resultat
![[8 - Datakomprimering-2025.03.13 08.41.31.jpg|550]]

Hvordan man kan beregne med matrisemultiplikasjon. Radene er a, b, c og d. De fire første kolonnene er databits, de tre siste er uttrykk for x, y og z.
![[8 - Datakomprimering-2025.03.13 08.40.12.jpg|550]]


## Eksempel 2:
$$
[1101] \to [1101\_100]
$$

## 4x4-representasjon
Man setter opp matrisen med databits i sorte ruter og paritetsbit i grønne. Den gule er total?
(15,11) - 15 bit block, 11 bit of message, 4 bits of redundancy. 

Extended Hamming-code
- Bit 0 kan brukes som en paritet for HELE blokken.
- Kan detektere flere feil


![[9 - Error Correction-2025.03.13 09.35.17.jpg|550]]


Kan regne på Hammingkode med posisjonsadresser. 
1. Putter alle adresser som er på/"1" over hverandre.
2. XORer alle kolonnene. Dette er en partalls paritetoperasjon.
3. Er det riktig så skal det komme ut \[0000\], er det en feil så blir resultatet posisjonen som er feil!

Her er posisjon 0110 feil
![[9 - Error Correction-2025.03.13 09.39.07.jpg|550]]


![[9 - Error Correction-2025.03.13 09.43.08.jpg|550]]


![[9 - Error Correction-2025.05.19 10.05.40.png|550]]

## Utvide Hammingkode
Paritetsbittene har
- en posisjon lik "the power of two": 2, 4, 8, 16, 32, 64, osv.
- altså er posisjonen beskrevet binært med kun en ener: 0001, 0010, 0100, 1000
Dette skalerer opp
![[9 - Error Correction-2025.05.19 08.47.16.png|250]]
![[9 - Error Correction-2025.05.19 11.13.40.png|550]]


## Syndrom
ERROR = Kode * Syndrom
![[9 - Error Correction-2025.05.19 11.10.08.png|550]]
p kan forkortes grovt:
$$
p = a \oplus b \oplus c
$$

## Hammingavstand og antall feil koden kan rette
Hammingavstand er et avstandsmål mellom to binære tall. 
- Måles som antall bit i samme posisjon som er forskjellig. Eks 11010 og 10101 har hammingavstand 4. 

Dersom to kodeord har avstanden $d=2t+1$, så kan den detektere opp til $2t$ feil og korrigere opp til t feil.
![[9 - Error Correction-2025.05.19 11.12.03.png|550]]


![[9 - Error Correction-2025.05.19 11.13.09.png|550]]


---


# Sykliske koder
![[9 - Error Correction-2025.03.25 12.25.56.png|550]]

![[9 - Error Correction-2025.03.25 12.26.34.png|550]]


## BCH
Bose, Chaudhuri og Hocquenghem
- Linære sysklisk kode
- Velger generatorpolynom ut fra t (antall feil som skal rettes)

Antall kodebit: $n = 2^m - 1, m \geq 3$
Antall databit: $k \geq n - m*t$
Graden til generatorpolynomet: $r = n - k$
Min distanse: $d_{min} \geq 2*t + 1$

![[9 - Error Correction-2025.05.19 11.54.00.png|550]]
![[9 - Error Correction-2025.05.19 11.54.27.png|550]]
![[9 - Error Correction-2025.05.19 11.55.37.png|550]]
![[9 - Error Correction-2025.05.19 11.55.50.png|550]]
![[9 - Error Correction-2025.05.19 11.57.02.png|550]]
![[9 - Error Correction-2025.05.19 11.57.24.png|550]]



![[9 - Error Correction-2025.05.19 11.07.10.png|550]]


## Reed-Solomon
Non-binary: Opererer ikke på en bits av gangen, men flere samtidig.
- Spesiell effektiv for "burst errors".
- Basert på polynomer og modulær aritmetikk

> Here we will discuss how it is better than binary BCH codes.
> - It has the highest **efficient use of redundancy**.
> - It is possible to **adjust block length and symbol size** in Reed-Solomon codes.
> - It provides a **wide range of code rates**.
> - In Reed-Solomon codes, there are **efficient decoding techniques** available.
> Despite all these advantages of Reed-Solomon codes it also has some disadvantages in comparison with the BCH code.
> - For BPSK modulation schemes Reed-Solomon codes don't perform well in comparison with BCH code
> - In Reed-Solomon codes, the Bit Error Ratio(BER) is not satisfying in comparison with the BCH codes.

### Parametre
- Ofte beskrevet som $RS(n, k)$ hvor 
	- n er totalt antall symboler i meldingen (blokklengden = $2m - 1$ ?)
	- k er antall faktiske data-/informasjonsymboler i meldingen.
	- paritetssymboler er 2t

Thorvaldsen: En (n, k) RS-kode har følgende parametre:
- Symbol lengde: `m` bits per symbol
- Blokk lengde: `n = 2^m - 1` symboler = `m(2^m - 1)` bits
- Data lengde: `k` symboler
- Sjekk kode: `n - k = 2t` symboler = `m(2t)` bits
- Minimum distanse: `d_min = 2t + 1` symboler
- Eksempel `t = 1` og `m = 2`:
	  - `n = 2^2 - 1` symboler = 3 symboler = 6 bit
	  - `n - k = 2 * t` symboler = 2 * 1 symboler = 2 bit
	  - Koden kan rette 1 feil

Howtogeek:
![[9 - Error Correction-2025.05.19 09.15.46.png|350]]
- (n, k) code is used to encode m-bit symbols.
- Block length(n) is given by 2m-1 symbols.
- In Reed-Solomon codes, message size is given by (n-2t) where t= number of errors corrected.
- Parity check size is given by = (n-k) or 2t symbols.
- Minimum distance(a) is given by = (2t+1).
- Message size is of k bits.

Yngve
![[9 - Error Correction-2025.05.19 12.05.46.png|550]]

### Enkode

Man benytter tre polynom for å lage kodepolynomet C(x)
- Meldingspolynomet m(x)
- Generatorpolynomet g(x)
- Ekstra "paritet"? p()
-  => Usystematisk kodepolynom $C(x) = m(x) * g(x)$
- "Prewarpet" meldingspolynom? Q(x) som gjør det systematisk
- => Systematisk kodepolynom $C(x) = Q(x) * g(x)$

g(x) er oppgitt

Q(x) skal bli 0?

#### Finite Field
Setter en begrensning ift. "Finite Field", som oftest 7.
- Får man ett tall som er utenfor 0-6 så må man legge til/ta fra 7
- ~~Du må tilpasse C(x) så det er innenfor 0-6, altså subtrahere med 7~~ 

![[9 - Error Correction-2025.05.19 12.14.16.png|550]]
$$
C(x) = m(x) * g(x)
$$
![[9 - Error Correction-2025.05.19 12.15.44.png|550]]
![[9 - Error Correction-2025.05.20 10.11.10.png|550]]



### Dekode
Se PP og oppgaver uke 13, 27.mars



### What is Reed–Solomon Code?[ GeeksforGeeks](https://www.geeksforgeeks.org/what-is-reed-solomon-code/)
#### Generator funksjonen
In Reed-Solomon codes, the generator function is generated using a special polynomial. In Reed-Solomon codes, all valid codewords are exactly divisible by the generator polynomial. The generator function is given by:
$$
g(x) = (x-α)(x-α^2)(x-α^3)......(x-α^{2t})
$$
#### Encoding
We perform encoding in Reed-Solomon codes with the following methods:
- Consider a Reed-Solomon code with parameters n(block size), k(message size), q(symbol size in bits). 
	- For encoding, we encode the message as a polynomial p(x) and then multiply it with a code generator polynomial g(x), where
$$ g(x) = (x-α)(x-α2)(x-α3)......(x-α2t)
$$
- Then we map the message vector \[x1,x2,.....,xk\] to a polynomial p(x) of degree \< k such that $px(αi) = xi$ for all i=1,2,3,....k
- Polynomial can be done using Lagrange interpolation.
- Sender calculates $s(x) = p(x)*g(x)$ and then sends over the coefficients of s(x)

#### Decoding
At the receiver end we perform the following methods:
- The receiver receives r(x) at the receiver end.
- If s(x)== r(x) then r(x)/g(x) has no remainder.
- If it has remainder, then r(x) = p(x) * g(x) + e(x) where e(x) is an error polynomial.

[Reed-Solomon Error Correcting Codes from the Bottom Up \| Electronics etc…](https://tomverbeure.github.io/2022/08/07/Reed-Solomon.html)

# Konvolusjonskoder


## Enkoding
Tabell til venstre er status-flagg for ulike situasjoner i Un-1 og Un-2.
I høyre tabell:
- Un (inn) shiftes inn i de tre venstre kolonnene
- Ut1 og Ut2 er utgangssignalet
- Nå og Neste er status progresjon
![[9 - Error Correction-2025.04.03 12.35.44.png|550]]

Kan settes opp som en tilstandsmaskin
![[9 - Error Correction-2025.04.03 12.36.24.png|550]]

Resultat
![[9 - Error Correction-2025.04.03 12.40.35.png]]

## Dekoding med feil
![[9 - Error Correction-2025.04.03 12.42.10.png]]

Starter i status a
![[9 - Error Correction-2025.04.03 12.42.33.png|550]]

Går kolonne for kolonne og sammenlikner tall. 
- Distanse er "hvor mye må jeg endre for å komme til det jeg ønsker".

Til slutt ser man bakover.
Rød linje er den korteste og dermed den mest sannsynlig riktige.
![[9 - Error Correction-2025.04.03 12.51.59.png|550]]



# Oppsummering
## Reed-Solomon Code Summary and Example

---

### 1. **Brief Description of Reed-Solomon and the Parameters Used**

Reed-Solomon (RS) codes are **block error-correcting codes** used to detect and correct multiple symbol errors in digital communication or storage systems. They work over **finite fields (Galois Fields)**.

#### Parameters:
- **n**: Length of the codeword (number of symbols after encoding)
- **k**: Number of message symbols (input)
- **t**: Number of correctable symbol errors, where  
  $$
  t = \frac{n - k}{2}
  $$
- Operate in a **Galois Field GF(q)** where \( q \) is usually a prime power.
- Use a **generator polynomial** \( g(x) \) constructed from roots of the form \( (\alpha^i - x) \), where \( \alpha \) is a primitive element in the field.

---

### 2. **Systematic vs. Unsystematic Encoding**

- **Systematic Encoding**:
  - The message is part of the final codeword.
  - Format:
    $$
    C(x) = m(x) \cdot x^{n-k} + \text{remainder of } m(x)x^{n-k} \mod g(x)
    $$

- **Unsystematic Encoding**:
  - The message is transformed and embedded into the code.
  - Format:
    $$
    C(x) = m(x) \cdot g(x)
    $$

---

### 3. **Step-by-Step Encoding Instructions**

#### Given:
- Message: \( m(x) = m_0 + m_1x + m_2x^2 \)
- Field: \( GF(7) \), primitive element \( \alpha = 3 \)
- Message length \( k = 3 \), \( t = 2 \) ⇒ \( n = 7 \)

#### Steps:
1. Multiply message polynomial by \( x^{n-k} \) ⇒ \( m(x) \cdot x^4 \)
2. Construct generator polynomial:
   $$
   g(x) = (x - \alpha^3)(x - \alpha^4)(x - \alpha^5)(x - \alpha^6)
   $$
3. Divide \( m(x)x^4 \) by \( g(x) \), get remainder \( p(x) \)
4. Final codeword:
   $$
   C(x) = m(x)x^4 + p(x)
   $$

---

### 4. **Decoding Instructions**

Given received word \( C'(x) = C(x) + E(x) \):

#### Steps:
1. **Syndrome Computation**:
   $$
   S_i = C'(\alpha^i), \quad \text{for } i = 3, 4, 5, 6
   $$
2. **Set up linear equations** from syndromes to solve for error locations and magnitudes.

3. **Solve for error polynomial** \( E(x) \):
   $$
   E(x) = e_1x^{i_1} + e_2x^{i_2}
   $$

4. **Subtract errors** from received word:
   $$
   C(x) = C'(x) - E(x)
   $$

5. **Extract message** from corrected codeword (first \( k \) symbols if systematic).

---

## Reed-Solomon Encoding/Decoding Example

---

### ✅ SETUP

- **GF(7)**, primitive element \( \alpha = 3 \)
- \( k = 3 \), \( t = 2 \) ⇒ \( n = 7 \)
- Message:
  $$
  m(x) = 2x^2 + 6x + 5 \Rightarrow [2, 6, 5]
  $$

---

### 🧮 ENCODING (Systematic)

1. **Multiply by \( x^4 \)**:
   $$
   m(x) \cdot x^4 = 2x^6 + 6x^5 + 5x^4
   $$

2. **Generator Polynomial**:
   $$
   g(x) = (x - 6)(x - 4)(x - 5)(x - 1) = x^4 + 5x^3 + 2x^2 + x + 5
   $$

3. **Divide**:
   $$
   \text{Divide } 2x^6 + 6x^5 + 5x^4 \text{ by } g(x)
   \Rightarrow \text{remainder } p(x) = x^3 + 6x^2 + 5x + 2
   $$

4. **Codeword**:
   $$
   C(x) = 2x^6 + 6x^5 + 5x^4 + x^3 + 6x^2 + 5x + 2
   \Rightarrow C = [2, 5, 6, 1, 5, 6, 2]
   $$

---

### ⚠️ Introduce Errors

- Original: [2, 5, 6, 1, 5, 6, 2]
- Corrupt positions 1 and 4:
  $$
  C' = [2, \underline{3}, 6, 1, \underline{6}, 6, 2]
  $$

---

### 🔍 DECODING

1. **Compute Syndromes**:  
   Evaluate \( C'(x) \) at \( \alpha^3, \alpha^4, \alpha^5, \alpha^6 \).  
   (For example, \( C'(6) \equiv 6 \mod 7 \), etc.)

   Result (simplified):
   $$
   S = [6, 2, 4, 1]
   $$

2. **Solve System**:
   Set up and solve for error positions and values using linear algebra in \( GF(7) \).  
   (Results from doc: Errors at positions 1 and 4 with values \( e_1 = 2 \), \( e_2 = 1 \))

3. **Correct Errors**:
   - Position 1: 3 → 3 + 2 = 5
   - Position 4: 6 → 6 + 1 = 5  
   Corrected: \([2, 5, 6, 1, 5, 6, 2]\)

4. **Extract Message**:
   $$
   \boxed{[2, 6, 5]}
   $$

---

### ✅ Final Summary

| Step         | Result                      |
|--------------|-----------------------------|
| Original     | [2, 6, 5]                   |
| Encoded      | [2, 5, 6, 1, 5, 6, 2]       |
| With Errors  | [2, 3, 6, 1, 6, 6, 2]       |
| Decoded      | [2, 6, 5]                   |
