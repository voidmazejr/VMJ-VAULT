**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]
**Type:** Anki-Karten-Entwurf
**Quelle:** [[VL.08 Minimale Spannbäume]]
**Topics:** #Anki #MST #Prim #Kruskal #Schnitteigenschaft

> [!note] Entwurf zum Übertragen in Anki. **Basic** = Front/Back. **Cloze** = Lückentext ({{c1::...}}). Bewusst atomar gehalten — eine Karte, eine Tatsache. Bei den Beweisen wird *pro Schritt* gefragt, nicht der ganze Beweis am Stück.

***

## 1. Grundbegriffe

| # | Typ | Front | Back |
|---|---|---|---|
| 1 | Basic | Was ist ein **gewichteter Graph** (formal)? | Tupel $G=(V,E,g)$ mit Gewichtsfunktion $g: E \to \mathbb{R}$; $g(v,w)$ = Gewicht der Kante $(v,w)$. Negative Gewichte erlaubt, wenn nicht ausgeschlossen. |
| 2 | Basic | Was sind **Inzidenzlisten** und wieso werden sie bei gewichteten Graphen statt Adjazenzlisten benutzt? | Listen der inzidenten **Kanten** (statt Nachbarknoten) pro Knoten — weil pro Kante das Gewicht gespeichert werden muss. Ungerichtet: jede Kante doppelt gespeichert. |
| 3 | Basic | Was ist ein **Spannbaum** von $G$? | Teilgraph, der **alle** Knoten enthält und ein **Baum** ist (zusammenhängend + zyklenfrei). |
| 4 | Basic | Was ist ein **minimaler Spannbaum (MST)**? | Spannbaum mit minimalem Gesamtgewicht; Gewicht = Summe der Kantengewichte. |
| 5 | Cloze | Jeder Spannbaum mit $V$ Knoten hat genau {{c1::$V-1$}} Kanten. | — |
| 6 | Basic | Wie viele Spannbäume hat ein vollständiger Graph mit $V$ Knoten? Wie heißt die Formel? | $V^{\,V-2}$ — **Cayleys Formel**. (Begründet, warum Brute-Force unmöglich ist.) |
| 7 | Basic | Wann ist der MST **eindeutig**? | Wenn alle Kantengewichte **verschieden** sind (dann ist jede minimal kreuzende Kante eindeutig). |

## 2. Äquivalente Spannbaum-Bedingungen

| # | Typ | Front | Back |
|---|---|---|---|
| 8 | Basic | Nenne die zwei „extremen" äquivalenten Spannbaum-Charakterisierungen. | **Maximal azyklisch** (Hinzufügen *irgendeiner* Kante erzeugt Zyklus) und **minimal zusammenhängend** (Entfernen *irgendeiner* Kante zerstört Zusammenhang). |
| 9 | Basic | An welcher Bedingung orientieren sich **Kruskal** bzw. **Reverse-Delete**? | Kruskal: maximal azyklisch (keine Zyklen erzeugen). Reverse-Delete: minimal zusammenhängend (Zusammenhang nicht zerstören). |

## 3. Schnitt & Schnitteigenschaft

| # | Typ | Front | Back |
|---|---|---|---|
| 10 | Basic | Was ist ein **Schnitt** durch einen Graphen? | Eine Teilmenge $S \subseteq V$, sodass $S$ und $V-S$ **beide nicht-leer** sind. |
| 11 | Basic | Was ist eine **kreuzende Kante**, was eine **minimal kreuzende Kante**? | Kreuzend: ein Endknoten in $S$, einer in $V-S$. Minimal kreuzend: kreuzende Kante mit minimalem Gewicht (kann mehrere geben). |
| 12 | Cloze | **Schnitteigenschaft:** Für jeden beliebigen Schnitt enthält jeder MST {{c1::eine der minimal kreuzenden Kanten}} dieses Schnitts. | — |
| 13 | Basic | Beweis Schnitteigenschaft — **Schritt 1**: Was nimmt man an? | Es gebe einen MST, der **keine** minimal kreuzende Kante $(v,w)$ des Schnitts enthält. |
| 14 | Basic | Beweis Schnitteigenschaft — **Schritt 2**: Was passiert beim Hinzufügen von $(v,w)$? | Es entsteht ein **Zyklus** (MST verbindet schon alle Knoten); dieser Zyklus enthält eine *weitere* kreuzende Kante $(t,u)$. |
| 15 | Basic | Beweis Schnitteigenschaft — **Schritt 3**: Wie folgt der Widerspruch? | Entferne $(t,u)$ → wieder Spannbaum. Da $g(v,w)<g(t,u)$, ist er **leichter** → Widerspruch zur MST-Annahme. |

## 4. Generischer Greedy-Ansatz

| # | Typ | Front | Back |
|---|---|---|---|
| 16 | Basic | Beschreibe den **generischen Greedy-Ansatz** für den MST. | Solange $ME$ kein Spannbaum: wähle einen Schnitt, dessen kreuzende Kanten alle nicht in $ME$ liegen, und füge eine **minimal kreuzende Kante** hinzu. |
| 17 | Basic | Was bleibt im generischen Ansatz offen — und wie hängt das mit Prim/Kruskal zusammen? | Die **Wahl des Schnitts $S$**. Genau hier unterscheiden sich Prim, Kruskal und Reverse-Delete; alle drei sind Spezialfälle. |
| 18 | Basic | Was, wenn $G$ **nicht zusammenhängend** ist? | Algorithmen auf die Zusammenhangskomponenten anwenden → man erhält einen minimalen **Spannwald**. |

## 5. Prim

| # | Typ | Front | Back |
|---|---|---|---|
| 19 | Basic | Idee von **Prims Algorithmus**? | Baum von einem Startknoten aus wachsen lassen; in jedem Schritt die minimal kreuzende Kante bzgl. des **markierten Bereichs** wählen, bis $V-1$ Kanten gewählt sind. |
| 20 | Basic | Womit ist Prim verwandt, und worin unterscheidet es sich? | Ähnlich zur **BFS** (markierter Bereich wächst). Unterschied: BFS nimmt den am längsten wartenden Knoten, Prim den über die **leichteste Kante** erreichbaren. |
| 21 | Basic | Warum prüft Prim beim `poll()` aus der PQ erneut `if (!marked[w])`? | Eine Kante in der PQ kann inzwischen **keine kreuzende Kante mehr** sein (beide Knoten markiert) → sie muss verworfen werden. |
| 22 | Cloze | Prim mit einfacher PQ: Laufzeit {{c1::$O(E \log E)$}}, Speicher {{c2::$O(V+E)$}}. | — |
| 23 | Cloze | Prim mit **indizierter** PQ: Laufzeit {{c1::$O(E \log V)$}}, Speicher {{c2::$O(V)$}}. | — |
| 24 | Basic | Welche Beobachtung erlaubt die indizierte-PQ-Verbesserung bei Prim? | Pro Knoten genügt die **kürzeste** ankommende kreuzende Kante → PQ-Länge sinkt von $E$ auf $V$. |
| 25 | Basic | Prim mit Fibonacci-Heap: Laufzeit? | $O(E + V \log V)$ [Fredman & Tarjan, 1987]. |

## 6. Kruskal & Reverse-Delete

| # | Typ | Front | Back |
|---|---|---|---|
| 26 | Basic | Idee von **Kruskals Algorithmus**? | Kanten **aufsteigend** nach Gewicht durchlaufen; eine Kante übernehmen, wenn sie **keinen Zyklus** mit den bisher gewählten bildet. |
| 27 | Basic | Warum braucht Kruskal **Union-Find**? | Der Zyklustest ("liegen $v,w$ schon in derselben Komponente?") läuft $E$-mal. Naiv mit DFS wäre es $O(VE)$ — zu langsam. Union-Find macht ihn quasi-konstant. |
| 28 | Basic | Was ist die Zyklus-Bedingung im Kruskal-Pseudocode? | `if UF.find(v) ≠ UF.find(w)` → verschiedene Komponenten → kein Zyklus → `union(v,w)` und Kante zum MST. |
| 29 | Cloze | Kruskal: Laufzeit {{c1::$O(E \log E)$}} (dominiert vom Sortieren der Kanten), Speicher {{c2::$O(E)$}}. | — |
| 30 | Basic | Warum kann Kruskal — anders als Prim — **kein `parent`-Array** beim Ablauf nutzen? | Kruskal baut einen **Wald** aus verschmelzenden Teilbäumen; beim Auswählen einer Kante steht noch nicht fest, wer Eltern- und wer Kindknoten wird. |
| 31 | Basic | Idee des **Reverse-Delete**-Algorithmus? | Kanten **absteigend** nach Gewicht durchlaufen und löschen, solange der Graph dadurch nicht unzusammenhängend wird. |

## 7. Synthese

| # | Typ | Front | Back |
|---|---|---|---|
| 32 | Basic | Was haben Prim und Kruskal grundsätzlich gemeinsam? | Beide sind **Greedy** und **Spezialfälle desselben generischen Ansatzes**; sie unterscheiden sich nur in der Reihenfolge/Art der Schnittwahl. |
| 33 | Basic | Wie groß ist der Schnitt, der durch Entfernen **einer** Baumkante eines Spannbaums entsteht? | Der Baum zerfällt in genau **zwei** Komponenten → der Schnitt wird von **genau einer** Baumkante gekreuzt. |
| 34 | Basic | Kann eine *nicht*-minimale kreuzende Kante eines Schnitts im MST liegen? | Ja — sie kann bezüglich eines **anderen** Schnitts minimal kreuzend sein. |
