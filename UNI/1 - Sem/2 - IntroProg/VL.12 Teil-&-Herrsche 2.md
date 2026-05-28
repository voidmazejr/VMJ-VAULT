**Class:** [[IntroProg]]  
**Date:** VL.12  
**Topics:** #TeileUndHerrsche #DivideAndConquer #Rekursionsgleichung #Mastertheorem #BinäreSuche #IntegerMultiplikation #Karatsuba #Laufzeit

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung generalisiert das algorithmische Prinzip „Teile & Herrsche" und führt das **Mastertheorem** ein.

- **Rekursionsgleichung** $T(n) = a \cdot T(n/b) + f(n)$ verstehen und anwenden
- **Binäre Suche** als Teile-&-Herrsche-Algorithmus analysieren
- **Integer-Multiplikation** (Schulmethode vs. Karatsuba-Algorithmus)
- **Mastertheorem**: Laufzeit direkt ablesen
- Wann lohnt sich Teile & Herrsche?

---

## 1. Teile & Herrsche – Generalisierung

### Prinzip (Wiederholung)

1. **Teile** Eingabe in mehrere Teile auf
2. **Löse** das Problem rekursiv auf den Teilen
3. **Füge** die Teillösungen zu einer Gesamtlösung zusammen

### Unterschiede zwischen T&H-Algorithmen

Teile-&-Herrsche-Algorithmen unterscheiden sich in:

- **Anzahl der Teilprobleme** ($a$)
- **Größe der Teilprobleme** ($n/b$, bestimmt Höhe des Rekursionsbaums)
- **Algorithmus** für das Zusammensetzen der Teillösungen ($f(n)$)
- **Rekursionsabbruch**

### Wann lohnt sich T&H?

Kann durch **Laufzeitanalyse** vorhergesagt werden. Die Laufzeit hängt ab von: Anzahl der Teilprobleme, Größe der Teilprobleme, Aufwand für das Zusammensetzen.

---

## 2. Allgemeine Rekursionsgleichung

### Form

$$\boxed{T(n) = a \cdot T!\left(\frac{n}{b}\right) + f(n)}$$

unter der Annahme $T(1) = \text{const}$, wobei:

|Parameter|Bedeutung|
|---|---|
|$a$|Anzahl der Unterprobleme|
|$n/b$|Eingabegröße pro Unterproblem (bestimmt Höhe des Rekursionsbaums)|
|$f(n)$|Aufwand für Aufteilen und Zusammenfügen|

### Rekursionsbaum

Die **Höhe** des Rekursionsbaums ist $h = \log_b n$.

Die Anzahl Blätter (unterste Ebene) ist $a^h = a^{\log_b n} = n^{\log_b a}$.

---

## 3. Binäre Suche

### Problem & Algorithmus

**Problem:** Finde Element $b$ in sortiertem Feld $A$  
**Prinzip:** Vergleiche $b$ mit dem mittleren Element, suche rekursiv im linken oder rechten Teilfeld.

### Pseudocode (vereinfacht, $b$ ist vorhanden)

```
BinäreSuche(A, b, p, r):   // p: Anfang, r: Ende
1. if p = r then return p
2. else
3.     q ← ⌊(p + r) / 2⌋
4.     if b ≤ A[q] then return BinäreSuche(A, b, p, q)
5.     else return BinäreSuche(A, b, q+1, r)

Aufruf: BinäreSuche(A, b, 1, n)
```

### Pseudocode (vollständig, ohne Annahme)

```
BinäreSuche(A, b, p, r):
1. if p = r and A[p] == b then return p          // gefunden
2. else if p = r and A[p] ≠ b then return -1     // nicht gefunden
3. else
4.     q ← ⌊(p + r) / 2⌋
5.     if b ≤ A[q] then return BinäreSuche(A, b, p, q)
6.     else return BinäreSuche(A, b, q+1, r)
```

### Laufzeitanalyse

$$T(n) = \begin{cases} 1 & \text{if } n = 1 \\ 5 + \max\left\{T\left(\lfloor n/2 \rfloor\right), T\left(\lceil n/2 \rceil\right)\right\} & \text{if } n > 1 \end{cases}$$

Als Rekursionsgleichung (vereinfacht):

$$T(n) = 1 \cdot T(n/2) + c$$

- $a = 1$ Unterproblem, Größe $n/2$, Aufwand pro Ebene: konstant $c$
- Höhe des Rekursionsbaums: $\log n$
- Pro Ebene: $c$ → Gesamtaufwand: $c \cdot \log n$

$$\boxed{T(n) = O(\log n)}$$

### Satz & Beweis (Korrektheit)

> **Satz:** `BinäreSuche(A, b, p, r)` findet den Index von $b$ in einem sortierten Feld $A[p..r]$, sofern $b$ vorhanden ist.

**Beweis per Induktion** über $n = r - p$:

- **(I.A.)** $n = 0$: $p = r$, Algorithmus gibt $p$ zurück ✅
- **(I.V.)** Für alle $m \leq n$ findet der Algorithmus den Index korrekt.
- **(I.S.)** Bei $n+1 = r - p$: $q = \lfloor(p+r)/2\rfloor$, es gilt $q \geq p$ und $q < r$.
    - Falls $b \leq A[q]$: Da $A$ sortiert, liegt $b \in A[p..q]$ → I.V. anwendbar ✅
    - Falls $b > A[q]$: Da $A$ sortiert, liegt $b \in A[q+1..r]$ → I.V. anwendbar ✅

### Vergleich: Binäre vs. lineare Suche

|$n$|$n$ (linear)|$\log n$ (binär)|
|---|---|---|
|10|10|3|
|100|100|6|
|1.000|1.000|10|
|10.000|10.000|13|
|100.000|100.000|17|

⚠️ **Beobachtung:** $\log n$ wächst extrem langsam — in der Praxis fast wie eine Konstante!

---

## 4. Integer-Multiplikation

### Problem

**Gegeben:** Zwei $n$-Bit Integer $X$, $Y$  
**Gesucht:** $2n$-Bit Integer $Z = X \cdot Y$

**Annahmen:**

- Addition von $n$-Bit Integers: $\Theta(n)$
- Multiplikation mit $2^k$: $\Theta(n + k)$ (Bit-Shift)

### Schulmethode: $\Theta(n^2)$

- $n$ Multiplikationen mit $2^k$
- $n-1$ Additionen, je $\Theta(n)$
- **Gesamt: $\Theta(n^2)$**

### Erster Versuch mit T&H: $\Theta(n^2)$

Zerlege $X = A \cdot 2^{n/2} + B$ und $Y = C \cdot 2^{n/2} + D$ (je $n/2$ Bits):

$$X \cdot Y = AC \cdot 2^n + (BC + AD) \cdot 2^{n/2} + BD$$

**4 Multiplikationen** von $n/2$-Bit Integers → Rekursionsgleichung:

$$T(n) = 4 \cdot T(n/2) + c \cdot n$$

**Rekursionsbaum-Analyse:**

- Höhe: $h = \log n$
- Blätter: $4^h = 4^{\log n} = n^{\log 4} = n^2$
- **Gesamtlaufzeit: $\Theta(n^2)$** — kein Gewinn gegenüber Schulmethode!

### Zweiter Versuch: Karatsuba-Algorithmus $O(n^{\log 3}) \approx O(n^{1{,}59})$

**Trick:** Berechne $BC + AD$ mit nur **einer** Multiplikation:

$$\boxed{(A + B)(C + D) - AC - BD = BC + AD}$$

Damit nur **3 Multiplikationen** nötig: $AC$, $BD$, $(A+B)(C+D)$

**Rekursionsgleichung:**

$$T(n) = 3 \cdot T(n/2) + c \cdot n$$

**Rekursionsbaum-Analyse:**

- Höhe: $h = \log n$
- Blätter: $3^h = 3^{\log n} = n^{\log 3} \approx n^{1{,}59}$
- **Gesamtlaufzeit: $O(n^{\log 3}) = O(n^{1{,}59})$**

### Laufzeitvergleich

| $n$   | $n^2$ (Schulmethode) | $n^{1{,}59}$ (Karatsuba) | Faktor |
| ----- | -------------------- | ------------------------ | ------ |
| 10    | 100                  | 39                       | 2,56   |
| 100   | 10.000               | 1.514                    | 6,6    |
| 1.000 | 1.000.000            | 58.885                   | 17     |

### Satz (Karatsuba)

> Die Laufzeit der verbesserten Integer-Multiplikation (Karatsuba) ist $O(3^{\log n}) = O(n^{\log 3}) \approx O(n^{1{,}59})$.

**Beweis:** Per Induktion. Zu zeigen: $T(n) \leq c \cdot 3^{\log n} - 2cn$.

---

## 5. Das Mastertheorem

### Allgemeine Rekursionsgleichung

$$T(n) = \begin{cases} a \cdot T(n/b) + f(n) & n > 1 \ \Theta(1) & n = 1 \end{cases}$$

mit $f(n) = O(n^k)$ für eine Konstante $k$.

### Mastertheorem

$$T(n) = \begin{cases} 
\Theta(n^{\log_b a}) & \text{Fall 1: } a > b^k \\ 
\Theta(n^k \log n) & \text{Fall 2: } a = b^k \\ 
\Theta(f(n)) & \text{Fall 3: } a < b^k 
\end{cases}$$

| Fall       | Bedingung | Dominiert                  | Laufzeit                                       |
| ---------- | --------- | -------------------------- | ---------------------------------------------- |
| **Fall 1** | $a > b^k$ | Rekursion (unterste Ebene) | $\Theta\left(n^{\log_b a}\right)$              |
| **Fall 2** | $a = b^k$ | Beide vergleichbar         | $\Theta\left(n^{\log_b a} \cdot \log n\right)$ |
| **Fall 3** | $a < b^k$ | Zusammenfügen              | $\Theta\left(n^k\right)$                       |

### Intuition

Der Rekursionsbaum hat Höhe $h = \log_b n$ und $a^h = n^{\log_b a}$ Blätter.

- **Fall 1:** Die meiste Arbeit fällt in den Blättern an → Blätteranzahl dominiert
- **Fall 2:** Aufwand auf jeder Ebene gleich groß → multipliziert mit $\log n$ Ebenen
- **Fall 3:** Die meiste Arbeit fällt in der Wurzel an → $f(n)$ dominiert

### Anwendungsbeispiele

|Algorithmus|Rekursionsgleichung|$a$|$b$|$k$|Fall|Laufzeit|
|---|---|---|---|---|---|---|
|**Merge Sort**|$T(n) = 2 T(n/2) + cn$|2|2|1|Fall 2 ($2 = 2^1$)|$O(n \log n)$|
|**Binäre Suche**|$T(n) = 1 \cdot T(n/2) + c$|1|2|0|Fall 2 ($1 = 2^0$)|$O(\log n)$|
|**Karatsuba**|$T(n) = 3 T(n/2) + cn$|3|2|1|Fall 1 ($3 > 2^1$)|$O(n^{\log_2 3}) \approx O(n^{1{,}59})$|
|**Integer (naiv)**|$T(n) = 4 T(n/2) + cn$|4|2|1|Fall 1 ($4 > 2^1$)|$O(n^{\log_2 4}) = O(n^2)$|

---

## 6. Rekursionsgleichungen auflösen: Methode

### Substitutionsmethode (Rekursionsbaum)

**Schema für $T(n) = a \cdot T(n/b) + f(n)$:**

1. Zeichne Rekursionsbaum
2. Bestimme Höhe: $h = \log_b n$
3. Bestimme Aufwand pro Ebene $i$: $a^i \cdot f(n/b^i)$
4. Summiere über alle Ebenen + Blätter

**Beispiel Binäre Suche** $T(n) \leq T(n/2) + c$:

```
Ebene 0:  n        → c
Ebene 1:  n/2      → c
Ebene 2:  n/4      → c
  ...
Ebene h:  1        → c
─────────────────────────
Summe: (log n + 1) · c = O(log n)
```

**Beispiel Merge Sort** $T(n) = 2 \cdot T(n/2) + cn$:

```
Ebene 0:  n            → cn
Ebene 1:  n/2, n/2     → cn
Ebene 2:  n/4 (×4)     → cn
  ...
Ebene h:  1 (×n)       → cn
─────────────────────────
Summe: log n · cn = O(n log n)
```

---

## 📌 Zusammenfassung

### Rekursionsgleichung auf einen Blick

$$T(n) = a \cdot T(n/b) + f(n)$$

- **Höhe des Baumes:** $h = \log_b n$
- **Blätter:** $a^{\log_b n} = n^{\log_b a}$

### Mastertheorem Entscheidung

```
Vergleiche a mit b^k (wobei f(n) = O(n^k)):
   a > b^k  →  Fall 1: O(n^{log_b a})
   a = b^k  →  Fall 2: O(n^{log_b a} · log n)
   a < b^k  →  Fall 3: O(n^k)
```

### Wichtige Algorithmen und ihre Laufzeiten

| Algorithmus             | $T(n) =$         | Laufzeit        |
| ----------------------- | ---------------- | --------------- |
| **Merge Sort**          | $2T(n/2) + O(n)$ | $O(n \log n)$   |
| **Binäre Suche**        | $T(n/2) + O(1)$  | $O(\log n)$     |
| **Karatsuba**           | $3T(n/2) + O(n)$ | $O(n^{1{,}59})$ |
| **Schulmultiplikation** | $4T(n/2) + O(n)$ | $O(n^2)$        |
| **Quick Sort** (avg)    | $2T(n/2) + O(n)$ | $O(n \log n)$   |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.06 Divide and Conquer]] – Teile & Herrsche I: Merge Sort
- [[VL.03 Komplexität]] – Laufzeitanalyse, $O$-, $\Omega$-, $\Theta$-Notation
- [[VL.10 Forgeschrittene Sortierverfahren]] – Quick Sort (Rekursionsgleichung)
- [[VL.07 Korrektheitsbeweis]] – Induktionsbeweise