**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #LineareGleichungssysteme #GaußAlgorithmus #Zeilenstufenform #Lösungsmenge #Rückwärtssubstitution

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt systematisch in das Lösen linearer Gleichungssysteme ein. Der Gauß-Algorithmus ist eines der fundamentalsten und praktisch wichtigsten Verfahren der linearen Algebra.

- **Matrixschreibweise** für lineare Gleichungssysteme
- **Elementare Zeilenoperationen** und ihre Eigenschaften
- **Gauß-Algorithmus** zur Lösung von LGS
- **Zeilenstufenform (ZSF)** und **normierte Zeilenstufenform (NZSF)**
- **Rückwärtssubstitution** zur Bestimmung der Lösung
- **Struktur der Lösungsmenge** (homogen vs. inhomogen)

---

## 1. Lineare Gleichungssysteme

### Definition

Ein **lineares Gleichungssystem (LGS)** mit $m$ Gleichungen in $n$ Unbekannten hat die Form:

$$\begin{cases}
a_{1,1}x_1 + a_{1,2}x_2 + \ldots + a_{1,n}x_n = b_1 \\
a_{2,1}x_1 + a_{2,2}x_2 + \ldots + a_{2,n}x_n = b_2 \\
\vdots \\
a_{m,1}x_1 + a_{m,2}x_2 + \ldots + a_{m,n}x_n = b_m
\end{cases}$$

- Die $x_j$ heißen **Unbekannte** oder **Variablen** und sind gesucht
- Die Koeffizienten $a_{i,j} \in K$ und $b_i \in K$ sind gegeben
- **Reelles LGS:** $K = \mathbb{R}$ (alle $a_{i,j}$ und $b_i$ reell)
- **Komplexes LGS:** $K = \mathbb{C}$ (Koeffizienten können komplex sein)

### Homogen vs. Inhomogen

- **Homogen:** Alle $b_i = 0$ (rechte Seite ist Nullvektor)
- **Inhomogen:** Mindestens ein $b_i \neq 0$

### Matrixschreibweise

Das LGS lässt sich kompakt schreiben als:

$$Ax = b$$

wobei:

$$A = \begin{bmatrix} a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\ a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m,1} & a_{m,2} & \cdots & a_{m,n} \end{bmatrix} \in K^{m,n}, \quad x = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} \in K^n, \quad b = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_m \end{bmatrix} \in K^m$$

**Notation:**
- $A \in K^{m,n}$ heißt **Koeffizientenmatrix** des LGS
- $b \in K^m$ heißt **rechte Seite** oder **Inhomogenität** des LGS
- $x \in K^n$ ist die **Lösung** (eventuell mehrere) von $Ax = b$

### Lösungsmenge

Die **Lösungsmenge** ist die Menge aller Lösungen:

$$L = L(A,b) := \{x \in K^n \mid Ax = b\}$$

### Spezialfall: Invertierbare Matrix

Ist $A \in K^{n,n}$ **invertierbar**, dann:

$$x = A^{-1}Ax = A^{-1}b$$

Die Lösung ist dann **eindeutig**: $L = \{A^{-1}b\}$.

Im Allgemeinen ist $A$ aber nicht invertierbar (oder nicht quadratisch), daher brauchen wir den Gauß-Algorithmus.

---

## 2. Elementare Zeilenoperationen

### Definition

Die folgenden Operationen werden als **elementare Zeilenoperationen** bezeichnet:

1. **Vertauschen** von zwei Zeilen
2. **Multiplizieren** einer Zeile mit einer Zahl $\lambda \neq 0$ (wobei $\lambda \in K$)
3. **Addition** des Vielfachen einer Zeile zu einer anderen Zeile

**Wichtige Eigenschaft:** Alle elementaren Zeilenoperationen sind **umkehrbar** (Äquivalenzumformungen), daher bleibt die **Lösungsmenge unverändert**!

---

## 3. Zeilenstufenform (ZSF)

### Definition

Eine Matrix $C \in K^{m,n}$ ist in **Zeilenstufenform (ZSF)**, falls gilt:

1. Der **erste Nichtnulleintrag** einer Zeile ist weiter rechts als die ersten Nichtnulleinträge der vorherigen Zeilen
2. Alle Zeilen mit nur Nullen sind **unter** den Zeilen mit Nichtnulleinträgen

**Allgemeine Form:**

$$C = \begin{bmatrix} 
0 & c_{1,j_1} & * & * & * & * & * & * & * & * \\
0 & 0 & 0 & c_{2,j_2} & * & * & * & * & * & * \\
0 & 0 & 0 & 0 & 0 & c_{3,j_3} & * & * & * & * \\
\vdots & \vdots & \vdots & \vdots & \vdots & \ddots & \ddots & \ddots & \vdots & \vdots \\
0 & 0 & 0 & 0 & 0 & 0 & \cdots & 0 & c_{r,j_r} & * \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0
\end{bmatrix}$$

wobei $c_{i,j_i} \neq 0$ für $i = 1, \ldots, r$ und $*$ für beliebige Einträge steht (null oder ungleich null).

Die Einträge $c_{i,j_i}$ bei den "Stufen" werden **Pivotelemente** genannt.

### Wichtige Bemerkungen

1. Die Zeilenstufenform der **Nullmatrix** ist $C = 0$
2. Der Gauß-Algorithmus gibt **einen** Rechenweg an, um $A$ in ZSF zu bringen – es gibt aber mehrere Wege!
3. Die Zeilenstufenform einer Matrix $A \neq 0$ ist **nicht eindeutig**: Multipliziert man eine Zeile mit $\lambda \neq 0$, erhält man eine andere ZSF

---

## 4. Gauß-Algorithmus

### Ziel

Bringe eine Matrix $A \in K^{m,n}$ auf **Zeilenstufenform** durch elementare Zeilenoperationen.

### Algorithmus

Für $A \neq 0$ gehe wie folgt vor:

**Schritt 1:** Suche die **erste von Null verschiedene Spalte** $j_1$

**Schritt 2:** Suche in dieser Spalte den **ersten Eintrag ungleich Null** (Pivotelement) und tausche ihn ggf. in die erste Zeile. Wir haben nun:

$$\begin{bmatrix} 0 & c_{1,j_1} & * \\ 0 & * & * \end{bmatrix} \quad \text{mit } c_{1,j_1} \neq 0$$

**Schritt 3:** **Unter dem Pivotelement** $c_{1,j_1}$ werden alle Einträge **eliminiert**, indem geeignete Vielfache der ersten Zeile von den anderen Zeilen abgezogen werden

**Schritt 4: Rekursion**
- Ist die Matrix in Zeilenstufenform → fertig
- Andernfalls haben wir:

$$\begin{bmatrix} 0 & c_{1,j_1} & * \\ 0 & 0 & A_1 \end{bmatrix} \quad \text{mit } c_{1,j_1} \neq 0$$

Die erste Zeile und die ersten Spalten (bis Spalte $j_1$) bleiben wie sie sind, und wir wenden das gleiche Verfahren auf die kleinere Matrix $A_1$ an.

### Beispiel: Zeilenstufenform

**Gegeben:** $A = \begin{bmatrix} 0 & 0 & 1 & -2 \\ 0 & 2 & 1 & 1 \\ 0 & 4 & 3 & 3 \end{bmatrix} \in \mathbb{R}^{3,4}$

**Schritt 1:** Erste Spalte $\neq 0$ ist $j_1 = 2$

**Schritt 2:** Erste Zeile hat 0, zweite Zeile hat $2 \neq 0$ → **Tausche Zeile I und II:**

$$\begin{bmatrix} 0 & 0 & 1 & -2 \\ 0 & 2 & 1 & 1 \\ 0 & 4 & 3 & 3 \end{bmatrix} \xrightarrow{\text{I} \leftrightarrow \text{II}} \begin{bmatrix} 0 & 2 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 4 & 3 & 3 \end{bmatrix}$$

**Schritt 3:** Eliminiere unter dem Pivot $c_{1,2} = 2$:

$$\begin{bmatrix} 0 & 2 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 4 & 3 & 3 \end{bmatrix} \xrightarrow{\text{III} - 2\text{I}} \begin{bmatrix} 0 & 2 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 1 & 1 \end{bmatrix}$$

**Schritt 4: Rekursion** – Wende Verfahren auf $A_1 = \begin{bmatrix} 0 & 1 & -2 \\ 0 & 1 & 1 \end{bmatrix}$ an:

$$\begin{bmatrix} 0 & 2 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 1 & 1 \end{bmatrix} \xrightarrow{\text{III} - \text{II}} \begin{bmatrix} 0 & 2 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 0 & 3 \end{bmatrix}$$

✓ **Zeilenstufenform erreicht!**

---

## 5. Normierte Zeilenstufenform (NZSF)

### Definition

Eine Zeilenstufenform $C$ ist in **normierter Zeilenstufenform (NZSF)**, falls:

1. Alle **Pivotelemente normiert** sind: $c_{i,j_i} = 1$
2. Alle Einträge **über den Pivotelementen** sind **Null**

**Allgemeine Form:**

$$C = \begin{bmatrix} 
0 & 1 & * & 0 & * & 0 & * & * & 0 & * \\
0 & 0 & 0 & 1 & * & 0 & * & * & 0 & * \\
0 & 0 & 0 & 0 & 0 & 1 & * & * & 0 & * \\
\vdots & \vdots & \vdots & \vdots & \vdots & \ddots & \ddots & \ddots & \vdots & \vdots \\
0 & 0 & 0 & 0 & 0 & 0 & \cdots & 0 & 1 & * \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0
\end{bmatrix}$$

**Wichtig:** Die normierte Zeilenstufenform einer Matrix ist **eindeutig**!

### Beispiel: NZSF

**Gegeben (ZSF):** $\begin{bmatrix} 2 & 4 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 0 & 3 \end{bmatrix}$

**Von unten nach oben normieren und eliminieren:**

$$\begin{bmatrix} 2 & 4 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 0 & 3 \end{bmatrix} \xrightarrow{\frac{1}{3}\text{III}} \begin{bmatrix} 2 & 4 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

$$\xrightarrow{\substack{\text{II} + 2\text{III} \\ \text{I} - \text{III}}} \begin{bmatrix} 2 & 4 & 1 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \xrightarrow{\text{I} - \text{II}} \begin{bmatrix} 2 & 4 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

$$\xrightarrow{\frac{1}{2}\text{I}} \begin{bmatrix} 1 & 2 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

✓ **Normierte Zeilenstufenform erreicht!**

---

## 6. Lösen von LGS mit Gauß-Algorithmus

### Erweiterte Koeffizientenmatrix

Um das LGS $Ax = b$ zu lösen, wenden wir den Gauß-Algorithmus auf die **erweiterte Koeffizientenmatrix** an:

$$[A \mid b] = \begin{bmatrix} a_{1,1} & a_{1,2} & \cdots & a_{1,n} & \mid & b_1 \\ a_{2,1} & a_{2,2} & \cdots & a_{2,n} & \mid & b_2 \\ \vdots & \vdots & \ddots & \vdots & \mid & \vdots \\ a_{m,1} & a_{m,2} & \cdots & a_{m,n} & \mid & b_m \end{bmatrix}$$

**Wichtig:** Die elementaren Zeilenoperationen auf $[A \mid b]$ **verändern die Lösungsmenge nicht**!

### Rückwärtssubstitution

Ist die Matrix in **ZSF** oder **NZSF**, bestimmen wir die Lösung(en) durch **Rückwärtssubstitution** (von unten nach oben einsetzen).

### Beispiel 1: Eindeutige Lösung

**Gegeben:** $\begin{bmatrix} 1 & 2 & -1 \\ 1 & 3 & 1 \\ 1 & 2 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 3 \\ 8 \\ 7 \end{bmatrix}$

**Erweiterte Koeffizientenmatrix:**

$$\begin{bmatrix} 1 & 2 & -1 & \mid & 3 \\ 1 & 3 & 1 & \mid & 8 \\ 1 & 2 & 1 & \mid & 7 \end{bmatrix} \xrightarrow{\substack{\text{II} - \text{I} \\ \text{III} - \text{I}}} \begin{bmatrix} 1 & 2 & -1 & \mid & 3 \\ 0 & 1 & 2 & \mid & 5 \\ 0 & 0 & 2 & \mid & 4 \end{bmatrix}$$

**Rückwärtssubstitution:**
- Zeile III: $2x_3 = 4 \implies x_3 = 2$
- Zeile II: $x_2 + 2x_3 = 5 \implies x_2 = 5 - 2(2) = 1$
- Zeile I: $x_1 + 2x_2 - x_3 = 3 \implies x_1 = 3 - 2(1) + 2 = 3$

**Lösung:** $L = \left\{\begin{bmatrix} 3 \\ 1 \\ 2 \end{bmatrix}\right\}$ (eindeutig)

### Beispiel 2: Keine Lösung

**Gegeben:** $\begin{bmatrix} 1 & 1 \\ 2 & 2 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 2 \\ 0 \end{bmatrix}$

**Erweiterte Koeffizientenmatrix:**

$$\begin{bmatrix} 1 & 1 & \mid & 2 \\ 2 & 2 & \mid & 0 \end{bmatrix} \xrightarrow{\text{II} - 2\text{I}} \begin{bmatrix} 1 & 1 & \mid & 2 \\ 0 & 0 & \mid & -4 \end{bmatrix}$$

**Zeile II:** $0x_1 + 0x_2 = -4$ → **Widerspruch!** ($0 = -4$ unmöglich)

**Lösung:** $L = \emptyset$ (keine Lösung)

### Beispiel 3: Unendlich viele Lösungen

**Gegeben:** $\begin{bmatrix} 1 & 1 \\ 2 & 2 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 2 \\ 4 \end{bmatrix}$

**Erweiterte Koeffizientenmatrix:**

$$\begin{bmatrix} 1 & 1 & \mid & 2 \\ 2 & 2 & \mid & 4 \end{bmatrix} \xrightarrow{\text{II} - 2\text{I}} \begin{bmatrix} 1 & 1 & \mid & 2 \\ 0 & 0 & \mid & 0 \end{bmatrix}$$

**Zeile II:** $0x_1 + 0x_2 = 0$ → für alle $x_1, x_2$ erfüllt  
**Zeile I:** $x_1 + x_2 = 2 \implies x_1 = 2 - x_2$

**Wähle** $x_2 = t \in \mathbb{R}$ **frei**, dann $x_1 = 2 - t$

**Lösung:** $L = \left\{\begin{bmatrix} 2-t \\ t \end{bmatrix} \, \Bigg| \, t \in \mathbb{R}\right\}$ (unendlich viele)

### Beispiel 4: Mehrere freie Parameter

**Gegeben:** $A = \begin{bmatrix} 2 & -1 & 3 & 0 \\ 2 & -1 & 3 & 1 \\ -2 & 4 & 0 & 1 \end{bmatrix}$, $b = \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}$

Nach Gauß-Algorithmus (Details im Skript):

$$[A \mid b] \to \begin{bmatrix} 2 & -1 & 3 & 0 & \mid & 1 \\ 0 & 3 & 3 & 1 & \mid & 2 \\ 0 & 0 & 0 & 1 & \mid & -1 \end{bmatrix}$$

**Pivotvariablen:** $x_1, x_2, x_4$ (gehören zu Stufen)  
**Freie Variable:** $x_3 = t \in \mathbb{R}$

**Rückwärts einsetzen:**
- $x_4 = -1$
- $3x_2 + 3x_3 + x_4 = 2 \implies x_2 = 1 - t$
- $2x_1 - x_2 + 3x_3 = 1 \implies x_1 = 1 - 2t$

**Lösung:**

$$L = \left\{\begin{bmatrix} 1-2t \\ 1-t \\ t \\ -1 \end{bmatrix} \, \Bigg| \, t \in \mathbb{R}\right\}$$

---

## 7. Struktur der Lösungsmenge

### Homogenes LGS: $Ax = 0$

Die Lösungsmenge $L(A,0)$ ist ein **Teilraum** von $K^n$:

1. $A \cdot 0 = 0 \implies 0 \in L(A,0)$
2. $x, y \in L(A,0) \implies A(x+y) = Ax + Ay = 0 + 0 = 0 \implies x+y \in L(A,0)$
3. $\lambda \in K, x \in L(A,0) \implies A(\lambda x) = \lambda Ax = \lambda \cdot 0 = 0 \implies \lambda x \in L(A,0)$

Nach dem **Teilraumkriterium** (Satz 10.4) ist $L(A,0)$ ein Teilraum von $K^n$ ✓

### Inhomogenes LGS: $Ax = b$ mit $b \neq 0$

Die Lösungsmenge $L(A,b)$ ist **kein Teilraum**, da $0 \notin L(A,b)$:

$$A \cdot 0 = 0 \neq b$$

### Struktur der Lösungsmenge (Satz)

**Satz:** Das LGS $Ax = b$ mit $A \in K^{m,n}$ und $b \in K^m$ habe eine Lösung $x_P \in K^n$. Diese spezielle Lösung wird auch **partikuläre Lösung** genannt. Dann gilt:

$$L(A,b) = \{x \in K^n \mid Ax = b\} = \{x_P + x \in K^n \mid Ax = 0\} =: x_P + L(A,0)$$

**Interpretation:** Jede Lösung des inhomogenen LGS ist die Summe aus:
- Einer **partikulären Lösung** $x_P$ des inhomogenen LGS
- Einer **Lösung des homogenen LGS** $L(A,0)$

### Beispiel: Struktur der Lösungsmenge

**Gegeben:** $A = \begin{bmatrix} 1 & 2 & 0 & 3 \\ 0 & 0 & 1 & 4 \\ 0 & 0 & 0 & 0 \end{bmatrix} \in \mathbb{R}^{3,4}$, $b = \begin{bmatrix} 1 \\ 3 \\ 0 \end{bmatrix} \in \mathbb{R}^3$

Die Matrix $A$ ist bereits in **NZSF**.

**Freie Variablen:** $x_2 = s \in \mathbb{R}$, $x_4 = t \in \mathbb{R}$

**Aus den Zeilen:**
- Zeile II: $x_3 + 4x_4 = 3 \implies x_3 = 3 - 4t$
- Zeile I: $x_1 + 2x_2 + 3x_4 = 1 \implies x_1 = 1 - 2s - 3t$

**Lösungsmenge:**

$$L(A,b) = \left\{\begin{bmatrix} 1-2s-3t \\ s \\ 3-4t \\ t \end{bmatrix} \, \Bigg| \, s,t \in \mathbb{R}\right\}$$

**Umschreiben:**

$$L(A,b) = \begin{bmatrix} 1 \\ 0 \\ 3 \\ 0 \end{bmatrix} + s \begin{bmatrix} -2 \\ 1 \\ 0 \\ 0 \end{bmatrix} + t \begin{bmatrix} -3 \\ 0 \\ -4 \\ 1 \end{bmatrix}$$

$$= \underbrace{\begin{bmatrix} 1 \\ 0 \\ 3 \\ 0 \end{bmatrix}}_{= x_P} + \underbrace{\text{span}\left\{\begin{bmatrix} -2 \\ 1 \\ 0 \\ 0 \end{bmatrix}, \begin{bmatrix} -3 \\ 0 \\ -4 \\ 1 \end{bmatrix}\right\}}_{= L(A,0)}$$

**Partikuläre Lösung:** $x_P = \begin{bmatrix} 1 \\ 0 \\ 3 \\ 0 \end{bmatrix}$ (erhalten durch $s = t = 0$)

---

## 📌 Zusammenfassung

### Gauß-Algorithmus

1. Bringe $[A \mid b]$ auf **Zeilenstufenform** durch elementare Zeilenoperationen
2. Optional: Bringe auf **normierte Zeilenstufenform** (eindeutig, leichter ablesbar)
3. Bestimme Lösung durch **Rückwärtssubstitution**

### Anzahl der Lösungen

Ein LGS $Ax = b$ kann haben:
- **Keine Lösung** ($L = \emptyset$): Widerspruch wie $0 = c$ mit $c \neq 0$ in ZSF
- **Genau eine Lösung** ($|L| = 1$): Alle Variablen sind Pivotvariablen
- **Unendlich viele Lösungen** ($|L| = \infty$): Mindestens eine freie Variable

### Struktur der Lösungsmenge

| LGS | Lösungsmenge | Struktur |
|-----|--------------|----------|
| **Homogen** $Ax = 0$ | $L(A,0)$ | **Teilraum** von $K^n$ |
| **Inhomogen** $Ax = b$ | $L(A,b) = x_P + L(A,0)$ | Partikuläre Lösung + homogene Lösungen |

### Wichtige Konzepte

- **Pivotvariablen:** Variablen zu Spalten mit "Stufen" (eindeutig bestimmt)
- **Freie Variablen:** Variablen zu Spalten ohne "Stufen" (frei wählbar)
- **Partikuläre Lösung:** Eine spezielle Lösung des inhomogenen LGS

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.10 Vektorräume]]: $L(A,0)$ als Teilraum
- [[VL.11 Basis und Dimension]]: Freie Variablen → Basis von $L(A,0)$
- [[VL.12 Matrizen]]: Matrixmultiplikation $Ax = b$
- [[VL.14 Gauss-Algorithmus]]: Bedingungen für Lösbarkeit, Dimension von $L(A,0)$
