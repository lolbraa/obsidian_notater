 
Matematisk notasjon er et språk snakket med symboler

# Utfallsrom S - alle hendelser
- Hendelser A og B i dette utfallsrommet
$P(A)=\text{sannsynlighet for at et enkelt utfall ligger i hendelsen A}$
- $P(\text{Terning viser 4})= \frac{\text{gunstige utfall}}{\text{mulige utfall}} = \frac{1}{6}$

# Mengdelære
- Union $\cup$
- Snitt $\cap$

# Komplement
- Dersom A er ei hending, og $\bar{A}$ er komplementet til A, så har vi $P(A) + P(\bar{A}) = 1$.
- Dette er det viktig å kjenne til ettersom vi kan ha at det er masse arbeid å  rekne ut $P(A)$ direkte, medan det er lett å rekne ut $P(\bar{A})$.

# Funksjon $X$ og svaret $x$
- Tilfeldige variabler  definert på utfallsrom $S$ - funksjoner som tar de ulike utfall i $S$ som argument, og returnerer ulike verdier av  som svar
- Stor $X$ er navnet på en funksjon. Liten $x$ er verdier som svar på $X$.


# Binomisk Forsøksrekke og Fordeling
Enten-eller, samme sannsynlighet $p$, uavhengig
- Myntkast, evt. terningkast
	- Enten/eller (kravet mitt, eller ikke suksess)
	- Samme sannsynlighet $P$ for "suksess"
	- Statistisk uavhengig
- Binomisk fordeling, "Gitt n observasjonar av vår binomiske forsøksrekke med sannsyn p for "suksess", kva er sannsynet for å sjå x "suksessar"?"
	- Terningkast, og vi er interessert i resultatet "6". Vi har kasta terningen 25 gongar, kor sannsynleg er det at vi har sett akkurat 4 tilfeller av "6". Dersom X tel talet terningar som viser "6", så kan vi formulere dette som $P(X = 4)$.
- Terningkast, og vi er interessert i resultatet "6". Vi har kasta terningen 25 gongar, kor sannsynleg er det at vi har sett minst 4 tilfeller av "6". Dersom X tel talet terningar som viser "6", så kan vi formulere dette som $P(X \leq 4)$.
- Tellevariabler
	- $X$ tallet .... som vi ser når ...

Tre krav:
1. Enten eller situasjoner
2. Det er samme sannsynligeht for suksess for hvert element
3. Hvert element er uavhengig av det foran og det neste


gitt n forsøk, telle suksesser -> binomisk fordeling
- "Ventetid", antall forsøk før suksess -> geometrisk

# Geometrisk fordeling 
Intensitet $\lambda$ = antall hendelser/tidslengde

# Hypotesetesting for sannsynligheten $p$ i binomisk fordeling
## Sette opp problemet
### 1. Les problemet for å formulere nullhypotesen   og alternativ hypotesen :
Nullhypotese, "referanse": $H_{0}$
Alternativhypotesen: $H_{1}$
- Tre alternativ:
	1. $H_{1}: p < p_{0}$ (ensidig, nedre hale)
	2. $H_{1}: p > p_{0}$ (ensidig, øvre hale)
	3. $H_{1}: p \ne p_{0}$ (tosidig)

### 2: Les problemet for å finne $n$, dvs. kor mange uavhengige observasjonar som har blitt samla inn.
- Her bør du reflektere over om det er greitt å hevde at dei observasjonane du har er uavhengige.
X binomisk
- n = tallet forsøkt
- p = sannsynlighet for suksess fra binomisk forsøksrekke

### 3. Les problemet for å finne $x$, dvs. kor mange av dei observasjonane som er "suksessar". 
- Hugs at "suksess" her viser til det vi tel, og at dette vil ikkje nødvendigvis alltid vil vere det du i vanleg daglegtale ville omtalt som positivt. Dersom $X$ vår tel talet studentar som står på eksamen er "suksess" = "stå på eksamen", men dersom vi i staden for lar $Y$ telje talet studentar som stryk på eksamen, så er "suksess" = "stryk på eksamen".

## Løse problemet
### Frå verdiane $n, x, p_{0}$ , og har vi no høve til å rekne ut kor sannsynleg det er å observere noko som er minst like mykje i favør av alternativhypotesen $H_{1}$, gitt at $H_{0}$ er sann.
- Når vi utførerer ein hypotesetest, uavhengig av kva for fordeling vi ser på, så vert dette sannsynet omtalt som $p$**-verdien**. 
- Dette kan fort bli kjelde til litt forvirring for mange studentar når det vi ser på er ei binomisk fordeling. Her har vi ein referanseparameter $p_{0}$ for sannsynet for "suksess". Vi vil undersøke om "ting har endra seg frå tidlegare" slik at vi no har fått eit sannsyn for suksess som har endra seg slik vi har spesifisert i $H_{1}$. I tillegg vil vi når vi kjem til estimering sjå at vi vil rekne ut eit punktestimat $\hat{p} = \frac{x}{n}$ av parameteren-$p$.
- Den $p$-verdien som vi reknar ut gjeld testen vår, og må ikkje blandast saman med det som vart nemnt ovanfor.

Det vi må ta stilling til er om det vi har observert er kompatibelt med "at ting er som før".
- Dersom $p$-verdien fortel oss at vi har sett noko som er "ganske uvanleg" gitt at er sann, så vil vi forkaste nullhypotesen $H_{0}$ til fordel for alternativhypotesen-$H_{1}$ .
- Dersom$p$-verdien fortel oss at vi har sett noko som er "ganske vanleg" gitt at er sann, så vil vi IKKJE forkaste nullhypotesen $H_{0}$ til fordel for alternativhypotesen-$H_{1}$ 
- For å kunne avgjere kva som er "ganske uvanleg" og "ganske vanleg", så opererer vi med omgrepet **signifikansnivå** $\alpha$. Ideen er at vi bestemmer oss for ein cut-off, t.d. $\alpha = 0.05$ (dvs. 5 %), og det som vi då treng ta stilling til er om den -verdien vi har rekna ut er over eller under $\alpha$.

I staden for å rekne ut ein-verdi kan vi alternativt operere med **forkastingsområder** (i øvre ende, nedre ende, eller begge endar, av fordelinga vår). Dette området skal ha eit areal som svarer til signifikansnivået $\alpha$, og ideen er at vi reknar ut ein testobservator (formel avhengig av fordelinga vi ser på), og så ser vi om denne verdien ligg i forkastingsområdet.
- I praksis svarer det å ligge i forkastingsområdet til å sjekke om testobservatoren ligg ovanfor eller nedanfor endepunkta i forkastingsområdet vi har rekna ut. Dersom du kjem over ein hypotesetest som viser til **kritisk verdiar**, så er det truleg desse endepunkta som det vert vist til.   
- Dersom vi skal gjennomføre ein test ofte, t.d. i samband med kvalitetskontroll, så kan det vere nyttig å kjenne dei kritiske verdiane. Då kan det vere nok å samanlikne det du har observert mot den kritiske verdien, utan å måtte gjennomføre nokon kompliserte utrekningar. 
- Med tilgang til dataverktøy, så er det ofte nokså enkelt å rekne ut p-verdiar, og denne gir oss eit litt betre grunnlag for å seie kor uvanleg det vi har observert faktisk er dersom nullhypotesen er sann.
- Dersom vi er interessert i å rekne på sannsynet for type II feil / styrken til testen, så må vi i den utrekninga som skal gjennomførast kjenne til forkastingsområdet for å kome i mål.


### Formulering av konklusjon
- **Formulering av konklusjonen på ein hypotesetest:**  
- Dersom du har rekna ut (eller fått oppgitt) ein p-verdi, så startar du med å samanlikne denne mot signifikansnivået $\alpha$.
	- $p-\text{verdi} < \alpha \to$ Vi har statistisk grunnlag til å forkaste $H_{0}$ til fordel for $H_{1}$ på signifikansnivå-$\alpha$.
	- $p-\text{verdi} > \alpha \to$ Vi har IKKJE statistisk grunnlag til å forkaste $H_{0}$ til fordel for $H_{1}$ på signifikansnivå-$\alpha$ .
- Du kan alternativt ha rekna ut (eller fått oppgitt) testobservator og kritisk region.
    - Dersom testobservatoren ligg innanfor den kritske regionen -> Vi har statistisk grunnlag til å forkaste $H_{0}$ til fordel for $H_{1}$ på signifikansnivå-$\alpha$.
- Dersom testobservatoren ligg utanfor den kritske regionen
	- Vi har IKKJE statistisk grunnlag til å fforkaste $H_{0}$ til fordel for $H_{1}$ på signifikansnivå-$\alpha$.
- **Legg til ein setning som viser tilbake til det problemet vi starta med.** Har vi eit problem som ser på feilproduserte varer frå ei produksjonlinje, så MÅ det her vere med noko som fortel den du skal kommunisere ditt resultat til om det du har funne ut tilseier om feilraten har blitt redusert...
- IKKJE KONKLUDER MED AT $H_{0}$ ER SANN ELLER $H_{1}$ ER SANN! Dei som hevdar noko slikt som konklusjon på ein hypotesetest fortener deng.


## Eksempel: Høy feilrate på produksjonslinje, hjalp vedlikehold?
### Oppsett
Feilrate 7% ---vedlikehold---> lavere feilrate?
	$P_{0}$                                                $P$

Nullhypotese, "referanse": $H_{0}: P = P_{0} = 0,07$
Alternativhypotesen: $H_{1}: p < p_{0}$ 
### Løs
Testet $n = 100$, fant $x = 2$ defekte

X teller tallet defekte av $n=100$ med $P = P_{0} = 0,07$

Observerte vi noe som er lite sannsynlig gitt $H_{0}$ er sant?
→ $p$-verdi for testobservasjoner
### Svarsetning
Sansynnligheten for å observere noe som er minst like mye i favør (i retning) av $H_{1}$ gitt $H_{0}$ sant         **Viktig for EKSAMEN**
$X \dots\dots 2$ 
    Hvilket tegn skal være her? 
	$=, <, >, \le, \geq$
    Tips: se på $H_{1}$

**I dette tilfellet, $X \leq 2$**
### Hva nå? 
$p-verdi = 0,020$ - Stor nok? Liten nok?
Sammenlikng med signifikantnivået $\alpha$.
- Typisk, for ingeniører, lik 0.05


## Generelt for hypotesetesting
### **Type I feil:** Alt er "som før", men vi ender likevel opp med observasjonar som får oss til å forkaste $H_{0}$ til fordel for $H_{1}$ på signifikansnivå-$\alpha$.
- Merk at sannsynet for å gjere denne feilen, gitt at $H_{0}$ er sann, er lik det signifikansnivået vi har valt å bruke.
### **Type II feil:** parameterverdien er ikkje lik den som er gitt i nullhypotesen $H_{0}$  , men dei observasjonane vi har er ikkje "ekstreme nok". Vi ender opp med å IKKJE forkaste $H_{0}$ til fordel for $H_{1}$ på signifikansnivå-$\alpha$.
- I motsetning til type I feil, så er sannsynet for type II feil avhenig av mange ting. Først og fremst er dette sannsynet avhengig av både referanseverdien $p_{0}$ og den faktiske parameterverdien $p_{ny}$; i tillegg vert dette sannsynet påverka av signifikansnivå $\alpha$ som vi skal bruke, og forma på alternativhypotesen $H_{1}$ verkar også inn. Og i tillegg har vi at talet observasjonar $n$ verkar inn på svaret.
- Dersom vi skal planlegge ei datainnsamling, bør vi før vi startar å gjort ei vurdering av kor mange uavhengige observasjonar $n$ vi bør ha for at vi skal få eit akseptabelt (dvs. lite nok) sannsyn for type II feil for ein gitt ny parameterverdi $p_{ny}$.
	- Dersom vi t.d. veit at ei produksjonslinje har eit sannsyn på 7 % for feilprodusert vare ($p_{0} = 0,07$), og vi etter vedlikehald/oppgradering skal teste om feilraten har blitt redusert. Vi veit ikkje om ting har blitt betre, men vi kan likevel bestemme oss for at vi for tilfellet ønskjer at sannynet for type II feil skal vere maksimalt 0.10. Frå dette kan vi då finne eit tal uahvengige observasjonar $n$ som sikrar oss at vi får den ønska situasjonen. 
	- Merk at vi for å gjere denne utrekninga må utføre ein analyse der vi treng dei kritiske verdiane (som for det binomiske tilfellet er avhengig av $p_{0}$, talet observasjonar , og vårt signifikansnivå $\alpha$ . Dersom vi vil jobbe direkte med den binomiske fordelinga, så er det for denne delen nødvendig med litt kode for å kome i mål. Alternativt kan ein analyse gjerast via normaltilnærming (via sentralgrenseteoremet, som vi møter seinare i pensum). 
	- Merk: Dette underpunktet som går på å finne talet uavhengige observasjonar vi treng i denne situasjonen er med til orientering. Eg vil ikkje ta inn spørsmål om det på eksamen.
	- MEN: Det som gjeld eit i utgangspunktet definert tal observasjonar (t.d.$n=100$) bør de kjenne til!
- Merk at sannsynet for type I feil og type II feil er relatert til testoppsettet vårt, og ikkje vert påverka av kva vi observerer når vi samlar inn data.
- **Styrken til ein hypotesetest:**
    - Styrken er ein funksjon, som er definert som $(1-P(\text{type II feil}))$, og dette omgrepet må de kjenne til.
    - Det er vanlegvis styrken til ein test (og ikkje sannsynet for type II feil) som vil bli oppgitt.


Kritisk region for testen vår - hva for observasjoner av X sine verdier tilsier forkast H0 til fordel for H1 på signifikantsnivå alpha?
X ~ bcn(n, p) og H1 p< 0,25
X > 7 observert, ikke forkast H0



# Estimat
## Punkt
Punktestimat $\hat{p}$ er en estimert verdi av $p$ (som er den sanne verdien) basert på dato.
$\hat{p} = \frac{x}{n}$

Punktestimat er bedre enn ingen ting - vær skeptisk til kvaliteten, vanskelig å vite grunnlag.
- Kan 

## Intervall
Intervallestimat er punktestimat +- konfidensintervall. 
- Det gir en større sjanse for at $p$-verdien er innenfor intervallet, men den kan fortsatt være utenfor intervallet og derfor kan man ikke stole på intervallet.

$x = [\hat{p}-noe, \hat{p}+noe]$
$100*(1-\alpha)$


```MATLAB
[p_hatt, p_konf_intervall] = binofit(4, 50, 0.05)
```

Flere punkter gir bedre konfidentsintervall

## Konklusjon
Hva forteller et 95% konfidensintervall oss?
	1. Et intervall konstruert på denne måten vil i 95% av tilfellene inneholde den sanne parameterverdien $p$.
	2. Vi kan ikke vite om det konkrete 95% konfidensintervall vi har konstruert, faktisk inneholder $p$.

Fallgruver å svare:
- FEIL: Punktestimatet $\hat{p}$ har en 95% sjanse å ligge inne i konfidensintervallet.
	- Intervallet er konstruert slik at $\hat{p}$ ligger inne i intervallet
- FEIL: Den sanne verdien $p$ har en 95% sjanse å ligge inne i konfidensintervallet.
	- Når vi har funnet et konkret intervall basert på observasjoner, så ligger enten $p$ i intervallet eller så ligger det ikke i intervallet.
	- Før man fikk konfidensintervallet kunne man si at det er 95% sannsynlighet for at $p$ vil ligge i konfidensintervallet.


# Normaltilnærming
Helt nødvendig å bruke imange tilfeller i gamle dager uten dataverktøy
- Er det greit å bruke binomisk fordeling (diskret, stolper). Lyver litt og lager en modell, men klarer ikke å regne på det. Lyver litt til, og ser på normaltilnærming i stedet (ikke diskret, bruker tabell for statistiske modeller).
- "$n \ge 30$"
- "$Var(X) > S$"
- Funksjonen Var(X) = $n*p(1-p)$