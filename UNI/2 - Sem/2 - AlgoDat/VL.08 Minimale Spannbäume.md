**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]
**Date:** 04-06-2026
**Topics:** #Graphen #GewichteteGraphen #MinimalerSpannbaum #MST #Schnitteigenschaft #Prim #Kruskal #ReverseDelete #Greedy #UnionFind
**Link:** [[VL.08 AlgoDat.pdf]]

***

## 🎯 Lernziele der Vorlesung

Stell dir vor, du sollst Städte mit Glasfaser verbinden. Jede mögliche Leitung kostet etwas. Du willst, dass am Ende **alle** Städte verbunden sind, aber so **billig wie möglich** — und ohne überflüssige Schleifen. Genau das ist das Problem des **minimalen Spannbaums (MST)**.

Die ganze Vorlesung dreht sich um eine einzige große Idee und ihre Anwendung:

- **Die Idee:** die *Schnitteigenschaft* — ein einfaches Argument, warum eine bestimmte Kante sicher in den MST gehört.
- **Die Anwendung:** drei Algorithmen (Prim, Kruskal, Reverse-Delete), die alle nur verschiedene Arten sind, dieselbe Idee anzuwenden.

Wenn du die Schnitteigenschaft verstehst, hast du die Vorlesung verstanden. Der Rest sind Details der Umsetzung.

***

## 1. Warum gewichtete Graphen?

In VL.07 hatten Kanten kein Gewicht — eine Kante war einfach „da oder nicht da". Für „kürzeste Verbindung" oder „billigstes Netz" reicht das nicht: wir müssen Kanten **vergleichen** können. Deshalb bekommt jede Kante eine Zahl.

$$\boxed{G = (V, E, g) \quad \text{mit Gewichtsfunktion } g: E \to \mathbb{R}}$$

$g(v,w)$ ist das Gewicht der Kante — Länge, Kosten, Fahrzeit, was auch immer. Negative Gewichte sind erlaubt (relevant erst im nächsten Kapitel).

> [!info] **Merkhilfe:** Das Gewicht klebt an der **Kante**, nicht am Knoten. Landkarte: Städte = Knoten, Straßen = Kanten, **Kilometer = Gewicht**.

### Was sich an der Implementierung ändert

Weil jetzt jede Kante eine Zahl mitschleppt, lohnt sich eine eigene `Edge`-Klasse, und die Nachbarschaftslisten speichern **Kanten statt Knoten** (man nennt sie dann *Inzidenzlisten*). Der praktische Effekt: wenn du über die Nachbarn eines Knotens iterierst, bekommst du `Edge`-Objekte, aus denen du Gewicht *und* beide Endpunkte ablesen kannst.

```java
public class Edge implements Comparable<Edge> {
    Edge(int v, int w, double weight)
    double weight()              // Gewicht
    int either()                 // irgendeiner der beiden Knoten
    int other(int v)             // der jeweils andere Knoten
    int compareTo(Edge that)     // vergleicht nach Gewicht
}

public class EdgeWeightedGraph {
    EdgeWeightedGraph(int V)
    int V(); int E();
    void addEdge(Edge e)
    Iterable<Edge> incident(int v)   // Kanten an v (nicht Nachbarknoten!)
    Iterable<Edge> edges()
}
```

> [!tip] **Warum `either()` / `other(v)`?** Bei einer *ungerichteten* Kante gibt es kein „von" und „nach". `either()` gibt dir einen Endpunkt, `other(v)` den anderen — so kannst du eine Kante benutzen, ohne ihre Richtung zu kennen. Das taucht in beiden Algorithmen unten auf.

***

## 2. Spannbaum & minimaler Spannbaum

### Spannbaum: das „Gerüst"

Ein **Spannbaum** ist ein Teilgraph, der alle Knoten verbindet und dabei ein Baum ist (zusammenhängend, keine Zyklen).

$$\boxed{\text{Spannbaum} = \text{verbindet alle Knoten} + \text{zusammenhängend} + \text{zyklenfrei}}$$

„Zyklenfrei" ist hier kein Zufall, sondern Sparsamkeit: ein Zyklus enthält eine Kante, die man **weglassen** könnte, ohne den Zusammenhang zu verlieren. Ein Spannbaum ist also ein Gerüst **ohne Verschwendung**.

### Minimaler Spannbaum: das billigste Gerüst

$$\boxed{\text{MST} = \text{Spannbaum mit kleinstem Gesamtgewicht} = \min \sum_{e \in T} g(e)}$$

Es kann **mehrere** MSTs mit gleichem Gewicht geben — aber nur einen eindeutigen, wenn alle Gewichte verschieden sind (dazu unten mehr).

### Eine Tatsache, die du im Schlaf können musst

$$\boxed{\text{Jeder Spannbaum mit } V \text{ Knoten hat genau } V-1 \text{ Kanten}}$$

Intuition: Fang mit einem Knoten an. Jede neue Kante, die du *ohne Zyklus* hinzufügst, hängt **genau einen** neuen Knoten an. Für $V$ Knoten brauchst du also $V-1$ solche Kanten — keine mehr, keine weniger.

### Warum überhaupt ein Algorithmus? Kann man nicht alle durchprobieren?

Nein. Ein vollständig verbundener Graph hat

$$\boxed{V^{\,V-2} \text{ Spannbäume} \quad (\text{Cayleys Formel})}$$

> [!warning] **Achtung:** Bei nur 10 Knoten sind das schon $10^8$ Spannbäume. Brute-Force ist chancenlos — wir brauchen etwas Schlaueres. Genau dafür gibt es die Schnitteigenschaft.

### Sechs Wege, dasselbe zu sagen

Ein Subgraph $T$ mit allen Knoten ist genau dann ein Spannbaum, wenn **eine** dieser (äquivalenten!) Bedingungen gilt — du musst sie nicht auswendig können, aber **zwei** davon sind die Seele zweier Algorithmen:

|                             | Bedingung                                                                                                                             | wird genutzt von   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| **maximal azyklisch**       | zyklenfrei, aber *jede* zusätzliche Kante erzeugt einen Zyklus                                                                        | **Kruskal**        |
| **minimal zusammenhängend** | zusammenhängend, aber *jede* entfernte Kante zerstört das                                                                             | **Reverse-Delete** |
| weitere                     | „$V-1$ Kanten + zusammenhängend", „$V-1$ Kanten + azyklisch", „genau ein Pfad zwischen je zwei Knoten", „azyklisch + zusammenhängend" | —                  |

> [!info] **Lies die Tabelle so:** Kruskal baut von unten auf und passt auf, *keinen Zyklus* zu erzeugen. Reverse-Delete reißt von oben ab und passt auf, *den Zusammenhang nicht* zu zerstören. Es sind buchstäblich zwei Seiten derselben Medaille.

***

## 3. Schnitte — das Werkzeug, um „welche Kante?" zu beantworten

Alle MST-Algorithmen müssen ständig entscheiden: *welche Kante nehme ich als nächstes sicher in den Baum?* Das Werkzeug dafür ist der **Schnitt**.

Ein **Schnitt** zieht eine Linie durch den Graphen und teilt die Knoten in zwei nicht-leere Gruppen $S$ und $V-S$.

$$\boxed{S \subseteq V, \quad S \neq \varnothing,\; V-S \neq \varnothing}$$

- **Kreuzende Kante:** eine Kante, die die Linie überquert (ein Endpunkt in $S$, einer in $V-S$).
- **Minimal kreuzende Kante:** die *leichteste* aller kreuzenden Kanten.

$$\boxed{E(S, V\setminus S) = \{(u,v) \in E \mid u \in S,\; v \notin S\}}$$

> [!tip] **Bild im Kopf:** Der Schnitt ist eine rote Linie quer durchs Bild. Die Kanten, die sie durchschneidet, sind die kreuzenden. Die *dünnste* (= billigste) davon ist die minimal kreuzende.

***

## 4. Die Schnitteigenschaft — der Kern der ganzen VL

> [!abstract] **Schnitteigenschaft:**
> Egal welchen Schnitt du wählst — eine **minimal kreuzende Kante** dieses Schnitts gehört **immer** zu einem MST.

Das ist die Erlaubnis, die wir brauchen: „Du darfst diese Kante bedenkenlos einbauen, sie ist garantiert Teil einer optimalen Lösung." Alle drei Algorithmen sind nur Strategien, *immer wieder* eine solche garantierte Kante zu finden.

### Warum stimmt das? (Austauschargument)

Der Beweis ist ein klassisches „Was wäre wenn nicht?" — und die Idee ist einprägsamer als die Formalität:

1. **Annahme:** Ein MST enthält die minimal kreuzende Kante $(v,w)$ *nicht*.
2. Bau $(v,w)$ trotzdem ein. Da der MST schon alles verbindet, schließt sich ein **Zyklus**. Ein Zyklus, der den Schnitt überquert, muss ihn **zweimal** überqueren → es gibt eine zweite kreuzende Kante $(t,u)$ im Zyklus.
3. $(v,w)$ war die *leichteste* kreuzende Kante, also $g(v,w) \le g(t,u)$.
4. **Tausch:** wirf $(t,u)$ raus, behalte $(v,w)$. Der Baum bleibt verbunden — aber er ist jetzt **leichter (oder gleich schwer)**. Das widerspricht der Annahme, der erste sei schon minimal gewesen. $\square$

> [!success] **Folgerung (wichtig!):** Sind alle Gewichte **verschieden**, ist die leichteste kreuzende Kante jedes Schnitts **eindeutig** → der **MST ist eindeutig**. Bei Gleichständen kann es mehrere geben.

***

## 5. Ein Bauplan für alle Algorithmen (generischer Greedy-Ansatz)

Aus der Schnitteigenschaft fällt ein Rezept fast von selbst heraus:

```
ME ← ∅
while ME ist noch kein Spannbaum:
    wähle einen Schnitt, dessen kreuzende Kanten noch NICHT in ME sind
    füge eine minimal kreuzende Kante hinzu
```

> [!note] **Warum ist das „greedy"?** In jedem Schritt schnappst du dir die lokal beste Kante und nimmst sie *nie wieder zurück*. Bei vielen Problemen ist das gierig und falsch — hier ist es dank Schnitteigenschaft beweisbar **richtig**.

Was bleibt offen? **Nur eine Frage:** *welchen Schnitt wählst du in jedem Schritt?* Genau hier — und nur hier — unterscheiden sich Prim, Kruskal und Reverse-Delete. Behalte das im Kopf, dann wirken die drei Algorithmen nicht wie drei Dinge zum Auswendiglernen, sondern wie drei Antworten auf *eine* Frage.

> [!info] **Voraussetzung:** Wir nehmen an, $G$ ist zusammenhängend. Ist er es nicht, lässt man die Algorithmen auf jeder Zusammenhangskomponente laufen und bekommt einen minimalen **Spannwald**.

**Warum findet das Rezept wirklich *alle* MST-Kanten?** Solange $ME$ noch kein Spannbaum ist, gibt es eine Knotengruppe, die noch nicht voll angebunden ist — nimm sie als $S$. Keine ihrer kreuzenden Kanten ist in $ME$, also kann der Algorithmus weitermachen. Er bleibt erst stehen, wenn wirklich alles verbunden ist. $\square$

***

## 6. Prim — den Baum wachsen lassen

> [!abstract] **Prims Schnittwahl:** Der Schnitt ist immer „**schon im Baum** vs. **noch draußen**". Nimm die leichteste Kante, die vom Baum nach draußen führt.

Das fühlt sich an wie **BFS aus VL.07** — ein markierter Bereich frisst sich nach außen. Der einzige Unterschied:

> [!tip] **Prim vs. BFS:** BFS nimmt als nächstes den Knoten, der *am längsten in der Warteschlange wartet* (FIFO). Prim nimmt den Knoten, der über die *billigste Kante* erreichbar ist (PriorityQueue nach Gewicht). Tausche „FIFO-Queue" gegen „Min-PQ" und aus BFS wird Prim.

### Implementierung mit PriorityQueue

```java
public class MSTPrim {
    protected PriorityQueue<Edge> pq;

    public MSTPrim(WeightedGraph G) {
        marked = new boolean[G.V()];
        parent = new int[G.V()];
        pq = new PriorityQueue<Edge>(G.V());

        visit(G, 0);                  // Startknoten 0 markieren + seine Kanten einreihen
        while (!pq.isEmpty()) {
            Edge e = pq.poll();       // leichteste Kante aus der PQ
            int v = e.either();
            int w = e.other(v);
            if (!marked[w]) {         // führt sie noch nach „draußen"?
                parent[w] = v;
                visit(G, w);
            } else if (!marked[v]) {
                parent[v] = w;
                visit(G, v);
            }
        }
    }

    public void visit(WeightedGraph G, int v) {
        marked[v] = true;
        for (Edge e : G.incident(v))
            if (!marked[e.other(v)]) pq.add(e);   // nur Kanten nach draußen
    }
}
```

> [!warning] **Die eine knifflige Stelle:** Eine Kante kann in der PQ liegen, während *beide* ihre Endpunkte inzwischen markiert wurden — dann führt sie nicht mehr nach draußen und wäre ein Zyklus. Deshalb der erneute Check `if (!marked[w])` *nach* dem `poll()`. Ohne diesen Check baust du Zyklen.

$$\boxed{\text{Prim (einfache PQ): } O(E \log E) \text{ Zeit}, \;\; O(V+E) \text{ Speicher}}$$

**Woher die $O(E \log E)$?** Jeder Knoten wird höchstens einmal `visit`-et → jede Kante landet höchstens einmal in der PQ → höchstens $E$ Einfügeoperationen zu je $O(\log E)$. Fertig.

### Schneller: indizierte PQ

**Beobachtung:** Sobald du für einen Knoten draußen eine *billigere* Verbindung gefunden hast, sind alle teureren Verbindungen zu ihm Müll. Statt also *alle* kreuzenden Kanten in der PQ zu horten, merkst du dir **pro Außenknoten nur die bisher billigste**.

```java
public void visit(WeightedGraph G, int v) {
    marked[v] = true;
    for (Edge e : G.incident(v)) {
        int w = e.other(v);
        if (marked[w]) continue;
        if (e.weight() < weightOfCE[w]) {   // billigere Anbindung an w gefunden
            parent[w] = v;
            weightOfCE[w] = e.weight();
            if (pq.contains(w)) pq.change(w, weightOfCE[w]);
            else                pq.add(w, weightOfCE[w]);
        }
    }
}
```

$$\boxed{\text{Prim (indizierte PQ): } O(E \log V) \text{ Zeit}, \;\; O(V) \text{ Speicher}}$$

> [!success] **Was hat sich verbessert?** Die PQ enthält jetzt höchstens $V$ Einträge (einen pro Außenknoten) statt $E$. Speicher fällt von $O(E)$ auf $O(V)$, und weil $\log V \le \log E$, sinkt auch die Laufzeit. Mit Fibonacci-Heap ginge sogar $O(E + V \log V)$.

***

## 7. Kruskal — die billigsten Kanten zuerst, Zyklen vermeiden

> [!abstract] **Kruskals Schnittwahl:** Geh *alle* Kanten von billig nach teuer durch. Nimm jede Kante, **außer** sie würde einen Zyklus schließen.

Der große Unterschied zu Prim: Prim hat *einen* wachsenden Baum. Kruskal hat anfangs **viele kleine Inselchen** (jeder Knoten ist seine eigene Insel), die nach und nach zu Brücken verbunden werden. Deshalb gibt es bei Kruskal auch **kein `parent`-Array** während des Ablaufs — beim Wählen einer Kante steht noch gar nicht fest, wer später Eltern- und wer Kindknoten wird.

### Das eine Problem: der Zyklustest

„Erzeugt diese Kante einen Zyklus?" ist gleichbedeutend mit: „**Sind ihre beiden Endpunkte schon auf derselben Insel?**" Den Test muss man $E$-mal machen. Naiv (mit Tiefensuche) kostet jeder Test $O(V)$ → insgesamt $O(VE)$ → **zu langsam**.

Die Rettung ist **Union-Find** (aus VL.03): eine Datenstruktur, die genau zwei Dinge quasi-umsonst kann — *„sind v und w auf derselben Insel?"* (`find`) und *„verschmelze zwei Inseln"* (`union`).

```
UF ← UnionFind(V)        // jeder Knoten startet als eigene Insel
MST ← ∅
sortiere alle Kanten aufsteigend nach Gewicht
for (v,w) in dieser Reihenfolge:
    if UF.find(v) ≠ UF.find(w):   // verschiedene Inseln → kein Zyklus
        UF.union(v, w)
        füge (v,w) zu MST hinzu
```

$$\boxed{\text{Kruskal: } O(E \log E) \text{ Zeit}, \;\; O(E) \text{ Speicher}}$$

> [!info] **Warum dominiert das Sortieren?** Dank Union-Find sind `find`/`union` so billig, dass sie kaum ins Gewicht fallen. Was übrig bleibt, ist das **Sortieren der Kanten** nach Gewicht — und das kostet $O(E \log E)$. Der eigentliche Algorithmus drumherum ist fast geschenkt.

> [!tip] **Warum *ist* Kruskals Kante immer eine minimal kreuzende?** Wenn du $(v,w)$ nimmst, betrachte den Schnitt „$v$s Insel vs. der Rest". $(v,w)$ kreuzt ihn (sonst wären $v,w$ schon zusammen). Und sie ist die *leichteste* kreuzende Kante, weil du die Kanten von billig nach teuer durchgehst — alle billigeren hast du schon geprüft. Damit ist Kruskal ein Spezialfall des generischen Ansatzes.

***

## 8. Reverse-Delete — der Vollständigkeit halber

> [!abstract] **Reverse-Delete:** Starte mit *allen* Kanten. Geh sie von **teuer nach billig** durch und **lösche** jede Kante, solange der Graph dabei zusammenhängend bleibt.

Das ist Kruskal von der anderen Seite: Kruskal *baut* nach der Regel „erzeuge keinen Zyklus" auf (maximal azyklisch), Reverse-Delete *reißt* nach der Regel „zerstöre den Zusammenhang nicht" ab (minimal zusammenhängend).

> [!note] In der Praxis selten benutzt: ein effizienter Zusammenhangstest ist aufwändig zu implementieren. Beste bekannte Laufzeit $O(E \log V (\log\log V)^3)$ [Thorup, 2000]. Im Skript nicht vertieft — kennen reicht.

***

## 9. 🔍 Durchgerechnetes Beispiel (Tafelgraph)

Graph mit Knoten $A,B,C,D,E$ und Kanten:
$AB{=}1,\; AC{=}2,\; AD{=}9,\; BC{=}6,\; BD{=}4,\; CD{=}5,\; CE{=}1,\; DE{=}7$.

**Kruskal** — Kanten aufsteigend, nimm wenn keine Zyklus-Gefahr:

| Kante | Gewicht | gleiche Insel? | Aktion |
|---|---|---|---|
| $CE$ | 1 | nein | ✅ nehmen → Inseln `{C,E}` |
| $AB$ | 1 | nein | ✅ nehmen → `{A,B}` |
| $AC$ | 2 | nein | ✅ nehmen → `{A,B,C,E}` |
| $BD$ | 4 | nein | ✅ nehmen → `{A,B,C,D,E}` — **fertig** (4 Kanten) |
| $CD$ | 5 | ja | ❌ Zyklus, überspringen |
| $BC,DE,AD$ | … | — | irrelevant, MST schon komplett |

**MST** $= \{AB, AC, BD, CE\}$, **Gewicht** $= 1+2+4+1 = \mathbf{8}$.

**Prim** ab $A$ — kommt über einen anderen Weg zum selben Baum:

$$A \xrightarrow{AB=1} B \;,\; A \xrightarrow{AC=2} C \;,\; C \xrightarrow{CE=1} E \;,\; B \xrightarrow{BD=4} D \quad\Rightarrow\quad \text{Gewicht } 8$$

> [!success] **Beobachtung:** Beide wählen die Kanten in **unterschiedlicher Reihenfolge** (Kruskal: $CE, AB, AC, BD$; Prim ab A: $AB, AC, CE, BD$), landen aber beim **selben MST** mit Gewicht 8 — weil hier alle relevanten Gewichte verschieden sind und der MST damit eindeutig ist. Das ist die Schnitteigenschaft bei der Arbeit.

***

## 10. Prim vs. Kruskal auf einen Blick

| | **Prim** | **Kruskal** |
|---|---|---|
| **Grundbild** | ein Baum wächst von einem Startknoten | viele Inseln verschmelzen |
| **Schnitt** | Baum vs. Rest | Insel von $v$ vs. Rest |
| **Reihenfolge** | leichteste Kante *aus dem Baum heraus* | alle Kanten global aufsteigend |
| **Schlüssel-Datenstruktur** | (indizierte) PriorityQueue | Sortierung + Union-Find |
| **Laufzeit** | $O(E\log V)$ (idx. PQ); $O(E+V\log V)$ (Fib.-Heap); $O(V^2)$ (Matrix) | $O(E \log E)$ (Sortieren dominiert) |
| **Speicher** | $O(V)$ bzw. $O(V+E)$ | $O(E)$ |
| **Gut wenn…** | dichter Graph (viele Kanten) | dünner Graph / Kanten schon sortiert |

> [!info] Beide sind **derselbe** generische Greedy-Ansatz — nur die Schnittwahl unterscheidet sich. Wenn du dich an *eine* Sache erinnerst: Prim wächst, Kruskal verschmilzt, und beide bauen in jedem Schritt eine minimal kreuzende Kante ein.

***

## 🤔 Verständnisfragen (erst selbst denken, dann aufklappen-Stil)

- **Wie viele Kanten hat ein (minimaler) Spannbaum — immer?** Ja, immer $V-1$.
- **Wie viele Baumkanten kreuzt ein Schnitt, der durch Entfernen *einer* Baumkante entsteht?** Genau eine — entfernt man eine Baumkante, zerfällt der Baum in zwei Teile, und nur diese eine Kante verband sie.
- **Muss die leichteste kreuzende Kante eines Schnitts im MST sein?** Ja — das ist exakt die Schnitteigenschaft.
- **Kann eine *nicht*-leichteste kreuzende Kante trotzdem im MST sein?** Ja — bezüglich eines *anderen* Schnitts kann sie dort die leichteste sein.

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Kernidee |
|---|---|
| **Gewichteter Graph $G=(V,E,g)$** | Kanten tragen Zahlen, damit man sie vergleichen kann |
| **Spannbaum** | verschwendungsfreies Gerüst, verbindet alle Knoten, $V-1$ Kanten |
| **MST** | das billigste solche Gerüst |
| **Schnitt** | Linie, die die Knoten in zwei Gruppen teilt |
| **Schnitteigenschaft** | die leichteste kreuzende Kante gehört garantiert in einen MST |
| **Generischer Greedy-Ansatz** | wiederholt eine garantierte Kante einbauen; nur die Schnittwahl variiert |
| **Union-Find** | macht Kruskals Zyklustest quasi-umsonst |

### Kernaussagen

- [p] **Schnitteigenschaft = das ganze Kapitel:** leichteste kreuzende Kante jedes Schnitts ist MST-sicher. Alles andere folgt daraus.
- [p] **Prim wächst, Kruskal verschmilzt** — aber beide sind derselbe Greedy-Ansatz, nur mit anderer Schnittwahl.
- [p] **Prim ≈ BFS** mit Min-PQ statt FIFO-Queue.
- [p] **Kruskal braucht Union-Find**, sonst wird der Zyklustest mit $O(VE)$ zu teuer; mit UF dominiert das Sortieren ($O(E\log E)$).
- [!] **Eindeutige Gewichte ⇒ eindeutiger MST.** Bei Gleichständen kann es mehrere geben.
- [!] **Kein Brute-Force:** $V^{V-2}$ Spannbäume (Cayley) — exponentiell.
- [c] **Falsch:** bei Prim die PQ-Kante ohne erneuten `marked`-Check verbauen → erzeugt Zyklen.
- [c] **Falsch:** Kruskal mit `parent`-Array während des Ablaufs — die Inseln haben noch keine Eltern/Kind-Struktur.

### Laufzeiten

| Algorithmus | Zeit | Speicher | Schlüssel |
|---|---|---|---|
| **Prim (einfache PQ)** | $O(E \log E)$ | $O(V+E)$ | PriorityQueue |
| **Prim (indizierte PQ)** | $O(E \log V)$ | $O(V)$ | IndexPQ |
| **Prim (Fibonacci-Heap)** | $O(E + V \log V)$ | $O(V+E)$ | Fibonacci-Heap |
| **Kruskal** | $O(E \log E)$ | $O(E)$ | Sortierung + Union-Find |
| **Reverse-Delete** | $O(E \log V (\log\log V)^3)$ | — | (komplex) |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.07 Graphen, Tiefen- & Breitensuche, Topologische Sortierung]]: ungewichtete Graphen & BFS — Prim ist im Kern BFS mit Min-PQ
- [[VL.03 Laufzeit, Tests, Datenstrukturen]]: PriorityQueue, indizierte PQ und Union-Find — die Bausteine von Prim und Kruskal
- [[VL.04 Backtracking & Gierige Algo]]: Greedy — hier ausnahmsweise beweisbar optimal (dank Schnitteigenschaft)
- **VL.09 (folgt):** kürzeste Wege in gewichteten Digraphen (Dijkstra, Bellman-Ford) — Dijkstra sieht Prim verblüffend ähnlich, optimiert aber Pfadlängen statt Kantengewichte
