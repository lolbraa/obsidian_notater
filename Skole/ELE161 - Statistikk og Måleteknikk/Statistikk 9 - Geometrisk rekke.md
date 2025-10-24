# Binomisk Forsøksrekke og Fordeling
Enten-eller, samme sannsynlighet $p$, uavhengig
Gitt n forsøk, telle suksesser -> binomisk fordeling
- "Ventetid", antall forsøk før suksess -> geometrisk

# Geometrisk fordeling  ???
Intensitet $\lambda$ = antall hendelser/tidslengde


# Poisson-prosess
- Antall hendelser i disjunkte tidsintervall er uavhengige
- Hastart (?) intensitet i ulike tidsintervall
- Lite sannsynlig med to samtidige endinger

Gitt tidsintervall t, og Poisson-prosess, hvor mange hendelser ser vi?
Diskret fordeling, verdimengde 0,1,2,....


Ventetid: Hvor lang tid må vi vente før hendelsen skjer?


# Eksempel Tilleggsoppave oppgave 7

a) 
Telleintervallet X Poissons-fordeling
- Poisson-prosess med intensitet $\lambda = 1 / 250 timer$
- Tidsintervall $t = 1000$ timer
	- X forteller antallet omstart i løpet av 1000 timer


b) 
"Akkurat en omstart", X = 1

c) 
"Minst en omstart", $X \ge 1$


Ventetid "Tid mellom to hendelser", Poisson-prosessen ekspansjonstal fordelt

d)  
I tid mellom to omstarter, ekspantielt fordelt $\lambda = \frac{1}{200}$
Sammenhengende (uten omstart) i mer enn 200, 400, 600 timer

$P (T > 200) = 0.449$
$P (T > 400) = 0.202$
$P (T > 600) = 0.091$



f) Gitta t den elektroniske komponenten har fungert i sammenhengende i 20 timer, hva er sannsynlighet for at den vil fungere i ytterligere 400 timer?
$T > 200$

GENERELT:
Gitt at.. betyr betinget sannsynlighet vilkårsblandet sannsynlighet og resulterer i:
$P(A|B) = \frac{P(A \cap B)}{P(B)}$

I dette tilfellet:
$P(T>600 | T >200) =  \frac{P(T>600 \cap T >200)}{P(T >200)}$
![[Pasted Image 20251016121538_149 1.png]]
