Sykt smart å ha det ja!  
Jeg har brukt en del tid på å finne ut av slike ting, men helt ærlig har jeg aldri funnet et godt svar.  

Før jeg babler om tankene jeg har gjort meg, så vil jeg påstå at du burde kjøpe UPS brukt. Det er veldig mange som ligger ute på Finn, og du kan få ett godt tilbud hvis du har på varsler og venter et par uker/måneder. Mange gis bort, og noen selges dyrt. Tilstandene varierer veldig, så nye batterier ofte verdt påkostningen. De fleste forbruker UPSer bruker 1-2 standard blybatterier du finner på Biltema eller Komplett, som dette [AGM-batteri 12 V | Clas Ohlson](https://www.clasohlson.com/no/p/36-5460). En UPS (med blybatterier) tåler ikke å stå uten vedlikeholdslading over lenger tid (6-24 måneder?), så får du tak i noe som har gjort det, eller er over 5 år gamle, burde du medberegne pris på nytt/nye batteri(er). Men før du skifter, test hvor lenge den tåler å gå.
  
Kapasitet:  
Kjøper man noe nytt så har produsenten gjerne (om så veldig vanskelig å finne) diverse grafer som forteller hvor lenge den kan gi en viss effekt (eller aller helst Volt-Ampere, selv om det ikke er stor forskjell). Si at NASen trekker 100-150 W eller VA så holder den kanskje 15 minutter eller en time, avhengig av hvor mye penger du ønsker å bruke.  
  
Kneejerck-reaksjonen tilsier jo at man burde kunne holde ut strømbrudd på en time, men da er spørsmålet: Trenger du egentlig å holde ut så lange strømbrudd?  
  
Jeg har skjønt at:  
1. Strømbrudd skjer veldig sjeldent, og er svært avhengig av nettet lokalt. Jeg har enda ikke opplevd ett her i Bergen, mens i Ramnes, der bedriften med Martin har serverne sine, har opplevd 2-3 ila. det siste året. Senest i går var strømmen borte i 45 minutt, men det tok UPSene seg av. I mange land sliter man med brownouts eller "skitten" strøm som ødelegger PCer, men det tror jeg er sjeldent her.  
2. Strømbrudd varer som oftest ikke lenge fordi strømnettet i Norge er bygd opp med stor redundans med "rundkoblinger"; nesten alle trafostasjoner har to strømlinjer til seg. Altså, faller det et tre over en luftlinje, så er sjansen stor for at man har en annen linje som kan ta over automatisk etter noen sekunder/minutter.  
3. Varer et strømbrudd lenger enn 10 minutter så kan det fort vare i flere timer. Derfor kan det være like greit å få utstyret til å skru seg av automatisk.  
  
Derfor har jeg konkludert med at jeg ikke gidder å bruke penger på stor kapasitet.  
  
  
Teknologi:  
Jeg leste ett eller annet sted at man burde ha noe "dobbelt linje"-ett eller annet, for det beskytter bedre fra støy utenfra. Det er altså forskjell på hvordan man gjør AC->DC/Batterier->AC. Dyrere modeller har sikkert bedre kvalitet på strømmen ut, men det igjen er sikkert ikke så viktig hvis man ikke har mye brownouts.  
Dog har jeg også lest om en type hvor UPSen faktisk hadde endt med å ødelegge alt ustyret hans, fordi den hadde sendt en stor voltagespike på utgangene. Det er jo et mareritt hvor kvalitet sikkert har mye å si.

Personlig har jeg hatt mest trøbbel med å få lest av UPSens verdier for å vite om strømmen har gått og hvor lenge som er igjen. Den eneste jeg har kjøpt ny (for mange år siden) var en BlueWalker PowerWalker VI 650 LCD (650VA 360W) fra Komplett. USB-driverne er utrolig dårlig, og det er mange som sliter med å få lest av status. Det er ganske kjedelig når man ønsker at NASen skal slå seg av når det kun gjenstår 15 minutter med kjøretid. En annen som vi har fått brukt, Eaton Ellipse MAX 850, har heller ingen enkel kobling.  For Ramnes har vi kjøpt flere av to varianter, Bluewalker PV UPS VI 2200 SHL og APC Smart-UPS RT 1000VA. Den første fungerte enkelt i Unraids innebygde UPS-greie med USB, mens den siste har kun kommunikasjon over serial, noe vi ikke har fått på plass ennå.
Derfor ville jeg forsøkt å finne informasjon om hvor bra produktet du sikter deg faktisk fungerer. Jeg tror APC er de som er best på dette.


Hvor viktig er det egentlig?
Det er ganske bra å ha UPS, men det er ikke livsviktig. En UPS hjelper på driftsikkerheten og for at maskinvaren skal vare lenger, men det er ingen god sikring mot tap av data alene. Det viktigste er å ha på plass 3-2-1-regelen for data-oppbevaring.
Så med mindre strømnettet er notorisk dårlig, ville jeg skrudd på varsel på Finn og ikke stresset med å få det på plass før nyttår. I hvert fall hvis du har mulighet til å kunne skru på maskina mens du er på juleferie via en bekjent eller teknologi, så skulle det skje et lite strømbrudd på julaften (den verste dagen for strømnettet i året) så får det opp og gå igjen. 
En siste ting: Maskinvaren i NASen min er ganske dårlig, så jeg har noen ganger måtte hard-restarte maskina, som kan medføre korrupsjon. Men enn så lenge har jeg ikke opplevd noe krise, så skulle det skje noe, så er det som oftest ikke verdens ende for hardware/daten.