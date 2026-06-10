**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]  
**Date:** 18-05-2026  
**Topics:** #DynamischeProgrammierung #Memoization #Tabulation #Fibonacci #WeightedIntervalScheduling #Knapsack #Editierdistanz
**Link:** [[VL.06 AlgoDat.pdf]]

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt in das Paradigma der dynamischen Programmierung ein und zeigt, wie man rekursive Optimierungs- und Zählprobleme durch systematisches Zwischenspeichern effizient löst.

- **Optimal Substructure**: Verstehen, wann sich eine optimale Gesamtlösung aus optimalen Lösungen von Teilproblemen zusammensetzt.
- **Overlapping Subproblems**: Erkennen, wann dieselben Teilprobleme mehrfach auftreten und daher gespeichert werden sollten.
- **Memoization vs. Tabulation**: Den Unterschied zwischen top-down und bottom-up sicher anwenden.
- **Rekursionsformeln aufstellen**: Für Optimierungsprobleme eine geeignete OPT-Funktion definieren.
- **Lösungsrekonstruktion**: Nicht nur den optimalen Wert, sondern auch die zugehörige Lösung bestimmen.
- **Laufzeiten einordnen**: Verstehen, warum DP oft exponentielle Rekursion in polynomielle Laufzeit überführt, aber nicht immer „echt effizient“ im Sinn der Bitkomplexität ist.

---

## 1. Abschnitt: Definitionen & Grundlagen

### Definition: Dynamische Programmierung

Dynamische Programmierung ist ein Lösungsparadigma, bei dem eine rekursive Formel für Teilprobleme aufgestellt und die Lösungen dieser Teilprobleme gespeichert werden, damit gleiche Teilprobleme nicht mehrfach berechnet werden.

$$\boxed{\text{DP} = \text{rekursive Teilproblemstruktur} + \text{Speicherung von Teillösungen}}$$

**Wichtige Begriffe:**

- **Optimal substructure**: Eine optimale Lösung lässt sich aus optimalen Lösungen kleinerer Teilprobleme aufbauen.
- **Overlapping subproblems**: Dieselben Teilprobleme tauchen in einem rekursiven Berechnungsbaum mehrfach auf.
- **Memoization**: Top-down-Berechnung mit Zwischenspeicherung bei Bedarf.
- **Tabulation**: Bottom-up-Berechnung aller benötigten Werte im Voraus.
- **Teilproblem**: Ein kleineres Problem derselben Struktur.
- **OPT-Funktion**: Funktion, die den optimalen Wert eines Teilproblems beschreibt.

### Abgrenzung zu Divide-and-Conquer

Divide-and-Conquer zerlegt ein Problem ebenfalls rekursiv, nutzt aber typischerweise **verschiedene** Teilprobleme, die unabhängig gelöst und kombiniert werden. Dynamische Programmierung wird dann besonders stark, wenn **dieselben** Teilprobleme immer wieder auftreten.

$$\boxed{\text{Divide-and-Conquer: zerlegen + kombinieren}}$$

$$\boxed{\text{Dynamic Programming: zerlegen + kombinieren + speichern}}$$

**Rolle:**

- Bei **Greedy**, **Branch-and-Bound** oder **Alpha-Beta** wird der Suchraum durch Weglassen reduziert.
- Bei **DP** wird Redundanz durch Wiederverwendung bereits berechneter Teilprobleme vermieden.

⚠️ **Achtung:** Eine rekursive Formel allein ist noch **keine** dynamische Programmierung. Erst das Zwischenspeichern bringt den Effizienzgewinn.

### Voraussetzungen für DP

Damit DP sinnvoll ist, braucht man typischerweise:

- Eine rekursive Beschreibung des Problems.
- Viele wiederkehrende Teilprobleme.
- Eine klare Abhängigkeit des Gesamtwerts von Teilwerten.

$$\boxed{\text{Anwendbarkeit} \Rightarrow \text{optimal substructure} \land \text{overlapping subproblems}}$$

**Merkhilfe:**

- **Divide-and-Conquer**: „Teile und herrsche.“
- **Dynamic Programming**: „Teile, speichere und verwende wieder.“

⚠️ **Achtung:** Wenn fast alle Teilprobleme verschieden sind, wird DP oft speicherintensiv und bringt weniger.

---

## 2. Abschnitt: Fibonacci als Einstiegsbeispiel

### Definition der Fibonacci-Zahlen

Die Fibonacci-Zahlen sind rekursiv definiert durch:
$$
\boxed{
F_n =
\begin{cases}
0 & \text{falls } n = 0 \\
1 & \text{falls } n = 1 \\
F_{n-1} + F_{n-2} & \text{falls } n \ge 2
\end{cases}
}
$$
**Bedeutung:**  
Die Formel ist sehr einfach, aber die naive rekursive Auswertung erzeugt viele doppelte Berechnungen.

### Naive rekursive Implementierung

```java
public static long fibonacci(int n) {
    if (n < 2) {
        return n;
    } else {
        return fibonacci(n-1) + fibonacci(n-2);
    }
}
```

### Rekursionsbaum und Redundanz

Die Berechnung von $F_6$ verzweigt in $F_5$ und $F_4$, diese wieder in ihre Vorgänger usw. Dabei werden dieselben Werte mehrfach ausgerechnet.

```text
                 F6
               /    \
             F5      F4
           /   \    /  \
         F4    F3  F3  F2
        / \    / \ / \ / \
      F3 F2  F2 F1 ...
```

**Beobachtung:**

- $F_2$ wird mehrfach berechnet.
- $F_3$ wird mehrfach berechnet.
- $F_4$ wird mehrfach berechnet.

❌ **Falsch:** „Die Rekursion ist effizient, weil sie elegant aussieht.“

### Laufzeit der naiven Rekursion

Der Rekursionsbaum ist höchstens binär verzweigt, daher liegt die Laufzeit grob in

$$\boxed{O(2^n)}$$

Genauer wächst die Anzahl der Aufrufe asymptotisch exponentiell, näherungsweise wie die Fibonacci-Zahlen selbst.

$$\lim_{n \to \infty} \frac{F_{n+1}}{F_n} = \varphi = \frac{\sqrt{5}+1}{2} \approx 1.618$$

Daher gilt näherungsweise:

$$F_n \approx 1.6^n$$

**Rolle:**  
Das Problem ist **nicht** die Rekursionsidee selbst, sondern die mehrfache Berechnung identischer Teilprobleme.

### Top-down mit Memoization

Die Idee: Ein Array speichert bereits berechnete Werte. Wenn ein Wert schon vorhanden ist, wird er direkt zurückgegeben.

```java
public class FibonacciTopDown { // memoization
    private static long[] F;

    public static long fibonacci(int n) {
        F = new long[n+1];
        F[0] = 0;
        F = 1;
        for (int k = 2; k <= n; k++) {
            F[k] = -1;
        }
        return fibo(n);
    }

    public static long fibo(int n) {
        if (F[n] < 0) {
            F[n] = fibo(n-1) + fibo(n-2);
        }
        return F[n];
    }
}
```

### Bottom-up mit Tabulation

Wenn sowieso alle kleineren Werte benötigt werden, ist bottom-up oft direkter.

```java
public static long fibonacci(int n) { // tabulation
    F = new long[n+1];
    F[0] = 0;
    F = 1;
    for (int k = 2; k <= n; k++) {
        F[k] = F[k-1] + F[k-2];
    }
    return F[n];
}
```

### Schritt-für-Schritt Beispiel

```text
Ausgangszustand:
F[0] = 0
F = 1

Schritt 1: k = 2
          F = F + F[0] = 1
          Zustand → [0, 1, 1]

Schritt 2: k = 3
          F = F + F = 2
          Zustand → [0, 1, 1, 2]

Schritt 3: k = 4
          F[4] = 3
          Zustand → [0, 1, 1, 2, 3]

Schritt 4: k = 5
          F[5] = 5

Schritt 5: k = 6
          F[6] = 8

✅ Ergebnis: F[6] = 8
```

### Speichereffizienz

Bei Fibonacci braucht man für den nächsten Wert nur die beiden letzten Werte. Daher reicht ein Array der Länge 2:

```java
public static long fibonacci(int n) {
    F = new long;
    F[0] = 0;
    F = 1;
    for (int k = 2; k <= n; k++)
        F[k%2] = F[(k-1)%2] + F[(k-2)%2];
    return F[n%2];
}
```

$$\boxed{\text{Speicherbedarf bei Fibonacci bottom-up} = O(1)}$$

⚠️ **Achtung:** Diese Speicherreduktion klappt nur, wenn ältere DP-Zustände später nicht mehr gebraucht werden.

### Nebenbemerkung zur tatsächlichen Laufzeit

Auf den ersten Blick scheint die DP-Version linear zu sein. Das ist aber bei großen Fibonacci-Zahlen nicht ganz korrekt, weil auch die **Zahlenwerte** selbst wachsen.

- Die Addition großer Zahlen kostet nicht konstant viel.
- Die Anzahl der Ziffern wächst mit $n$.
- Daher liegt die tatsächliche Laufzeit hier eher in

$$\boxed{O(n^2)}$$

**Merkhilfe:**  
DP reduziert die Anzahl der **Zustände**, aber nicht automatisch die Kosten jeder einzelnen **Operation**.

---

## 3. Abschnitt: Allgemeines DP-Schema

### Rekursionsformel für Optimierungsprobleme

Für viele DP-Probleme wird zuerst eine Funktion $OPT$ definiert, die den optimalen Wert eines Teilproblems beschreibt.

$$\boxed{\text{Gesucht: } OPT(\text{Teilproblem})}$$

Dann geht man typischerweise so vor:

1. Definiere ein geeignetes Teilproblem.
2. Formuliere Randfälle.
3. Betrachte eine optimale Lösung als gegeben.
4. Führe eine Fallunterscheidung durch.
5. Leite daraus eine Rekursionsformel ab.
6. Speichere berechnete Werte in Tabelle oder Matrix.

### Wert vs. Lösung

Ein wichtiger Punkt bei Optimierungsproblemen:

$$\boxed{\text{Die Rekursionsformel liefert oft nur den optimalen Wert, nicht die Lösung selbst.}}$$

Deshalb braucht man häufig:

- **1. Durchlauf**: Berechnung des optimalen Werts.
- **2. Durchlauf**: Rekonstruktion der konkreten Lösung.

⚠️ **Achtung:** Wer nur die DP-Tabelle berechnet, hat oft noch **nicht** die ausgewählten Objekte, Intervalle oder Operationen.

### Top-down oder bottom-up?

|Strategie|Idee|Vorteil|Nachteil|
|---|---|---|---|
|**Top-down / Memoization**|Berechne nur bei Bedarf|Gut, wenn nicht alle Zustände gebraucht werden|Rekursion, evtl. Overhead|
|**Bottom-up / Tabulation**|Fülle Tabelle systematisch|Einfach, iterativ, oft klarer|Rechnet evtl. unnötige Zustände|
|**Speicheroptimiertes DP**|Nur relevante Zeilen/Spalten behalten|Weniger Speicher|Lösung oft nicht mehr rekonstruierbar|

✅ **Richtig:** Bottom-up ist gut, wenn klar ist, dass fast alle Zustände benötigt werden.  
⚠️ **Achtung:** Speicheroptimierung kann die Rekonstruktion der Lösung unmöglich machen.  
❌ **Falsch:** „Bottom-up ist immer besser.“

---

## 4. Abschnitt: Gewichtete Intervallauswahl

### Problemdefinition

Gegeben sind Intervalle $I_k = [s_k, f_k)$ mit Gewichten $w_k$. Gesucht ist eine Menge kompatibler Intervalle mit maximalem Gesamtgewicht.

$$\boxed{ \text{Finde } S \subseteq {1,\dots,n} \text{ kompatibel, sodass } \sum_{k \in S} w_k \text{ maximal ist} }$$

**Intuition:**  
Im ungewichteten Fall genügt ein Greedy-Verfahren. Im gewichteten Fall kann Greedy aber stark scheitern.

⚠️ **Achtung:** „Frühestes Ende“ ist hier **nicht** allgemein optimal.

### Vorgängerfunktion (p(j))

Die Intervalle seien nach Endzeit sortiert. Dann definiert man:

$$\boxed{ p(j) = \begin{cases} \max { i \in \mathbb{N} \mid i < j \text{ und } i \text{ kompatibel mit } j } & \text{falls existent} \ 0 & \text{sonst} \end{cases} }$$

**Bedeutung:**  
$p(j)$ ist das letzte Intervall vor $j$, das noch mit $j$ zusammen gewählt werden darf.

### Rekursionsformel

Definiere:

$$\boxed{\text{OPT}(k) = \text{optimaler Wert für Intervalle } 1,\dots,k}$$

Dann gilt:
$$
\boxed{
OPT(k) =
\begin{cases}
0 & \text{falls } k = 0 \\
\max\left(w_k + OPT(p(k)),\, OPT(k-1)\right) & \text{sonst}
\end{cases}
}
$$
**Fallunterscheidung:**

- **Fall 1:** Intervall $k$ wird gewählt $\Rightarrow$ dann darf nur bis $p(k)$ ergänzt werden.
- **Fall 2:** Intervall $k$ wird nicht gewählt $\Rightarrow$ dann bleibt das Problem $1,\dots,k-1$.

### Algorithmus

```pseudocode
WeightedIntervalScheduling(Intervalle):
1. Sortiere Anfragen nach Endzeit
2. Berechne p[1..n]
3. m[0] ← 0
4. for k = 1 to n
5.     m[k] ← max(w[k] + m[p[k]], m[k-1])
6. return m[n]
```

### Rekonstruktion der Lösung

```pseudocode
findSolution(k):
1. if k = 0
2.     return ∅
3. else if w[k] + m[p[k]] > m[k-1]
4.     return {k} ∪ findSolution(p[k])
5. else
6.     return findSolution(k-1)
```

### Schritt-für-Schritt Beispiel

```text
Betrachte Intervall k.

Frage 1: Nehme ich k?
    Ja  → Gewinn = w[k] + m[p[k]]

Frage 2: Lasse ich k weg?
    Nein → Gewinn = m[k-1]

Dann:
m[k] = max(beide Möglichkeiten)
```

✅ **Ergebnisidee:**  
Jedes Intervall erzeugt genau eine lokale Entscheidung „nehmen oder nicht nehmen“, aber beide Fälle werden über gespeicherte Teilprobleme effizient bewertet.

### Laufzeitanalyse

|Operation|Laufzeit|Bemerkung|
|---|---|---|
|**Sortieren nach Endzeiten**|$O(n \log n)$|Vorbereitung|
|**Berechnung von $p(k)$**|$O(n \log n)$|z.B. über Sortierung/Suche|
|**Füllen des Arrays $m$**|$O(n)$|Ein Durchlauf|
|**Gesamt**|$\boxed{\Theta(n \log n)}$|dominiert durch Vorbereitung|
|**Speicher**|$\boxed{\Theta(n)}$|Array $m$|

⚠️ **Achtung:** Im Gegensatz zu Fibonacci kann der Speicher hier nicht einfach auf konstante Größe reduziert werden, weil auf unterschiedliche frühere Zustände $m[p(k)]$ zugegriffen wird.

---

## 5. Abschnitt: 0/1-Rucksackproblem

### Problem

Gegeben sind Objekte mit Gewicht $w_k$ und Wert $v_k$ sowie eine Kapazität $W$. Jedes Objekt darf entweder ganz genommen oder gar nicht genommen werden.

$$\boxed{ \text{Maximiere } \sum v_k \text{ unter } \sum w_k \le W \text{ und } x_k \in {0,1} }$$

### Warum der erste Ansatz scheitert

Naiv könnte man definieren:

$$OPT(k) = \text{optimaler Wert für Objekte } 1,\dots,k$$

Das reicht aber **nicht**, denn wenn Objekt $k$ gewählt wird, muss man wissen, wie viel Restkapazität noch frei ist.

⚠️ **Achtung:** Für DP muss der Zustand **alle Informationen enthalten**, die für spätere Entscheidungen relevant sind.

### Richtiger Zustand

$$\boxed{OPT(k,W) = \text{optimaler Wert für Objekte } 1,\dots,k \text{ bei Kapazität } W}$$

### Rekursionsformel

$$\boxed{
OPT(k,W) =
\begin{cases}
0 & \text{falls } k = 0 \\
OPT(k-1,W) & \text{falls } w_k > W \\
\max\left(v_k + OPT(k-1, W-w_k),\, OPT(k-1,W)\right) & \text{sonst}
\end{cases}
}$$

**Fallunterscheidung:**

- Objekt $k$ passt nicht hinein.
- Objekt $k$ passt hinein, wird aber nicht gewählt.
- Objekt $k$ passt hinein und wird gewählt.

### Top-down-Implementierung

```java
public class Knapsack {

    public int W, K;
    public int[] weight;
    public double[] value;
    private double[][] M;
    private Queue<Integer> inventory = new LinkedList<>();

    public Knapsack(int[] weight, double[] value, int W) {
        this.W = W;
        this.K = weight.length - 1;
        this.weight = weight;
        this.value = value;
        M = new double[K+1][W+1];
        for (int w = 0; w <= W; w++) {
            M[0][w] = 0.0;
            for (int k = 1; k <= K; k++)
                M[k][w] = -1.0;
        }
    }

    public double opt(int k, int w) {
        if (M[k][w] < 0)
            if (weight[k] > w)
                M[k][w] = opt(k-1, w);
            else
                M[k][w] = Math.max(value[k] + opt(k-1, w-weight[k]),
                                   opt(k-1, w));
        return M[k][w];
    }

    public void findSolution(int k, int w) {
        if (k == 0) return;
        else if (weight[k] > w)
            findSolution(k-1, w);
        else if (value[k] + M[k-1][w-weight[k]] > M[k-1][w]) {
            findSolution(k-1, w-weight[k]);
            inventory.add(k);
        } else
            findSolution(k-1, w);
    }
}
```

### ASCII-Diagramm der Matrixstruktur

```text
        Kapazität w →
      0  1  2  3  ... W
k=0   0  0  0  0  ... 0
k=1   .  .  .  .  ... .
k=2   .  .  .  .  ... .
k=3   .  .  .  .  ... .
...
k=K   .  .  .  .  ... .
```

Jeder Zustand $(k,w)$ fragt:

- Nimm Objekt $k$?
- Oder nimm es nicht?

### Laufzeit und Speicher

$$\boxed{\text{Laufzeit} = O(KW)}$$

$$\boxed{\text{Speicher} = O(KW)}$$

|Größe|Komplexität|Erklärung|
|---|---|---|
|**Zeit**|$O(KW)$|Jeder Zustand $(k,w)$ wird höchstens einmal berechnet|
|**Speicher**|$O(KW)$|Matrix aller Zustände|
|**Rekonstruktion**|zusätzlich möglich|über zweiten Durchlauf|

### Pseudopolynomielle Laufzeit

Das wirkt zunächst überraschend, weil 0/1-Knapsack NP-vollständig ist.

**Auflösung:**  
Die Laufzeit hängt nicht nur von der Anzahl der Eingabeobjekte ab, sondern direkt von der **numerischen Größe** $W$.

$$\boxed{\text{pseudopolynomiell} = \text{polynomiell in Eingabelänge und Zahlenwerten}}$$

Wenn $W$ mit $n$ Bits dargestellt wird, kann gelten:

$$W \le 2^n - 1$$

Dann wird aus $O(KW)$ in Bitlänge:

$$\boxed{O(K \cdot 2^n)}$$

also exponentiell.

⚠️ **Achtung:** Polynomial in einem Zahlenwert ist nicht automatisch polynomial in der Eingabelänge in Bits.

### Schleifeninvariante / Zustandsinvariante

Für eine bottom-up-Version wäre eine natürliche Invariante:

- Nach Verarbeitung der ersten $k$ Zeilen enthält jeder Eintrag $M[i][w]$ für $0 \le i \le k$ den optimalen Wert für die ersten $i$ Objekte bei Kapazität $w$.

✅ **Korrektheit:**  
Wenn die Invariante erhalten bleibt und die letzte Zeile vollständig ist, enthält $M[K][W]$ den optimalen Wert.

---

## 6. Abschnitt: Editierdistanz

### Definition

Die Editierdistanz zwischen zwei Strings $a$ und $b$ ist die minimale Anzahl elementarer Operationen, um $a$ in $b$ umzuwandeln.

Erlaubte Operationen:

- **D**: Delete
- **I**: Insert
- **S**: Substitute
- **–**: Übernehmen eines gleichen Zeichens, Kosten $0$

$$\boxed{\text{Editierdistanz}(a,b) = \min \text{ Anzahl von D, I, S}}$$

### Schreibweisen

- $a[1:i]$: Präfix der ersten $i$ Zeichen von $a$
- $a[1:0]$: leerer String
- $a[i] \ne b[j]$ sei

$$a[i] \ne b[j] =
\begin{cases}
0 & \text{falls } a[i] = b[j] \\
1 & \text{sonst}
\end{cases}$$

### Rekursionsformel

Definiere:

$$\boxed{OPT(i,j) = \text{Editierdistanz zwischen } a[1:i] \text{ und } b[1:j]}$$

Randfälle:

$$\boxed{OPT(i,0) = i}$$

$$\boxed{OPT(0,j) = j}$$

Rekursionsfall:

$$\boxed{
OPT(i,j) =
\min\left\{
\begin{array}{ll}
OPT(i, j-1) + 1 & \text{Einfügen von } b[j] \\
OPT(i-1, j) + 1 & \text{Löschen von } a[i] \\
OPT(i-1, j-1) + (a[i] \ne b[j]) & \text{Ersetzen oder Übernehmen}
\end{array}
\right.
}$$

### Matrixstruktur

![[VL.Skript AlgoDat-1779215588727.webp]]

Jeder Eintrag hängt nur von drei Nachbarn ab:

- links
- oben
- links-oben

### Bottom-up-Algorithmus

```pseudocode
EditDistance(a, b):
1. Erzeuge Matrix D[0..|a|][0..|b|]
2. Initialisiere D[i][0] ← i
3. Initialisiere D[0][j] ← j
4. for i = 1 to |a|
5.     for j = 1 to |b|
6.         D[i][j] ← min(
7.             D[i][j-1] + 1,
8.             D[i-1][j] + 1,
9.             D[i-1][j-1] + kosten(a[i], b[j])
10.        )
11. return D[|a|][|b|]
```

### Java-Implementierung

```java
public class EditDistance {
    private String a, b;
    private int an, bn;
    private int D[][];

    public EditDistance(String a, String b) {
        this.a = a;
        this.b = b;
        an = a.length();
        bn = b.length();
        D = new int[an + 1][bn + 1];
        for (int i = 0; i <= an; i++) {
            D[i][0] = i;
        }
        for (int j = 0; j <= bn; j++) {
            D[0][j] = j;
        }
    }

    public int distance() {
        for (int i = 1; i <= an; i++) {
            for (int j = 1; j <= bn; j++) {
                int d1 = D[i][j-1] + 1;
                int d2 = D[i-1][j] + 1;
                int d3 = D[i-1][j-1] + (a.charAt(i-1) == b.charAt(j-1) ? 0 : 1);
                D[i][j] = Math.min(Math.min(d1, d2), d3);
            }
        }
        return D[an][bn];
    }
}
```

⚠️ **Achtung:** In Java liefert `a.charAt(i-1)` das $i$-te Zeichen im mathematischen Sinn. Deshalb wirkt die Implementierung um 1 verschoben gegenüber der Formel.

### Beispiel: ALGODAT → DAGOBERT

Eine mögliche Folge ist:

```text
D A G O B E R T
A L G O D A T
i d s s i
```

Das ergibt Distanz $5$.

Die vollständige DP-Matrix für dieses Beispiel ist:

![[VL.06 Dynamisches Programmieren-1779215642735.webp]]

✅ **Ergebnis:** Die Editierdistanz von `ALGODAT` zu `DAGOBERT` ist $5$.

### Speicheroptimierung

Da nur die vorherige Zeile oder Spalte gebraucht wird, kann man den Speicher auf zwei Zeilen reduzieren.

$$\boxed{\text{Speicheroptimierung möglich: } O(\min(|a|, |b|))}$$

⚠️ **Achtung:** Dann ist die Rekonstruktion der konkreten Editierfolge nicht mehr direkt möglich.

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Dynamic Programming**|Lösen rekursiver Teilprobleme mit Speicherung von Zwischenergebnissen|
|**Optimal substructure**|Optimale Gesamtlösung enthält optimale Teillösungen|
|**Overlapping subproblems**|Dieselben Teilprobleme treten mehrfach auf|
|**Memoization**|Top-down mit Berechnung bei Bedarf|
|**Tabulation**|Bottom-up mit systematischem Tabellenaufbau|
|**Lösungsrekonstruktion**|Zweiter Durchlauf, um aus dem Optimalwert die konkrete Lösung zu erhalten|
|**Pseudopolynomiell**|Polynomial in Zahlenwerten, aber nicht unbedingt in der Bitlänge|

### Kernaussagen

✅ **DP vermeidet redundante Berechnungen** – gleiche Teilprobleme werden nur einmal gelöst.  
✅ **Eine gute Zustandsdefinition ist entscheidend** – beim Knapsack muss z.B. die Restkapazität Teil des Zustands sein.  
✅ **Top-down und bottom-up sind zwei Realisierungen derselben Rekursionsidee** – sie unterscheiden sich vor allem in Berechnungsreihenfolge und Speicherverhalten.  
⚠️ **Achtung:** Der optimale Wert ist oft nicht automatisch die optimale Lösung selbst.  
⚠️ **Achtung:** Speicheroptimierung kann die Rekonstruktion der Lösung verhindern.  
❌ **Falsch:** „DP macht jedes schwere Problem effizient lösbar.“

### Wichtige Algorithmen / Formeln

| Algorithmus / Formel            | Laufzeit                                                               | Anwendung                                         |
| ------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------- |
| **Fibonacci naiv**              | $O(2^n)$                                                               | Beispiel für redundante Rekursion                 |
| **Fibonacci mit DP**            | nominal $O(n)$ Zustände, tatsächlich wegen großer Zahlen eher $O(n^2)$ | Einstieg in Memoization/Tabulation                |
| **Gewichtete Intervallauswahl** | $\Theta(n \log n)$                                                     | Auswahl kompatibler Intervalle mit Maximalgewicht |
| **0/1-Knapsack (DP)**           | $O(KW)$                                                                | Ganzzahliger Rucksack, pseudopolynomiell          |
| **Editierdistanz**              | $O(\lvert a \rvert \cdot \lvert b \rvert)$                             | String-Ähnlichkeit, diff, Bioinformatik\|         |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Backtracking & Gierige Algo]]: Gewichtete Intervallauswahl zeigt, wann Greedy nicht mehr ausreicht.
- [[VL.06 Divide and Conquer]]: DP erweitert die rekursive Zerlegung um systematische Zwischenspeicherung.
- [[Komplexitätstheorie]]: Das Knapsack-Beispiel illustriert den Unterschied zwischen polynomial und pseudopolynomiell.
- [[Rekursion und Induktion]]: Rekursionsformeln und Korrektheitsargumente bauen direkt darauf auf.
- [[String-Algorithmen]]: Editierdistanz ist ein klassisches Problem des approximativen Matchings.