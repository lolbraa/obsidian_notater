# Oppbygning 
![[3 - Transistor-2025.01.28 08.52.18.jpg|550]]



# Fundamental regning
![[3 - Transistor-2025.01.27 11.30.15.jpg]]

## KCL: Strøm inn = strøm ut
Ulike bøker setter ulike retninger på strømmene, men vi bruker
- PNP: $I_{C}$ og $I_{B}$ Inn, $I_{E}$ ut.

## Diode-knekkspenninger
For å lede må spenningsdifferansen over base-emitter være 0.6-0.7 V.

Opererer gjerne basis-emitter lederetning, basis-collector i sperreretning

Metning:
- 

### NPN
V_Emitter må være 0.7 V **lavere** enn V_Base.
V_Collector må være **minst** samme som V_Base


### PNP
V_Emitter må være 0.7 V **høyere** enn V_Base.
V_Collector må være **maks** samme som V_Base





Basis-Emitter tåler lite spenning/strøm i sperreretning. Tar du mer enn 5V kverker du mest sannsynlig transistoren.

## Områder
![[3 - Transistor-2025.01.28 08.51.30.jpg]]



### Aktivt
### Metning
Ønsker man å bruke transistor som bryter, ønsker man at den enten leder bra eller ikke.

## Forsterkningsfaktorer
beta: felles emitter strømforsterkningsfaktor
alpha: felles basis strømforsterkningsfaktor

Man anser en transistor som en forsterker siden den er en **spenningstyrt strømkilde** når man opererer i aktivt område. Såkalt transkonduktansforsterker (spenning->strøm)


## Early Voltage $U_A$

The **Early voltage** ($U_A$), also commonly denoted as $V_A$ is a key parameter in transistor physics that describes how the collector current ($I_C$ varies with the collector-emitter voltage ($V_{CE}$. It is named after **James M. Early**, who first described this effect.

### What is the Early Voltage?

In an ideal **current source**, the collector current $I_C$ in a transistor should be independent of $V_{CE}$. However, in real **bipolar junction transistors (BJTs)**, the output characteristics are **not perfectly horizontal**—instead, they have a slight positive slope. This effect is caused by the widening of the **base-collector depletion region**, which slightly reduces the base width and increases $I_C$ as $V_{CE}$ increases.

This effect is mathematically expressed as:

$$
I_C = I_S e^{V_{BE}/V_T} \left(1 + \frac{V_{CE}}{V_A} \right)
$$

where:  
- $I_S$ is the **saturation current**,  
- $V_{BE}$ is the **base-emitter voltage**,  
- $V_T$ is the **thermal voltage** (~25mV at room temperature),  
- $V_A$ is the **Early voltage**.

### Interpretation of $V_A$
- A **larger $V_A$** means **less variation** in $I_C$ with $V_{CE}$, making the transistor behave more like an **ideal current source**.
- A **smaller $V_A$** means a stronger dependency of $I_C$ on $V_{CE}$, leading to higher **output conductance** and lower **output resistance**.
- In the given problem, $U_A = \infty V$ suggests an **idealized assumption** where the transistor has **no Early effect**, meaning the collector current is assumed to be **completely independent** of $V_{CE}$.

### Effect on Amplifier Design
The Early voltage affects the **output resistance** of the transistor:

$$
r_o = \frac{V_A}{I_C}
$$

A higher $V_A$ leads to a higher $r_o$, which means:  
- **Better gain stability** in common-emitter amplifiers.  
- **Improved linearity** in amplifier circuits.  
- **Lower distortion** in high-precision analog circuits.

Since real transistors have **finite $V_A$** (typically **50V to 200V** for most BJTs), their output characteristics always show **some** dependence on $V_{CE}$.




# Biasing
Biasing gjør det mulig å få en nesten lineær krets av en transistor.


# Analyse
Har i all hovedsak tre modeller for å beskrive en transistor

| Modell         | Bruksområde                             | Fordeler                                                                                                                             | Ulemper                          |
| -------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------- |
| **Ebers-Moll** | Stor-signal analyse, DC-punkt           | Fullstendig transistorbeskrivelse. Basert på diodelikninger, hvor transistoren er to dioder. Fungerer for aktivt, metning og cutoff. | Ikke egnet for småsignal-analyse |
| **T-modellen** | Småsignal-analyse, lav/middels frekvens | Intuitiv, enkel                                                                                                                      | Mindre presis enn hybrid-π       |
| **Hybrid-π**   | Småsignal-analyse, høyfrekvent analyse  | Presis, inkluderer frekvenseffekter                                                                                                  | Litt mer kompleks                |