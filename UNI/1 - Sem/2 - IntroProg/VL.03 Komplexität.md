**Class:** [[IntroProg]]  
**Date:** VL.3  
**Topics:** #Laufzeitanalyse #Komplexität #BigO #Omega #Theta #AsymptotischeAnalyse #Maschinenmodell

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung vermittelt die **mathematischen Grundlagen zur Analyse von Algorithmen**. Ziel ist es, die Effizienz von Algorithmen formal zu bewerten.

- Verständnis des **Maschinenmodells** (Random Access Machine)
- **Laufzeitanalyse** von Algorithmen
- **O-Notation** und asymptotische Schranken
- **Ω-Notation** und **Θ-Notation**
- **Worst-Case, Average-Case, Best-Case** Analysen
- **Raumkomplexität** (Speicherplatzanalyse)

---

## 1. Grundlagen der Laufzeitanalyse

### Warum Laufzeitanalyse?

**Kernfrage:** Wie kann man die Laufzeit eines Algorithmus vorhersagen?

Die Laufzeit hängt ab von:
- **Größe der Eingabe** (Parameter $n$)
- **Art der Eingabe** (z.B. sortiert vs. unsortiert)

**Beispiel Insertion Sort:**
- Schnell auf aufsteigend sortierten Arrays
- Langsam auf absteigend sortierten Arrays

### Ziel der Analyse

Finde **Schranken** (Garantien) für die Laufzeit:
- **Obere Schranken:** $f$ mit $f(n) \geq T(n)$
- **Untere Schranken:** $f$ mit $f(n) \leq T(n)$

---

## 2. Maschinenmodell (Random Access Machine)

Um Algorithmen unabhängig von Hardware zu analysieren, benötigen wir ein abstraktes Maschinenmodell.

### Uniformes Modell

- **Eine Pseudocode-Instruktion** braucht **einen Zeitschritt**
- Wird eine Instruktion $r$-mal aufgerufen → $r$ Zeitschritte
- Die **Zahlengröße spielt keine Rolle**

### Logarithmisches Modell (üblich)

- **Rechen- und Speicheroperationen** werden per Bit berechnet
- Die Größe der Zahlen ist wichtig und geht **logarithmisch** ein
- Operation auf $k$-Bit-Zahlen (Zahlen bis $2^k$) braucht $k$ Zeitschritte
- Wird $r$-mal aufgerufen → $r \cdot k$ Zeitschritte

⚠️ **Hinweis:** Oft sind die Ergebnisse gleich, da der Zahlenbereich auf `int`, `long` beschränkt ist (konstante Bitlänge).

---

## 3. Laufzeitanalyse - Beispiele

### Beispiel 1: Linearer Algorithmus

```
LineareMethode(int n)
1. sum ← 0                    // 1 Zeitschritt
2. for i ← 1 to n do          // n+1 Zeitschritte
3.     sum ← sum + 1          // n Zeitschritte
```

**Laufzeit:** $T(n) = 1 + (n+1) + n = 2n + 2$

### Beispiel 2: Quadratischer Algorithmus

```
QuadratischeMethode(int n)
1. sum ← 0                    // 1 Zeitschritt
2. for i ← 1 to n do          // n+1 Zeitschritte
3.     for j ← 1 to n do      // n * (n+1) Zeitschritte
4.         sum ← sum + 1      // n² Zeitschritte
```

**Laufzeit:** $T(n) = 1 + (n+1) + n(n+1) + n^2 = 2n^2 + n + 2$

### Beispiel 3: Kubischer Algorithmus

```
KubischeMethode(int n)
1. sum ← 0                    // 1 Zeitschritt
2. for i ← 1 to n do          // n+1 Zeitschritte
3.     for j ← 1 to n do      // n * (n+1) Zeitschritte
4.         for k ← 1 to n do  // n² * (n+1) Zeitschritte
5.             sum ← sum + 1  // n³ Zeitschritte
```

**Laufzeit:** $T(n) = 1 + (n+1) + n(n+1) + n^2(n+1) + n^3$

---

## 4. Asymptotische Analyse

### Problem mit exakten Laufzeiten

- **Konstante Faktoren** sind wenig aussagekräftig
- Hängen von Rechnerarchitektur, Compiler, Implementierung ab
- Beispiel: $100n$ vs. $5n^2$
  - Für kleine $n$: $5n^2$ schneller
  - Für große $n$: $100n$ wird **beliebig viel schneller**

### Idee der asymptotischen Analyse

1. **Ignoriere konstante Faktoren**
2. Betrachte das **Verhältnis von Laufzeiten** für $n \to \infty$
3. Klassifiziere Laufzeiten durch **einfache Vergleichsfunktionen**

---

## 5. O-Notation (Obere Schranke)

### Definition

$$f(n) \in O(g(n)) = \{f(n) : \exists c > 0, \exists n_0 > 0, \forall n \geq n_0 : f(n) \leq c \cdot g(n)\}$$

**Interpretation:** $f(n)$ wächst für $n \to \infty$ **höchstens so stark** wie $g(n)$.

### Beispiele

| Aussage | Korrekt? | Begründung |
|---------|----------|------------|
| $10n \in O(n)$ | ✅ | Wähle $c = 10$, $n_0 = 1$ |
| $10n \in O(n^2)$ | ✅ | $n^2$ wächst stärker als $n$ |
| $n^2 \in O(1000n)$ | ❌ | $n^2$ wächst stärker als $n$ |
| $O(1000n) = O(n)$ | ✅ | Konstanten werden ignoriert |

### Hierarchie

$$O(1) \subseteq O(\log n) \subseteq O(n) \subseteq O(n \log n) \subseteq O(n^2) \subseteq O(n^c) \subseteq O(2^n) \subseteq O(n!)$$

(für $c \geq 2$)

---

## 6. Ω-Notation (Untere Schranke)

### Definition

$$f(n) \in \Omega(g(n)) = \{f(n) : \exists c > 0, \exists n_0 > 0, \forall n \geq n_0 : f(n) \geq c \cdot g(n)\}$$

**Interpretation:** $f(n)$ wächst für $n \to \infty$ **mindestens so stark** wie $g(n)$.

### Beispiele

| Aussage | Korrekt? |
|---------|----------|
| $10n \in \Omega(n)$ | ✅ |
| $1000n \in \Omega(n^2)$ | ❌ |
| $n^2 \in \Omega(n)$ | ✅ |
| $\Omega(1000n) = \Omega(n)$ | ✅ |

### Beziehung zu O-Notation

$$f(n) \in \Omega(g(n)) \Leftrightarrow g(n) \in O(f(n))$$

---

## 7. Θ-Notation (Präzise Schranke)

### Definition

$$f(n) \in \Theta(g(n)) \Leftrightarrow f(n) \in O(g(n)) \text{ und } f(n) \in \Omega(g(n))$$

**Alternativ:**
$$f(n) \in \Theta(g(n)) = \{f(n) : \exists c_1 > 0, \exists c_2 > 0, \exists n_0 > 0, \forall n \geq n_0 : c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)\}$$

**Interpretation:** $f(n)$ und $g(n)$ wachsen **gleich stark**.

### Beispiele

| Aussage | Korrekt? |
|---------|----------|
| $1000n \in \Theta(n)$ | ✅ |
| $10n^2 + 1000n \in \Theta(n^2)$ | ✅ |
| $n^{1-\sin(n)} \in \Theta(n)$ | ❌ |

---

## 8. Weitere Notationen

### o-Notation (Echte obere Schranke)

$$f(n) \in o(g(n)) = \{f(n) : \forall c > 0, \exists n_0 > 0, \forall n \geq n_0 : f(n) < c \cdot g(n)\}$$

**Beispiele:**
- $n \in o(n^2)$ ✅
- $n \notin o(n)$ ❌

### ω-Notation (Echte untere Schranke)

$$f(n) \in \omega(g(n)) = \{f(n) : \forall c > 0, \exists n_0 > 0, \forall n \geq n_0 : f(n) > c \cdot g(n)\}$$

**Beispiele:**
- $n^2 \in \omega(n)$ ✅
- $n \notin \omega(n)$ ❌

### Zusammenfassung der Notationen

| Notation | Bedeutung | Vergleich |
|----------|-----------|-----------|
| $f \in o(g)$ | Wachstum von $f$ **<** Wachstum von $g$ | < |
| $f \in O(g)$ | Wachstum von $f$ **≤** Wachstum von $g$ | ≤ |
| $f \in \Theta(g)$ | Wachstum von $f$ **=** Wachstum von $g$ | = |
| $f \in \Omega(g)$ | Wachstum von $f$ **≥** Wachstum von $g$ | ≥ |
| $f \in \omega(g)$ | Wachstum von $f$ **>** Wachstum von $g$ | > |

---

## 9. Typische Laufzeitklassen

Von schnell zu langsam:

| Klasse | Name | Beispiel |
|--------|------|----------|
| $O(1)$ | Konstant | Array-Zugriff `A[5]` |
| $O(\log n)$ | Logarithmisch | Binäre Suche |
| $O(\sqrt{n})$ | Wurzel | Primzahltest |
| $O(n)$ | Linear | Lineares Suchen |
| $O(n \log n)$ | Super-linear | Merge Sort, Quick Sort |
| $O(n^2)$ | Quadratisch | Insertion Sort, Selection Sort, Bubble Sort |
| $O(n^c)$ | Polynomiell | (für $c > 2$) |
| $O(2^n)$ | Exponentiell | Subset-Probleme |
| $O(n!)$ | Faktoriell | Traveling Salesman (brute force) |

---

## 10. Laufzeitanalyse: Best, Average, Worst Case

### Definitionen

**Worst-Case Analyse** (üblich):
- $T(n) =$ Maximum über alle Eingaben der Größe $n$
- Garantie für **jede** Eingabe

**Average-Case Analyse:**
- $T(n) =$ Durchschnitt über alle Eingaben der Größe $n$
- Hängt von Verteilung der Eingaben ab

**Best-Case Analyse** (selten):
- $T(n) =$ Minimum über alle Eingaben der Größe $n$
- **Keine** Garantie für beliebige Eingaben

---

## 11. Laufzeitanalyse der Sortieralgorithmen

### Insertion Sort - Detailliert

```
InsertionSort(Array A)
1. for j ← 2 to length(A) do          // n Zeitschritte
2.     key ← A[j]                      // n-1 Zeitschritte
3.     i ← j-1                         // n-1 Zeitschritte
4.     while i>0 and A[i]>key do       // n-1 + ∑tj Zeitschritte
5.         A[i+1] ← A[i]               // ∑tj Zeitschritte
6.         i ← i-1                     // ∑tj Zeitschritte
7.     A[i+1] ← key                    // n-1 Zeitschritte
```

Wobei $t_j$ = Anzahl Wiederholungen der while-Schleife bei Index $j$

**Gesamtlaufzeit:** $T(n) = 5n - 4 + 3\sum_{j=2}^{n} t_j$

#### Worst-Case (absteigend sortiert)

$t_j = j - 1$ für jedes $j$

$$T(n) = 5n - 4 + 3\sum_{j=2}^{n}(j-1) = 2n - 4 + 3\sum_{j=1}^{n}j$$

$$= 2n - 4 + 3 \cdot \frac{n(n+1)}{2} = \frac{3n^2 + 7n - 8}{2}$$

$$\Rightarrow T(n) \in \Theta(n^2)$$

#### Best-Case (aufsteigend sortiert)

$t_j = 0$ für jedes $j$ (while-Schleife wird nie ausgeführt)

$$T(n) = 5n - 4 = O(n)$$

### Selection Sort

```
SelectionSort(Array A)
1. for j ← 1 to length(A) - 1 do
2.     min ← j
3.     for i ← j + 1 to length(A) do
4.         if A[i] < A[min] then min ← i
5.     swap(A, min, j)
```

**Worst-Case Laufzeit:**
- Suchen des Minimums: Im $j$-ten Durchlauf $c''(n-j+1)$ Operationen
- Gesamt: $T(n) = c' \cdot n + c'' \sum_{i=1}^{n-1}i = c' \cdot n + c'' \cdot \frac{n(n-1)}{2}$

$$\Rightarrow T(n) \in \Theta(n^2)$$

⚠️ **Wichtig:** Selection Sort hat **immer** $O(n^2)$ Laufzeit, unabhängig von der Eingabe!

### Bubble Sort

```
BubbleSort(Array A)
1. for j ← length(A) - 1 downto 1 do
2.     for i ← 1 to j do
3.         if A[i] > A[i+1] then swap(A, i, i+1)
```

**Worst-Case Laufzeit:** $T(n) \in \Theta(n^2)$

### Count Sort

```
CountSort(Array A_in, Array A_out)
1. C ist Hilfsarray mit 0 initialisiert  // O(m)
2. for j ← 1 to length(A_in) do          // O(n)
3.     C[A_in[j]] ← C[A_in[j]] + 1       // O(n)
4. k ← 1                                 // O(1)
5. for j ← 1 to length(C) do             // O(m)
6.     for i ← 1 to C[j] do              // O(n) insgesamt
7.         A_out[k] ← j                  // O(n)
8.         k ← k + 1                     // O(n)
```

**Laufzeit:** $T(n, m) = O(n + m)$

⚠️ **Ist $m = O(n)$, dann hat Count Sort lineare Laufzeit!**

---

## 12. Zusammenfassung der Sortieralgorithmen

| Algorithmus | Best Case | Average Case | Worst Case | Speicher |
|-------------|-----------|--------------|------------|----------|
| **Insertion Sort** | $\Theta(n)$ | $\Theta(n^2)$ | $\Theta(n^2)$ | $O(1)$ |
| **Selection Sort** | $\Theta(n^2)$ | $\Theta(n^2)$ | $\Theta(n^2)$ | $O(1)$ |
| **Bubble Sort** | $\Theta(n)$ | $\Theta(n^2)$ | $\Theta(n^2)$ | $O(1)$ |
| **Count Sort** | $\Theta(n+m)$ | $\Theta(n+m)$ | $\Theta(n+m)$ | $O(m)$ |

---

## 13. Raumkomplexität (Speicherplatzanalyse)

### Wichtige Aspekte

- **Speicherbedarf** ist wichtig, aber oft **weniger selektiv** als Laufzeit
- Unterschiedliche Algorithmen haben meist nur **konstante Faktoren** Unterschied
- **Trade-off:** Zeit kann durch Speicher ersetzt werden (und umgekehrt)
  - Beispiel: **Memoization** - Ergebnisse speichern statt neu berechnen
- Speicherbedarf wächst meist mit Datenmenge
- **Mehr als quadratisches Wachstum ist selten**

### Beispiele

- **Insertion Sort, Selection Sort, Bubble Sort:** $O(1)$ zusätzlicher Speicher (in-place)
- **Count Sort:** $O(m)$ für Hilfsarray

---

## 📌 Zusammenfassung

### Rechenmodell
- Abstrahiert von Hardware-Details
- Jede Pseudocode-Operation = 1 Zeitschritt

### Laufzeitanalyse
- **Normalerweise Worst-Case**
- **Asymptotische Analyse** für $n \to \infty$
- **Ignorieren von Konstanten** → O-Notation

### Notationen
- **O:** Obere Schranke ($\leq$)
- **Ω:** Untere Schranke ($\geq$)
- **Θ:** Präzise Schranke ($=$)
- **o, ω:** Echte Schranken (<, >)

### Laufzeitklassen
$$O(1) < O(\log n) < O(n) < O(n \log n) < O(n^2) < O(2^n) < O(n!)$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Algorithmen-pseudocode]] - Insertion Sort Algorithmus
- [[VL.02 Simple-Sort]] - Selection Sort, Bubble Sort, Count Sort
- [[VL.07 Korrektheitsbeweis]] - Korrektheit und Terminierung
- [[VL.10 Forgeschrittene Sortierverfahren]] - Quick Sort $O(n \log n)$, Radix Sort