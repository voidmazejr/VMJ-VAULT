**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]  
**Date:** 04-05-2026  
**Topics:** #Backtracking #Greedy #Permutationen #Rösselsprung #Sudoku #Baumsuche #DFS #BFS #Knapsack #TU-Berlin
**Link:** [[VL.04 AlgoDat.pdf]]

---

## 🎯 Lernziele der Vorlesung

VL.04 führt zwei fundamentale algorithmische Paradigmen ein: **Backtracking** als vollständige Suche im Baum der Teillösungen, und **Greedy** als direkte, gierige Optimalauswahl ohne Rücksetzen.

- **Backtracking-Bausteine**: Validitätstest, Kandidatengenerierung, Erweiterung, Undo
- **Permutationen**: Vollständige Aufzählung via Backtracking, Laufzeit $O(N!)$
- **Rösselsprung**: Backtracking mit echten Sackgassen; Warnsdorff-Heuristik
- **Generelles Backtrack-Prinzip**: Abstraktes rekursives Schema für alle Backtracking-Probleme
- **Sudoku**: Optimierungen durch Vorausschau & eingegrenzte Auswahl (MRV)
- **Bäume & Baumdurchsuchung**: Tiefensuche (DFS) vs. Breitensuche (BFS), Terminologie
- **Backtracking als DFS**: Warum Tiefensuche Speicher spart
- **Greedy-Paradigma**: Lokale Optimalität, Shortest Superstring, Knapsack-Varianten
- **Greedy auf Graphen**: Kruskal, Prim, Dijkstra, A* (Ausblick)

---

## 1. Einordnung: Algorithmenparadigmen

### Definition (Paradigmenübersicht)

Alle in diesem Kurs behandelten Paradigmen lassen sich als **Suche im Baum der Teillösungen** modellieren:

$$\boxed{\text{Lösungssuche} = \text{Traversierung eines Baums von Teillösungen}}$$

```
┌──────────────────────────────────────────────────────────────────┐
│              SUCHE IM BAUM DER TEILLÖSUNGEN                      │
│                                                                  │
│  Backtracking  →  vollständige DFS, Rücksetzen bei Sackgasse     │
│  Branch&Bound  →  DFS + Abschneiden hoffnungsloser Äste          │
│  Greedy        →  direkter Pfad, kein Rücksetzen                 │
│  Dyn. Prog.    →  überlappende Teilprobleme + Memoization        │
└──────────────────────────────────────────────────────────────────┘
```

**Vergleich der Paradigmen:**

| Paradigma | Strategie | Optimalität | Laufzeit (typisch) |
|---|---|---|---|
| **Backtracking** | Alle Äste, Rücksetzen | Vollständig (alle/eine Lösung) | $O(k^N)$ oder $O(N!)$ |
| **Branch & Bound** | Abschneiden nach Schranken | Optimal | Besser als reines Backtracking |
| **Greedy** | Lokal bestes Element, kein Undo | Problemabhängig | Meist $O(N \log N)$ |
| **Dynamische Programmierung** | Memoization, Bottom-Up | Optimal | Polynomiell |

---

## 2. Backtracking – Grundprinzip

### Definition

$$\boxed{
\text{Backtracking} = \text{Schrittweise Generierung von Teillösungen; bei Misserfolg: Rückschritt zum letzten Verzweigungspunkt}
}$$

> 💡 **Merkhilfe:** Backtracking = „Ausprobieren + Zurückgehen" – wie ein Labyrinth mit Gedächtnis. Man läuft immer weiter, bis man nicht mehr weiterkommt, und kehrt dann zum letzten Abzweig zurück.

### Was brauchen wir?

Jedes Backtracking-Problem benötigt exakt diese Bausteine:

- **Validitätstest** – Ist die (Teil-)Lösung gültig? (`true`/`false`)
- **Kandidatengenerierung** – Alle zulässigen nächsten Schritte aufzählen
- **Anfangslösung** – Startpunkt (meistens: leere Teillösung)
- **Erweiterung** – Teillösung um einen Schritt ausbauen (`doMove`)
- **Rückgängigmachen** – Letzten Schritt zurücknehmen (`undoMove`)
- **Orchestrierung** – Meist Rekursion, da `undo` damit trivial ist (Stack-Frame wird verlassen)

⚠️ **Achtung:** Es gibt immer nur **eine** aktuelle Teillösung im Speicher. Das ist der entscheidende Vorteil gegenüber der Breitensuche, die viele Teillösungen parallel halten müsste.

### Generelles Backtracking-Schema

```pseudocode
backtracking(k):
  if isSolution(k):
    processSolution()           // Lösung gefunden → verarbeiten
    return
  candidates ← generateCandidates(k)
  for each c in candidates:
    makeMove(c)                 // Teillösung um c erweitern
    backtracking(k + 1)         // rekursiv tiefer gehen
    undoMove(c)                 // Schritt rückgängig machen
```

---

## 3. Beispiel: Aufzählung aller Permutationen

### Problem

Alle Permutationen der Zahlen $0, 1, \ldots, N{-}1$ aufzählen. Jede Zahl darf nur einmal vorkommen.

- **Teillösung**: Sequenz der bisher gewählten Zahlen (Länge $< N$)
- **Vollständige Lösung**: Sequenz der Länge $N$
- ✅ Jede Teillösung ist immer erweiterbar (keine echten Sackgassen!)

### Ablauf für $N = 3$ (Baum der Teillösungen)

```
                     []
              /       |       \
           [0]       [1]       [2]
          /   \     /   \     /   \
       [0,1] [0,2] [1,0][1,2][2,0][2,1]
         |     |     |    |    |    |
      [0,1,2][0,2,1][1,0,2][1,2,0][2,0,1][2,1,0]
        ✅    ✅     ✅    ✅    ✅    ✅
```

**Schritt-für-Schritt-Ablauf:**

```
Schritt 1: [] → wähle 0 → [0]
Schritt 2: [0] → wähle 1 → [0,1]
Schritt 3: [0,1] → wähle 2 → [0,1,2]  ✅ Lösung!
Schritt 4: Backtrack → zurück zu [0,1], keine Kandidaten mehr
Schritt 5: Backtrack → zurück zu [0], wähle 2 → [0,2]
Schritt 6: [0,2] → wähle 1 → [0,2,1]  ✅ Lösung!
... (analog für Äste [1,...] und [2,...])
```

### Java-Implementierung

```java
public class Permutations {
    private int N;
    private int[] a;

    public Permutations(int N) {
        this.N = N;
        a = new int[N];
        backtracking(0);
    }

    // Kandidatenliste: Zahlen, die noch nicht benutzt wurden
    public Iterable<Integer> candidateList(int k) {
        LinkedList<Integer> c = new LinkedList<>();
        boolean[] used = new boolean[N];
        for (int i = 0; i < k; i++) used[a[i]] = true;
        for (int i = 0; i < N; i++) if (!used[i]) c.add(i);
        return c;
    }

    public void backtracking(int k) {
        if (k == N) {
            printSolution();           // ✅ Lösung gefunden
        } else {
            for (Integer c : candidateList(k)) {
                a[k] = c;              // makeMove
                backtracking(k + 1);  // rekursiv weiter
                // undoMove implizit: a[k] wird beim nächsten c überschrieben
            }
        }
    }

    public void printSolution() {
        for (int i : a) System.out.print(i + " ");
        System.out.println();
    }
}
```

### Laufzeitanalyse Permutationen

| Ebene | Knoten | Verzweigungen |
|---|---|---|
| 0 (Wurzel) | 1 | $N$ |
| 1 | $N$ | $N-1$ |
| 2 | $N(N-1)$ | $N-2$ |
| $\vdots$ | $\vdots$ | $\vdots$ |
| $N$ (Blätter) | $N!$ | 0 |

$$\boxed{T(N) \in O(N!)}$$

⚠️ **Achtung:** $N! \gg 2^N$ für große $N$ – Backtracking über alle Permutationen ist extrem teuer.

---

## 4. Beispiel: Rösselsprung

### Problem

Gegeben ein $n \times n$-Schachbrett mit einem Springer: Finde eine Zugfolge, bei der **jedes Feld genau einmal besucht** wird.

- **Geschlossener Rösselsprung**: Endposition = Startposition
- ✅ Für alle $n \geq 5$ existieren Lösungen. Für $n < 5$: ❌ keine Lösung.

### Unterschied zu Permutationen

| Merkmal | Permutationen | Rösselsprung |
|---|---|---|
| Sackgassen möglich? | ❌ Nein – immer erweiterbar | ✅ Ja – alle Felder blockiert |
| Backtracking-Auslöser | Nur wenn Lösung vollständig | Auch bei leerer Kandidatenliste |
| Ziel | **Alle** Lösungen | **Eine** Lösung reicht |
| Kandidatengenerierung | Unbenutzte Zahlen | Gültige Springerzüge |

### Benötigte Klassen

```
Position  →  (x, y) auf dem Brett
Move      →  ein Springerzug (Δx, Δy)
Board     →  Spiellogik + alle Backtracking-Methoden
  ├── validMoves()    – mögliche Züge generieren
  ├── isSolved()      – ist jedes Feld genau einmal besucht?
  ├── doMove(move)    – Zug ausführen, Feld markieren
  └── undoMove(move)  – Zug zurücknehmen, Feld entmarkieren
```

### Pseudocode: Rösselsprung-Backtracking

```pseudocode
backtracking(board):
  if board.isSolved():
    printSolution(board)
    return true                    // eine Lösung gefunden → abbrechen
  for move in board.validMoves():
    board.doMove(move)             // Zug ausführen
    if backtracking(board):
      return true                  // Lösung weiterpropagieren
    board.undoMove(move)           // ❌ kein Erfolg → Rücksetzen
  return false                     // Sackgasse
```

### Schritt-für-Schritt-Beispiel (Anfang, 5×5)

```
Startfeld: (0,0)   Springer-Züge: (±1,±2) und (±2,±1)

Zug 1: (0,0) → (1,2)
  S . . . .
  . . . . .
  . S . . .
  . . . . .
  . . . . .

Zug 2: (1,2) → (0,4)
  S . . . .
  . . . . .
  . S . . .
  . . . . .
  S . . . .

→ falls Sackgasse: undoMove() zurück bis zum letzten offenen Ast
```

### Warnsdorff-Heuristik (Effizienz-Optimierung)

$$\boxed{\text{Wähle als nächsten Zug das Feld mit den \textbf{wenigsten} Folgemöglichkeiten.}}$$

> 💡 **Rolle:** Keine Garantie für Korrektheit, aber drastische Reduktion des Suchraums. Ohne Heuristik: exponentiell. Mit Warnsdorff: meist in $O(N^2)$ lösbar.

> 💡 **Intuition:** „Besuche zuerst die schlechtesten Felder" – Randfelder haben weniger Züge, später sind sie schwer erreichbar.

---

## 5. Generelles Backtrack-Prinzip

### Kanonische Form

$$\boxed{
\texttt{backtracking(k):} \quad
\begin{cases}
\texttt{processSolution()} & \text{falls } \texttt{isSolution(k)} \\
\forall c \in \texttt{candidates(k)}: \texttt{make} \to \texttt{recurse} \to \texttt{undo} & \text{sonst}
\end{cases}
}$$

```pseudocode
backtracking(k):
  if isSolution(k):
    processSolution()
    return
  for each candidate c in generateCandidates(k):
    makeMove(c)           // Teillösung erweitern
    backtracking(k + 1)   // in die Tiefe
    undoMove(c)           // Schritt zurücknehmen (Backtrack!)
```

### Variationen nach Ziel

| Ziel | Anpassung |
|---|---|
| **Alle Lösungen** | `processSolution()` speichert, danach weiter in der Schleife |
| **Eine Lösung** | `return true` nach erster Lösung, nach oben propagieren |
| **Optimale Lösung** | Lösung speichern + mit bisherigem Besten vergleichen |

### Verschiedene Teillösungsgenerierungen (Damenproblem, $n=8$)

| Methode | Kandidaten für $n=8$ | Beschreibung |
|---|---|---|
| Alle Platzierungen | $\binom{64}{8} = 4.426.165.368$ | Beliebige 8 Felder |
| Eine Dame pro Spalte | $n^n = 16.777.216$ | Spaltenweise |
| Permutationen der Zeilen | $n! = 40.320$ | Eine Dame pro Zeile & Spalte |
| Mit Symmetrieausnutzung | $92$ | Nur freie Lösungen |

✅ **Fazit:** Smarte Kandidatengenerierung = entscheidend. Faktor $\approx 48.000.000\times$ weniger Knoten!

---

## 6. Beispiel: Sudoku

### Problem

$9 \times 9$-Gitter, aufgeteilt in $3 \times 3$-Blöcke. Jede Zeile, jede Spalte und jeder Block enthält die Ziffern $1$–$9$ genau einmal.

### Backtracking-Abbildung

| Backtracking-Element | Sudoku-Entsprechung |
|---|---|
| Teillösung | Bisher belegte Kästchen |
| Kandidaten für Schritt $k$ | Ziffern, die in Zeile, Spalte, Block noch fehlen |
| Teillösung vollständig? | Alle 81 Felder gefüllt |
| Schritt ausführen | Ziffer in Kästchen speichern |
| Schritt rückgängig | Ziffer aus Kästchen löschen |

### Optimierungsstufen

**Basisvariante:** Nimm immer das erste leere Kästchen (der Reihe nach).

**Verbesserung 1 – Vorausschauende Kandidatenmenge:**
> Falls für *irgendeines* der noch leeren Kästchen keine gültigen Kandidaten existieren → sofort leere Kandidatenliste zurückgeben. Ast wird nicht weiter expandiert.

**Verbesserung 2 – Eingegrenzte Auswahl (MRV):**
> Wähle als nächstes Kästchen immer dasjenige mit den **wenigsten** gültigen Kandidaten (Minimum Remaining Values). Kombiniert mit Verbesserung 1.

### Effizienzvergleich (Anzahl benötigter Lösungsschritte)

| Auswahlmethode | Leichtes Rätsel | Mittleres Rätsel | Schweres Rätsel |
|---|---|---|---|
| Der Reihe nach | 1.904 | 832.863 | ❌ terminiert nicht |
| + Vorausschau | 127 | 142 | 12.507.212 |
| + Eingegrenzt + Vorausschau | 48 | 65 | 10.374 |

✅ **Fazit:** Kombination beider Optimierungen = Faktor $> 1000$ schneller bei schweren Rätseln!

---

## 7. Einschub: Bäume und Baumdurchsuchung

### Definition (Baum)

$$\boxed{
\text{Baum} = \text{Azyklischer, zusammenhängender Graph mit ausgezeichneter Wurzel und Nachfolgerrelation}
}$$

**Wichtige Begriffe:**

- **Wurzel**: Ausgezeichneter Knoten ohne Vorgänger
- **Blatt**: Knoten ohne Nachfolger
- **Innerer Knoten**: Knoten mit mindestens einem Nachfolger
- **Pfad**: Folge $v_0, v_1, \ldots, v_k$ mit $v_{i+1}$ Nachfolger von $v_i$
- **Tiefe** eines Knotens: Länge des Pfades von der Wurzel
- **Höhe** des Baumes: Maximale Tiefe aller Blätter

### ASCII-Diagramm: Baum-Terminologie

```
            A          ← Wurzel (Tiefe 0)
           / \
          B   C        ← innere Knoten (Tiefe 1)
         / \   \
        D   E   F      ← Blätter (Tiefe 2)

Höhe des Baumes = 2
Pfad A→C→F hat Länge 2
```

### Tiefensuche (DFS) vs. Breitensuche (BFS)

| Eigenschaft | Tiefensuche (DFS) | Breitensuche (BFS) |
|---|---|---|
| **Richtung** | Erst in die Tiefe | Erst in die Breite |
| **Datenstruktur** | Stack (implizit: Rekursion) | Queue (explizit) |
| **Besuchsreihenfolge** | A→B→D→E→C→F | A→B→C→D→E→F |
| **Speicherbedarf** | $O(\text{Höhe})$ | $O(\text{max. Breite})$ |
| **Backtracking nutzt** | ✅ DFS | ❌ BFS (zu viel Speicher) |
| **Kürzeste Wege (ungew.)** | ❌ | ✅ |

```
DFS:                         BFS:
A → B → D (Blatt)            Ebene 0: A
    ↑ backtrack              Ebene 1: B, C
    E (Blatt)                Ebene 2: D, E, F
    ↑ backtrack
C → F (Blatt)
```

> 💡 **Merkhilfe:** DFS = „Taucher" (so tief wie möglich zuerst); BFS = „Wellen" (Ebene für Ebene).

---

## 8. Backtracking als Suche im Baum der Teillösungen

### Der Baum der Teillösungen

$$\boxed{
\text{Knoten} = \text{Teillösung}, \quad \text{Kante} = \text{Auswahlschritt}, \quad \text{Blatt} = \text{Vollständige Lösung oder Sackgasse}
}$$

```
Teillösungsbaum für Permutationen N=3:

                   []
             /      |      \
           [0]     [1]     [2]
           / \     / \     / \
        [0,1][0,2][1,0][1,2][2,0][2,1]
          |    |    |    |    |    |
         ✅   ✅   ✅   ✅   ✅   ✅
       ← Lösungen nur an den Blättern →
```

### Warum Backtracking immer DFS verwendet

```
┌─────────────────────────────────────────────────────┐
│  DFS (Backtracking):                                │
│  Speicher = O(Tiefe) = nur aktueller Pfad           │
│  → immer nur EINE Teillösung im Speicher ✅         │
│                                                     │
│  BFS (Alternative):                                 │
│  Speicher = O(Knotenanzahl pro Ebene)               │
│  → bei N=10, k=10 Kandidaten: 10^10 Knoten ❌       │
└─────────────────────────────────────────────────────┘
```

### Effizienz-Varianten des Backtrackings

| Variante | Idee | Beispiel |
|---|---|---|
| **Pruning (Abschneiden)** | Teillösung bereits ungültig → Ast nicht expandieren | Sudoku: Kästchen ohne Kandidaten |
| **Heuristik** | Aussichtsreichste Kinder zuerst wählen | Warnsdorff beim Rösselsprung |
| **Symmetrie** | Äquivalente Teillösungen nur einmal betrachten | Damenproblem: Spiegelungen |
| **Branch & Bound** | Obere/untere Schranken berechnen, schlechte Äste kappen | 0/1-Knapsack |

---

## 9. Greedy-Algorithmen

### Definition

$$\boxed{
\text{Greedy} = \text{Schrittweise Wahl des lokal besten Kandidaten, ohne spätere Revision}
}$$

> 💡 **Analogie:** Beim Buffet immer das beste verfügbare Stück nehmen – ohne zurückzugehen. Manchmal optimal, manchmal nicht.

**Wichtiger Unterschied zu Backtracking:** Greedy macht **keine** `undoMove()`-Schritte. Jede Wahl ist endgültig.

### Generelles Greedy-Schema

```pseudocode
greedy(problem):
  solution ← leer
  while solution noch unvollständig:
    candidate ← besterKandidat(problem, solution)   // lokale Optimierung
    if candidate ist zulässig:
      solution.add(candidate)                        // endgültige Entscheidung
  return solution
```

### Beispiel: Shortest Superstring

**Problem:** Finde den kürzesten String, der alle gegebenen Strings als Teilstring enthält.

**Greedy-Strategie:** In jedem Schritt das Paar mit der **größten Überlappung** zusammenführen.

**Schritt-für-Schritt:**

```
Eingabe: catgc | ctaagt | gcta | ttca | atgcatc
Gesamtlänge: 26

Schritt 1: catgc + atgcatc → Überlappung "atgc" (Länge 4)
           → catgcatc

Schritt 2: gcta + ctaagt → Überlappung "cta" (Länge 3)
           → gctaagt

Schritt 3: ttca + catgcatc → Überlappung "tca" (Länge 3)
           → ttcatgcatc

Schritt 4: ttcatgcatc + gctaagt → Überlappung "t" ?
           → gctaagttcatgcatc  (Länge 16)

Ergebnis: gctaagttcatgcatc  ← 16 statt 26 Zeichen ✅
```

⚠️ **Greedy ist hier nicht immer optimal!** Gegenbeispiel:

```
Eingabe: abcd, cdef, fabc, efab

Greedy:
  efab + abcd → efabcd  (Überlappung "ab")
  efabcd + cdef → efabcdcdef (Überlappung "cd")
  Ergebnis: Länge 10 ❌

Optimal:
  fabc + abcdef → ... → fabcdefab  Länge 9 ✅
```

### Das Knapsack-Problem

**Problem:** Gegeben $n$ Objekte mit Wert $v_i$ und Gewicht $w_i$, sowie Kapazität $W$. Maximiere den Gesamtwert.

$$\boxed{\max \sum_{i=1}^{n} v_i \cdot x_i \quad \text{unter der Bedingung} \quad \sum_{i=1}^{n} w_i \cdot x_i \leq W}$$

**Varianten und Lösbarkeit:**

| Variante | $x_i$ | NP-vollständig? | Greedy optimal? | Lösungsansatz |
|---|---|---|---|---|
| **0/1 Knapsack** | $\{0, 1\}$ | ✅ Ja | ❌ Nein | Dyn. Prog. / Branch & Bound |
| **Bounded Knapsack** | $\{0,\ldots,b_i\}$ | ✅ Ja | ❌ Nein | Dynamische Programmierung |
| **Unbounded Knapsack** | $\mathbb{N}$ | ✅ Ja | ❌ Nein | Dynamische Programmierung |
| **Teilbares Knapsack** | $[0,1]$ (Bruchteil) | ❌ Nein | ✅ Ja | Greedy nach $v_i/w_i$ |

> 💡 **Merkhilfe:** Nur wenn Objekte **teilbar** sind, führt Greedy (sortiert nach Dichte $v_i/w_i$, absteigend) zur Optimallösung.

**NP-Vollständigkeit des 0/1-Knapsacks:**
- Entscheidungsversion (Wert $\geq V$ erreichbar?) ist **NP-vollständig**
- Es gibt keinen bekannten polynomiellen Algorithmus
- Aber: **Pseudo-polynomieller** DP-Algorithmus in $O(n \cdot W)$
- Sowie ein **FPTAS** (Fully Polynomial-Time Approximation Scheme)

### Greedy auf Graphen (Ausblick)

| Algorithmus | Greedy-Kriterium | Problem |
|---|---|---|
| **Kruskal** | Leichteste Kante ohne Zyklus | Minimaler Spannbaum |
| **Prim** | Leichteste Kante zum aktuellen Baum | Minimaler Spannbaum |
| **Dijkstra** | Unbesuchter Knoten mit kleinstem Abstand | Kürzeste Wege |
| **A\*** | Dijkstra + Heuristikfunktion $h(v)$ | Heuristisch geführte Suche |

---

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Backtracking** | DFS durch Baum der Teillösungen; immer nur eine Teillösung im Speicher |
| **Pruning** | Ungültige Äste früh abschneiden → enorme Effizienzgewinne |
| **DFS vs. BFS** | Backtracking verwendet DFS: $O(\text{Tiefe})$ Speicher statt $O(\text{Breite})$ |
| **Warnsdorff-Heuristik** | Feld mit wenigsten Folgemöglichkeiten zuerst besuchen |
| **MRV-Heuristik** | Kästchen mit wenigsten Kandidaten zuerst wählen (Sudoku) |
| **Greedy** | Lokal optimale Wahl ohne Rücksetzen; nicht immer global optimal |
| **Teilbares Knapsack** | Einzige Knapsack-Variante, die Greedy optimal löst |

### Kernaussagen

✅ **Backtracking** speichert immer nur eine Teillösung → $O(\text{Tiefe})$ Speicher  
✅ **Pruning** kann exponentiell viele Knoten einsparen  
✅ **Greedy** ist effizient ($O(N \log N)$), aber Optimalität muss bewiesen werden  
⚠️ **Achtung:** Greedy beim 0/1-Knapsack liefert **keine** garantiert optimale Lösung  
❌ **Falsch:** „Backtracking und BFS sind gleichwertig" – BFS braucht exponentiell mehr Speicher  

### Wichtige Algorithmen und Formeln

| Algorithmus / Formel | Laufzeit | Anwendung |
|---|---|---|
| **Backtracking (Permutationen)** | $O(N!)$ | Vollständige Aufzählung |
| **Backtracking (allgemein)** | $O(k^N)$ | $k$ Kandidaten pro Schritt |
| **Greedy Teilbares Knapsack** | $O(N \log N)$ | Sortieren nach $v_i/w_i$ |
| **Knapsack (0/1, DP)** | $O(N \cdot W)$ | Pseudo-polynomiell |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.03 Laufzeit, Tests, Datenstrukturen]]: Priority Queue & Union-Find werden von Greedy-Graphalgorithmen (Dijkstra, Kruskal) benötigt
- [[VL.05 Branch-&-Bound, Minimax & Alpha-Beta Suche]]: Fortsetzung: Intervallauswahl, Intervallverteilung, Scheduling mit formalen Optimalitätsbeweisen
- [[VL.05 Branch-&-Bound, Minimax & Alpha-Beta Suche]]: Verfeinerung von Backtracking mit Schranken für das 0/1-Knapsack-Problem
- [[VL.06 Dynamisches Programmieren]]: Optimale Lösung für 0/1-Knapsack, gewichtete Intervallauswahl, Editierdistanz
