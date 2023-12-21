**LS-koppling**
LS-koppling gäller för de fall då elektrostatisk växelverkan är mycket starkare än spinn-orbit. Därmed räknar vi först ut den elektrostatiska effekten varefter vi lägger till spinn-orbit effekter som en mindre störning på LS-tillstånden. LS-koppling gäller för de flesta atomer men små till medium Z. 

Liten bokstav på $j, l, s$ avser individuella elektroners rörelsemängdsmoment medan stor bokstav $J, L, S$ avser den totala för hela atomen. För väte och alkali-atomer gör det ingen skillnad dock.

Det gäller att:
$L = \sum_i l_i$
$S=\sum_is_i$

Eftersom fulla skal inte har netto noll rörelsemängdsmoment behöver räkningen endast utföras för valenselektroner.

Tillstånd definierade av $L$ och $S$ värden kallas *termer*. För varje atomisk term får vi det totala rörelsemängdsmomentet av:
$J=L + S$

Spinn-orbit-växelverkan, för hela atomen ges av:
$$\Delta E_{so} \propto -\mu^{atom}_{spin} \cdot B^{atom}_{orbital}\propto L\cdot S$$
där superskript indikerar att vi tar resultantvärdet för hela atomen.

Det viktiga:
- Spinn-orbit-växelverkan splittrar LS-termer i nivåer märkta av J
- Splittringen är mycket mindre än energiskillnaden mellan olika LS-termer

Varje nivår är betecknad:
${}^{(2S+1)}{L_J}$
Faktorn $(2S + 1)$ avser multipliciteten. Det indikerar degenerationen av nivån p.g.a spinn d.v.s. antalet $M_S$-tillstånd. Om $S = 0$ har vi multiplicitet 1 och termerna blir kallade *singlets*. För $S = 1/2$ har vi mulitplicitet 2 och termerna kallas dubblett. För S = 1, multiplicitet 3, triplett.

![[Pasted image 20231219123613.png|550]]

**Urvalsregler för elektriska dipoler i LS-koppling**
Urvalsregleran är samma som i [[F4 - Övergångar och linjebredder|Föreläsning 4]], med tillägget att vi måste ha hela atomens rörelsemängdsmoment i åtanke. Reglerna blir:
- Pariteten av vågfunktionen måste ändras.
- $\Delta l = \pm 1$ för elektronen som byter skal
- $\Delta L = 0, \pm 1$, men $L = 0  \rightarrow 0$ är förbjudet.
- $\Delta J  = 0, \pm 1$, men $J = 0  \rightarrow 0$ är förbjudet.
- $\Delta S = 0$.

**Hunds regler**
För att hitta grundtillståndet för atomer med LS-koppling gör följande:
1. Maximera spinn och sätt $S = \sum m_s$.
2. Därefter, maximera orbitalrörelsemängdsmoment och sätt $L=\sum m_l$
3. Sist, $J=|L-S|$ om skalet är mindre är halvfullt, annars $J=L+S$.

Se tabeller på s. 101-102 samt exempel för tydlig redovisning av metodik.

**jj-koppling**
Om spinn-orbit-växelverkan är starkare än resterande elektrostatisk växelverka så gäller *jj-koppling*. I denna regim kopplas rörelsemängdsmomentet från orbital och spinn för de enskilda elektronerna först, varefter resultanten $J$ fås genom att addera alla individuella $j$.
$j_i=l_i+s_i$
$J=\sum^N_{i=1}j_i$
Dessa J-tillstånd splittras sedan av den svagare resterande elektrostatiska potentialen, som agerar som störning.

Notera att värdena av $L$ och $S$ inte är kända i jj-koppling precis som värdena av $j$ för individuella elektorner inte är kända under LS-koppling.
![[Pasted image 20231219123527.png|550]]
Jämför med LS-koppling ovan.
