**Class:** [[IntroProg]]  
**Date:** VL.7  
**Topics:** #Korrektheitsbeweise #Schleifeninvariante #VollständigeInduktion #MaximumSuche #InsertionSort #Beweis

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt **formale Korrektheitsbeweise** für Algorithmen – wie man mathematisch beweist, dass ein Algorithmus korrekt funktioniert.

- Verständnis von **mathematischen Beweisen**
- Konzept der **Schleifeninvariante**
- **Vollständige Induktion** als Beweismethode
- **Korrektheitsbeweis** für einfache Algorithmen
- **Korrektheitsbeweis** für Insertion Sort

---

## 1. Was ist ein mathematischer Beweis?

### Informelle Definition

Ein **Beweis** ist eine **Herleitung einer Aussage** aus:
- Bereits bewiesenen Aussagen
- Grundannahmen (**Axiomen**)

### Grundannahmen in der Algorithmik

**Axiom:** Ein Pseudocode-Befehl wird **gemäß seiner Spezifikation** ausgeführt.

**Beispiele:**
- `x ← x + 1` erhöht die Variable `x` um 1
- `A[i] ← 5` setzt das Element an Position `i` auf 5
- `if x > 0 then ...` führt den `then`-Zweig nur aus, wenn `x > 0`

---

## 2. Wann ist ein Algorithmus korrekt?

### Definition: Korrektheit

Ein Algorithmus ist **korrekt**, wenn er **für jede zulässige Eingabe** die in der Problembeschreibung **spezifizierte Ausgabe** berechnet.

### Beispiel: Sortieren

**Problem:**
- **Eingabe:** Folge von $n$ Zahlen $(a_1, a_2, \ldots, a_n)$
- **Ausgabe:** Permutation $(a'_1, a'_2, \ldots, a'_n)$ mit $a'_1 \leq a'_2 \leq \ldots \leq a'_n$

**Korrektheit bedeutet:**
Für **jede** gültige Eingabe sortiert der Algorithmus korrekt.

---

## 3. Triviales Beispiel: Einfacher Korrektheitsbeweis

### Algorithmus

```
EinfacherAlgorithmus(n)
1. X ← 10
2. Y ← n
3. X ← X + Y
4. return X
```

### Behauptung

Der Algorithmus gibt den Wert $10 + n$ zurück.

### Beweis (Schritt für Schritt)

**Zu Beginn:** Alle Variablen außer Parameter $n$ sind undefiniert.

**Zeile 1:** `X ← 10`
- Nach Ausführung: $X = 10$

**Zeile 2:** `Y ← n`
- Nach Ausführung: $Y = n$

**Zeile 3:** `X ← X + Y`
- Vor Ausführung: $X = 10$, $Y = n$
- Nach Ausführung: $X = 10 + n$

**Zeile 4:** `return X`
- Da $X = 10 + n$, wird $10 + n$ zurückgegeben ✓

### Prinzip

⚠️ **Ein Korrektheitsbeweis vollzieht das Programm Schritt für Schritt nach.**

---

## 4. Problem: Schleifen

### Herausforderung

Bei Algorithmen mit **Schleifen** wissen wir nicht, wie viele Durchläufe erfolgen:
- Anzahl hängt von der **Eingabelänge** ab
- Wir können nicht jeden einzelnen Durchlauf einzeln nachvollziehen

### Beispiel

```
for j ← 2 to length(A) do
    // Irgendwas
```

Bei `length(A) = 1000` müssten wir 999 Durchläufe einzeln nachweisen → **unpraktisch!**

### Lösung: Schleifeninvariante

Wir benötigen eine **Aussage**, die den Zustand **nach beliebig vielen Durchläufen** beschreibt.

---

## 5. Schleifeninvariante

### Definition

Eine **Schleifeninvariante** ist eine Aussage $A(i)$, die:

1. **Zu Beginn des ersten Durchlaufs** gilt (Initialisierung)
2. **Zu Beginn jedes $i$-ten Durchlaufs** gilt (in Abhängigkeit von $i$)
3. Eine Aussage über den **Austrittszustand** erlaubt

### Austrittszustand

Die Schleife wird beendet, wenn die **Schleifenbedingung nicht mehr gilt**.

**Beispiel:**
```
for j ← 2 to length(A) do
    // ...
```

**Austrittszustand:** $j = \text{length}(A) + 1$

### Konventionen für for-Schleifen

- **Laufvariable** wird **am Ende** des Durchlaufs erhöht
- Bei **Initialisierung** hat die Laufvariable den **Startwert**
- Die **Invariante** darf (und sollte) von der Laufvariable abhängen

---

## 6. Beispiel: Maximum-Suche

### Algorithmus

```
Max-Search(Array A)
1. max ← 1
2. for j ← 2 to length(A) do
3.     if A[j] > A[max] then max ← j
4. return max  // max ist Index des maximalen Elements
```

### Schleifeninvariante

**Invariante:** $A[\text{max}]$ ist ein größtes Element aus $A[1 \ldots j-1]$.

### Beweis der Invariante

**Lemma:** Die `for`-Schleife erfüllt die Invariante.

**Beweis:**

**Initialisierung (j = 2):**
- Vor Schleifeneintritt: `max = 1` (Zeile 1)
- $A[1 \ldots 1]$ enthält nur $A[1]$
- Da $A[\text{max}] = A[1]$, ist $A[\text{max}]$ das größte Element aus $A[1 \ldots 1]$ ✓

**Induktionsvoraussetzung (I.V.):**
Sei die Invariante erfüllt für $j = j_0 < \text{length}(A) + 1$.

**Induktionsschritt ($j_0 \to j_0 + 1$):**
Betrachte Durchlauf mit $j = j_0$.

**Fall 1:** $A[j] \leq A[\text{max}]$
- `then`-Zweig wird **nicht** ausgeführt
- $A[\text{max}]$ bleibt unverändert
- Nach I.V. ist $A[\text{max}]$ größtes Element aus $A[1 \ldots j-1]$
- Also auch größtes Element aus $A[1 \ldots j]$ ✓
- Am Ende wird $j$ erhöht → Invariante gilt für $j+1$ ✓

**Fall 2:** $A[j] > A[\text{max}]$
- Nach I.V. ist $A[\text{max}]$ größtes Element aus $A[1 \ldots j-1]$
- Da $A[j] > A[\text{max}]$, ist $A[j]$ größer als alle Elemente aus $A[1 \ldots j-1]$
- Also ist $A[j]$ größtes Element aus $A[1 \ldots j]$
- `max ← j` setzt $\text{max} = j$
- Damit ist $A[\text{max}]$ größtes Element aus $A[1 \ldots j]$ ✓
- Am Ende wird $j$ erhöht → Invariante gilt für $j+1$ ✓

### Korrektheit von Max-Search

**Satz:** Max-Search gibt den Index eines maximalen Elements zurück.

**Beweis:**

Am Ende der Schleife gilt:
- $j = \text{length}(A) + 1$
- Nach Invariante: $A[\text{max}]$ ist größtes Element aus $A[1 \ldots j-1]$
- Also: $A[\text{max}]$ ist größtes Element aus $A[1 \ldots \text{length}(A)]$
- Zeile 4 gibt `max` zurück ✓

---

## 7. Vollständige Induktion (Wiederholung)

### Prinzip

Um ein Prädikat $p: \mathbb{N}_0 \to \{\text{WAHR}, \text{FALSCH}\}$ zu beweisen:

**Induktionsanfang (I.A.):**
Zu beweisen: $p(0)$ ist WAHR

**Induktionsvoraussetzung (I.V.):**
Für alle $n \leq n_0$ gilt: $p(n)$ ist WAHR

**Induktionsschritt (I.S.):**
Zu beweisen: $p(n)$ ist WAHR für $n \leq n_0 \Rightarrow p(n+1)$ ist WAHR

**Induktionsschluss:**
Für alle $n \in \mathbb{N}_0$ gilt: $p(n)$ ist WAHR

### Beispiel: Gaußsche Summenformel

**Behauptung:** 
$$p(n): 1 + 2 + 3 + \ldots + n = \frac{n(n+1)}{2}$$

**Beweis:**

**Induktionsanfang ($n = 1$):**
$$1 = \frac{1(1+1)}{2} = \frac{2}{2} = 1 \quad \checkmark$$

**Induktionsvoraussetzung:**
Für $n = n_0$ gilt: $1 + 2 + \ldots + n_0 = \frac{n_0(n_0+1)}{2}$

**Induktionsschritt ($n_0 \to n_0 + 1$):**
$$\begin{align}
1 + 2 + \ldots + n_0 + (n_0+1) &= \frac{n_0(n_0+1)}{2} + (n_0+1) \quad \text{(nach I.V.)} \\
&= (n_0+1) \left(\frac{n_0}{2} + 1\right) \\
&= (n_0+1) \cdot \frac{n_0 + 2}{2} \\
&= \frac{(n_0+1)(n_0+2)}{2} \quad \checkmark
\end{align}$$

---

## 8. Korrektheitsbeweis: Insertion Sort

### Algorithmus

```
InsertionSort(Array A)
1. for j ← 2 to length(A) do
2.     key ← A[j]
3.     i ← j-1
4.     while i>0 and A[i]>key do
5.         A[i+1] ← A[i]
6.         i ← i-1
7.     A[i+1] ← key
```

### Zwei verschachtelte Invarianten

Wir benötigen **zwei Invarianten**:
1. **Äußere Schleife** (`for`-Schleife)
2. **Innere Schleife** (`while`-Schleife)

---

## 9. Äußere Schleifeninvariante (for-Schleife)

### Invariante

**Invariante (äußere Schleife):** 
$$A[1 \ldots j-1] \text{ ist sortiert}$$

### Zustände

- **Initialisierung:** $j = 2$, $A[1 \ldots 1]$ ist sortiert (ein Element) ✓
- **Austrittszustand:** $j = \text{length}(A) + 1$
  - Nach Invariante: $A[1 \ldots \text{length}(A)]$ ist sortiert ✓

### Visualisierung

```
Iteration j=2:  [8] | 15, 3, 14, 7, 6, 18, 19
                 ↑
              sortiert

Iteration j=3:  [8, 15] | 3, 14, 7, 6, 18, 19
                 ↑─────↑
                sortiert

Iteration j=4:  [3, 8, 15] | 14, 7, 6, 18, 19
                 ↑─────────↑
                  sortiert
...
```

---

## 10. Innere Schleifeninvariante (while-Schleife)

### Invariante

**Invariante (innere Schleife):**
$$A[1 \ldots j-1] \setminus \{A[i+1]\} \text{ ist sortiert} \land A[i \ldots j-1] > \text{key}$$

**Bedeutung:**
- $A[1 \ldots j-1]$ ohne das Element an Position $i+1$ ist sortiert
- Alle Elemente von $A[i]$ bis $A[j-1]$ sind größer als `key`

### Initialisierung (innere Schleife)

- $i = j-1$
- $A[1 \ldots j-1]$ ist sortiert (nach äußerer Invariante)
- Falls $A[i] > \text{key}$: Schleife wird betreten ✓

### Austrittszustand (innere Schleife)

**Zwei Möglichkeiten:**

1. **$i = 0$:** `key` ist kleiner als alle Elemente in $A[1 \ldots j-1]$
2. **$A[i] \leq \text{key}$:** Richtige Position für `key` gefunden

In beiden Fällen:
$$A[i] \leq \text{key} < A[i+2 \ldots j-1]$$

### Detaillierter Ablauf

```
j=5, key=7, A = [3, 8, 14, 15, 7, 6, 18, 19]
                  ↑──────────↑
                  sortiert

i=4: A[4]=15 > 7 → Verschiebe 15 nach rechts
     A = [3, 8, 14, 15, 15, 6, 18, 19]
     i=3

i=3: A[3]=14 > 7 → Verschiebe 14 nach rechts
     A = [3, 8, 14, 14, 15, 6, 18, 19]
     i=2

i=2: A[2]=8 > 7 → Verschiebe 8 nach rechts
     A = [3, 8, 8, 14, 15, 6, 18, 19]
     i=1

i=1: A[1]=3 ≤ 7 → STOP
     Füge 7 an Position i+1=2 ein
     A = [3, 7, 8, 14, 15, 6, 18, 19]
          ↑─────────────↑
          sortiert
```

---

## 11. Vollständiger Beweis für Insertion Sort

### Lemma (innere Schleife)

Die `while`-Schleife erfüllt die Invariante:
$$A[1 \ldots j-1] \setminus \{A[i+1]\} \text{ ist sortiert} \land A[i \ldots j-1] > \text{key}$$

**Beweis:** (Per Induktion über $i$, analog zu Max-Search)

### Lemma (äußere Schleife)

Die `for`-Schleife erfüllt die Invariante:
$$A[1 \ldots j-1] \text{ ist sortiert}$$

**Beweis:**

**Initialisierung ($j = 2$):**
- $A[1 \ldots 1]$ enthält ein Element → sortiert ✓

**Induktionsvoraussetzung:**
Für $j = j_0$ ist $A[1 \ldots j_0-1]$ sortiert.

**Induktionsschritt ($j_0 \to j_0 + 1$):**
- Zu Beginn: $A[1 \ldots j_0-1]$ sortiert (I.V.)
- `key ← A[j_0]`
- Innere Schleife fügt `key` korrekt in $A[1 \ldots j_0-1]$ ein
- Nach innerer Schleife: $A[1 \ldots j_0]$ sortiert ✓
- $j$ wird erhöht → Invariante gilt für $j_0 + 1$ ✓

### Hauptsatz: Korrektheit von Insertion Sort

**Satz:** Nach Aufruf von `InsertionSort(A)` ist $A$ sortiert.

**Beweis:**

Am Ende der äußeren Schleife:
- $j = \text{length}(A) + 1$
- Nach äußerer Invariante: $A[1 \ldots j-1] = A[1 \ldots \text{length}(A)]$ ist sortiert ✓

---

## 12. Invarianten als Programmierhilfe

### Praktischer Nutzen

⚠️ **Invarianten sollten zur Kommentierung von Schleifen benutzt werden!**

### Assertions (Zusicherungen)

Invarianten können zur **Laufzeit überprüft** werden:

```c
// C-Code mit Assertions
for (int j = 2; j <= n; j++) {
    // INVARIANTE: A[1..j-1] ist sortiert
    assert(is_sorted(A, 1, j-1));
    
    key = A[j];
    // ... (Rest des Algorithmus)
}
```

**Vorteile:**
- Fehler werden **früh erkannt**
- **Debugging** wird einfacher
- **Dokumentation** der Logik

---

## 📌 Zusammenfassung

### Korrektheit von Algorithmen

**Definition:**
Ein Algorithmus ist korrekt, wenn er für **jede zulässige Eingabe** die **spezifizierte Ausgabe** berechnet.

### Beweismethoden

| Konzept | Verwendung |
|---------|------------|
| **Schritt-für-Schritt-Beweis** | Einfache, schleifenfreie Algorithmen |
| **Schleifeninvariante** | Algorithmen mit Schleifen |
| **Vollständige Induktion** | Beweis der Invariante |

### Schleifeninvariante

**Eigenschaften:**
1. Gilt zu **Beginn** des ersten Durchlaufs
2. Gilt zu **Beginn jedes** Durchlaufs
3. Ermöglicht Aussage über **Austrittszustand**

**Beweisschritte:**
1. **Initialisierung:** Invariante gilt am Anfang
2. **Erhaltung:** Wenn Invariante gilt, gilt sie nach einem Durchlauf auch
3. **Terminierung:** Bei Austritt folgt Korrektheit

### Vollständige Induktion

**Schema:**
1. **Induktionsanfang:** $p(0)$ beweisen
2. **Induktionsvoraussetzung:** $p(n)$ annehmen
3. **Induktionsschritt:** $p(n) \Rightarrow p(n+1)$ beweisen
4. **Induktionsschluss:** $\forall n: p(n)$

### Beispiele

| Algorithmus | Invariante |
|-------------|------------|
| **Max-Search** | $A[\text{max}]$ ist größtes Element aus $A[1 \ldots j-1]$ |
| **Insertion Sort (äußere)** | $A[1 \ldots j-1]$ ist sortiert |
| **Insertion Sort (innere)** | $A[1 \ldots j-1] \setminus \{A[i+1]\}$ sortiert, $A[i \ldots j-1] > \text{key}$ |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Algorithmen-pseudocode]] – Insertion Sort Algorithmus
- [[VL.03 Komplexität]] – Laufzeitanalyse (separates Thema von Korrektheit)
- [[VL.06 Divide and Conquer]] – Korrektheit von MergeSort (ähnliche Techniken)