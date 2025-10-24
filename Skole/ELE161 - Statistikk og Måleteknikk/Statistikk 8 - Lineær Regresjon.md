# Par av observasjoner
$(x,y)$ - par av observasjon.
I noen tilfeller kan det være sammenheng mellom X og Y.

# Lineær regresjon
Generelt:
$$
Y = \beta_{1} X_{1} + \beta_{2} X_{2} + \dots + \beta_{n} X_{n} + \alpha + e
$$

I vår sammenheng:
$$
Y = \beta X + \alpha + e
$$
- $e$ er støy, tilfeldig variasjon, $e$~$N(0,0_{e})$ (normalfordelt)
- $\hat{\alpha}$ er Intercept estimat
- $\hat{\beta}$ er estimat x1

Gjerne gitt i en standardisert tabell. 
- Da får man også R-squared som også er viktig. Forteller om det er god eller dårlig; modellen sin forklaringskraft; hvor mye av variasjonen til Y rent forenklet av variasjonen til X. Hvis den er nærme 1 så vet du at Y er riktig for en X. 

Man må også forklare hva dette betyr

Som en funksjon, $y(x)$; gitt verdi X kan ha
$$
y(x) = E(Y|X=x) = E(\beta X+\alpha+e|X=x) = E(\beta x + \alpha + e) = \beta x + \alpha + E(e) = \beta x+\alpha
$$
- $E$ betyr forventet


Av og til vil vi kunne transformere til lineært $Y= C e^{hX} \to \ln() \to \ln(Y) = hC+hX$




# Eksempel
## 2023 kontinuasjon
![[Statistikk 8 - Lineær Regresjon-1760686474686.webp|500x450]]
Informasjon å hente ut
Y -> batterispenning, volt
X -> temperatur, grader Celcius
$$
x_{i} \in (25.42 C, 38.35C)
$$
$$
y(x) = E(Y|X=x) = \beta x + \alpha = -0.057x + 5.367
$$
![[Statistikk 8 - Lineær Regresjon-1760687501304.webp|500x55]]
![[Statistikk 8 - Lineær Regresjon-1760687490203.webp|500x259]]
Gyldighetsroma (?)
$$
\hat{\alpha} = 5.367
$$
$$
\hat{\beta} = -0.057
$$
$$
\hat{y}(x) =  \hat{\beta} x + \hat{\alpha} = -0.057x + 5.367
$$
### Konfidensinterval
![[Statistikk 8 - Lineær Regresjon-1760687444830.webp|500x346]]
Formelen er type: $\text{estimat} \pm \text{kvantil} * \text{estimat av standardavvik (SE)}$


### Hypotesetesting for $\beta$
fortsettelse av oppgaven over.

Les tekst, referanseverdi $\beta_{0}$ for $H_{0}$
Lest tekst, format på $H_{1}$, $\beta <, \neq \text{ eller } > \beta_{0}$
Tabell har p-verdi, men for hvilken test?

Hvis $H_{0}: \beta = \beta_{0} = 0$ da er det ingen lineær samenheng
$H_{1}: \beta\neq 0$

Testobservator
$$
T_{obs} = \frac{\text{estimert verdi av }\beta - \text{referanseverdi av }\beta}{\text{estimert standardavvik for } \beta \text{-utrekning}} = \frac{\hat{\beta} - \beta_{0}}{SE(\hat{\beta})} = \frac{-0.057041 -0}{0.0034127} = -16.714
$$
