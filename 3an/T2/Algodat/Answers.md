1. Explain what O(n), Ω(n), and Θ(n) mean.
	1. O(n) är värsta fall, upper bound. Ω(n) är bästa fall, lower bound. Theta(n) är tight bound, ofta Big O(n) tänk linear search. Kan ej existera om det inte finns accurate representation.
2. **B** Suppose you have invented a greedy algorithm that finds an optimal solution to a problem. Explain two approaches to prove its output really is optimal.
	1. Finns tre: a) Jämför med optimala lösningen och visa att den giriga är minst lika bra i varje steg; induktion. b) Utgå från en optimal och ändra stegvis (utan att ändra optimaliteten) och tills den är lika med den giriga. c) Motsägelse: utgå från att den inte är optimal, jämför resultatet med en optimal. Eftersom resultatet från giriga är minst lika bra som optimalas resultat är den giriga optimal.
3. Explain what is meant by a divide-and-conquer algorithm (söndra-och-härska).
	1. Divide: dela upp problemet i ej överlappande subproblem (ofta rekursion) så mycket det går.
	   **R** Conquer: lös subproblemen individuellt, direkt eller med...
	   Combine: kombinera lösningerna.
	   Ex. merge sort: sorterar arrayen genom uppdelning, sorterar de, kombinera O(nlogn) ist för O(n^2). Lab 4 Closest Points
4. Explain what is meant by dynamic programming (dynamisk programmering).
	1. **R** Vid överlappande subproblem (till skillnad från divide and conquer). Dela i subproblem, lös varje problem EN gång, spara resultatet för framtida användning (memoization). Ex. Gorilla lab 5, 
5. With open addressing, how can pairs be deleted?
	1. Genom att markera platserna med en markör "deleted" så fungerar probing som det ska. Om det blir för mycket deleted kan man städa upp genom att reinserta allt. Insert är inga problem
6. What does quadratic probing (kvadratisk prövning) mean with hash tables?
	1. Att om en plats är upptagen tar vi en plats 1, 4, 9, 16 mod N osv. långt bort för att snabbt fly undan för att minska kluster. (problem: om två nycklar har samma hash får vi sekundär clustering pga samma positioner)
7. What does double hashing (dubbel hashning) mean? Why can α be larger with double hashing than with quadratic probing?
	1. Använder två hashfunktioner för att för att minimera kollisionsrisken. Genom att ha två lämpligt valda funktioner kan de komplettera varandra där den ena "stallar"
8. Explain what the Master theorem is about.
	1. **R** En formel för att bestäma T(n) för rekursiva algoritmer där det är tre closed form solutions.
9. Explain how hollow heaps work. Focus on the simplest version with multiple root nodes.
	1. **AAAA**
10. What can make the naïve version of union-find slow?
	1. Långa paths till root gör find O(n) då den i värsta fall går igenom alla andra noder. Kan bli O(1)* med rätt path compression - alla barn pekar på root.
11. Explain how union-find can be made faster than as in the naïve version.
	1. Path compression, alla barn pekar direkt på root efter find.
	   Union-by-size, minsta läggs till största => minskar djup => förenklar find.
12. What does it mean that a directed graph is strongly connected (starkt sammankopplad), and how can you use BFS to determine if a graph is strongly connected?
	1. **R** Komma från varje nod till varje annan nod åt båda håll. BFS från godtycklig nod, om vi besökt alla noder, vänd kanter och gör bfs igen från s igen. Om alla noder besökts  => starkt sammankopplad.
13. Explain how Tarjan’s algorithm can find the strongly connected components in a directed graph.
	1. ![[Pasted image 20240612213125.png|450]]

14. What is a bipartite graph (bipartit graf), and how can you determine if a graph is bipartite?
	1. V kan delas i två disjunkta mängder där alla kanter kopplar en Vertex i ena setet med en vertex i andra. Inga kanter mellan vertex i de disjunkta mängdrna. BFS, växla mellan U och V set, om två grannoder har samma färg NEJ.
15. Explain how Dijkstra’s algorithm works and why it is correct.
	1. **R**
16. Explain what can happen if there are negative edge weights (negativa kanter).
	1. **R**
17. Explain how the Bellman-Ford algorithm works and why it is correct.
	1. **R**
18. Explain what a minimum spanning tree (minimalt uppspännande träd) is and how it can be found using Prim’s and Kruskal’s algorithms.
	1. Spanning tree innehållar alla noder med en delmängd av kanterna (undirected tree). Minimal om summan av edge costs är minimerat.
	   **R** Kruskal: (Greedy) lägg till edge med minst cost, lägg till nästa med minst. Kolla med union find om kantens noder delar root, om ja är det cykel så vi går till nästa edge ist. Annars mergar vi och lägger till edgen i mst. mst är separata tills vi är klara. vi plockar edges. Greedy (ta minsta edge just nu). O(ElogE)=O(ElogN)
	   Prim: (Greedy) Börja med en nod och välj grannen som inte är besökt med minimum cost. Ignorera efges mellan två besökta noder. Fortsätt till alla noder är besökta. O(E logV). E kanter log V för att hitta edge. Vi plockar noder.
19. What is a safe edge (säker kant) for miminum spanning trees?
	1. En kant som inte ksapar en cykel.
20. What is network flow (nätverksflöde) about? Give an example of when it can be used.
	1. **R** En graf där kanter har en kapacitet. Bestämma max flow, min cut, t.ex. koppla städer med tåg eller delegera arbetsuppgifter, bipartite.
21. Explain the Ford-Fulkerson algorithm and why it is correct. What is its time complexity, and why?
	1. **R** i) Hitta korstast väg BFS.
	   ii) välj edge med lägst kapacitet.
	   iii) alla edges flöde ökar med denna. total flow ökar
	   iv) Kör om med alla kanter som inte har full kapacitet, tills det inte finns någon mer som ökar.
	   Viktigt: edges kan användas baklänges då flöde minskar. Detta sker parallellt
	   BEVIS O(NXADX)

22. Explain the Goldberg-Tarjan (preflow-push) algorithm and why it is correct.
	1. **R** Istället för att långsamt bygga upp flöde, börjar vi med max flöde ut från start noden. Vi har excess flow som vi pushar till noder med lägre höjd. om det inte finns ökar vi höjden tills den kan. till slut har allt flow antingen pushats till slut eller tillbaka till början. Då har vi flow in = flow ut. Stable matching. O(V^2E) ?
23. Explain why the Gale-Shapley algorithm finds a stable matching (stabil matchning)?
	1. Genom att börja från mest önskad till minst för "studenterna" garanterar vi att "studenternas" sida kommer vara nöjda. I andra hand ser vi att "företagen" ersätter sin "student" så fort en annan student önskar "företaget" i fråga. På så vis går vi från två håll och möts på mitten där vi har en stabil matchning. Mer specifikt med ett fall, om en student gillar ett annat företag mer men de ej är i par så betyder det antingen att studenten föredrar företaget den är matchad med, eller att företaget föredrar studenten mer, då de i annat fall hade blivit matchade.
24. Explain the time complexity of Gale-Shapley.
	1. I värsta fall har varje student gått igenom hela sin lista innan den hittar sitt företag vilket innebär att vi har O(n^2).
25. What is sequence alignment and how can it be done?
	1. **R** Se hur bra 2 strängar passar. Iterativt eller rektursivt går vi igenom fallen att sätta in tomt eller ej utefter en kostnadsmatris. 
26. What does it mean that a problem is NP-complete (NP-fullständigt) ?
	1. **R** NP: Problem vars lösning kan verifiries som korrekt eller inkorrekt i polynomial time.
	   Np-complete: 
27. If you want to prove that a new problem is NP-complete, how would you do?
	1. 
28. Explain how the first NP-complete problem was shown to be NP-complete.
	1. 
29. Explain how it can be shown that Hamiltonian cycle (Hamiltonsk cykel) is NP-complete.
	1. 
30. Explain how it can be shown that the Traveling salesman problem (Handelsresandeproblemet) is NP-complete.
	1. 
31. Explain how it can be shown that graph coloring (graffärgning) is NP-complete.
	1. 
32. Explain what unit propagation (unär propagering) in SAT-solvers mean.
	1. 
33. Explain what the simplex algorithm can do (but not why it works).
	1. 
34. Explain what the branch-and-bound paradigm (förgrena-och-begränsa) is and can used exploited in integer linear programming (heltalsprogrammering).
	1. 
35. What is a convex hull?
	1. 
36. Explain the Graham scan algorithm
	1. 
37. Explain the main ideas of the Preparata-Hong algorithm
	1. 
38. Why is it important to compare either α or β with γ first in different situations? What is likely to happen otherwise? You do not need to explain exactly when which is compared with γ first!
	1. 
39. How can you know if a point p is between q and r on a line?
	1. 
40. How can you know the direction (left, right, or straight) when going from a point pr through ps to pt ?
	1. 