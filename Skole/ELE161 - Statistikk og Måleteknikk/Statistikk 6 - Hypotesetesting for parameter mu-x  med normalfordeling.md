
Fokus er på hypotesetesting for parameteren $µx$ for ein normalfordelt tilfeldig variabel X. Tilsvarande som det er for konfidensintervall, så er det variasjonar avhengig av om vi har eit kjent eller ukjent standardavvik.
- Fokus på bruk av MATLAB-skript for dette
- Merk at det er same vokabular her som det vi møtte for hypotesetesting av binomisk fordelte tilfeldige variablar: Nullhypotese og alternativ hypotese, signifikansnivå, $p$-verdi, type I og type II feil, og styrke. For dette tilfellet vil vi også ha at det er formlar som vi kan bruke for å planlegge datainnsamling, relatert til kor mange uavhengige observasjonar som er nødvendig for å få akseptable nivå både på type I og type II feil.
- Vi vil også kommentere korleis vi via normaltilnærming kan utføre ein del hypotesetestar for andre situasjon også, men det vert etter planen først tatt i detalj neste veke.
- Det vi vil snakke om vil vere frå følgjande kapittel i læreboka: kap. 7.3, 7.4, 7.6
- For ordens skuld bør de kjenne til at enkelte har misbrukt $p$-verdiar...
	- [https://www.datacamp.com/tutorial/p-hacking](https://www.datacamp.com/tutorial/p-hacking)[](https://www.explainxkcd.com/wiki/index.php/1478:_P-Values)
	- [https://www.explainxkcd.com/wiki/index.php/1478:_P-Values](https://www.explainxkcd.com/wiki/index.php/1478:_P-Values)
- Og av og til kan andre strategiar også vere nyttige å ha høyrt om:  
    [John Rauser keynote: "Statistics Without the Agonizing Pain" -- Strata + Hadoop 2014](https://www.youtube.com/watch?v=5Dnw46eC-0o)



## Eksempel 7.8 s 265
Erfaring med at vekten på skolebarn er normalfordelt med $µ = 35 kg$. 
Observasjoner er $31, 29, 26, 33, 40, 28, 30, 25$
Konfidensintervallet er $\alpha = 0.01$.

Har µ blitt endret?
- > avta
- < minke
- $\ne$ endret

Setter opp hypotesetesting:
- $H_{0} : µ = 35$
- $H_{0} : µ \ne 35$

Konkludere:  
- $p-verdi < \alpha$, forkast $H_{0}$ på $\alpha$-nivå
- $p-verdi > \alpha$, IKKE grunnlagg til å forkaste $H_{0}$ på $\alpha$-nivå
- + legg til hort setning relatert til problmstillinga
- "Det vi har observert gir oss/gir oss ikke grunnlag til å forkaste"

Type 1 feil er mulig i alle tilfeller og kommer an på $\alpha$





# z- eller t-test: Kjent eller ukjent $\sigma_{X}$



# Mer generelt når ikke direkte normalfordelt
Sentralgrenseteoremet: Sum av mange nok identiske fordelte observasjoner er tilnærmet normalfordelt
Samle mange sett og observasjoner