**Class:** [[IntroProg]]  
**Date:** VL.2  
**Topics:** #SelectionSort #BubbleSort #CountSort #Sortieren #Stabilität #VergleichendesSortieren

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung stellt weitere **einfache Sortierverfahren** vor und führt **nicht-vergleichende Sortieralgorithmen** ein.

- Verständnis von **Selection Sort** (Sortieren durch Auswählen)
- Verständnis von **Bubble Sort** (Sortieren durch Vertauschen)
- Kenntnis von **Count Sort** (Sortieren durch Zählen)
- Unterscheidung zwischen **vergleichenden** und **nicht-vergleichenden** Sortierverfahren
- Konzept der **Stabilität** von Sortieralgorithmen

---

## 1. Klassifikation von Sortierverfahren

### Überblick

Sortierverfahren werden in zwei Hauptgruppen eingeteilt:

#### 1. Vergleichende Sortierverfahren

**A. Einfache Verfahren:**
- **Insertion Sort** (Sortieren durch Einfügen)
- **Selection Sort** (Sortieren durch Auswählen)
- **Bubble Sort** (Sortieren durch Vertauschen)

**B. Fortgeschrittene Verfahren:**
- **Quick Sort** (Sortieren durch Gruppieren)
- **Merge Sort** (Sortieren durch Mischen)

#### 2. Nicht-vergleichende Sortierverfahren

- **Count Sort** (Sortieren durch Zählen)
- **Radix Sort** (Sortieren durch Fachverteilen)

---

## 2. Selection Sort

### Idee

- Finde das **Minimum** der unsortierten Restfolge
- **Vertausche** es mit dem aktuellen Element
- Verkleinere den unsortierten Teil um 1

### Visualisierung

```
Sortiert | Unsortiert
---------|----------
         | [8 15 3 14 7 6 18 19]    (j=1, finde min=3)
[3]      | [15 8 14 7 6 18 19]      (swap 8 ↔ 3)
[3 6]    | [8 14 7 15 18 19]        (j=2, finde min=6, swap 15↔6)
[3 6 7]  | [14 8 15 18 19]          (j=3, finde min=7, swap 8↔7)
[3 6 7 8]| [14 15 18 19]            (j=4, finde min=8, swap 14↔8)
...
```

### Pseudocode

```
SelectionSort(Array A)
1. for j ← 1 to length(A) - 1 do
2.     min ← j
3.     for i ← j + 1 to length(A) do
4.         if A[i] < A[min] then min ← i
5.     swap(A, min, j)
```

### Funktionsweise

**Zeile 1:** Äußere Schleife läuft von Position 1 bis $n-1$

**Zeilen 2-4:** Finde Index des kleinsten Elements in $A[j+1 \ldots n]$
- Initialisiere `min = j`
- Durchlaufe Rest des Arrays
- Aktualisiere `min`, wenn kleineres Element gefunden

**Zeile 5:** Vertausche `A[min]` mit `A[j]`

### Invariante

> Nach $j$ Iterationen sind die ersten $j$ Elemente sortiert und enthalten die $j$ kleinsten Elemente des gesamten Arrays.

### Beispiel

**Gegeben:** `8 15 3 14 7 6 18 19`

| Iteration | j | min gefunden | Nach swap |
|-----------|---|--------------|-----------|
| 1 | 1 | 3 (Position 3) | `3 15 8 14 7 6 18 19` |
| 2 | 2 | 6 (Position 6) | `3 6 8 14 7 15 18 19` |
| 3 | 3 | 7 (Position 5) | `3 6 7 14 8 15 18 19` |
| 4 | 4 | 8 (Position 5) | `3 6 7 8 14 15 18 19` |
| 5 | 5 | 14 (Position 5) | `3 6 7 8 14 15 18 19` |
| ... | ... | ... | ... |

---

## 3. Bubble Sort

### Idee

- **Vergleiche** benachbarte Elemente
- **Vertausche** sie, wenn sie in falscher Reihenfolge sind
- Das größte Element "**blubbert**" (bubbles) nach oben/rechts
- Wiederhole für immer kleinere unsortierte Bereiche

### Visualisierung

```
[8 15 3 14 7 6 18 19]    Maximum blubbert nach rechts →
[8 3 14 7 6 15 18 19]    (15 > 3, swap)
[8 3 14 7 6 15 18 19]    (15 < 18, kein swap)
...
[3 8 14 7 6 15 18 19]    Nach 1. Durchlauf: 19 an Position
```

### Pseudocode

```
BubbleSort(Array A)
1. for j ← length(A) - 1 downto 1 do
2.     for i ← 1 to j do
3.         if A[i] > A[i+1] then swap(A, i, i+1)
```

### Funktionsweise

**Zeile 1:** Äußere Schleife läuft **rückwärts** von $n-1$ bis $1$
- Definiert die Grenze des unsortierten Bereichs

**Zeilen 2-3:** Innere Schleife "blubbert" das Maximum nach rechts
- Vergleiche alle benachbarten Paare von $1$ bis $j$
- Vertausche, wenn linkes Element größer als rechtes

### Invariante

> Nach $k$ Durchläufen sind die letzten $k$ Elemente sortiert (die $k$ größten Elemente).

### Besonderheit

⚠️ Bubble Sort kann in beide Richtungen arbeiten:
- **Standard:** Maxima wandern nach rechts
- **Alternativ:** Minima wandern nach links

---

## 4. Gemeinsamkeiten der einfachen Sortierverfahren

Alle drei Verfahren (**Insertion Sort, Selection Sort, Bubble Sort**):

1. **Vergleichsbasiert:** Sortieren durch Vergleichen von Elementen
2. **Schrittweise Verkleinerung:** Verkleinern das unsortierte Problem in jedem Schritt um 1
3. **In-place:** Benötigen keinen zusätzlichen Speicher (außer konstanten Overhead)
4. **Einfach zu verstehen:** Intuitive Funktionsweise

---

## 5. Stabilität von Sortierverfahren

### Definition

Ein Sortieralgorithmus ist **stabil**, wenn er die **Reihenfolge von Datensätzen mit gleichem Sortierschlüssel bewahrt**.

### Beispiel

**Eingabe:**

| ID | Name | Sortierschlüssel |
|----|------|------------------|
| 1 | Anton | 1 |
| 4 | Karla | 4 |
| 3 | Otto | 3 |
| 5 | Bettina | 5 |
| 3 | Herbert | 3 |
| 8 | Yves | 8 |
| 1 | Paula | 1 |

**Stabiles Sortieren:**
```
1 Anton
1 Paula      ← Reihenfolge von Anton/Paula bleibt erhalten
3 Otto
3 Herbert    ← Reihenfolge von Otto/Herbert bleibt erhalten
4 Karla
5 Bettina
8 Yves
```

**Instabiles Sortieren:**
```
1 Paula
1 Anton      ← Reihenfolge wurde vertauscht!
3 Otto
3 Herbert
4 Karla
5 Bettina
8 Yves
```

### Stabilität der besprochenen Algorithmen

- **Insertion Sort:** ✅ Stabil (wenn `<` statt `≤` verwendet)
- **Selection Sort:** ❌ Instabil
- **Bubble Sort:** ✅ Stabil (wenn `>` statt `≥` verwendet)

---

## 6. Count Sort (Nicht-vergleichendes Sortieren)

### Voraussetzungen

⚠️ **Count Sort funktioniert nur unter bestimmten Bedingungen:**

1. **Kleiner Wertebereich:** Werte müssen aus einem überschaubaren Bereich stammen (z.B. 1-100)
2. **Ganzzahlige Werte:** Werte müssen zum Indizieren eines Arrays geeignet sein
3. **Mehrfache Vorkommen:** Es ist wahrscheinlich, dass Werte mehrfach auftreten

### Idee

1. **Zähle** die Häufigkeit jedes Elements
2. **Berechne** daraus die Position im Zielarray
3. **Kopiere** Elemente entsprechend ihrer Häufigkeit in das Ausgabearray

### Pseudocode

```
CountSort(Array A_in, Array A_out)
1. C ist Hilfsarray mit 0 initialisiert
2. for j ← 1 to length(A_in) do
3.     C[A_in[j]] ← C[A_in[j]] + 1
4. k ← 1
5. for j ← 1 to length(C) do
6.     for i ← 1 to C[j] do
7.         A_out[k] ← j
8.         k ← k + 1
```

**Erklärung:**
- **Zeilen 2-3:** Zähle Häufigkeiten (Wert selbst ist Index!)
- **Zeile 4:** Ausgabeposition initialisieren
- **Zeilen 5-8:** Füge jedes Element entsprechend seiner Häufigkeit ein

### Beispiel 1: Einfach

**Eingabe:** `3 5 2 3 2 2 3`

**Schritt 1: Zählen**

| Wert | 1 | 2 | 3 | 4 | 5 |
|------|---|---|---|---|---|
| Anzahl | 0 | 3 | 3 | 0 | 1 |

**Schritt 2: Ausgeben**

```
Wert 1: 0-mal → nichts
Wert 2: 3-mal → [2, 2, 2, ...]
Wert 3: 3-mal → [2, 2, 2, 3, 3, 3, ...]
Wert 4: 0-mal → nichts
Wert 5: 1-mal → [2, 2, 2, 3, 3, 3, 5]
```

**Ausgabe:** `2 2 2 3 3 3 5` ✓

### Beispiel 2: Detailliert

**Eingabe:** `3 1 3 3 5 7 2 8 9 7 6 3 8 1 8 8`

**Zählarray C:**

| Index (Wert) | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|--------------|---|---|---|---|---|---|---|---|---|-----|
| Anzahl | 2 | 1 | 4 | 0 | 1 | 1 | 2 | 4 | 1 | 0 |

**Ausgabe:** `1 1 2 3 3 3 3 5 6 7 7 8 8 8 8 9`

### Komplexität

- **Zählen:** $O(n)$ - durchlaufe Eingabearray
- **Ausgeben:** $O(n + m)$ - durchlaufe Wertebereich $m$ und füge $n$ Elemente ein
- **Gesamt:** $O(n + m)$

⚠️ **Nicht immer sinnvoll einsetzbar:**
- Wenn **Stabilität** erforderlich ist (diese Version ist nicht stabil)
- Wenn der **Wertebereich zu groß** ist (z.B. $m = 10^9$)
- Bei **Floating-Point-Zahlen** (keine ganzzahligen Indizes)

---

## 📌 Zusammenfassung

### Vergleichende Sortierverfahren

| Algorithmus | Idee | Invariante | Stabil |
|-------------|------|------------|--------|
| **Insertion Sort** | Element in sortierte Folge einfügen | Erste $j-1$ Elemente sortiert | ✅ |
| **Selection Sort** | Minimum finden und vertauschen | Erste $j$ Elemente sind die $j$ kleinsten | ❌ |
| **Bubble Sort** | Benachbarte Elemente vertauschen | Letzte $k$ Elemente sortiert | ✅ |

### Nicht-vergleichende Sortierverfahren

| Algorithmus | Komplexität | Voraussetzung |
|-------------|-------------|---------------|
| **Count Sort** | $O(n + m)$ | Kleiner Wertebereich $m$, ganzzahlige Werte |

### Gemeinsame Eigenschaften (Insertion, Selection, Bubble)

- Alle drei verkleinern das Problem schrittweise um 1
- Alle drei verwenden verschachtelte Schleifen
- Alle drei sind vergleichsbasiert

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Algorithmen-pseudocode]] – Insertion Sort als Grundlage
- [[VL.03 Komplexität]] – Laufzeitanalyse aller Sortierverfahren
- [[VL.10 Forgeschrittene Sortierverfahren]] – Quick Sort, Radix Sort