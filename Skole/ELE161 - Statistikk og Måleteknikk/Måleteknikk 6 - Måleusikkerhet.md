
# Målinger
Vi skiller mellom direkte og indirekte målinger
- Direkte er faktiske målte datapunkter
	- feks. målinger gjort med målebånd, klokke, avlesning av gradestokk, osv.
- Indirekte er beregninger basert på målte datapunkter
	- feks. fart fra lengde og tid, resistans vha. målebro

Grunnsetninger i måling
1. Det finnes en sann verdi for målestørrelsen på det tidspunktet målingen utføres
2. Det er alltid tvil om nøyaktigheten til et måleresultat (pga målefeil: tilfeldige feil, systematiske feil og menneskelige feil)
	- Bedre presisjon - redusert tilfeldige feil
	- Bedre nøyaktighet - redusert systemfeil

# Sensitivitetsanalyse
## Sensitiviteteskoeffisient
$$
S = \frac{\text{Endring i utgangsdata}}{\text{Endring i inngangsdata}}
$$


![[Måleteknikk 6 - Måleusikkerhet-1758198669934.webp|500x351]]


Fordelingsfunksjonen er en normalfordeling som laget basert på målinger???
- Standardavviket forteller om bredden til fordelingsfunksjonen
# Standardavvik
Viser spredningen av verdier som kan være sanne.
1. Reppterte målinger fordeler seg rund den sanne verdien (så sant det ikke er systematisk feil tilstede).
2. Ved en enkelt måling viser denne fordelingen sannsynligheten for hvor den sanne verdien er.

## Standard usikkerhet u(x)
**Standard usikkerhet**: Usikkerhet utrykt som et standardavvik.
$$
u(x) = \sigma
$$

### Eksempel
Standard usikkerhet = 0.15. Normalfordeling med sentrum i 12.5. 
- Hvis vi måler 12.5 - det er 68% sannsynlighet for at den sanne verdien er mellom 12.35 og 12.65.
- Dvs. måleverdi +- standard usikkerhet
![[Måleteknikk 6 - Måleusikkerhet-1759404457479.webp|500x249]]



## Ekspandert Usikkerhet, U(x)
Usikkerhet med et høyere konfidensnivå
$$
U(x) = k * u(x)
$$
- k = dekningfaktor
- u(x) = standard usikkerhet

![[Måleteknikk 6 - Måleusikkerhet-1759404292750.webp|650x350]]


### Eksempel
Hva er standard usikkerhet når
- $U(x) = 20mA\text{ ved }99.00\% \text{ konf.nivå}$
	- $u(x) = \frac{20mA}{2.2573} = 7.77mA$
- $U(x) = 0.04s\text{ ved }90.00\% \text{ konf.nivå}$
	- $u(x) = 24.32ms$
- $U(x) = 1m \text{ med }99.73\% \text{ konf.nivå}$
	- $u(x) = 0.3\bar{3}m$


# Rektangulær fordelingsfunksjon



# Usikkerhet i utgangsdata
![[Måleteknikk 6 - Måleusikkerhet-1760006904297.webp|500x267]]![[Måleteknikk 6 - Måleusikkerhet-1760006914530.webp|500x352]]

![[Måleteknikk 6 - Måleusikkerhet-1760007102702.webp|500x654]]
![[Måleteknikk 6 - Måleusikkerhet-1760007458317.webp|500x251]]




# Hvordan skrive måleresultat inklusive måleusikkerhet
- Runde av til ett eller to gjeldende siffer
- Siste gjeldende siffer i måle**resultatet** skal være samme desimal som **siste gjeldende siffer i usikkerheten**
	- Ett siffer er ofte tilfellet i industrien, mens to bruker også ofte.
- $v = 6,4 m/s$ $U(v) = 0,060 m/s$ 
- blir til $v = 6,40 \pm 0,06 m/s$ eller $v = 6,400 \pm 0,060 m/s$
![[Måleteknikk 6 - Måleusikkerhet-1760014299712.webp|500x612]]




# Type A og B usikkerhet
## Tilfeldige feil 
– på grunn av støy, avlesningsfeil, etc

Standardavvik σ
Type A usikkerhet: etablert ved spredning i repeterte målinger

## Systematiske feil
-på grunn av skjevheter i instrument, feil i konstanter, etc
Gjennomsnittsverdien er ikke lik den sanne verdien på grunn av systematiske feil i målingen.

Hvis en kjenner slike systematiske effekter så korrigerer man for dem.
Hvis man ikke kjenner dem vil de representere en usikkerhet.
Type B usikkerhet: etablert på andre måter ut fra kjennskapen til målingen

## Total standard usikkerhet
Type A er $u(x_{A})$, type B er $u(x_{B})$
$$
u(x) = \sqrt{ u(x_{A})^2 + u(x_{B})^2 }
$$

## Eksempel 
![[Måleteknikk 6 - Måleusikkerhet-1760614327941.webp|500x207]]

# Usikkerhet i gjennomsnitt $u(\bar{x}_{})$
![[Måleteknikk 6 - Måleusikkerhet-1760614163821.webp|500x303]]
## Type A og B
$$
u(\bar{x}_{A}) = \frac{u({x}_{A})}{\sqrt{ n }}
$$
$$
u(\bar{x}_{B}) = u({x}_{B})
$$
blir sammenlagt til total satndard usikkerhet i gjennomsnitt av repeterte målinger
$$
u(\bar{x}) = \sqrt{ (\frac{u({x}_{A})}{\sqrt{ n }})^2 + u(x_{B})^2 }
$$

![[Måleteknikk 6 - Måleusikkerhet-1760614345871.webp|500x250]]

# Korrelerte usikkerheter