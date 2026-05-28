**Class:** [[IntroProg]]  
**Date:** VL.10  
**Topics:** #Quicksort #RadixSort #CountSort #Sortierverfahren #TeileUndHerrsche #NichtVergleichend #Stabilität #Komplexität #UntereSchranke

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt **fortgeschrittene Sortierverfahren** und die theoretischen Grenzen des Sortierens.

- **Quicksort** als schnelles vergleichendes Sortierverfahren
- **Partition-Algorithmus** und Pivot-Wahl
- **Stabilität** von Sortierverfahren
- **Untere Schranke** für vergleichende Sortierverfahren: $\Omega(n \log n)$
- **Nicht-vergleichende Sortierverfahren**: Count Sort, Radix Sort
- Wann sind digitale Sortierverfahren sinnvoll?

---

## 1. Überblick Sortierverfahren

### Klassifikation

**Vergleichende Sortierverfahren:**
- **Einfach:** Insertion Sort, Selection Sort, Bubble Sort
- **Fortgeschritten:** Merge Sort, Heap Sort, **Quick Sort**

**Nicht-vergleichende Sortierverfahren:**
- **Count Sort**
- **Radix Sort**

### Vergleich der wichtigsten Verfahren

| Verfahren | Best Case | Average Case | Worst Case | Speicher | Stabil |
|-----------|-----------|--------------|------------|----------|--------|
| **Insertion Sort** | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | ✅ |
| **Selection Sort** | $O(n^2)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | ❌ |
| **Bubble Sort** | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | ✅ |
| **Merge Sort** | $O(n \log n)$ | $O(n \log n)$ | $O(n \log n)$ | $O(n)$ | ✅ |
| **Heap Sort** | $O(n \log n)$ | $O(n \log n)$ | $O(n \log n)$ | $O(1)$ | ❌ |
| **Quick Sort** | $O(n \log n)$ | $O(n \log n)$ | $O(n^2)$ | $O(\log n)$ | ❌* |
| **Count Sort** | $O(n+k)$ | $O(n+k)$ | $O(n+k)$ | $O(k)$ | ✅ |
| **Radix Sort** | $O(d \cdot n)$ | $O(d \cdot n)$ | $O(d \cdot n)$ | $O(n+k)$ | ✅ |

\*kann stabil implementiert werden

---

## 2. Quicksort - Grundprinzip

### Idee: Sortieren durch Gruppieren

**Prinzip "Teile und Herrsche":**

1. **Teile (Partition):** Wähle ein **Pivot-Element** und partitioniere das Array:
   - Alle Elemente **< Pivot** → linke Gruppe
   - Alle Elemente **≥ Pivot** → rechte Gruppe
   
2. **Herrsche (Rekursion):** Sortiere beide Gruppen rekursiv

3. **Kombiniere:** Kein explizites Kombinieren nötig – Pivot liegt bereits richtig!

### Visualisierung

```
Ausgangszustand:
[6, 4, 1, 8, 9]  Pivot = 6

Nach Partition:
[4, 1] | 6 | [8, 9]
 ↓       ↓     ↓
links  richtig rechts

Rekursion auf [4,1] und [8,9]:
[1, 4] | 6 | [8, 9]

Ergebnis:
[1, 4, 6, 8, 9]
```

### Besonderheit

⚠️ **Im Gegensatz zu Merge Sort:**
- **Merge Sort:** Einfaches Teilen, aufwändiges Kombinieren
- **Quick Sort:** Aufwändiges Teilen (Partition), triviales Kombinieren

---

## 3. Quicksort - Partition-Algorithmus

### Prinzip bei Arrays

**Ausgangszustand:**

```
[x x x x x x x x]
 start        pivot,end
```

**Nach Partition:**

```
[x x x x | x | x x x]
 < pivot pivot  ≥ pivot
```

**Pivot liegt jetzt an der richtigen finalen Position!**

### Ring-Tausch Methode (für Arrays)

1. Wähle **Pivot** (z.B. letztes Element)
2. Durchlaufe Array von links:
   - Elemente **< Pivot** → nach vorne
   - Elemente **≥ Pivot** → bleiben rechts
3. Vertausche Pivot mit erstem Element ≥ Pivot
4. Rekursion auf beide Teile

### Beispiel: Array-Partition

```
Eingabe: [6, 4, 1, 8, 9]  Pivot = 9

Schritt 1: Elemente < 9 nach links bewegen
[6, 4, 1, 8 | 9]
           part

Schritt 2: Tausche Pivot mit erstem ≥ Pivot
[6, 4, 1, 8, 9]  (Pivot bleibt)

Rekursion: links=[6,4,1,8], rechts=[]
```

---

## 4. Quicksort mit Listen

### Partition bei Listen

**Vorteil:** Einfacher als bei Arrays – kein "Ringtausch" nötig!

**Vorgehen:**
1. Wähle **Pivot** (z.B. erstes Element)
2. Erstelle **zwei neue Listen:**
   - `left`: Elemente **< Pivot**
   - `right`: Elemente **≥ Pivot**
3. Füge Elemente durch Durchlaufen ein
4. Rekursiv sortieren
5. Verketten: `left → Pivot → right`

### Beispiel: Listen-Partition

```
Ausgangsliste:
6 → 4 → 1 → 8 → 9 → NULL

Wähle Pivot = 6:

Left (< 6):   1 → 4 → NULL
Pivot:        6
Right (≥ 6):  8 → 9 → NULL

Nach rekursivem Sortieren:
Left:   1 → 4 → NULL
Right:  8 → 9 → NULL

Verkettung:
1 → 4 → 6 → 8 → 9 → NULL
```

### Pseudocode

```c
QuickSort(list tosort):
  if tosort.first = tosort.last then
      return
  
  list left, right
  pivot ← Partition(tosort, left, right)
  
  QuickSort(left)
  QuickSort(right)
  
  // Listen zusammenfügen
  if left.first = NULL then
      tosort.first ← pivot
  else
      tosort.first ← left.first
      left.last.next ← pivot
 
  if right.first = NULL then
      pivot.next ← NULL
      tosort.last ← pivot
  else
      pivot.next ← right.first
      tosort.last ← right.last
```

---

## 5. Quicksort - Komplexität

### Best Case: $O(n \log n)$

**Bedingung:** Partition teilt Array **immer in der Mitte**

```
         n              ← n Vergleiche
       /   \
      n/2  n/2          ← n Vergleiche gesamt
     / \   / \
   n/4 ... n/4          ← n Vergleiche gesamt
   
Höhe: log n
Pro Ebene: O(n)
Gesamt: O(n log n)
```

### Worst Case: $O(n^2)$

**Bedingung:** Partition teilt **extrem ungleich** (z.B. immer 0 vs. n-1)

**Beispiel:** Array bereits sortiert, Pivot = letztes Element

```
Eingabe: [1, 2, 3, 4, 5]  Pivot = 5
         ↓
Left: [1,2,3,4], Right: []

Eingabe: [1, 2, 3, 4]  Pivot = 4
         ↓
Left: [1,2,3], Right: []

... (n-1 Schritte mit je O(n) Aufwand)

Gesamt: n + (n-1) + (n-2) + ... + 1 = O(n²)
```

### Average Case: $O(n \log n)$

**Im Durchschnitt** teilt Partition relativ gleichmäßig

$$T_{\text{avg}} = O(n \log n)$$

⚠️ **Wichtig:** Quick Sort ist **in der Praxis sehr schnell**, obwohl Worst Case schlecht ist!

---

## 6. Quicksort - Pivot-Wahl Strategien

### Problem

Bei **ungünstiger Pivot-Wahl** → $O(n^2)$ Laufzeit

**Beispiel:** Fast sortierte Arrays mit Pivot = letztes Element

### Verbesserungsstrategien

| Strategie | Beschreibung | Vorteil |
|-----------|--------------|---------|
| **Zufälliger Index** | Wähle Pivot zufällig aus $[\text{start}, \text{end}]$ | Verhindert systematische Worst Cases |
| **Median-of-Three** | Pivot = Median von $\{f_{\text{start}}, f_{\frac{\text{start}+\text{end}}{2}}, f_{\text{end}}\}$ | Bessere Balance bei fast sortierten Arrays |
| **Kleinere Teilfolge zuerst** | Sortiere kleinere Partition zuerst | Minimiert Rekursionstiefe |

### Beispiel: Median-of-Three

```
Array: [8, 3, 5, 1, 9, 7, 2]
        ↑     ↑           ↑
      first middle      last

Kandidaten: {8, 5, 2}
Median: 5

Verwende 5 als Pivot!
```

**Resultat:** Auch bei fast sortierten Arrays bleibt Laufzeit $O(n \log n)$

---

## 7. Stabilität von Quicksort

### Erinnerung: Was ist Stabilität?

**Definition:** Ein Sortierverfahren ist **stabil**, wenn Elemente mit **gleichem Schlüssel** ihre **relative Reihenfolge** behalten.

**Beispiel:**

```
Eingabe:  [2₁, 3, 2₂, 5, 2₃, 1, 8]
                     (Indizes zur Unterscheidung)

Stabil:   [1, 2₁, 2₂, 2₃, 3, 5, 8]  ✅
Instabil: [1, 2₃, 2₁, 2₂, 3, 5, 8]  ❌
```

### Quicksort-Stabilität

**Standardimplementierung:** ❌ **Instabil**

**Grund:** Bei Partition können gleiche Elemente ihre Reihenfolge ändern

### Stabile Quicksort-Variante (nur bei Listen!)

**Bedingungen für Stabilität:**

1. **Pivot = erstes Element**
2. **Partition:**
   - `< Pivot` → linke Liste (am **Ende** einfügen)
   - `≥ Pivot` → rechte Liste (am **Ende** einfügen)

**Beispiel:**

```
[2₁, 3, 2₂, 5, 2₃, 1, 8]  Pivot = 2₁

Left (< 2₁):   [1]
Pivot:         2₁
Right (≥ 2₁):  [3, 2₂, 5, 2₃, 8]  (Reihenfolge erhalten!)

Nach Rekursion bleibt Reihenfolge: 2₁ vor 2₂ vor 2₃ ✅
```

⚠️ **Wichtig:** Bei anderem Pivot (z.B. letztes Element) wird Quicksort instabil!

---

## 8. Quicksort vs. Merge Sort

### Speicherbedarf

| Aspekt | Quick Sort | Merge Sort |
|--------|------------|------------|
| **Zusatzarray** | Nein | Ja (Größe $n$) |
| **Rekursionsstack** | $O(\log n)$ bis $O(n)$ | $O(\log n)$ |
| **Gesamt** | $O(\log n)$ | $O(n)$ |

### Optimierung des Rekursionsstacks

**Problem:** Bei Quicksort kann Stack sehr groß werden (Worst Case: $O(n)$)

**Lösung:** 
- **Kleinere Partition zuerst sortieren**
- Reduziert maximale Rekursionstiefe auf $O(\log n)$

**Beispiel:**

```
Nach Partition: [10 Elemente] | Pivot | [100 Elemente]

Ohne Optimierung:
- Sortiere links (10)  → Stack-Tiefe: 1
- Sortiere rechts (100) → Stack-Tiefe: 1 + log(100) ≈ 8

Mit Optimierung:
- Sortiere links (10) zuerst → Stack-Tiefe: log(10) ≈ 4
- Dann rechts (100) → Stack-Tiefe maximal log(100) ≈ 7
```

### Zusammenfassung

**Heap Sort:** 
- ✅ $O(n \log n)$ garantiert
- ✅ $O(1)$ zusätzlicher Speicher
- ✅ Einfache Implementierung

---

## 9. Untere Schranke für vergleichende Sortierverfahren

### Satz

**Jedes Sortierverfahren, das auf paarweisem Vergleich von Elementen beruht, hat eine Komplexität von:**

$$\boxed{\Omega(n \log n)}$$

**Bedeutung:** 
- Merge Sort, Heap Sort, Quick Sort (Average) sind **optimal**!
- Keine vergleichenden Verfahren können schneller sein (asymptotisch)

---

## 10. Beweis: Entscheidungsbaum

### Idee

Jedes **vergleichende Sortierverfahren** kann als **binärer Entscheidungsbaum** dargestellt werden:

- **Innere Knoten:** Vergleich zweier Elemente ($a_i \leq a_j$?)
- **Kanten:** Ergebnis des Vergleichs (ja/nein)
- **Blätter:** Mögliche Permutationen (sortierte Ausgabe)

### Beispiel: $n = 3$

```
             f₁ ≤ f₂?
            /        \
          ja          nein
          /            \
     f₁ ≤ f₃?      f₂ ≤ f₃?
     /    \         /    \
   ja     nein    ja     nein
   /        \     /        \
f₂≤f₃?   f₂≤f₃? f₁≤f₃?  f₁≤f₃?
 /  \     /  \   /  \    /  \
123 132 213 231 213 312 312 321

Blätter: 3! = 6 Permutationen
```

### Analyse

**Anzahl Blätter:** $n!$ (alle möglichen Permutationen)

**Höhe eines Binärbaums:** Baum mit $L$ Blättern hat Höhe $\geq \log_2 L$

**Also:**

$$h \geq \log_2(n!)$$

### Stirling-Approximation

$$n! \approx \sqrt{2\pi n} \left(\frac{n}{e}\right)^n$$

**Logarithmieren:**

$$\log_2(n!) \approx \log_2\left(\sqrt{2\pi n}\right) + n \log_2\left(\frac{n}{e}\right)$$

$$= \frac{1}{2}\log_2(2\pi n) + n \log_2 n - n \log_2 e$$

**Vereinfacht:**

$$\log_2(n!) = \Theta(n \log n)$$

### Fazit

$$\boxed{h \geq \log_2(n!) = \Omega(n \log n)}$$

**Jeder Pfad** von Wurzel zu Blatt = **eine Sortierung**

→ **Worst Case** = längster Pfad = Baumhöhe = $\Omega(n \log n)$

✅ **Merge Sort, Heap Sort sind optimal!**

---

## 11. Nicht-vergleichende Sortierverfahren

### Motivation

**Problem:** Vergleichende Verfahren können nicht schneller als $O(n \log n)$ sein

**Lösung:** Unter **speziellen Bedingungen** geht es schneller!

**Ansatz:** Verwende **Struktur der Daten** statt Vergleichen

### Voraussetzungen

1. **Kleiner Wertebereich** (Count Sort)
2. **Digitale Darstellung** möglich (Radix Sort)
3. Oft: **Ganzzahlige Schlüssel**

---

## 12. Count Sort (Wiederholung)

### Idee

**Zähle**, wie oft jeder Wert vorkommt → berechne **finale Position**

### Voraussetzungen

- Werte aus **kleinem Bereich** $[0, k]$
- $k = O(n)$ für optimale Laufzeit

### Algorithmus

```
CountSort(A, k):
1. Initialisiere Zähler-Array C[0..k] mit 0
2. for i ← 1 to n do
3.     C[A[i]] ← C[A[i]] + 1     // Zähle
4. for i ← 1 to k do
5.     C[i] ← C[i] + C[i-1]      // Kumulativ
6. for i ← n downto 1 do
7.     B[C[A[i]]] ← A[i]         // Platziere
8.     C[A[i]] ← C[A[i]] - 1
```

### Beispiel

```
Eingabe A: [3, 1, 3, 3, 5, 7, 2, 8, 9, 7, 6, 3, 8, 1, 8, 8]
           n = 16, k = 10

Schritt 1: Zähle
C: [0, 2, 1, 4, 0, 1, 1, 2, 4, 1, 0]
    0  1  2  3  4  5  6  7  8  9  10

Schritt 2: Kumulativ
C: [0, 2, 3, 7, 7, 8, 9, 11, 15, 16, 16]

Schritt 3: Platziere (von rechts nach links für Stabilität)
Ausgabe: [1, 1, 2, 3, 3, 3, 3, 5, 6, 7, 7, 8, 8, 8, 8, 9]
```

### Komplexität

$$T = O(n + k)$$

**Optimal wenn:** $k = O(n)$ → $T = O(n)$

✅ **Stabil:** Durchlaufen von rechts nach links erhält Reihenfolge

❌ **Problem:** Bei großem $k$ (z.B. 32-Bit Integer) unpraktisch!

---

## 13. Radix Sort

### Idee

**Sortiere stellenweise** von der **niedrigsten zur höchsten Stelle**

**Nutze Count Sort** für jede Stelle (stabil!)

### Voraussetzungen

- Werte können als **Ziffernfolge** dargestellt werden
- Alphabet der Größe $b$ (z.B. $b=10$ für Dezimal)
- Maximaler Wert: $N$
- Anzahl Stellen: $d = \log_b N$

### Algorithmus

```
RadixSort(A, d):
1. for i ← 1 to d do
2.     CountSort(A, nach Stelle i)
```

**Wichtig:** Beginne mit **niedrigster Stelle** (Einerstelle)!

### Beispiel: Dezimalsystem

**Eingabe:** `[333, 78, 77, 3, 37, 38]`

```
Schritt 1: Sortiere nach Einerstelle
[333, 3, 77, 37, 78, 38]
  3   3   7   7   8   8

Schritt 2: Sortiere nach Zehnerstelle
[3, 333, 37, 38, 77, 78]
 0   3    3   3   7   7

Schritt 3: Sortiere nach Hunderterstelle
[3, 37, 38, 77, 78, 333]
 0   0   0   0   0   3

✅ Sortiert!
```

### Warum von rechts nach links?

**Grund:** Count Sort ist **stabil**!

**Beispiel:**

```
[123, 223]

Nach Einerstelle (3):  [123, 223]  (beide enden auf 3)
Nach Zehnerstelle (2): [123, 223]  (Reihenfolge erhalten!)
Nach Hunderterstelle:  [123, 223]  (1 < 2)

Würde man links beginnen:
Nach Hunderterstelle:  [123, 223]  (1 < 2)
Nach Zehnerstelle:     [123, 223]  (beide = 2, Reihenfolge verloren!)
Nach Einerstelle:      [123, 223]  (Zufall ob richtig!)
```

---

## 14. Radix Sort - Komplexität

### Laufzeit

**Gegeben:**
- $n$ Elemente
- Größter Wert: $N$
- Basis: $b$ (Alphabet-Größe)
- Anzahl Stellen: $d = \log_b N$

**Pro Stelle:** Count Sort → $O(n + b)$

**Insgesamt:**

$$T = d \cdot O(n + b) = O(d \cdot (n + b))$$

$$= O(\log_b N \cdot (n + b))$$

### Spezialfälle

**Fall 1:** $b = O(n)$ und $\log_b N = O(1)$

$$T = O(n)$$

**Beispiel:** Sortiere $n$ Zahlen im Bereich $[0, n^2]$ mit $b = n$
- $d = \log_n(n^2) = 2$ → konstant!
- $T = O(2 \cdot (n + n)) = O(n)$

**Fall 2:** Typisch für 32-Bit Integer mit $b = 256$ (Byte)
- $d = 4$ Bytes
- $T = O(4n) = O(n)$

### Speicherplatz

$$S = O(n + b)$$

- Output-Array: $O(n)$
- Count-Array: $O(b)$

---

## 15. Wann welches Verfahren?

### Entscheidungsbaum

```
┌─ Ist Wertebereich klein (k = O(n))?
│  ├─ JA → Count Sort (O(n))
│  └─ NEIN ↓
│
├─ Sind Werte digital darstellbar?
│  ├─ JA → Radix Sort (O(d·n))
│  └─ NEIN ↓
│
├─ Ist Stabilität wichtig?
│  ├─ JA → Merge Sort (O(n log n), stabil)
│  └─ NEIN ↓
│
├─ Ist minimaler Speicher wichtig?
│  ├─ JA → Heap Sort (O(n log n), in-place)
│  └─ NEIN ↓
│
└─ Quick Sort (O(n log n) average, schnell in Praxis)
```

### Praktische Empfehlungen

| Szenario                        | Verfahren              | Begründung                   |
| ------------------------------- | ---------------------- | ---------------------------- |
| **Kleine Arrays** ($n < 20$)    | Insertion Sort         | Einfach, geringer Overhead   |
| **Ganzzahlen, kleiner Bereich** | Count Sort             | $O(n)$, sehr schnell         |
| **Ganzzahlen, großer Bereich**  | Radix Sort             | $O(d \cdot n)$ mit $d$ klein |
| **Stabilität erforderlich**     | Merge Sort             | Garantiert stabil            |
| **Wenig Speicher**              | Heap Sort              | $O(1)$ zusätzlich            |
| **Allgemeiner Fall**            | Quick Sort             | Schnellste in der Praxis     |
| **Garantierte Laufzeit**        | Merge Sort / Heap Sort | $O(n \log n)$ Worst Case     |

---

## 📌 Zusammenfassung

### Quicksort

**Prinzip:** Partition (Teile nach Pivot) → Rekursion

**Laufzeit:**
- Best/Average: $O(n \log n)$
- Worst: $O(n^2)$ (vermeidbar durch gute Pivot-Wahl)

**Eigenschaften:**
- ✅ Sehr schnell in der Praxis
- ✅ In-place (fast)
- ❌ Instabil (Standard)
- ❌ Worst Case quadratisch

### Untere Schranke

**Theorem:** Vergleichende Sortierverfahren benötigen mindestens $\Omega(n \log n)$ Vergleiche

**Beweis:** Entscheidungsbaum mit $n!$ Blättern hat Höhe $\geq \log_2(n!) = \Omega(n \log n)$

### Nicht-vergleichende Sortierverfahren

**Count Sort:**
- Laufzeit: $O(n + k)$
- Bedingung: Kleiner Wertebereich $k$
- Stabil: ✅

**Radix Sort:**
- Laufzeit: $O(d \cdot (n + b))$ mit $d = \log_b N$
- Typisch: $O(n)$ für Ganzzahlen
- Stabil: ✅
- Sortiert stellenweise

### Vergleich aller Verfahren

| Verfahren          | Laufzeit          | Speicher    | Stabil | Anwendung                 |
| ------------------ | ----------------- | ----------- | ------ | ------------------------- |
| **Insertion Sort** | $O(n^2)$          | $O(1)$      | ✅      | Kleine $n$, fast sortiert |
| **Merge Sort**     | $O(n \log n)$     | $O(n)$      | ✅      | Stabilität wichtig        |
| **Heap Sort**      | $O(n \log n)$     | $O(1)$      | ❌      | Wenig Speicher            |
| **Quick Sort**     | $O(n \log n)$ avg | $O(\log n)$ | ❌      | Allgemein, schnell        |
| **Count Sort**     | $O(n+k)$          | $O(k)$      | ✅      | Kleiner Wertebereich      |
| **Radix Sort**     | $O(d \cdot n)$    | $O(n+b)$    | ✅      | Ganzzahlen, Strings       |


---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Simple-Sort]] – Count Sort Grundlagen
- [[VL.03 Komplexität]] – Komplexitätsanalyse
- [[VL.06 Divide and Conquer]] – Merge Sort, Rekursionsprinzip
- [[VL.09 Heaps]] – Heap Sort

---

## Cheat Sheet: Quicksort Implementierung

### Array-basierter Quicksort (C)

```c
// Partition: Letztes Element als Pivot
int partition(int A[], int low, int high) {
    int pivot = A[high];
    int i = low - 1;  // Index für kleinere Elemente
    
    for (int j = low; j < high; j++) {
        if (A[j] < pivot) {
            i++;
            swap(&A[i], &A[j]);
        }
    }
    swap(&A[i+1], &A[high]);
    return i + 1;
}

// Quicksort rekursiv
void quicksort(int A[], int low, int high) {
    if (low < high) {
        int part = partition(A, low, high);
        quicksort(A, low, part - 1);
        quicksort(A, part + 1, high);
    }
}

// Aufruf
quicksort(array, 0, n-1);
```

### Optimierte Version mit Median-of-Three

```c
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int median_of_three(int A[], int low, int high) {
    int mid = (low + high) / 2;
    
    // Sortiere low, mid und high
    if (A[low] > A[mid])
        swap(&A[low], &A[mid]);
    if (A[low] > A[high])
        swap(&A[low], &A[high]);
    if (A[mid] > A[high])
        swap(&A[mid], &A[high]);
    
    // Bringe Median an die Position vor high (oder high), 
    // um ihn als Pivot zu verwenden.
    // In dieser Version setzen wir ihn an die Stelle 'high'.
    swap(&A[mid], &A[high]);
    
    return A[high]; // Gibt das Pivot-Element zurück
}
```