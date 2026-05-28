**Class:** [[IntroProg]]  
**Date:** VL.6  
**Topics:** #TeileUndHerrsche #DivideAndConquer #MergeSort #Rekursion #Merge #IterativerMergeSort #Laufzeitanalyse

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt die **algorithmische Methode "Teile & Herrsche"** ein und demonstriert sie am Beispiel von **MergeSort**.

- Verständnis des **Teile-und-Herrsche-Prinzips**
- **MergeSort-Algorithmus** rekursiv und iterativ
- **Merge-Operation** zum Zusammenfügen sortierter Teilfolgen
- **Laufzeitanalyse** mit Rekursionsgleichungen
- **Beweis** der $O(n \log n)$ Laufzeit per Induktion

---

## 1. Algorithmische Methode: Teile & Herrsche

### Prinzip (Divide & Conquer)

**Drei Schritte:**

1. **Teile (Divide):** Zerlege die Eingabe in mehrere **Teilprobleme**
2. **Herrsche (Conquer):** Löse die Teilprobleme **rekursiv**
3. **Kombiniere (Combine):** Füge die **Teillösungen** zur Gesamtlösung zusammen

### Wichtig

⚠️ **Rekursionsabbruch** erforderlich!  
Bei Sortieren: Folgen der Länge 1 sind bereits sortiert.

### Visualisierung am Beispiel Sortieren

```
Eingabe: [15, 7, 6, 13, 25, 4, 9, 12]

Schritt 1 - TEILE:
[15, 7, 6, 13] | [25, 4, 9, 12]

Schritt 2 - HERRSCHE (rekursiv sortieren):
[6, 7, 13, 15] | [4, 9, 12, 25]

Schritt 3 - KOMBINIERE (merge):
[4, 6, 7, 9, 12, 13, 15, 25]
```

---

## 2. MergeSort - Rekursive Variante

### Algorithmus

```
MergeSort(Array A, p, r)  // Sortiere A[p,...,r]
1. if p < r then                 // p ≥ r: nichts zu tun (Abbruch)
2.     q ← ⌊(p+r)/2⌋             // Berechne Mitte
3.     MergeSort(A, p, q)        // Sortiere linke Hälfte
4.     MergeSort(A, q+1, r)      // Sortiere rechte Hälfte
5.     Merge(A, p, q, r)         // Zusammenfügen
```

**Aufruf:** `MergeSort(A, 1, n)` für Array `A[1...n]`

### Schritt-für-Schritt Beispiel

```
MergeSort(A, 1, 8) mit A = [15, 7, 6, 13, 25, 4, 9, 12]

                    [15, 7, 6, 13, 25, 4, 9, 12]
                    /                          \
           [15, 7, 6, 13]                   [25, 4, 9, 12]
           /            \                   /            \
      [15, 7]        [6, 13]           [25, 4]        [9, 12]
      /    \         /    \            /    \         /    \
    [15]  [7]      [6]  [13]        [25]  [4]      [9]  [12]
      \    /         \    /            \    /         \    /
      [7, 15]       [6, 13]           [4, 25]       [9, 12]
           \            /                   \            /
         [6, 7, 13, 15]                   [4, 9, 12, 25]
                    \                          /
                    [4, 6, 7, 9, 12, 13, 15, 25]
```

**Wichtige Beobachtung:**
- **Aufsteigend** (Teilen): Keine Arbeit, nur Aufteilung
- **Absteigend** (Kombinieren): Die eigentliche Arbeit passiert beim Mergen

---

## 3. Die Merge-Operation

### Idee

Gegeben: Zwei **sortierte** Teilarrays `A[p...q]` und `A[q+1...r]`  
Gesucht: Ein sortiertes Array `A[p...r]`

**Strategie:** Vergleiche die jeweils kleinsten Elemente beider Hälften und füge das kleinere ein.

### Algorithmus

```
Merge(Array A, p, q, r)  // Merge A[p,...,q] und A[q+1,...,r]
1.  Array B                      // Hilfsarray, Länge r-p+1
2.  i ← p, j ← q+1               // Zeiger auf linke/rechte Hälfte
3.  b ← 1                        // Zeiger auf B
4.  while i ≤ q and j ≤ r do    // Solange beide Hälften Elemente haben
5.      if A[i] ≤ A[j] then
6.          B[b++] ← A[i++]      // Links kleiner → nehme von links
7.      else
8.          B[b++] ← A[j++]      // Rechts kleiner → nehme von rechts
9.  while i ≤ q do               // Restliche linke Elemente
10.     B[b++] ← A[i++]
11. while j ≤ r do               // Restliche rechte Elemente
12.     B[b++] ← A[j++]
13. A[p,...,r] ← B               // Kopiere B zurück nach A
```

⚠️ **Notation:** `B[b++]` bedeutet: Erst zuweisen, dann `b` erhöhen.

### Detailliertes Beispiel

```
Merge(A, 1, 4, 8)
Eingabe: A = [6, 7, 13, 15, 4, 9, 24, 25]
                ↑←─────q──→↑  ↑←──────r──→↑
              p=1          q=4 q+1=5       r=8

Schritt-für-Schritt:

i=1, j=5, b=1:  A[1]=6, A[5]=4    → 4 < 6  → B[1]=4, j=6
i=1, j=6, b=2:  A[1]=6, A[6]=9    → 6 < 9  → B[2]=6, i=2
i=2, j=6, b=3:  A[2]=7, A[6]=9    → 7 < 9  → B[3]=7, i=3
i=3, j=6, b=4:  A[3]=13, A[6]=9   → 9 < 13 → B[4]=9, j=7
i=3, j=7, b=5:  A[3]=13, A[7]=24  → 13 < 24 → B[5]=13, i=4
i=4, j=7, b=6:  A[4]=15, A[7]=24  → 15 < 24 → B[6]=15, i=5
i=5, j=7: Linke Hälfte fertig, Zeilen 11-12: Kopiere Rest
                → B[7]=24, B[8]=25

Ergebnis: B = [4, 6, 7, 9, 13, 15, 24, 25]
Kopiere nach A: A = [4, 6, 7, 9, 13, 15, 24, 25]
```

### Laufzeit von Merge

**Jedes Element wird genau einmal betrachtet und kopiert:**
$$T_{\text{Merge}}(n) = O(n)$$

wobei $n = r - p + 1$ (Länge des zu mergenden Bereichs).

---

## 4. Laufzeitanalyse von MergeSort

### Rekursionsgleichung aufstellen

```
MergeSort(Array A, p, r)         Laufzeit:
1. if p < r then                    1
2.     q ← ⌊(p+r)/2⌋                1
3.     MergeSort(A, p, q)           T(n/2)
4.     MergeSort(A, q+1, r)         T(n/2)
5.     Merge(A, p, q, r)            cn
```

**Annahme:** $n$ ist Zweierpotenz (vereinfacht Analyse, ohne Rundung).

**Gesamt:**
$$T(n) = \begin{cases}
C & \text{falls } n = 1 \\
2T(n/2) + cn & \text{falls } n > 1
\end{cases}$$

wobei $c$ eine geeignete Konstante ist.

### Intuitive Auflösung (Rekursionsbaum)

```
Ebene 0:                  n                      cn
                        /   \
Ebene 1:            n/2     n/2                2·cn/2 = cn
                   /  \     /  \
Ebene 2:        n/4  n/4 n/4  n/4             4·cn/4 = cn
                 ⋮    ⋮   ⋮    ⋮
                 ⋮    ⋮   ⋮    ⋮
Ebene log n:    1   1...1   1                 n·C
                ←─── n Blätter ──→

Höhe: log₂ n
Arbeit pro Ebene: cn (außer Blätter: n·C)
Gesamt: cn·log n + n·C ≤ (c+C)n log n = O(n log n)
```

**Jede Ebene:** $cn$ Arbeit (außer Blätter)  
**Anzahl Ebenen:** $\log_2 n + 1$  
**Gesamt:** $O(n \log n)$

### Formaler Beweis per Induktion

**Satz:** MergeSort hat Laufzeit $O(n \log n)$.

**Beweis:**

Sei $T(2) \leq C'$ und $C^* \geq \max\{c, C'\}$.

Zu zeigen: $T(n) \leq C^* n \log n$ für alle $n \geq 2$.

**Induktionsanfang (I.A.):**
$$T(2) \leq C' \leq C^* \cdot 2 \cdot \log 2 = 2C^*$$ ✓

**Induktionsvoraussetzung (I.V.):**
Für alle $m < n$ gilt: $T(m) \leq C^* m \log m$

**Induktionsschritt (I.S.):**
$$\begin{align}
T(n) &\leq 2T(n/2) + cn \\
&\leq 2 \cdot C^* \frac{n}{2} \log(n/2) + cn \quad \text{(nach I.V.)} \\
&= C^* n (\log n - 1) + cn \\
&= C^* n \log n - C^* n + cn \\
&\leq C^* n \log n - C^* n + C^* n \quad \text{(da } c \leq C^*\text{)} \\
&= C^* n \log n
\end{align}$$

Also gilt: $T(n) = O(n \log n)$ ✓

---

## 5. Vergleich mit anderen Sortieralgorithmen

| Algorithmus | Best Case | Average Case | Worst Case | Speicher |
|-------------|-----------|--------------|------------|----------|
| **Insertion Sort** | $\Theta(n)$ | $\Theta(n^2)$ | $\Theta(n^2)$ | $O(1)$ |
| **Selection Sort** | $\Theta(n^2)$ | $\Theta(n^2)$ | $\Theta(n^2)$ | $O(1)$ |
| **Bubble Sort** | $\Theta(n)$ | $\Theta(n^2)$ | $\Theta(n^2)$ | $O(1)$ |
| **MergeSort** | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $O(n)$ |

**Vorteile von MergeSort:**
✅ **Garantiert** $O(n \log n)$ in allen Fällen  
✅ **Stabil** (erhält Reihenfolge gleicher Elemente)  
✅ **Vorhersagbare Performance**

**Nachteile:**
❌ **Zusätzlicher Speicher** $O(n)$ für Hilfsarray  
❌ **Overhead** durch Rekursion und Kopieren

---

## 6. Iterativer MergeSort

### Idee

Statt rekursiv von oben nach unten zu teilen, **von unten nach oben** arbeiten:
1. Merge Paare von 1-Element-Arrays → 2-Element-Arrays
2. Merge Paare von 2-Element-Arrays → 4-Element-Arrays
3. Merge Paare von 4-Element-Arrays → 8-Element-Arrays
4. ...bis gesamtes Array sortiert ist

### Visualisierung

```
Eingabe:    [30, 24, 44, 58, 92, 51, 44, 85, 30, 16]

step=1:     [24, 30][44, 58][51, 92][44, 85][16, 30]
            ↑merge↑ ↑merge↑ ↑merge↑ ↑merge↑ ↑merge↑

step=2:     [24, 30, 44, 58][44, 51, 85, 92][16, 30]
            ↑─────merge────↑ ↑─────merge────↑

step=4:     [24, 30, 44, 44, 51, 58, 85, 92][16, 30]
            ↑────────────merge───────────────↑

step=8:     [16, 24, 30, 30, 44, 44, 51, 58, 85, 92]
```

### Algorithmus

```
IterativMergeSort(Array A)  // Sortiere A[1,...,n]
1.  step ← 1                           // Schrittweite
2.  while step < n do                  // Solange nicht fertig
3.      left ← 1                       // Linke Grenze
4.      while left ≤ n - step do      // Für alle Teilarrays
5.          middle ← left + step - 1  // Mitte berechnen
6.          middle ← min(middle, n)   // Nicht über Array hinaus
7.          right ← left + 2*step - 1 // Rechte Grenze
8.          right ← min(right, n)     // Nicht über Array hinaus
9.          Merge(A, left, middle, right)
10.         left ← left + 2*step      // Nächstes Paar
11.     step ← step * 2                // Verdopple Schrittweite
```

### Detailliertes Beispiel

```
A = [30, 24, 44, 58, 92, 51, 44, 85, 30, 16]

step=1:
  left=1: Merge(A,1,1,2)   → [24,30|44,58,92,51,44,85,30,16]
  left=3: Merge(A,3,3,4)   → [24,30,44,58|92,51,44,85,30,16]
  left=5: Merge(A,5,5,6)   → [24,30,44,58,51,92|44,85,30,16]
  left=7: Merge(A,7,7,8)   → [24,30,44,58,51,92,44,85|30,16]
  left=9: Merge(A,9,9,10)  → [24,30,44,58,51,92,44,85,16,30]

step=2:
  left=1: Merge(A,1,2,4)   → [24,30,44,58|51,92,44,85,16,30]
  left=5: Merge(A,5,6,8)   → [24,30,44,58,44,51,85,92|16,30]
  left=9: Merge(A,9,10,10) → [24,30,44,58,44,51,85,92,16,30]

step=4:
  left=1: Merge(A,1,4,8)   → [24,30,44,44,51,58,85,92|16,30]
  left=9: (left > n-step, keine Aktion)

step=8:
  left=1: Merge(A,1,8,10)  → [16,24,30,30,44,44,51,58,85,92]

Fertig!
```

### Vergleich: Rekursiv vs. Iterativ

**Gemessene Laufzeiten (in Millisekunden):**

| Anzahl Elemente | Rekursiv | Iterativ |
|-----------------|----------|----------|
| 100 | 4.50 | 3.72 |
| 200 | 9.98 | 8.36 |
| 400 | 21.88 | 18.68 |
| 800 | 47.92 | 41.24 |
| 1600 | 103.83 | 91.16 |
| 3200 | 224.86 | 199.01 |

**Iterativ ist ~12-13% schneller** (kein Rekursions-Overhead)

---

## 7. Unterscheidungsmerkmale von Teile-&-Herrsche-Algorithmen

Teile-&-Herrsche-Algorithmen unterscheiden sich in:

1. **Anzahl der Teilprobleme**
   - MergeSort: 2 Teilprobleme
   - QuickSort: 2 Teilprobleme
   - Andere: 3 oder mehr

2. **Größe der Teilprobleme**
   - MergeSort: Jeweils $n/2$
   - QuickSort: Variabel (abhängig von Pivot)

3. **Kombinationsalgorithmus**
   - MergeSort: Merge (aufwändig, $O(n)$)
   - QuickSort: Trivial (nur Konkatenation)

4. **Rekursionsabbruch**
   - Meist: Einzelne Elemente oder kleine Arrays
   - MergeSort: Array der Länge 1

---

## 📌 Zusammenfassung

### Teile & Herrsche Prinzip

**3 Schritte:**
1. **Teile** die Eingabe in Teilprobleme
2. **Herrsche** über Teilprobleme rekursiv
3. **Kombiniere** Teillösungen zur Gesamtlösung

### MergeSort

**Eigenschaften:**
- **Laufzeit:** $\Theta(n \log n)$ in allen Fällen
- **Speicher:** $O(n)$ für Hilfsarray
- **Stabil:** Ja (erhält Reihenfolge gleicher Elemente)
- **Vergleichsbasiert:** Ja

**Kern-Operationen:**
- **Teilen:** Trivial (Mitte berechnen)
- **Kombinieren:** Merge in $O(n)$

### Laufzeit-Rekursion

$$T(n) = 2T(n/2) + cn = O(n \log n)$$

**Rekursionsbaum:**
- Höhe: $\log n$
- Arbeit pro Ebene: $cn$
- Gesamt: $cn \log n$

### Varianten

| Variante | Vorteile | Nachteile |
|----------|----------|-----------|
| **Rekursiv** | Einfacher zu verstehen | Rekursions-Overhead |
| **Iterativ** | ~12% schneller | Etwas komplexer |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Algorithmen-pseudocode]] – Insertion Sort mit $O(n^2)$ zum Vergleich
- [[VL.02 Simple-Sort]] – Einfache Sortierverfahren
- [[VL.03 Komplexität]] – Laufzeitanalyse, O-Notation
- [[VL.10 Forgeschrittene Sortierverfahren]] – Quick Sort (anderes Teile-&-Herrsche-Prinzip)
- [[VL.12 Teil-&-Herrsche 2]] – Mastertheorem zur Lösung von Rekursionsgleichungen