**F1**
Perfect matching: alla är matchade.
Unstable matching: Two pairs där två hellre vill vara med varandra.
Stable matching: Perfect matching with no unstable pairs
Gale-Shapley + hint for lab 1 (s 26)
Gale-Shapley perks: Perfect stable matching
c is valid for s if (s,c) is a pair in a stable matching
best c is most preferred by ss which is valid for it.

**F2**
separate chaining = öppen hashtabell = länkade listor (s.14) (m < n)
open addressing = sluten hashtabell = begränsad array m probing (m > n)
alpha = n/m
Inte garanterat att vi hittar tom position vid probing om inte m är primtal och $\alpha < \frac{1}{2}$ vid quadratic. 
Vid double hashing blir alla positioner funna om h2 är rleativt primtal till m.
Inget klart bästa val vid hash tables.
adjacency matrix: kant lagrad i m\[i]\[j] resp m\[j]\[i]. O(n) att hitta alla grannar O(1) att se om det är en kant. Bra för att kolla om granne
adjacency list: varje nod har en lista med neighbors. Bra för att lista alla grannar
Kan använda båda
Simple path: alla noder i pathen är distinkta
connected: om en undirected graf har en path mellan alla par av noder
cycle: path som är simple och går i en cykel lol
tree: en connected undirected utan någon cykel. har n-1 kanter.
DFS: rekursivt kolla alla noder som ej är besökta. O(n+m)
BFS: kolla alla noder med avstånd k O(n+m)

**F3**
mutually reachable: path from u to v and v to u
strongly connected: a driected graph where every pair is mutually reachable
Tarjans algorithm
Greedy: enkel regel utan "all" information
Bevisa greedy algoritm är optimal 2 sätt
Intervallschemläggning
compatible: requests are not overlapping
Greedy schemaläggning: lägst finish time. Bevisa genom "stay ahead". O(nlogn) - sortera i ökande tid, sen en linear pass.
Deadline problemt **Gör senare**

**F4**
Dijkstra: För att hitta kortaste väg i directed med vikter. Använder prioritetskö genom heap för Q med d(v) som nycklar. Funkar med undirected men ej med negativa vikter. O(mlogn), varje edge m kan minska en key log n. m>n-1 om alla noder nås från s. från heap (nlogn) vilekt är mindre
Spanning tree: alla noder, max alla kanter
Minimal spanning tree, spanning med minsta totala edge cost
Safe edge: en edge är safe om en delmängd av kanterna i en MST uniont med en kant (u,v) också är en delmängd av kanter i MST. Lemma - om A till hör S i cutten (S, V-S) och ingen kant i A korsar cutten då är varje kant med min weight i G som korsar cutten safe.
Jarniks/Prim. Plocka kanter som grenar iväg från vår byggande graf med minst weight. använd heap priority queue för att plocka. där d(v) är key men bara för edge inte path som dijkstra. O(mlogn) samma princip som dijkstra. Förutsätter undirected
Kruskal. Gå igenom alla kanter, se till att inte cykler bildas genom union find. O(mlogm) då det värsta är sortering, vidare = O(mlogn^2)=O(mlogn) då m är som mest n^2
Union find, se instud.

**F5**
Divide and conquer. Dela problem i två subproblem med n/2 items. Lös varje subproblem. Kombinera lösningar.
Master theorem ger os explicit form för tidskomplexiteten för en rekursionsrelation.
Closest point in plane. O(nlogn)
Jarvis march.  Två nästa punkter ska vara en vänstersväng. O(n^2) jämför varje punkt med alla andra punkter om alla punkter är del av konvex hull.
Graham scan. O(nlogn)
Preparata-Hong. O(nlogn). Divide and conquer nere och uppetills du har tre eller två punkter. mergea genom att ta punkterna från respektive sida längst till höger. kolla när linjen mellan två punkterna i fråga har högre lutning än första alpha sen beta. annars jobba till nästa punkt. ordning viktig. tvärtom ordning för vänster sida.
Dynamic praktsikt när det inte finns en greedy algoritm


**F7**
Ford-Fulkerson. Terminates om man inte har särksilt utvalda irrationella tal med oändlig precision. O(Cm) där C är summan av kapaciteter.
Bipartite graph matching kan lösas med Ford-fulkerson eller preflow push.



***Läs i reading afvice om att det är main ideas främst han vill ha osv***






heap