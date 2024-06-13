**Dopplerkylning**
<mark style="background: #FFF3A3A6;">Genom att sända fotoner med ett vågtal en aning förskjuten från absorptionsvågtalet ser vi till att just atomerna i motsatta riktningen absorberar i.o.m. dopplereffekten. Resten av atomerna har inte ett vågtal som överrensstämmer och blir därmed ej absorberade.</mark> Därefter emitteras fotonen spontant med en genomsnittlig tid $\tau$. Riktningen är dock slumpmässig så nettokraften för all rekyl blir 0, vilket ger den totala kraften till att bli den ursprungliga från lasern.
![[Pasted image 20231222164337.png]]
![[Pasted image 20231222164354.png]]
![[Pasted image 20231222164359.png|300]]
<mark style="background: #FFF3A3A6;">Dock finns det en gräns för hur låg temperatur som kan nås, då vi får en viss breddning på grund av osäkerheten i energi.</mark> Detta omöjliggör det att få en perfekt inställning av $\delta$.

**Optisk sirap och magneto-optisk fälla**
Genom att placera två lasrar i varje riktning x, y, z kan vi kyla atomer i alla dess komponenter. Vi får en optisk sirap.

Om vi även lägger till en spole över och nedanför med motsatta strömriktningar får vi en magneto-optisk fälla. Vi får då ett kvadrupolfält.
![[Pasted image 20231222165824.png]]

Jag fattar inte riktigt, men hon har den här bilden:
![[Pasted image 20231222165845.png|450]]

**Experimentella övervägningar**
För att se till att den optimala kraften används måste vi se till att inställningen justerade till just $\frac{v_{x}}{\lambda}$. Denna minskar då $v_{x}$ minskar vilket betyder att vi antingen måste justera laserfrekvensen, eller genom att hålla en fix laserfrekvens samtidigt som övergångsfrekvensen justeras med ett magnetfält.

I den andra metoden använder man en spole med avtagande magnetfält där övergångsenergin förskjuts av Zeemaneffekten. Minskningen av $B$ längs spolen kompenserar för minskningen av $v_{x}$. Denna metod används ofta för att sakta ner snabba atomer till en sådan hastighet att en magneto-optisk fälla kan användas.

![[Pasted image 20231222171114.png|400]]

Temperaturen för en kyld gas kan mätas genom att att stänga av all kylning och mäta expansionen av gasen som funktion av tid.

**Kylning bortom Dopplergränsen**
Vid laserkylning har man märkt att ämnet blir lägre än den förutspådda dopplergränsen. <mark style="background: #FFF3A3A6;">Detta då atomerna fortsätter absorbera och emittera fotoner p.g.a. interferens mellan lasrarna</mark>. Det viktiga från detta är att laserkylningens gräns egentligen är mycket lägre än Dopplergränsen.


**Bose-Einsteinkondensation**
Laserkylning följer klassisk mekanik, men om vi jobbar med kvantmekanik kan vi sänka temperaturen ytterlgiare. <mark style="background: #FFF3A3A6;">Om vi kan se till att våra atomer är bosoner finns det ingen lägre begränsing av energi tillstånd</mark>. Detta gör vi genom att se till att atomens totala spinn är ett heltal:
$$S_{atom}=S_{electrons} \oplus I$$
Eftersom antalet protoner är samma som elektroner behöver vi endast se om antalet neutroner är jämnt, i så fall har vi en boson, annars en fermion.

<mark style="background: #FFF3A3A6;">Om bosonerna är *icke-växelverkande* kommer de kondensera vid en kritisk temperatur $T_{c}$. Icke-växelverkande innebär att de är helt fria och innehar därmed endast kinetisk energi. Vid $T_{c}$ sker en fasövergång där en makroskopisk andel av partiklar kondenserar till ett nollhastighetstillstånd. Resten av partiklarna forsätter fördela sig termiskt bland de ändliga hastigheternas tillstånd.</mark>

Andelen partiklar i nollhastighetstillstånd ges av $N_0$:
![[Pasted image 20231222174353.png|200]]

En annan syn på kondensationsprocessen är att se på de Broglie-våglängden av partiklarna. Om partiklarna inte växelverkar är all energi kinetisk vilket bestäms av den fria termiska energin:
$$E=\frac{p^{2}}{2m}=\frac{1}{2m}\left( \frac{h}{\lambda_{deB}} \right)^{2}=\frac{3}{2}k_{B}T$$
Härifrån kan vi lösa ut $\lambda_{deB} = \frac{h}{\sqrt{ 3mk_{B}T }}$. <mark style="background: #FFF3A3A6;">Då T minskar ökar våglängden tills atomerna vågor till slut överlappar och börjar växelverka vilket får de att bilda en gemensam "superatom" med en gemensam vågfunktion, med andra ord ett BEC</mark>. Villkoret är att den effektiva partikelvolymen ska vara samma som partikeldensiteten: $N \sim \frac{1}{\lambda_{deB}^{3}}$. Genom att lösa detta får vi så nära som på en ungefärlig konstant samma resultat som för det tidigare synsättet.
![[Pasted image 20231222175512.png|150]]

<mark style="background: #FFF3A3A6;">För att skapa ett BEC är metoden följande:
1. Fånga en atomgas och kyl de till rekylgränsen med hjälp av laserkylning.
2. Stäng av laserkylning så att temperaturen kan bli ännu lägre.
3. Kyl gasen med evaporative cooling tills kondensation har skett.</mark>

<mark style="background: #FFF3A3A6;">Evaporative cooling innebär att man långsamt sänker mangetfältets styrka för att minska djupet på den magnetiska potentialen, vilket får de snabbaste atomerna att fly. Kvar har vi de långsammaste.</mark>
![[Pasted image 20231222180645.png|450]]

Resultatet blir att den genomsnittliga kinetiska energin sjunker vilket är ekvivalent med att temperaturen sjunker.

En nyckelaspekt med BEC är att atomerna i det kondenserade tillståndet delar en gemensam vågfunktion vilket orsakar en ökad koherens. Detta gör att atomstrålar från kondensat, kallat atomlasrar, kan bilda interferensmönster när de överlappar. Detta går ej med vanliga atomstrålar där atomerna har slumpmässiga faser.