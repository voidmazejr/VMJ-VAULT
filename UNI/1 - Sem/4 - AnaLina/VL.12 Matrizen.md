**Class:** [[AnaLina]]  
**Date:** 10-01-2026 
**Topics:** #Matrizen #Matrizenmultiplikation #InverseMatrix #Transponierte #Adjungierte

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt Matrizen als fundamentales Werkzeug der linearen Algebra ein. Matrizen sind essentiell für die effiziente Lösung linearer Gleichungssysteme und die Darstellung linearer Abbildungen.

- **Definition** von Matrizen und grundlegende Notation
- **Addition und Skalarmultiplikation** von Matrizen
- **Matrizenmultiplikation** und ihre Eigenschaften
- **Inverse Matrizen** und Invertierbarkeit
- **Transponierte und Adjungierte** Matrix

---

## 1. Definition von Matrizen

### Grundlegende Definition

Für Zahlen $a_{i,j} \in K$, $i = 1, \ldots, m$, $j = 1, \ldots, n$, heißt das Zahlenschema

$$A = \begin{pmatrix} a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\ a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m,1} & a_{m,2} & \cdots & a_{m,n} \end{pmatrix} = [a_{i,j}] = [a_{i,j}]_{\substack{i=1,\ldots,m \\ j=1,\ldots,n}}$$

eine **$m \times n$-Matrix** mit Einträgen in $K$ (wobei $K = \mathbb{R}$ oder $K = \mathbb{C}$).

- **Notation:** $K^{m,n}$ bezeichnet die Menge aller $m \times n$-Matrizen mit Einträgen in $K$
- Eine Matrix heißt **quadratisch**, falls $m = n$ gilt
- **Kurzform:** "$m \times n$-Matrix über $K$" (lies: "$m$ kreuz $n$ Matrix über $K$")

### Wichtige Bemerkungen

1. **Indexregel:** Die Indizes $i, j$ folgen der Regel **"Zeile, Spalte"**
   - $a_{i,j}$ ist der Eintrag in Zeile $i$ und Spalte $j$

2. **Sprachliches:**
   - **Singular:** die Matrix, **Plural:** die Matrizen
   - ❌ Falsch: "die Matrixen"
   - Eine "Matrize" (ohne n) bezeichnet eine Gussform, Druckvorlage oder Zahnfüllungshilfe

3. **Alternative Notation:** Man schreibt auch $a_{ij}$ statt $a_{i,j}$, wenn keine Verwechslungsgefahr besteht

### Spezielle Matrizen

**Nullmatrix:**
$$0 = 0_{m,n} = [0] = \begin{pmatrix} 0 & 0 & \cdots & 0 \\ 0 & 0 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 0 \end{pmatrix} \in K^{m,n}$$

**Einheitsmatrix** (oder Identität):
$$I_n := \begin{pmatrix} 1 & 0 & \cdots & 0 \\ 0 & 1 & \ddots & \vdots \\ \vdots & \ddots & \ddots & 0 \\ 0 & \cdots & 0 & 1 \end{pmatrix} \in K^{n,n}$$

### Vektoren als spezielle Matrizen

**Zeilenvektor:** Ist $m = 1$, so ist
$$A = [a_{1,1} \quad a_{1,2} \quad \cdots \quad a_{1,n}] \in K^{1,n}$$

**Spaltenvektor:** Ist $n = 1$, so ist
$$A = \begin{pmatrix} a_{1,1} \\ a_{2,1} \\ \vdots \\ a_{m,1} \end{pmatrix} \in K^{m,1}$$

Man nennt $A$ einen **Spaltenvektor** oder kurz **Vektor** in $K^{m,1}$ und schreibt kürzer:
$$K^m := K^{m,1}$$

### Beispiele

**Beispiel 1:**
$$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}$$
ist eine $2 \times 3$-Matrix mit $a_{2,1} = 4$.

**Beispiel 2:**
$$B = \begin{pmatrix} 1+i & 1-i \\ 2i & 42 \end{pmatrix}$$
ist eine $2 \times 2$-Matrix über $\mathbb{C}$.

**Beispiel 3: Spaltenvektoren**
$$\begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \quad \begin{pmatrix} 2 \\ -5 \end{pmatrix} \in \mathbb{R}^2, \qquad \begin{pmatrix} -1 \\ 6 \\ 2 \end{pmatrix} \in \mathbb{R}^3, \qquad \begin{pmatrix} 1+i \\ 4 \\ \sqrt{2}i \end{pmatrix} \in \mathbb{C}^3$$

Spaltenvektoren in $\mathbb{R}^2$ sind genau die Punkte der Ebene. Vektoren in $\mathbb{R}^3$ sind die Punkte des dreidimensionalen Raums.

---

## 2. Addition und Skalarmultiplikation

### Definition

Seien $A = [a_{i,j}]$, $B = [b_{i,j}] \in K^{m,n}$ zwei $m \times n$-Matrizen und $\lambda \in K$.

**Summe von $A$ und $B$:**
$$A + B = [a_{i,j} + b_{i,j}] \in K^{m,n}$$

**Skalarmultiplikation:**
$$\lambda A = [\lambda a_{i,j}] \in K^{m,n}$$

**Wichtig:** Nur Matrizen **gleicher Größe** dürfen addiert werden!

### Beispiel

Für $A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}$ und $B = \begin{pmatrix} 3 & 1 & -1 \\ 2 & 0 & 1 \end{pmatrix}$ ist:

$$A + B = \begin{pmatrix} 4 & 3 & 2 \\ 6 & 5 & 7 \end{pmatrix}$$

$$(-1) \cdot A = \begin{pmatrix} -1 & -2 & -3 \\ -4 & -5 & -6 \end{pmatrix}, \quad 2 \cdot B = \begin{pmatrix} 6 & 2 & -2 \\ 4 & 0 & 2 \end{pmatrix}$$

### Rechenregeln

**Für Addition** (für $A, B, C \in K^{m,n}$):

1. $(A + B) + C = A + (B + C)$ (Assoziativität)
2. $A + B = B + A$ (Kommutativität)

**Für Skalarmultiplikation** (für $A, B \in K^{m,n}$ und $\alpha, \beta \in K$):

1. $\alpha(\beta A) = (\alpha\beta)A$
2. $\alpha(A + B) = \alpha A + \alpha B$ (Distributivität)
3. $(\alpha + \beta)A = \alpha A + \beta A$ (Distributivität)

### Vektorraumstruktur

$K^{m,n}$ ist mit Addition und Skalarmultiplikation ein $K$-**Vektorraum**.

**Basis von** $K^{m,n}$: $\{E_{i,j} \mid i = 1, \ldots, m; \, j = 1, \ldots, n\}$

wobei $E_{i,j} \in K^{m,n}$ eine $1$ in Eintrag $(i,j)$ hat und alle anderen Einträge null sind.

**Dimension:**
$$\dim(K^{m,n}) = mn$$

---

## 3. Matrizenmultiplikation

### Motivation: Zeilen- und Spaltenvektor

Für einen Zeilenvektor $A = [a_{1,1} \quad a_{1,2} \quad \cdots \quad a_{1,n}] \in K^{1,n}$ und einen Spaltenvektor $B = \begin{pmatrix} b_{1,1} \\ b_{2,1} \\ \vdots \\ b_{n,1} \end{pmatrix} \in K^{n,1}$ definieren wir:

$$AB := [a_{1,1}b_{1,1} + a_{1,2}b_{2,1} + \ldots + a_{1,n}b_{n,1}] = \left[\sum_{k=1}^{n} a_{1,k}b_{k,1}\right] \in K^{1,1}$$

### Beispiel: Zeilen- mal Spaltenvektor

$$[2 \quad 1] \begin{pmatrix} -1 \\ 3 \end{pmatrix} = [2 \cdot (-1) + 1 \cdot 3] = [1] \in K^{1,1}$$

$$[1 \quad 2 \quad 3] \begin{pmatrix} 7 \\ -1 \\ 5 \end{pmatrix} = [1 \cdot 7 + 2 \cdot (-1) + 3 \cdot 5] = [20] \in K^{1,1}$$

### Definition der Matrizenmultiplikation

Seien $A = [a_{i,j}] \in K^{m,n}$ und $B = [b_{i,j}] \in K^{n,p}$.

**Wichtig:** Die Anzahl der Spalten von $A$ muss gleich der Anzahl der Zeilen von $B$ sein!

$$AB := \left[\sum_{k=1}^{n} a_{i,k}b_{k,j}\right] = [a_{i,1}b_{1,j} + a_{i,2}b_{2,j} + \ldots + a_{i,n}b_{n,j}] \in K^{m,p}$$

**Interpretation:** Der Eintrag $(i,j)$ im Produkt $AB$ entsteht durch Multiplikation von Zeile $i$ von $A$ mit Spalte $j$ von $B$.

Ausgeschrieben:

$$AB = \begin{pmatrix} \sum_{k=1}^{n} a_{1,k}b_{k,1} & \sum_{k=1}^{n} a_{1,k}b_{k,2} & \cdots & \sum_{k=1}^{n} a_{1,k}b_{k,p} \\ \sum_{k=1}^{n} a_{2,k}b_{k,1} & \sum_{k=1}^{n} a_{2,k}b_{k,2} & \cdots & \sum_{k=1}^{n} a_{2,k}b_{k,p} \\ \vdots & \vdots & \ddots & \vdots \\ \sum_{k=1}^{n} a_{m,k}b_{k,1} & \sum_{k=1}^{n} a_{m,k}b_{k,2} & \cdots & \sum_{k=1}^{n} a_{m,k}b_{k,p} \end{pmatrix}$$

### Beispiele

**Beispiel 1:**
$$\begin{pmatrix} 1 & 2 \\ 0 & 3 \end{pmatrix} \begin{pmatrix} 7 \\ -1 \end{pmatrix} = \begin{pmatrix} 1 \cdot 7 + 2 \cdot (-1) \\ 0 \cdot 7 + 3 \cdot (-1) \end{pmatrix} = \begin{pmatrix} 5 \\ -3 \end{pmatrix}$$

**Beispiel 2:**
$$\begin{pmatrix} 1 & 1 \\ 1 & 0 \\ 0 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} 5 & 1 & 1 \\ 4 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 9 & 1 & 2 \\ 5 & 1 & 1 \\ 4 & 0 & 1 \\ 1 & 1 & 0 \end{pmatrix}$$

**Beispiel 3:**
$$\begin{pmatrix} 1 & 2 & 3 & -1 \\ 0 & 1 & 0 & 2 \end{pmatrix} \begin{pmatrix} 1 & -1 & 0 \\ 1 & 2 & -1 \\ 0 & 0 & 3 \\ 1 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 2 & 3 & 6 \\ 3 & 2 & 1 \end{pmatrix}$$

**Beispiel 4: Einheitsmatrix**
$$\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} a & b \\ c & d \end{pmatrix} = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$$

Multiplikation mit der Einheitsmatrix $I_2$ ändert die Matrix nicht. Dies entspricht $1 \cdot x = x$ für reelle oder komplexe $x$.

### Rechenregeln für die Matrizenmultiplikation

Für Matrizen $A, B, C$ mit geeigneter Größe und $\alpha \in K$ gilt:

1. $A(BC) = (AB)C$ (Assoziativität)
2. $A(B + C) = AB + AC$ (Distributivität)
3. $(A + B)C = AC + BC$ (Distributivität)
4. $\alpha(AB) = (\alpha A)B = A(\alpha B)$
5. $I_m A = A = A I_n$ für $A \in K^{m,n}$

### ⚠️ Wichtige Warnung: Keine Kommutativität!

**Die Matrizenmultiplikation ist NICHT kommutativ!**

Im Allgemeinen gilt: $AB \neq BA$

**Beispiel:**
$$AB = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix}$$

$$BA = \begin{pmatrix} 1 & 0 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 2 \end{pmatrix}$$

Also: $AB \neq BA$ ✓

### Zusammenhang mit Abbildungen

Eine Matrix $A \in K^{m,n}$ definiert eine Abbildung $A : K^n \to K^m$, $\vec{x} \mapsto A\vec{x}$.

Das Produkt $AB$ entspricht der **Komposition** der beiden Abbildungen $\vec{x} \mapsto B\vec{x}$ und $\vec{x} \mapsto A\vec{x}$.

Dies erklärt, warum Matrizenmultiplikation nicht kommutativ ist (wie auch Komposition von Abbildungen nicht kommutativ ist).

---

## 4. Inverse Matrizen

### Definition

Eine quadratische Matrix $A \in K^{n,n}$ heißt **invertierbar**, falls es eine Matrix $B \in K^{n,n}$ gibt mit

$$BA = I_n \quad \text{und} \quad AB = I_n$$

Die Matrix $B$ ist dann **eindeutig bestimmt**, wird die **Inverse** von $A$ genannt und mit $A^{-1}$ bezeichnet.

### Beweis der Eindeutigkeit

Angenommen, $A$ hat zwei Inverse $B$ und $C$ mit $BA = I_n = AB$ und $CA = I_n = AC$. Dann:

$$B = BI_n = B(AC) = (BA)C = I_n C = C$$

Also ist die Inverse eindeutig bestimmt ✓

### Hinweis zur Prüfung

Man kann zeigen, dass für quadratische Matrizen es ausreicht, **nur eine** der beiden Gleichungen $BA = I_n$ **oder** $AB = I_n$ zu überprüfen – die andere gilt dann automatisch.

### Beispiele

**Beispiel 1: Invertierbare Matrix**

Die Matrix $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ ist invertierbar mit Inverse $A^{-1} = \begin{pmatrix} 1 & -1 \\ 0 & 1 \end{pmatrix}$, denn:

$$A^{-1}A = \begin{pmatrix} 1 & -1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} = I_2$$

**Beispiel 2: Nicht invertierbare Matrix**

Ist $A = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}$ invertierbar?

Angenommen ja, dann gibt es $B = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$ mit:

$$\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} = BA = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} a+b & a+b \\ c+d & c+d \end{pmatrix}$$

Aus der ersten Zeile: $1 = a+b$ und $0 = a+b$ → Widerspruch: $1 = 0$ ✗

Also ist $A$ **nicht invertierbar**.

### Eigenschaften invertierbarer Matrizen

Sind $A, B \in K^{n,n}$ invertierbar, so gelten:

1. $A^{-1}$ ist invertierbar mit $(A^{-1})^{-1} = A$

2. $AB$ ist invertierbar mit $(AB)^{-1} = B^{-1}A^{-1}$ **(Reihenfolge beachten!)**

**Beweis von Eigenschaft 2:**

$$(B^{-1}A^{-1})(AB) = B^{-1}(A^{-1}A)B = B^{-1}I_n B = B^{-1}B = I_n$$

Genauso: $(AB)(B^{-1}A^{-1}) = I_n$ ✓

---

## 5. Transponierte

### Definition

Die **Transponierte** der Matrix $A = [a_{i,j}] \in K^{m,n}$ ist die $n \times m$-Matrix

$$A^T := [b_{i,j}] \in K^{n,m}, \quad \text{wobei } b_{i,j} = a_{j,i}$$

Bei der Transposition werden also die **Zeilen von** $A$ **zu den Spalten von** $A^T$.

(Lies: $A^T$ als "A transponiert")

### Beispiele

**Beispiel 1:**
$$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix} \in \mathbb{R}^{2,3} \implies A^T = \begin{pmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{pmatrix} \in \mathbb{R}^{3,2}$$

**Beispiel 2: Vektoren**

Beim Transponieren werden Zeilenvektoren zu Spaltenvektoren und umgekehrt:

$$\begin{pmatrix} 2 \\ 3 \\ -1 \end{pmatrix}^T = [2 \quad 3 \quad -1]$$

$$[2 \quad 3 \quad -1]^T = \begin{pmatrix} 2 \\ 3 \\ -1 \end{pmatrix}$$

### Rechenregeln für die Transponierte

Für $A, B \in K^{m,n}$, $C \in K^{n,\ell}$ und $\alpha \in K$ gilt:

1. $(A^T)^T = A$
2. $(A + B)^T = A^T + B^T$
3. $(\alpha A)^T = \alpha A^T$
4. $(AC)^T = C^T A^T$ **(Reihenfolge vertauscht!)**

---

## 6. Adjungierte

### Definition

Die **Adjungierte** der Matrix $A = [a_{i,j}] \in \mathbb{C}^{m,n}$ ist die $n \times m$-Matrix

$$A^H := [b_{i,j}] \in \mathbb{C}^{n,m}, \quad \text{wobei } b_{i,j} = \overline{a_{j,i}}$$

(Lies: $A^H$ als "A hermitesch" oder "A adjungiert")

**Alternative Notation:** Statt $A^H$ wird auch $A^*$ verwendet.

**Interpretation:** Die Adjungierte von $A$ ist die Transponierte, wo zusätzlich alle Einträge komplex konjugiert werden.

### Beispiele

$$\begin{pmatrix} 1 \\ 1+i \end{pmatrix}^H = [1 \quad 1-i]$$

$$\begin{pmatrix} 1+i & 2 & 2+3i \\ -1 & 0 & -2i \end{pmatrix}^H = \begin{pmatrix} 1-i & -1 \\ 2 & 0 \\ 2-3i & 2i \end{pmatrix}$$

### Rechenregeln für die Adjungierte

Für $A, B \in \mathbb{C}^{m,n}$, $C \in \mathbb{C}^{n,\ell}$ und $\alpha \in \mathbb{C}$ gilt:

1. $(A^H)^H = A$
2. $(A + B)^H = A^H + B^H$
3. $(\alpha A)^H = \overline{\alpha} A^H$ **(Skalar wird konjugiert!)**
4. $(AC)^H = C^H A^H$ **(Reihenfolge vertauscht!)**

---

## 📌 Zusammenfassung

| Operation | Notation | Definition | Dimension | Wichtig |
|-----------|----------|------------|-----------|---------|
| **Addition** | $A + B$ | $[a_{i,j} + b_{i,j}]$ | gleich bleibend | Nur gleiche Größen! |
| **Skalarmultiplikation** | $\lambda A$ | $[\lambda a_{i,j}]$ | gleich bleibend | Eintragsweise |
| **Multiplikation** | $AB$ | $[\sum_k a_{i,k}b_{k,j}]$ | $(m \times n)(n \times p) = (m \times p)$ | Nicht kommutativ! |
| **Inverse** | $A^{-1}$ | $A^{-1}A = AA^{-1} = I_n$ | gleich (nur quadratisch) | $(AB)^{-1} = B^{-1}A^{-1}$ |
| **Transponierte** | $A^T$ | $b_{i,j} = a_{j,i}$ | $(m \times n) \to (n \times m)$ | $(AC)^T = C^T A^T$ |
| **Adjungierte** | $A^H$ | $b_{i,j} = \overline{a_{j,i}}$ | $(m \times n) \to (n \times m)$ | $(AC)^H = C^H A^H$ |

**Wichtigste Eigenschaften:**
- $K^{m,n}$ ist ein Vektorraum mit $\dim(K^{m,n}) = mn$
- Matrizenmultiplikation ist **nicht kommutativ**: $AB \neq BA$ im Allgemeinen
- Einheitsmatrix: $I_n A = A = A I_n$
- Bei Produkten von Inversen/Transponierten: **Reihenfolge vertauscht sich**

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Abbildungen]]: Matrizen als Darstellung linearer Abbildungen
- [[VL.10 Vektorräume]]: $K^{m,n}$ als Vektorraum
- [[VL.11 Basis und Dimension]]: Basis von $K^{m,n}$ und Dimension
- [[VL.13 Lineare Gleichungssysteme]]: Matrizen zur Darstellung von LGS
- [[VL.14 Gauss-Algorithmus]]: Berechnung der Inversen
- [[VL.15 Lineare Abbildungen]]: Matrizen repräsentieren lineare Abbildungen
