**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]
**Date:** 11-05-2026
**Topics:** #Minimax #AlphaBeta #Negamax #BranchAndBound #Spielbaum #Rucksackproblem #Optimierung
**Link:** 

***

## 🎯 Lernziele der Vorlesung

Minimax, Alpha-Beta-Suche und Branch-and-Bound sind Verfahren zur exakten Entscheidungsfindung in Spielbäumen und Optimierungsproblemen. Sie erkunden Lösungsräume systematisch, schneiden aber durch Schranken aussichtslose Äste ab – ohne dabei das optimale Ergebnis zu verlieren.

- **Minimax-Verfahren**: Optimale Strategie für Zwei-Spieler-Nullsummenspiele durch rekursiv alternierende Max/Min-Auswahl bestimmen.
- **Alpha-Beta-Suche**: Beschneidung irrelevanter Spielbaum-Äste über Schranken $\alpha$ und $\beta$, ohne das Minimax-Ergebnis zu verändern.
- **Negamax**: Elegante Variante von Alpha-Beta, die beide Spieler symmetrisch mit einer einzigen Funktion behandelt.
- **Branch-and-Bound**: Erkundung des Entscheidungsbaums für Optimierungsprobleme mit Upper- und Lower-Bounds.
- **Upper Bound / Lower Bound**: Verstehen, wie Schranken den Suchraum einengen und wann Teillösungen sicher verworfen werden dürfen.
- **0/1-Rucksackproblem**: Branch-and-Bound konkret auf ein NP-vollständiges Optimierungsproblem anwenden.

***

## 1. Minimax-Verfahren

### Definition: Spielmodell

Das Minimax-Verfahren modelliert Zwei-Spieler-Nullsummenspiele: Spieler **A maximiert**, Spieler **B minimiert** das Ergebnis. Beide spielen **optimal**.

$$\boxed{
\operatorname{Minimax}(s) =
\begin{cases}
\operatorname{score}(s) & \text{falls } s \text{ Endknoten} \\
\max\limits_{s' \in \operatorname{Nachf.}(s)} \operatorname{Minimax}(s') & \text{falls A am Zug} \\
\min\limits_{s' \in \operatorname{Nachf.}(s)} \operatorname{Minimax}(s') & \text{falls B am Zug}
\end{cases}
}$$

**Wichtige Begriffe:**
- **Max-Knoten**: Knoten, an dem A zieht – wählt den größten Nachfolgerwert.
- **Min-Knoten**: Knoten, an dem B zieht – wählt den kleinsten Nachfolgerwert.
- **Bewertungsfunktion** `score()`: Ordnet Endzuständen einen numerischen Wert zu.
- **Vollständige Minimax-Suche**: Suche bis zu allen Blattknoten (Endzuständen).
- **Unvollständige Minimax-Suche**: Abbruch bei Tiefenlimit + heuristische Positionsbewertung.
- **Ruhesuche (Quiescence Search)**: Verlängerung über das Tiefenlimit hinaus, solange Bewertungen stark schwanken (z. B. bei Schlagabtausch).

**Rolle:** Minimax ist das spieltheoretische Grundprinzip – A fragt immer „Wie groß kann ich das Ergebnis mindestens machen?", B fragt „Wie klein kann ich es mindestens halten?".

⚠️ **Achtung:** Bei komplexen Spielen wie Schach ist vollständige Minimax-Suche unpraktikabel, da der Spielbaum exponentiell groß wird.

### Algorithmus

```pseudocode
MinimaxA(Zustand):
1. if Zustand ist Endzustand then
2.     return score(Zustand)
3. best ← -∞
4. for jeder erlaubte Zug z do
5.     führe z aus
6.     wert ← MinimaxB(Zustand)
7.     mache z rückgängig
8.     if wert > best then best ← wert
9. return best

MinimaxB(Zustand):
1. if Zustand ist Endzustand then
2.     return score(Zustand)
3. best ← +∞
4. for jeder erlaubte Zug z do
5.     führe z aus
6.     wert ← MinimaxA(Zustand)
7.     mache z rückgängig
8.     if wert < best then best ← wert
9. return best
```

### Implementierung (Java)

```java
public int scorePlayerA() {
    if (game.isFinal()) return game.score();
    int maxScore = Integer.MIN_VALUE;
    for (int move : Game.moves) {
        game.doMove(move);
        int score = scorePlayerB();
        game.undoMove(move);
        if (score > maxScore) maxScore = score;
    }
    return maxScore;
}

public int scorePlayerB() {
    if (game.isFinal()) return game.score();
    int minScore = Integer.MAX_VALUE;
    for (int move : Game.moves) {
        game.doMove(move);
        int score = scorePlayerA();
        game.undoMove(move);
        if (score < minScore) minScore = score;
    }
    return minScore;
}
```

### Schritt-für-Schritt Beispiel: BestDifference

Zahlenfolge `[2, 8, 3, 5, 4, 1]`. A und B ziehen abwechselnd von links oder rechts. `score() = values[first] - values[last]`.

```
Ausgangszustand:
[2, 8, 3, 5, 4, 1]
A ist am Zug (Max-Knoten)

Schritt 1: A betrachtet linken Zug (nimmt 2).
           B ist am Zug → [8, 3, 5, 4, 1]

Schritt 2: B betrachtet rechten Zug (nimmt 1).
           → [8, 3, 5, 4]

... (weitere Züge bis Endzustand)

Schritt n: Verbleiben [3, 5] → score = 3 - 5 = -2

Schritt n+1: B vergleicht beide Antworten:
             min(-2, 1) = -2   → B wählt -2

Schritt n+2: A vergleicht alle Äste:
             max(-2, -2) = -2  → A-Knoten erhält -2

✅ Ergebnis: Minimax-Wert der Wurzel = -2
   Der Dreiecke-Richtung im Baum zeigt: ▽ = Max, △ = Min
```

> 💡 **Merkhilfe:** Die Richtung des Dreiecks an einem Knoten zeigt an, ob maximiert (▽) oder minimiert (△) wird.

### Minimax vs. Backtracking

| Eigenschaft | Backtracking | Minimax |
|---|---|---|
| **Rückgabe** | Lösbarkeit (bool) | Bewertung der Spielposition |
| **Rekursion** | Einfach rekursiv | Alternierend rekursiv |
| **Zusatzelement** | – | Bewertungsfunktion `score()` |
| **Abbruch** | Unzulässige Teillösung | Endzustand erreicht |

### Laufzeitanalyse

$$\boxed{T = O(b^d)}$$

- $b$: Verzweigungsgrad (Anzahl möglicher Züge pro Stellung)
- $d$: Tiefe des Suchbaums
- **Worst Case**: Alle Blätter werden bewertet → exponentiell.

***

## 2. Alpha-Beta-Suche

### Definition: Alpha und Beta

Alpha-Beta-Pruning optimiert Minimax durch Schneiden von Ästen, die das Endergebnis nicht beeinflussen können.

$$\boxed{
\alpha = \text{bisher bestes Ergebnis für A (untere Schranke an Max-Knoten)}
}$$

$$\boxed{
\beta = \text{bisher bestes Ergebnis für B (obere Schranke an Min-Knoten)}
}$$

$$\boxed{\text{Pruning tritt auf, wenn: } \alpha \geq \beta}$$

**Wichtige Begriffe:**
- **Alpha-Cutoff**: An einem Min-Knoten wird abgebrochen, wenn ein Wert $\leq \alpha$ gefunden wird – A hätte diesen Zug sowieso verworfen.
- **Beta-Cutoff**: An einem Max-Knoten wird abgebrochen, wenn ein Wert $\geq \beta$ gefunden wird – B hätte diesen Ast sowieso vermieden.
- **Zugordnung**: Reihenfolge der getesteten Züge; entscheidend für die Stärke des Prunings.

> 💡 **Merkhilfe:** „Alpha hält die Latte für A hoch" – alles darunter ist für A uninteressant. „Beta setzt Bs Limit" – alles darüber würde B vermeiden.

### Motivation

Spieler A hat für Zug 1 bereits den Wert `3` gesichert (α = 3). Bei Zug 2 findet A sofort eine starke Erwiderung von B mit Wert `−5`. Da B optimal spielt, wird er diese Antwort wählen und Zug 2 kann niemals besser als `−5` werden. A wird Zug 2 sowieso verwerfen – alle anderen Antworten von B bei Zug 2 müssen nicht betrachtet werden.

### Algorithmus

```pseudocode
AlphaBetaA(Zustand, α, β):
1. if Zustand ist Endzustand then
2.     return score(Zustand)
3. for jeder erlaubte Zug z do
4.     führe z aus
5.     wert ← AlphaBetaB(Zustand, α, β)
6.     mache z rückgängig
7.     if wert > α then
8.         α ← wert
9.     if α ≥ β then
10.        return α           // ✂️ Beta-Cutoff
11. return α

AlphaBetaB(Zustand, α, β):
1. if Zustand ist Endzustand then
2.     return score(Zustand)
3. for jeder erlaubte Zug z do
4.     führe z aus
5.     wert ← AlphaBetaA(Zustand, α, β)
6.     mache z rückgängig
7.     if wert < β then
8.         β ← wert
9.     if β ≤ α then
10.        return β           // ✂️ Alpha-Cutoff
11. return β
```

### Implementierung (Java)

```java
public int scoreA(int alpha, int beta) {
    if (game.isFinal()) return game.score();
    for (int move : Game.moves) {
        game.doMove(move);
        int score = scoreB(alpha, beta);
        game.undoMove(move);
        if (score > alpha) {
            alpha = score;
            if (alpha >= beta) return alpha; // ✂️ cutoff
        }
    }
    return alpha;
}

public int scoreB(int alpha, int beta) {
    if (game.isFinal()) return game.score();
    for (int move : Game.moves) {
        game.doMove(move);
        int score = scoreA(alpha, beta);
        game.undoMove(move);
        if (score < beta) {
            beta = score;
            if (beta <= alpha) return beta; // ✂️ cutoff
        }
    }
    return beta;
}
```

### Schritt-für-Schritt Beispiel

```
A kennt bereits Zug 1 → Wert = 3
Intervall: [α, β] = [3, +∞]

Schritt 1: A prüft Zug 2 → neuer Teilbaum wird geöffnet.

Schritt 2: B antwortet auf Zug 2 mit Wert −5.
           β ← −5

Schritt 3: Vergleich: α = 3 ≥ β = −5 → PRUNING ✂️
           Alle weiteren Antworten von B unter Zug 2 werden NICHT betrachtet.

✅ Ergebnis: A wählt Zug 1 mit Wert 3.
```

### Schleifeninvariante (Korrektheitsbeweis)

**Invariante am A-Knoten:** Nach der Auswertung der ersten $i$ Züge enthält $\alpha$ den bisher maximalen Wert unter diesen $i$ Zügen.

**Anfang ($i=0$):** Vor dem ersten Zug ist $\alpha = -\infty$ (kein Zug bewertet). ✅

**Erhaltung:** Für Zug $i+1$: Falls $\operatorname{wert}_{i+1} > \alpha$, wird $\alpha$ aktualisiert → $\alpha$ bleibt das Maximum. ✅

**Abbruch (Pruning):** Falls $\alpha \geq \beta$: B hat bereits eine Alternative, die diesen Ast für B besser macht als das, was A hier erreichen kann. Alle restlichen Züge sind irrelevant für die Minimax-Entscheidung. ✅

✅ **Sicherheit:** Alpha-Beta liefert immer dasselbe Ergebnis wie vollständiges Minimax.

### Laufzeitanalyse

| Szenario | Laufzeit | Erklärung |
|---|---|---|
| **Worst Case** | $O(b^d)$ | Schlechteste Zugordnung, kein Pruning |
| **Best Case** | $O(b^{d/2})$ | Ideale Zugordnung, maximales Pruning |
| **Average Case** | $O(b^{3d/4})$ | Zufällige Zugordnung |

$$\boxed{\text{Best Case: } O(b^{d/2}) \Rightarrow \text{effektive Suchtiefe verdoppelt sich gegenüber Minimax}}$$

⚠️ **Zugordnung ist entscheidend!** Bessere Züge zuerst → mehr Cutoffs → schnellere Suche. Im Skript wird die **Killer-Heuristik** als Technik zur Verbesserung der Zugordnung genannt.

***

## 3. Negamax-Variante der Alpha-Beta-Suche

### Idee und Definition

Die Negamax-Variante nutzt die Symmetrie von Minimax: Beide Spieler **maximieren** aus ihrer eigenen Sicht. Bei jedem Spielerwechsel wird das **Vorzeichen der Bewertung umgekehrt**, da der Gegner das Negative des eigenen Ergebnisses bewertet.

$$\boxed{
\operatorname{Negamax}(s, \alpha, \beta) = -\operatorname{Negamax}(s', -\beta, -\alpha)
}$$

Die Endbewertung hängt vom aktuellen Spieler ab:

$$\operatorname{score}(s) \cdot \operatorname{player}$$

wobei $\operatorname{player} \in \{+1, -1\}$ angibt, wer gerade am Zug ist.

### Algorithmus

```pseudocode
Negamax(Zustand, player, α, β):
1. if Zustand ist Endzustand then
2.     return player * score(Zustand)
3. for jeder erlaubte Zug z do
4.     führe z aus
5.     wert ← -Negamax(Zustand, -player, -β, -α)  // Vorzeichen + Tausch!
6.     mache z rückgängig
7.     if wert > α then
8.         α ← wert
9.     if α ≥ β then
10.        return α   // ✂️ Cutoff
11. return α
```

### Implementierung (Java)

```java
public int negamax(int player, int alpha, int beta) {
    if (game.isFinal()) return player * game.score();
    for (int move : Game.moves) {
        game.doMove(move);
        int score = -negamax(-player, -beta, -alpha); // Negation + Tausch
        game.undoMove(move);
        if (score > alpha) {
            alpha = score;
            if (alpha >= beta) return alpha; // ✂️ cutoff
        }
    }
    return alpha;
}
```

> 💡 **Merkhilfe:** Beim rekursiven Aufruf werden drei Dinge gleichzeitig gespiegelt: Vorzeichen, Spielerrolle und die Reihenfolge von $\alpha$/$\beta$.

⚠️ **Achtung:** `−β` und `−α` werden beim Aufruf vertauscht übergeben – das Intervall dreht sich um.

***

## 4. Branch-and-Bound

### Definition: Konzept

Branch-and-Bound ist ein Verfahren zur exakten Lösung von **Optimierungsproblemen** durch systematische Suche mit Schranken. Es erzeugt wie Backtracking Teillösungen in einer Baumstruktur, stoppt aber zusätzlich, wenn eine Teillösung keine bessere Lösung mehr liefern kann.

$$\boxed{
\text{Verwirf Teillösung } \tau \text{ genau dann, wenn } \operatorname{UpperBound}(\tau) \leq \operatorname{LowerBound}
}$$

**Zwei namensgebende Schranken:**
- **Upper Bound (obere Schranke)**: Maximales Potenzial einer Teillösung – kann von keiner Fortsetzung übertroffen werden.
- **Lower Bound (untere Schranke)**: Wert der besten bisher gefundenen vollständigen Lösung.

**Rolle:** Branch = Verzweigung im Entscheidungsbaum. Bound = Schranken, die bestimmen, ob sich weiteres Suchen lohnt.

### Vier Entwurfsfragen

Um Branch-and-Bound für ein konkretes Problem zu implementieren, müssen laut Skript vier Fragen beantwortet werden:

1. **Branching**: Welche Entscheidung erzeugt die Baumverzweigung? (z. B. „Objekt $X$ nehmen oder nicht")
2. **Auswahlreihenfolge**: In welcher Reihenfolge werden Entscheidungen getroffen? (Ziel: gute Lösungen früh finden)
3. **Bounding**: Wie wird der Upper Bound berechnet? (häufig durch relaxierte Problembedingungen)
4. **Initiallösung**: Wie wird schnell eine zulässige Anfangslösung erzeugt? (oft greedy)

### Allgemeiner Pseudocode

```pseudocode
BranchAndBound(Teillösung, LowerBound):
1.  if Teillösung ist vollständige Lösung then
2.      if Wert(Teillösung) > LowerBound then
3.          speichere Teillösung als beste Lösung
4.          LowerBound ← Wert(Teillösung)
5.      return LowerBound
6.  generiere Kandidaten für den nächsten Schritt
7.  for jeden Kandidaten k do
8.      erweitere Teillösung mit k
9.      UB ← UpperBound(erweiterte Teillösung)
10.     if UB > LowerBound then
11.         LowerBound ← BranchAndBound(erweiterte Teillösung, LowerBound)
12.     mache Erweiterung rückgängig
13. return LowerBound
```

⚠️ **Wichtig:** Der Branch-and-Bound-Ablauf startet immer bei der **leeren Teillösung**. Die Initiallösung dient nur zur Initialisierung des Lower Bounds, nicht als Startpunkt der Rekursion.

### Initiallösung

Der Pruning-Mechanismus greift erst, sobald eine erste vollständige Lösung gefunden wurde. Da die Tiefensuche bei manchen Problemen lang braucht, kann man vorab eine schnelle (meist suboptimale) Initiallösung berechnen – z. B. mit einem **Greedy-Algorithmus**. Deren Wert wird dann als initialer Lower Bound verwendet.

***

## 5. Branch-and-Bound für das 0/1-Rucksackproblem

### Problemdefinition

$$\boxed{
\text{Maximiere } \sum_{i \in S} v_i \quad \text{unter der Bedingung} \quad \sum_{i \in S} w_i \leq W, \quad x_i \in \{0, 1\}
}$$

- $K$ Objekte mit Gewichten $w_i$ und Werten $v_i$
- Rucksack-Kapazität $W$
- Gesucht: Teilmenge mit maximalem Wert ohne Kapazitätsüberschreitung

### Entscheidungsbaum (Branching)

Jede Ebene entspricht einer binären Entscheidung über Objekt $i$: aufnehmen oder weglassen.

```
                  leere Teillösung
                  /              \
         Objekt 1 rein       Objekt 1 raus
         /       \            /           \
  Obj. 2 rein  Obj. 2 raus  ...           ...
      ...          ...
```

**Auswahlreihenfolge**: Objekte werden nach **absteigendem $v_i/w_i$-Verhältnis** sortiert. So werden gute Lösungen früher gefunden → stärkeres Pruning.

### Upper Bound: Greedy-Schranke

Der Upper Bound wird berechnet, indem das Restproblem als **teilbares Rucksackproblem** (Fractional Knapsack) gelöst wird:

$$\boxed{
\operatorname{UpperBound}(\tau) = \text{Wert der bisherigen Teillösung} + \text{Greedy-Lösung für Restkapazität und Restobjekte}
}$$

**Warum ist das eine gültige obere Schranke?**

Da das teilbare Problem eine **Relaxation** des 0/1-Problems ist (mehr Lösungen erlaubt), gilt:

$$\operatorname{OPT}_{0/1}(\text{Fortsetzung}) \leq \operatorname{OPT}_{\text{teilbar}}(\text{Fortsetzung}) = \operatorname{UpperBound}$$

✅ Kein 0/1-Wert kann je größer sein als der UpperBound → das Pruning ist korrekt.

### Implementierung (Java)

```java
int best = Integer.MIN_VALUE;

void bnb(int item, int capacity, int value) {
    if (item == items.length) {
        best = Math.max(best, value);
        return;
    }
    // Pruning: Obere Schranke berechnen
    if (upperBound(item, capacity, value) <= best) return; // ✂️
    // Ast 1: Objekt aufnehmen
    if (items[item].weight <= capacity) {
        bnb(item + 1,
            capacity - items[item].weight,
            value + items[item].value);
    }
    // Ast 2: Objekt weglassen
    bnb(item + 1, capacity, value);
}

double upperBound(int item, int capacity, int value) {
    double ub = value;
    int cap = capacity;
    for (int i = item; i < items.length && cap > 0; i++) {
        if (items[i].weight <= cap) {
            ub += items[i].value;
            cap -= items[i].weight;
        } else {
            ub += (double) items[i].value / items[i].weight * cap;
            cap = 0;
        }
    }
    return ub;
}
```

⚠️ **Achtung:** Die Objekte müssen **nach $v_i/w_i$ absteigend sortiert** sein, damit die Greedy-Schranke korrekt funktioniert.

### Schritt-für-Schritt Beispiel

Objekte (sortiert nach $v_i/w_i$ absteigend):

| Objekt | Gewicht | Wert | $v/w$ |
|---|---|---|---|
| 1 | 2 | 6 | 3.0 |
| 2 | 2 | 5 | 2.5 |
| 3 | 5 | 9 | 1.8 |
| 4 | 6 | 8 | 1.33 |

Kapazität $W = 6$.

```
Ausgangszustand:
best = -∞  (oder Greedy-Initiallösung)

[Wurzel] leere Teillösung
  UpperBound: Obj1(w=2,v=6) + Obj2(w=2,v=5) + 2/5*9 = 6+5+3.6 = 14.6
  → 14.6 > best: weiter erkunden

  [Obj1 rein] wert=6, kap=4
    UpperBound: 6 + Obj2(w=2,v=5) + 2/5*9 = 6+5+3.6 = 14.6
    → weiter erkunden

    [Obj2 rein] wert=11, kap=2
      UpperBound: 11 + 2/5*9 = 11+3.6 = 14.6
      → weiter erkunden

      [Obj3 rein] Gewicht 5 > Kapazität 2 → nicht zulässig
      [Obj3 raus]
        [Obj4 raus] → Blatt! wert=11, best=11 ✅

    [Obj2 raus] wert=6, kap=4
      UpperBound: 6 + 4/5*9 = 6+7.2 = 13.2
      13.2 > best=11 → weiter erkunden
      ...

  [Obj1 raus] wert=0, kap=6
    UpperBound: Obj2(w=2,v=5)+Obj3(w=5,v=9)... → 14
    14 > best=11 → weiter erkunden
    ...

✅ Bestes Ergebnis: Objekte 1 und 2 → Wert = 11
```

### Laufzeitanalyse

| Szenario | Laufzeit | Anmerkung |
|---|---|---|
| **Worst Case** | $O(2^K)$ | Kein Pruning, wie Backtracking |
| **Best Case** | $O(K)$ | Fast alle Äste abgeschnitten |
| **Praktisch** | Deutlich $< O(2^K)$ | Abhängig von Schrankenqualität |

$$\boxed{\text{Branch-and-Bound: } O(2^K) \text{ im Worst Case}}$$

⚠️ **Das Problem bleibt NP-vollständig** – Branch-and-Bound löst es nicht in Polynomialzeit.
❌ **Falsch:** „Branch-and-Bound garantiert polynomielle Laufzeit."

***

## 6. Vergleich der Verfahren

| Verfahren | Problemtyp | Pruning-Kriterium | Worst Case | Eigenschaft |
|---|---|---|---|---|
| **Backtracking** | Suche / Aufzählung | Unzulässige Teillösung | $O(k^d)$ | Vollständige Suche |
| **Minimax** | Spielbäume | – (kein Pruning) | $\Theta(b^d)$ | Optimale Spielentscheidung |
| **Alpha-Beta** | Spielbäume | $\alpha \geq \beta$ | $O(b^d)$ bis $O(b^{d/2})$ | Gleiches Ergebnis wie Minimax |
| **Branch-and-Bound** | Optimierung | $\text{UB} \leq \text{LB}$ | $O(2^n)$ | Exakte Optimierung mit Pruning |

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Minimax** | Rekursiv alternierende Max/Min-Auswahl für optimale Spielstrategie |
| **$\alpha$** | Untere Schranke – bisher bestes Ergebnis für den Max-Spieler A |
| **$\beta$** | Obere Schranke – bisher bestes Ergebnis für den Min-Spieler B |
| **Pruning (Alpha-Beta)** | Abschneiden bei $\alpha \geq \beta$ |
| **Negamax** | Symmetrische Alpha-Beta-Variante mit Vorzeichenwechsel und $\alpha$/$\beta$-Tausch |
| **Lower Bound (B&B)** | Wert der besten bisher gefundenen vollständigen Lösung |
| **Upper Bound (B&B)** | Maximales Potenzial einer Teillösung (z. B. Greedy-Relaxation) |
| **Branch-and-Bound** | Exakte Optimierung durch Schranken-basiertes Verwerfen von Teilbäumen |

### Kernaussagen

✅ **Alpha-Beta liefert dasselbe Ergebnis wie Minimax** – nur schneller durch Pruning.  
✅ **Negamax vereinfacht Alpha-Beta** – beide Spieler nutzen dieselbe Funktion mit Vorzeichentausch.  
✅ **Die Greedy-Schranke ist korrekt** – da das teilbare Rucksackproblem eine Relaxation ist, überschätzt es den 0/1-Wert nie unterschätzt.  
✅ **Initiallösung verbessert B&B-Effizienz** – höherer Start-LB schneidet mehr Äste ab.  
⚠️ **Zugordnung ist entscheidend** für Alpha-Beta – schlechteste Zugordnung → kein Pruning → wie reines Minimax.  
⚠️ **Auswahlreihenfolge ist entscheidend** für B&B – Objekte nach $v/w$ sortieren für frühere gute Lösungen.  
❌ **Falsch:** Alpha-Beta verändert das Minimax-Ergebnis.  
❌ **Falsch:** Branch-and-Bound löst NP-vollständige Probleme in Polynomialzeit.

### Wichtige Algorithmen / Formeln

| Algorithmus | Laufzeit (Worst) | Laufzeit (Best) | Anwendung |
|---|---|---|---|
| **Minimax** | $\Theta(b^d)$ | $\Theta(b^d)$ | Spielbaum vollständig |
| **Alpha-Beta** | $O(b^d)$ | $O(b^{d/2})$ | Spielbaum mit Pruning |
| **Negamax** | wie Alpha-Beta | wie Alpha-Beta | Kompaktere Spielbaum-Implementierung |
| **Branch-and-Bound** | $O(2^K)$ | $O(K)$ | 0/1-Rucksack, Optimierungsprobleme |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Backtracking & Gierige Algo]]: Minimax und Branch-and-Bound sind beide Erweiterungen von Backtracking – Minimax fügt Bewertung hinzu, B&B fügt Schranken hinzu.
- [[VL.08 Dynamisches Programmieren]]: Für das 0/1-Rucksackproblem existiert eine DP-Lösung in $O(K \cdot W)$; für BestDifference ist DP laut Skript sogar effizienter als Minimax/Alpha-Beta.
- [[VL.13 Heuristische Algorithmen]]: Killer-Heuristik, Ruhesuche und A* zeigen, wie heuristische Ideen exakte Suchverfahren praktisch beschleunigen.