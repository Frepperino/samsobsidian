Totalt rörelsemängdsmoment $\mathbf{J}$, specificerat med kvanttalet $J$, är en bevarad storhet d.v.s. är konstant utan yttre verkan.

Elektroner i omloppsbana har två typer av rörelsemängdsmoment, spinn och "orbital".

**Orbital**
Klassiskt: $L = r \times p$
Kvantmekansikt: $\hat{L}_x=-i\hbar\left(y\frac{\partial}{\partial z}-z\frac{\partial}{\partial y}\right)$ ,
$\hat{L}_y=-i\hbar\left(z\frac{\partial}{\partial x}-x\frac{\partial}{\partial z}\right)$,
$\hat{L}_z=-i\hbar\left(x\frac{\partial}{\partial y}-y\frac{\partial}{\partial x}\right)$,
$\mathbf{\hat{L}}^2 = \hat{L}_x^2+\hat{L}_y^2+\hat{L}_z^2$

Lite om kommutatorer...
Sammanfattning:
- Vi kan känna till $|L^2|$ och magnituden av en av rörelsemängdsmomentkomponenterna samtidigt.
- Vi använder $L_z$ för att det är matematiskt bekvämt.
- Vi kan inte veta värdet på alla tre rörelsemängdsmomentkomponenter samtidigt.

$|\mathbf{l}|^2=l(l+1)\hbar^2$,
$l_z=m\hbar$
Notera att detta är i små bokstäver då vi avser en enda elektron.

Degenerationen $2(2l + 1)$ gäller då vi inte har externa magnetiska eller elektriska fält.

<mark style="background: #FFF3A3A6;">En förklaring till att "förbjudna" övergångar kan ske är antagandet att $l$ är konservativt, vilket stämmer just då kraften är radiell d.v.s. centralfältsapproximation. När vi i praktiken får krafter som inte följer approximationen kan dessa övergångar ske, om än mycket mer sällan.</mark>

Fyllda skals totala orbitalrörelsemängdsmoment är noll då de har lika många positiva som negativa $m_l$ tillstånd. För $l = 0$ blir det inget bidrag heller.

**Spinn**
Två kvanttal analogt med orbital,
$s = 1/2$
$m_s=\pm1/2$
$|\mathbf{s}|^2=s(s+1)\hbar^2$
$s_z=m_s\hbar$

**Addition av rörelsemängsmoment**
För $C = A + B$ kan $C$ anta alla värden mellan $|A| + |B|$ och $||A|-|B||$

**Spin-Orbit Coupling**
Orbital- och spinnrörelsemängdsmoment är ej helt oberoende av varandra, utan interagerar genom *spin-orbit interaction*. <mark style="background: #FFF3A3A6;">Detta uppkommer genom att den magnetiska dipolen som kommer från spinn växelverkar med det magnetiska fältet som elektronen upplever p.g.a. dess kretsande rörelse.</mark> Detta kan skrivas som:

$$\hat{H}=-\mu_{spin}\cdot B_{orbital} \propto l \cdot s$$
Växelverkan ökar med ökande Z.

**Koppling med enelektronsatomer**
Totala rörelsemängdsmomentet:
$j = l + s$
$|j|^2=j(j+1)\hbar^2$
$j_z=m_j\hbar$
$m_j=j,(j-1),...,-j$
De tillåtna värdena för $j$ ges av  $j = l \oplus s$. Eftersom $s=1/2$ får vi att $j=(l \pm 1/2)$ förutom då $l=0$ där vi inte har $l=-1/2$.
Notera att i fall då $l = 0$ får vi att $j$, det totala rörelsemängdsmomentet, endast uppkommer på grund av spinn.

**Koppling i flerelektronsatomer**
Nu tar vi med:
$\hat{H} = \hat{H}_0 + \hat{H}_1 + \hat{H}_2$
<mark style="background: #FFF3A3A6;">Memorera namn på bild:</mark>
![[Pasted image 20231219115143.png|550]]

Vi har:
- LS-koppling då $\hat{H}_1 \gg \hat{H}_2$
- jj-koppling då $\hat{H}_2 \gg \hat{H}_1$
