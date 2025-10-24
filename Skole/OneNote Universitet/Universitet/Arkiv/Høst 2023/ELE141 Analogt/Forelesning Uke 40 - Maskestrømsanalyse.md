> [!caution] This page contained a drawing which was not converted.   

# Knutepunktsanalyse

Setter opp likninger som automatisk følger KVL.  
Så setter man opp for KCL og løser for informasjonen for hvert kretselement.
 
# Maskestrømanalyse

Setter opp likninger som automatisk følger KCL.  
Så setter man opp KVL og løser for informasjonen for hvert kretselement.
 
Fungerer kun for "plan"-kretser - kretser uten ledninger som krysser hverandre.
 
## Tre

På en graf av en krets har man n noder.  
Man skriver på strømmer med retning. Eventuelle påskrevne spenninger må følge passiv fortegnskonvensjon.
 
Et tre er sammenhengende og omslutter alle nodene, men er ikke en sløyfe.  
Man starter i en node og markerer grener ut fra det.  
Treet består av n-1 grener.
 
## Likninger

Alle tregrenstrømmer kan beskrives ved hjelp av de andre grenstrømmene - som ikke er en del av treet. Man får da et sett unike likninger!
 
KCL: Som i knutepunktsanalyse ser man på et strømmer som forlater en node. Man ser på nodene som er omsluttet i treet.
 
Man definerer positive strømmer i retning strømmen i grenen.
 
Summerer spenningen i hver maske (må følge passiv fortegnsregel) etter KVL.

- U_R = R * I_A
   

Symmetri i likningene (hvis kun uavhengige kilder) om den skrå i midten fra topp venstre til bunn høyre.  
De på skrå er sum av resistansene i hver maske.
 ![Oh 2101 /IOB -Y JIP 9 ool ](Exported%20image%2020240415112030-0.jpeg)  
![—f— レ Ha 丁 = 工 、 一 工 2 ー 5 工 ー 50 → 5 ( 工 「 エ ろ ) ャ 20 ( ー 2 0 工 + 工 L) 工 ー 5 工 ー h 工 十 ん 工 50 ニ 0 ](Exported%20image%2020240415112030-1.jpeg) ![—e 2 も レ Ha ぞ レ 丁 ニ エ ー エ = Iu 2 ー 5 工 ー 2 矼 + DI 工 ー 5 。 → 5 ( 工 、 一 ャ 2 。 は ー ゝ 工 十 / 0 工 ー 50 ニ 0 丁 ご . 獺 ェ ニ 2 4 [ こ 26.04 ](Exported%20image%2020240415112030-2.jpeg) ![ア ご q ス 丁 ご / / 収 20 レ : ノ 90 ー ノ ー 工 十 工 ー 30J ー / の + 9 こ ~ 2 。 い ナ ク エ ノ り エ っ 工 = 幻 , ナ & + 仔 0 = 〇 ](Exported%20image%2020240415112030-3.jpeg)

![220V 十 2 効 レ 2 。 。 2 % を 一 々 。 。 ](Exported%20image%2020240415112030-4.jpeg)                                                                                                                                                                                                                         ![16 Α ](Exported%20image%2020240415112030-5.jpeg)