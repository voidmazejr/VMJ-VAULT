**Class:** [[IntroProg]]  
**Date:** VL.9  
**Topics:** #Heaps #Prioritätenschlangen #Heapsort #BinäreHalden #Heapify #BuildHeap #HeapOperationen #MaxHeap #MinHeap

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt **Heaps (Halden)** als effiziente Datenstruktur für Prioritätenschlangen und das **Heapsort-Verfahren**.

- Verständnis von **Prioritätenschlangen**
- **Heap-Eigenschaft** (Max-Heap, Min-Heap)
- **Binäre Halden** als Array-Implementierung
- **Heapify-Operation** und Laufzeitanalyse
- **Build-Heap** Algorithmus in $O(n)$
- **Heap-Operationen**: Insert, Extract-Max
- **Heapsort** Algorithmus in $O(n \log n)$

---

## 1. Prioritätenschlangen / Heaps

### Was ist eine Prioritätenschlange?

Eine **Prioritätenschlange** (Priority Queue) ist eine **abstrakte Datenstruktur**, bei der:

- Jedes Element einen **Schlüssel** (Priorität) hat
- Der Zugriff auf das **Maximum** (oder Minimum) effizient ist
- Basiert meist auf einem **partiell geordneten Baum**

### Anwendungen

- **Sortieren** (Heapsort)
- **Scheduling** (Betriebssysteme)
- **Zugriff auf Min/Max** in $O(1)$
- **Dijkstra-Algorithmus** (kürzeste Wege)
- **Event-Simulation**

---

## 2. Heap-Bedingung

### Max-Heap-Bedingung

**Definition:** In einem **Max-Heap** gilt für jeden Knoten:

$$\text{Schlüssel(Parent)} \geq \text{Schlüssel(Kind)}$$

**Konsequenz:** Das **maximale Element** ist immer an der **Wurzel**.

### Visualisierung

```
       15
      /  \
    12    10
   / \    /
  3   7  2
```

**Array-Darstellung:** `[15, 12, 10, 3, 7, 2]`

### Min-Heap-Bedingung

**Analog:** Für einen **Min-Heap** gilt:

$$\text{Schlüssel(Parent)} \leq \text{Schlüssel(Kind)}$$

**Konsequenz:** Das **minimale Element** ist an der Wurzel.

---

## 3. Binäre Halden als Arrays

### Array-Darstellung

Ein **vollständiger Binärbaum** lässt sich effizient als **Array** darstellen:

**Eigenschaften:**

- Alle Ebenen sind **voll** bis auf die letzte (linksvoll)
- Keine Pointer nötig!
- Zwei Attribute: `length(A)` und `heap-size(A)` mit `heap-size(A) ≤ length(A)`

### Beispiel

```
Array:  [15, 12, 10, 3, 7, 2]
Index:   1   2   3   4  5  6

       15 (1)
      /      \
   12 (2)    10 (3)
   /  \      /
  3(4) 7(5) 2(6)
```

### Navigation im Array

| Operation     | Formel                     |
| ------------- | -------------------------- |
| **Wurzel**    | Index `1`                  |
| **Parent(i)** | `i / 2` (Integer-Division) |
| **Left(i)**   | `2 * i`                    |
| **Right(i)**  | `2 * i + 1`                |

**Beispiele:**

- Parent von Index 5: `5/2 = 2`
- Linkes Kind von Index 2: `2*2 = 4`
- Rechtes Kind von Index 2: `2*2+1 = 5`

⚠️ **Wichtig:** Heap-Arrays starten bei **Index 1**, nicht 0!

---

## 4. Max-Heap-Eigenschaft (formal)

### Definition

Für jeden Knoten $i$ außer der Wurzel gilt:

$$A[\text{Parent}(i)] \geq A[i]$$

**Äquivalent für Min-Heap:**

$$A[\text{Parent}(i)] \leq A[i]$$

### Beispiel

```
Array: [15, 12, 10, 3, 7, 2]

✅ A[1]=15 ≥ A[2]=12  (Parent von 2)
✅ A[1]=15 ≥ A[3]=10  (Parent von 3)
✅ A[2]=12 ≥ A[4]=3   (Parent von 4)
✅ A[2]=12 ≥ A[5]=7   (Parent von 5)
✅ A[3]=10 ≥ A[6]=2   (Parent von 6)
```

---

## 5. Heapify-Operation

### Zweck

**Heapify(A, i)** stellt die Heap-Eigenschaft für den Unterbaum mit Wurzel $i$ wieder her.

**Voraussetzung:**

- Die Unterbäume von `Left(i)` und `Right(i)` sind **bereits Heaps**
- Nur `A[i]` verletzt möglicherweise die Heap-Eigenschaft

### Algorithmus

```
Heapify(A, i):
1.  l ← Left(i)
2.  r ← Right(i)
3.  if l ≤ heap-size(A) and A[l] > A[i] then
4.      largest ← l
5.  else
6.      largest ← i
7.  if r ≤ heap-size(A) and A[r] > A[largest] then
8.      largest ← r
9.  if largest ≠ i then
10.     A[i] ↔ A[largest]
11.     Heapify(A, largest)
```

### Funktionsweise

1. **Finde größtes Element** unter `A[i]`, `A[Left(i)]`, `A[Right(i)]`
2. Wenn `A[i]` nicht das Größte ist:
    - **Tausche** `A[i]` mit dem größten Kind
    - **Rekursiv** Heapify für den betroffenen Unterbaum aufrufen

### Beispiel: Heapify(A, 1)

**Ausgangszustand:** `[4, 12, 10, 3, 7, 2]`

```
Schritt 1: A[1]=4 verletzt Heap-Eigenschaft
          4
        /   \
      12     10
     / \     /
    3   7   2
    
Schritt 2: Tausche A[1] mit A[2] (12 ist größer)
          12
        /    \
       4      10
      / \     /
     3   7   2

Schritt 3: Heapify(A, 2) - tausche A[2] mit A[5]
          12
        /    \
       7      10
      / \     /
     3   4   2

✅ Heap-Eigenschaft hergestellt!
```

---

## 6. Heapify - Laufzeitanalyse

### Satz

Die Laufzeit von `Heapify(A, i)` ist $O(h)$, wobei $h$ die **Höhe** des Knotens $i$ ist.

### Beweis (Induktion über $h$)

**Induktionsanfang ($h = 0$):**

- Knoten ist Blatt
- Zeile 4/6: `largest` wird auf `i` gesetzt
- Zeile 7/8: Keine Änderung
- Zeile 9-11: Kein rekursiver Aufruf
- Laufzeit: $c$ (konstant)

**Induktionsvoraussetzung:**

- Für Knoten der Höhe $h$ ist die Laufzeit $\leq c \cdot h$

**Induktionsschritt ($h \to h+1$):**

- Zeile 3-8: Konstante Zeit $c$
- Zeile 10-11: Rekursiver Aufruf mit Kind der Höhe $h$
- Nach I.V.: Laufzeit des Rekursionsaufrufs $\leq c \cdot h$
- **Gesamtlaufzeit:** $c + c \cdot h = c(h+1)$

**Für vollständigen Heap:** $h = \log n$

$$\boxed{T_{\text{Heapify}} = O(\log n)}$$

---

## 7. Build-Heap - Heap aufbauen

### Idee

**Baue Heap von unten nach oben auf:**

- Jedes **Blatt** ist bereits ein Heap (Höhe 0)
- Für alle inneren Knoten (von rechts nach links): Heapify aufrufen

### Algorithmus

```
Build-Heap(A):
1. heap-size(A) ← length(A)
2. for i ← length(A)/2 downto 1 do
3.     Heapify(A, i)
```

**Warum `length(A)/2`?**

- Knoten mit Index $> \lfloor n/2 \rfloor$ sind **Blätter**
- Blätter erfüllen automatisch die Heap-Eigenschaft

### Beispiel: Build-Heap

**Input:** `[3, 7, 10, 12, 2, 4]`

```
Start:         3
             /   \
           7      10
          / \     /
        12   2   4

i=3: Heapify(A,3) → keine Änderung (10 > 4)
i=2: Heapify(A,2) → tausche 7 mit 12
              3
            /   \
          12     10
         / \     /
        7   2   4

i=1: Heapify(A,1) → tausche 3 mit 12, dann 3 mit 7
             12
           /    \
          7      10
         / \     /
        3   2   4

✅ Heap aufgebaut!
```

---

## 8. Build-Heap - Laufzeitanalyse

### Einfache Analyse (zu pessimistisch)

- $n$ Knoten im Baum
- Jedes Heapify: $O(\log n)$
- $n$ Aufrufe von Heapify

$$\Rightarrow O(n \log n)$$

❌ **Aber:** Diese Analyse ist **nicht scharf**!

### Schärfere Analyse

**Beobachtung:** In einem vollständigen Binärbaum der Höhe $H$:

- $2^0 = 1$ Knoten mit Höhe $H$ (Wurzel)
- $2^1 = 2$ Knoten mit Höhe $H-1$
- $2^2 = 4$ Knoten mit Höhe $H-2$
- $\vdots$
- $2^H$ Knoten mit Höhe $0$ (Blätter)

**Gesamtlaufzeit:**

$$T = O\left(\sum_{h=0}^{H} h \cdot 2^{H-h}\right)$$

### Umformung

$$\begin{align} T &= O\left(\sum_{h=0}^{H} h \cdot 2^{H-h}\right) \ &= O\left(\sum_{h=0}^{H} \frac{h \cdot 2^H}{2^h}\right) \ &= O\left(2^H \cdot \sum_{h=0}^{H} \frac{h}{2^h}\right) \end{align}$$

**Geometrische Reihe:**

$$\sum_{k=0}^{\infty} k \cdot q^k = \frac{q}{(1-q)^2} \quad \text{für } |q| < 1$$

Mit $q = \frac{1}{2}$:

$$\sum_{h=0}^{\infty} \frac{h}{2^h} = \frac{1/2}{(1/2)^2} = \frac{1/2}{1/4} = 2$$

**Also:**

$$T = O(2^H \cdot 2)$$

Da $2^H < n$ (vollständiger Baum mit $n$ Knoten):

$$\boxed{T_{\text{Build-Heap}} = O(n)}$$

✅ **Heap kann in linearer Zeit aufgebaut werden!**

---

## 9. Heap-Extract-Max

### Zweck

Entfernt und gibt das **maximale Element** (Wurzel) zurück.

### Algorithmus

```
Heap-Extract-Max(A):
1. if heap-size(A) < 1 then
2.     error "Heap ist leer"
3. max ← A[1]
4. A[1] ← A[heap-size(A)]
5. heap-size(A) ← heap-size(A) - 1
6. Heapify(A, 1)
7. return max
```

### Funktionsweise

1. **Speichere** Maximum `A[1]`
2. **Ersetze** Wurzel durch letztes Element
3. **Verkleinere** Heap-Größe
4. **Stelle Heap-Eigenschaft** mit Heapify wieder her

### Beispiel

```
Start: [12, 7, 10, 3, 2, 4]
          12
        /    \
       7      10
      / \     /
     3   2   4

Schritt 1: max = 12
Schritt 2: A[1] = A[6] = 4
Schritt 3: heap-size = 5

          4
        /   \
       7     10
      / \
     3   2

Schritt 4: Heapify(A, 1)
          10
        /    \
       7      4
      / \
     3   2

✅ Neues Maximum: 10
```

### Laufzeit

$$\boxed{O(\log n)}$$

---

## 10. Heap-Insert

### Zweck

Fügt ein neues Element in den Heap ein.

### Algorithmus

```
Heap-Insert(A, key):
1. heap-size(A) ← heap-size(A) + 1
2. i ← heap-size(A)
3. while i > 1 and A[Parent(i)] < key do
4.     A[i] ← A[Parent(i)]
5.     i ← Parent(i)
6. A[i] ← key
```

### Funktionsweise

1. **Vergrößere** Heap um 1
2. **Füge neues Element** am Ende ein
3. **"Bubble up":** Lasse Element aufsteigen, bis Heap-Eigenschaft erfüllt

### Beispiel: Heap-Insert(A, 11)

```
Start: [10, 7, 4, 3, 2]
          10
        /    \
       7      4
      / \
     3   2

Schritt 1: Füge 11 am Ende ein
          10
        /    \
       7      4
      / \     /
     3   2  11

Schritt 2: 11 > 4 → tausche
          10
        /    \
       7      11
      / \     /
     3   2   4

Schritt 3: 11 > 10 → tausche
          11
        /    \
       7      10
      / \     /
     3   2   4

✅ Heap-Eigenschaft hergestellt!
```

### Laufzeit

$$\boxed{O(\log n)}$$

(Element kann maximal bis zur Wurzel aufsteigen, Höhe = $\log n$)

---

## 11. Heapsort

### Idee

1. **Build-Heap:** Baue Heap aus unsortiertem Array → $O(n)$
2. **Wiederhole** $n-1$ mal:
    - **Tausche** Wurzel (Maximum) mit letztem Element
    - **Verkleinere** Heap-Größe
    - **Heapify** die neue Wurzel → $O(\log n)$

### Algorithmus

```
Heapsort(A):
1. Build-Heap(A)
2. for i ← length(A) downto 2 do
3.     A[1] ↔ A[i]
4.     heap-size(A) ← heap-size(A) - 1
5.     Heapify(A, 1)
```

### Beispiel

**Input:** `[11, 7, 10, 3, 2, 4]`

```
Nach Build-Heap:
[11, 7, 10, 3, 2, 4]
          11
        /    \
       7      10
      / \     /
     3   2   4

Iteration 1: Tausche 11 mit 4, Heapify
[10, 7, 4, 3, 2 | 11]
          10
        /    \
       7      4
      / \
     3   2

Iteration 2: Tausche 10 mit 2, Heapify
[7, 3, 4, 2 | 10, 11]
          7
        /   \
       3     4
      /
     2

... (fortsetzung)

Endergebnis:
[2, 3, 4, 7, 10, 11]
```

### Laufzeit

$$\boxed{T_{\text{Heapsort}} = O(n) + n \cdot O(\log n) = O(n \log n)}$$

**Komponenten:**

- Build-Heap: $O(n)$
- $n-1$ mal Heapify: $(n-1) \cdot O(\log n) = O(n \log n)$

---

## 12. Korrektheitsbeweis: Build-Heap

### Satz

Nach Ausführung von `Build-Heap(A)` erfüllt das Array `A` die Heap-Eigenschaft.

### Beweis (Schleifeninvariante)

**Invariante:** Zu Beginn jeder Iteration gilt:

> Alle Knoten mit Index $> i$ haben bereits die Heap-Eigenschaft in ihren Unterbäumen.

**Initialisierung:**

- $i = \lfloor n/2 \rfloor$
- Alle Knoten $> \lfloor n/2 \rfloor$ sind **Blätter** → erfüllen Heap-Eigenschaft trivial

**Erhaltung:**

- **Vorher:** Unterbäume der Kinder von $i$ sind Heaps (Inv.)
- Nach `Heapify(A, i)`: Unterbaum von $i$ ist Heap
- $i$ wird dekrementiert
- **Nachher:** Alle Knoten $> i-1$ sind Heaps ✓

**Terminierung:**

- Nach Schleife: $i = 0$
- Alle Knoten $> 0$ (d.h. alle Knoten) sind Heaps
- Insbesondere Wurzel (Index 1) → **gesamtes Array ist Heap** ✓

---

## 13. Heap-Operationen - Zusammenfassung

|Operation|Beschreibung|Laufzeit|
|---|---|---|
|`Build-Heap(A)`|Heap aus Array aufbauen|$O(n)$|
|`Heapify(A, i)`|Heap-Eigenschaft wiederherstellen|$O(\log n)$|
|`Heap-Insert(A, key)`|Element einfügen|$O(\log n)$|
|`Heap-Extract-Max(A)`|Maximum entfernen und zurückgeben|$O(\log n)$|
|`Heap-Maximum(A)`|Maximum zurückgeben (ohne Entfernen)|$O(1)$|

---

## 📌 Zusammenfassung

### Heap-Eigenschaften

**Max-Heap:**

- Wurzel enthält **Maximum**
- Parent $\geq$ Kinder
- Zugriff auf Maximum in $O(1)$

**Min-Heap:**

- Wurzel enthält **Minimum**
- Parent $\leq$ Kinder
- Zugriff auf Minimum in $O(1)$

### Array-Implementierung

```
Index:     1   2   3   4   5   6
Array:   [15, 12, 10, 3, 7, 2]

Navigation:
- Parent(i) = i/2
- Left(i)   = 2*i
- Right(i)  = 2*i+1
```

### Wichtige Algorithmen

| Algorithmus    | Laufzeit      | Anwendung                         |
| -------------- | ------------- | --------------------------------- |
| **Heapify**    | $O(\log n)$   | Heap-Eigenschaft lokal herstellen |
| **Build-Heap** | $O(n)$        | Gesamten Heap aufbauen            |
| **Heapsort**   | $O(n \log n)$ | Sortieren                         |

### Vorteile von Heapsort

✅ **Garantierte Laufzeit:** $O(n \log n)$ im Worst Case  
✅ **In-Place:** Kein zusätzlicher Speicherplatz nötig  
✅ **Einfache Implementierung**

❌ **Nachteil:** Nicht stabil (gleiche Elemente können Reihenfolge ändern)

### Vergleich mit anderen Sortierverfahren

|Verfahren|Worst Case|Average Case|Speicher|Stabil|
|---|---|---|---|---|
|**Heapsort**|$O(n \log n)$|$O(n \log n)$|$O(1)$|❌|
|**Merge Sort**|$O(n \log n)$|$O(n \log n)$|$O(n)$|✅|
|**Quick Sort**|$O(n^2)$|$O(n \log n)$|$O(\log n)$|❌|
|**Insertion Sort**|$O(n^2)$|$O(n^2)$|$O(1)$|✅|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Bäume]] – Binärbäume, Baumhöhe
- [[VL.06 Divide and Conquer]] – Merge Sort (ähnliche Laufzeit)
- [[VL.10 Fortgeschrittene Sortierverfahren]] – Quick Sort, Radix Sort
- [[VL.11 AVL Bäume]] – Balancierte Bäume für effiziente Suche

---

## Cheat Sheet: Heap-Operationen

```c
// Array-basierte Heap-Implementierung (Max-Heap)
// Array-Indizes starten bei 1!

#define PARENT(i) ((i)/2)
#define LEFT(i)   (2*(i))
#define RIGHT(i)  (2*(i)+1)

// Heapify: Stelle Heap-Eigenschaft für Unterbaum i her
void heapify(int A[], int heap_size, int i) {
    int l = LEFT(i);
    int r = RIGHT(i);
    int largest = i;
    
    if (l <= heap_size && A[l] > A[i])
        largest = l;
    if (r <= heap_size && A[r] > A[largest])
        largest = r;
    
    if (largest != i) {
        swap(&A[i], &A[largest]);
        heapify(A, heap_size, largest);
    }
}

// Build-Heap: Baue Heap in O(n)
void build_heap(int A[], int n) {
    for (int i = n/2; i >= 1; i--) {
        heapify(A, n, i);
    }
}

// Heapsort: Sortiere Array in O(n log n)
void heapsort(int A[], int n) {
    build_heap(A, n);
    int heap_size = n;
    
    for (int i = n; i >= 2; i--) {
        swap(&A[1], &A[i]);
        heap_size--;
        heapify(A, heap_size, 1);
    }
}

// Extract-Max: Entferne und gib Maximum zurück
int extract_max(int A[], int *heap_size) {
    if (*heap_size < 1) {
        fprintf(stderr, "Heap underflow\n");
        exit(1);
    }
    int max = A[1];
    A[1] = A[*heap_size];
    (*heap_size)--;
    heapify(A, *heap_size, 1);
    return max;
}

// Insert: Füge Element ein
void heap_insert(int A[], int *heap_size, int key) {
    (*heap_size)++;
    int i = *heap_size;
    
    while (i > 1 && A[PARENT(i)] < key) {
        A[i] = A[PARENT(i)];
        i = PARENT(i);
    }
    A[i] = key;
}
```