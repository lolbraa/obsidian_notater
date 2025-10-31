Ingen konkrete regnestykker eller formler (?), heller forklare og vise forståelse
# Måleteknikk
[[Måleteknikk 1 - Temperatur og resistans]]
1. Hvordan måler man temperatur elektrisk? Hvorfor gjør man det i stedet for fysisk avlesning av gradestokk?
2. Grunnleggende om PTC, NTC, osv. Karakteristikker, grafene, egenskapene 
3. Effekt som er innafor på en thermistor
4. Sett opp en målebro. Hva måler vi, hva kan vi få ut? Fortelle om en målebro
5. Når en skal måle resistans har en ulike arrangement med ledninger. Fortell om de ulike løsningen (2,3,4-ledere).
6. Signalgang i måleteknikk
	1. Hva skal man med flere ledninger for målearrangement?
7. Utregning av respons temperaturforandring i legeme
	1. IKKE fysikken bak
[[Måleteknikk 4 - Strømningsmåling]]
8. Beskrive standardbetingelser (og hvordan regne noe av det?)
9. Tegne enkel Venturi differensialtrykk-måler
[[Måleteknikk 5 - Nivåmåling]]
10. Hva kan være det første man måler med differensialtrykk ???
11. Kunne fortelle diverse om differensialtrykk, deriblant hvordan løse høyder osv.
[[Måleteknikk 6 - Måleusikkerhet]]
12. Hvordan skrive vi et måleresultat inklusiv måleusikkerhet. 
	- Runde av til ett eller to gjeldende siffer
	- Siste gjeldende siffer i måle**resultatet** skal være samme desimal som **siste gjeldende siffer i usikkerheten**
		- Ett siffer er ofte tilfellet i industrien, mens to bruker også ofte.
	- $v = 6,4 m/s$ $U(v) = 0,060 m/s$ 
	- blir til $v = 6,40 \pm 0,06 m/s$ eller $v = 6,400 \pm 0,060 m/s$
[[Måleteknikk 7 - Signalbehandling]]
13. Hva er et filter? Filter er en innretning som endrer på et signal ved å dempe eller fjerne enkelte av frekvensene som signalet består av
14. Hva er lavpass, høypass, båndpass, båndstopp
15. Hvor fort er dempingen i et filter, "hvor fort faller frekvensresponsen"

# Statistikk
Blir ikke spurt om å regne, men fortelle om hvilke verktøy/modeller som passer til å løse en gitt oppgave
1. Lineær regresjon kommer uansett
2. Binomisk fordeling, "Gitt n observasjonar av vår binomiske forsøksrekke med sannsyn p for "suksess", kva er sannsynet for å sjå x "suksessar"?"
3. Hypotesetesting, men ikke regning (?)
	1. Oppsett og ordlegging: Sansynnligheten for å observere noe som er minst like mye i favør (i retning) av $H_{1}$ gitt $H_{0}$ sant
4. Konfidensintervall
	1. Forskjell mellom Punktestimat og Intervallestimat
	2. Hva forteller et 95% konfidensintervall oss?
		1. Et intervall konstruert på denne måten vil i 95% av tilfellene inneholde den sanne parameterverdien $p$.
		2. Vi kan ikke vite om det konkrete 95% konfidensintervall vi har konstruert, faktisk inneholder $p$.
5. Kan komme spørsmål om Sentralgrenseteoremet.
6. Uansett hva slags hypotesetesting: Utregning gir p-verdi på feks 0.025 
	- **Hva forteller en p-verdi oss?**
	- Sannsynlighet for å se noe som er minst like ekstremt i retning $H_1$, gitt at $H_0$ er sant
	- Hypotesetestene
	- Konkludere basert på hypotesetester

Lineær regresjon (GARANTERT)
7. Vi vil få spørsmål om lineær regresjon med tabell av estimater (?), som på alle tidligere eksamener, og så måtte forklare hva det betyr
	1. Gitt to sett med verdier/tabeller, ville du valgt den med lav eller høy R-squared? Høy, det er best modell.
8. Får en oppgave med en del tekst og informasjon
	1. Hente ut informasjon
	2. Sjekke at det du ønsker å finne er innenfor $X_{min}$ og $X_{max}$. Innenfor (og litt utenfor) område fungerer modellen for interpolasjon, utenfor kan man ikke garantere noe
	3. Får (gjerne?) en standard tabell (lineær modell tilpasning ?) med all nødvendig informasjon
		1. Les ut $\hat{\alpha}$ og $\hat{\beta}$ - forventede/estimerte verdier - og putt i $\hat{y}(x) = \hat{\beta}x + \hat{\alpha}$
		2. R-squared forteller om hvor mye variasjon i x-retning forteller om y-retning. = 1 betyr støyfritt og bra. Ingeniørtommelfingerregel >0.65 er cutoff. Veldig avhengig av fagfelt.
		3. $\text{estimat} \pm \text{kvantil} * \text{estimat av standardavvik (SE)}$, feks:  $\hat{\beta} \pm \text{kvantil} * SE(\hat{\beta})$
		4. Basert på observasjonene kan man regne ut 95% konfidensintervall for $\beta$. Er det korrekt å konkludere at $\beta$ ligger i dette intervallet? **NEI**, hvis man beregner mange intervall, forteller konfidensintervallet at 95% av disse vil inneholde det sanne gjennomsnittet.

Poisson-prosess, vilkårbundet sannsyn
10. Ventetid "Tid mellom to hendelser", Poisson-prosessen ekspansjonstal fordelt
11. Det vil komme spørsmål av samme format som [[Statistikk 9 - Geometrisk rekke#Eksempel Tilleggsoppave oppgave 7]].

