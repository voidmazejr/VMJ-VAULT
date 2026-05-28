**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Eigenwerte #Eigenvektoren #CharakteristischesPolynom #Eigenraum #Vielfachheit

---

## 🎯 Lernziele der Vorlesung

Eigenwerte und Eigenvektoren sind wichtige Kenngrößen einer Matrix und beschreiben, wie eine Matrix Vektoren streckt.

- **Eigenwerte und Eigenvektoren** von Matrizen
- **Charakteristisches Polynom** und Berechnung von Eigenwerten
- **Eigenraum** und **geometrische Vielfachheit**
- **Algebraische Vielfachheit** 
- Lineare Unabhängigkeit von Eigenvektoren

---

## 1. Geometrische Motivation

### Multiplikation mit Matrizen - Visualisierung

Betrachte das Quadrat mit Ecken $\vec{0} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$, $\vec{e}_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$, $\vec{e}_1 + \vec{e}_2 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$, $\vec{e}_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$.

**Beispiel 1:** $A = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix}$

Multiplikation bewirkt:
- Streckung um Faktor 2 in $x$-Richtung: $A\begin{pmatrix} 1 \\ 0 \end{pmatrix} = 2\begin{pmatrix} 1 \\ 0 \end{pmatrix}$
- $y$-Richtung bleibt gleich: $A\begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$

**Beispiel 2:** $A = \frac{1}{2}\begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix}$

- Richtung $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$ wird um 2 gestreckt: $A\begin{pmatrix} 1 \\ 1 \end{pmatrix} = 2\begin{pmatrix} 1 \\ 1 \end{pmatrix}$
- Richtung $\begin{pmatrix} 1 \\ -1 \end{pmatrix}$ bleibt gleich: $A\begin{pmatrix} 1 \\ -1 \end{pmatrix} = \begin{pmatrix} 1 \\ -1 \end{pmatrix}$

**Beispiel 3:** $A = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}$ (Quadrat wird plattgedrückt!)

- Streckung mit 2 in Richtung $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$: $A\begin{pmatrix} 1 \\ 1 \end{pmatrix} = 2\begin{pmatrix} 1 \\ 1 \end{pmatrix}$
- Streckung mit 0 in Richtung $\begin{pmatrix} 1 \\ -1 \end{pmatrix} \in \text{Kern}(A)$

**Beispiel 4:** $A = \begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}$ (Drehstreckung)

Hier ist nicht ersichtlich, ob $A$ Vektoren in eine Richtung streckt.

---

## 2. Definition von Eigenwerten und Eigenvektoren

### Definition (Eigenwerte und Eigenvektoren)

Sei $A \in K^{n,n}$ eine quadratische Matrix. Gilt

$$\boxed{A\vec{v} = \lambda\vec{v} \quad \text{mit } \lambda \in K \text{ und } \vec{v} \in K^n, \vec{v} \neq \vec{0}}$$

so heißt:

1. $\lambda$ ein **Eigenwert** von $A$ mit zugehörigem Eigenvektor $\vec{v}$
2. $\vec{v}$ ein **Eigenvektor** von $A$ zum Eigenwert $\lambda$

Die Gleichung $A\vec{v} = \lambda\vec{v}$ heißt **Eigenwertgleichung**.

**Geometrische Interpretation:** Multiplikation eines Eigenvektors mit $A$ bewirkt eine **Streckung um den Faktor $\lambda$**.

### Wichtige Bemerkungen

1. ✅ **Eigenwerte können 0 sein**
2. ❌ **Eigenvektoren können nie $\vec{0}$ sein** (sonst gilt $A\vec{0} = \vec{0} = \lambda\vec{0}$ für jedes $\lambda \in K$, was nicht interessant ist)

### Beispiel

Für $A = \begin{pmatrix} 3 & -4 \\ 2 & -3 \end{pmatrix}$:

$$A\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} -1 \\ -1 \end{pmatrix} = (-1)\begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

$$A\begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix} = 1 \cdot \begin{pmatrix} 2 \\ 1 \end{pmatrix}$$

Also hat $A$ die Eigenwerte $\lambda_1 = -1$ (mit Eigenvektor $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$) und $\lambda_2 = 1$ (mit Eigenvektor $\begin{pmatrix} 2 \\ 1 \end{pmatrix}$).

---

## 3. Eigenraum und geometrische Vielfachheit

### Definition (Eigenraum)

Sei $A \in K^{n,n}$ mit einem Eigenwert $\lambda \in K$.

**1. Eigenraum** von $A$ zum Eigenwert $\lambda$:

$$\boxed{V_\lambda = V_\lambda(A) = \{\vec{v} \in K^n \mid A\vec{v} = \lambda\vec{v}\}}$$

**2. Geometrische Vielfachheit** des Eigenwerts $\lambda$:

$$\boxed{g(\lambda) = g(\lambda, A) = \dim(V_\lambda(A))}$$

### Wichtige Eigenschaften des Eigenraums

**1. Eigenraum als Kern:**

$$A\vec{v} = \lambda\vec{v} \iff (A - \lambda I_n)\vec{v} = \vec{0}$$

Daher: $$\boxed{V_\lambda = \text{Kern}(A - \lambda I)}$$

Insbesondere ist $V_\lambda$ ein **Teilraum** des $K^n$.

**2. Eigenvektoren und Nullvektor:**

$$V_\lambda = \{\text{Eigenvektoren zum Eigenwert } \lambda\} \cup \{\vec{0}\}$$

**3. Geometrische Vielfachheit:**

$g(\lambda)$ = Dimension des Eigenraums = **maximale Anzahl linear unabhängiger Eigenvektoren** zu $\lambda$

### Beispiel

Für $A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \in \mathbb{R}^{3,3}$:

$A\begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$, also ist $1$ ein Eigenwert.

**Eigenraum:**

$$V_1 = \text{Kern}(A - I_3) = \text{Kern}\begin{pmatrix} 0 & 2 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} = \left\{\begin{pmatrix} a \\ 0 \\ b \end{pmatrix} \mid a, b \in \mathbb{R}\right\}$$

**Geometrische Vielfachheit:** $g(1, A) = \dim(V_1(A)) = 2$

---

## 4. Berechnung von Eigenwerten

### Charakteristisches Polynom

**Beobachtung:**

$$A\vec{v} = \lambda\vec{v} \text{ mit } \vec{v} \neq \vec{0} \iff (A - \lambda I)\vec{v} = \vec{0} \text{ mit } \vec{v} \neq \vec{0}$$

$$\iff A - \lambda I \text{ ist nicht invertierbar} \iff \det(A - \lambda I) = 0$$

Die Eigenwerte sind also **Nullstellen** eines Polynoms!

### Definition (Charakteristisches Polynom)

Sei $A \in K^{n,n}$.

**1. Charakteristisches Polynom** von $A$:

$$\boxed{p_A(z) := \det(A - zI_n)}$$

**2. Algebraische Vielfachheit** des Eigenwerts $\lambda$:

Die **Vielfachheit der Nullstelle** $\lambda$ im charakteristischen Polynom.

**Bezeichnung:** $a(\lambda) = a(\lambda, A)$

### Eigenschaften des charakteristischen Polynoms

Das charakteristische Polynom hat die Form:

$$p_A(z) = (-z)^n + a_{n-1}z^{n-1} + \ldots + a_1 z + a_0$$

vom **Grad $n$**.

Nach dem **Fundamentalsatz der Algebra** hat $p_A$ immer $n$ komplexe Nullstellen (mit Vielfachheiten gezählt).

Sind $\lambda_1, \ldots, \lambda_r$ die verschiedenen Nullstellen von $p_A$, so gilt:

$$p_A(z) = (-1)^n(z - \lambda_1)^{a(\lambda_1)}(z - \lambda_2)^{a(\lambda_2)} \cdots (z - \lambda_r)^{a(\lambda_r)}$$

Dann gilt:

1. $A$ hat die Eigenwerte $\lambda_1, \ldots, \lambda_r$ (keine weiteren)
2. Die Summe der algebraischen Vielfachheiten ist $n$: $$a(\lambda_1) + \ldots + a(\lambda_r) = n$$
3. $A$ hat **höchstens $n$ verschiedene Eigenwerte** (falls $r = n$)

---

## 5. Berechnung von Eigenwerten und Eigenvektoren

### Algorithmus

Ist $A \in K^{n,n}$ gegeben, berechne:

**Schritt 1:** Berechne das charakteristische Polynom $p_A(z) = \det(A - zI_n)$

**Schritt 2:** Berechne die Nullstellen von $p_A$ → **Eigenwerte** von $A$

**Schritt 3:** Für jeden Eigenwert $\lambda$ löse das homogene LGS:

$$(A - \lambda I_n)\vec{v} = \vec{0}$$

Die Lösungen $\vec{v} \neq \vec{0}$ sind die **Eigenvektoren** zum Eigenwert $\lambda$.

### Beispiel 1: Reelle Matrix mit reellen Eigenwerten

Für $A = \begin{pmatrix} 1 & 3 \\ 3 & 1 \end{pmatrix}$:

**Schritt 1:** Charakteristisches Polynom:

$$p_A(z) = \det(A - zI_2) = \det\begin{pmatrix} 1-z & 3 \\ 3 & 1-z \end{pmatrix} = (1-z)^2 - 9$$

$$= 1 - 2z + z^2 - 9 = z^2 - 2z - 8 = (z-4)(z+2)$$

**Schritt 2:** Eigenwerte: $\lambda_1 = -2$, $\lambda_2 = 4$ (beide mit $a(\lambda_i) = 1$)

**Schritt 3:** Eigenräume:

Für $\lambda_1 = -2$:

$$A + 2I_2 = \begin{pmatrix} 3 & 3 \\ 3 & 3 \end{pmatrix} \to \begin{pmatrix} 3 & 3 \\ 0 & 0 \end{pmatrix}$$

$$V_{-2}(A) = \text{Kern}(A + 2I_2) = \text{span}\left\{\begin{pmatrix} 1 \\ -1 \end{pmatrix}\right\}$$

Also $g(-2, A) = 1$.

Für $\lambda_2 = 4$:

$$V_4(A) = \text{Kern}(A - 4I_2) = \text{Kern}\begin{pmatrix} -3 & 3 \\ 3 & -3 \end{pmatrix} = \text{span}\left\{\begin{pmatrix} 1 \\ 1 \end{pmatrix}\right\}$$

Also $g(4, A) = 1$.

### Beispiel 2: Komplexe Matrix

Für $A = \begin{pmatrix} 2i & 1+i \\ 0 & 1 \end{pmatrix}$:

**Charakteristisches Polynom:**

$$p_A(z) = (z - 2i)(z - 1)$$

**Eigenwerte:** $\lambda_1 = 2i$, $\lambda_2 = 1$ (beide mit $a(\lambda_i) = 1$)

**Eigenraum für $\lambda_1 = 2i$:**

$$A - 2iI_2 = \begin{pmatrix} 0 & 1+i \\ 0 & 1-2i \end{pmatrix} \to \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$$

$$V_{2i}(A) = \text{span}\left\{\begin{pmatrix} 1 \\ 0 \end{pmatrix}\right\}$$

**Eigenraum für $\lambda_2 = 1$:**

$$A - I_2 = \begin{pmatrix} 2i-1 & 1+i \\ 0 & 0 \end{pmatrix} \to \begin{pmatrix} 1 & \frac{1-3i}{5} \\ 0 & 0 \end{pmatrix}$$

$$V_1(A) = \text{span}\left\{\begin{pmatrix} -1+3i \\ 5 \end{pmatrix}\right\} = \text{span}\left\{\begin{pmatrix} \frac{-1+3i}{5} \\ 1 \end{pmatrix}\right\}$$

### Beispiel 3: Reelle Matrix mit komplexen Eigenwerten

Für $A = \begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix} \in \mathbb{R}^{2,2} \subseteq \mathbb{C}^{2,2}$:

**Charakteristisches Polynom:**

$$p_A(z) = \det(A - zI_2) = \det\begin{pmatrix} -z & 1 \\ -1 & -z \end{pmatrix} = z^2 + 1 = (z-i)(z+i)$$

**Eigenwerte:** $\lambda_1 = i$, $\lambda_2 = -i$ (beide mit $a(\lambda_i) = 1$)

Als **reelle** Matrix betrachtet hat $A$ **keine reellen** Eigenwerte!

### Beispiel 4: Algebraische vs. geometrische Vielfachheit

Für $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$:

**Charakteristisches Polynom:**

$$p_A(z) = \det\begin{pmatrix} 1-z & 1 \\ 0 & 1-z \end{pmatrix} = (1-z)^2$$

**Eigenwert:** $\lambda = 1$ mit **algebraischer Vielfachheit** $a(1, A) = 2$

**Eigenraum:**

$$\text{Kern}(A - I_2) = \text{Kern}\begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} = \text{span}\left\{\begin{pmatrix} 1 \\ 0 \end{pmatrix}\right\}$$

**Geometrische Vielfachheit:** $g(1, A) = 1 < 2 = a(1, A)$

**Wichtig:** Die geometrische und algebraische Vielfachheit sind **nicht immer gleich**!

---

## 6. Wichtige Sätze

### Satz (Eigenwerte von Dreiecksmatrizen)

Ist $A \in K^{n,n}$ eine **obere oder untere Dreiecksmatrix**, so sind die Eigenwerte von $A$ genau die **Diagonaleinträge**.

**Beweis-Idee:** Für obere Dreiecksmatrix:

$$p_A(z) = \det\begin{pmatrix} a_{1,1}-z & a_{1,2} & \cdots & a_{1,n} \\ 0 & a_{2,2}-z & \cdots & a_{2,n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & a_{n,n}-z \end{pmatrix} = (a_{1,1}-z)(a_{2,2}-z) \cdots (a_{n,n}-z)$$

Die Nullstellen sind $a_{1,1}, a_{2,2}, \ldots, a_{n,n}$.

### Satz (Beziehung zwischen Vielfachheiten)

Ist $A \in K^{n,n}$ mit Eigenwert $\lambda \in K$, so gilt:

$$\boxed{1 \leq g(\lambda) \leq a(\lambda)}$$

Die **geometrische Vielfachheit** ist immer **kleiner oder gleich** der **algebraischen Vielfachheit**.

### Beispiel

Für $A = \begin{pmatrix} 1 & 1 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 4 \end{pmatrix}$:

**Eigenwerte:** $\lambda_1 = 1$ (mit $a(1) = 2$) und $\lambda_2 = 4$ (mit $a(4) = 1$)

**Geometrische Vielfachheiten:**

$$g(1) = \dim(\text{Kern}(A - I_3)) = 3 - \text{Rang}(A - I_3) = 3 - \text{Rang}\begin{pmatrix} 0 & 1 & 1 \\ 0 & 0 & 1 \\ 0 & 0 & 3 \end{pmatrix} = 1$$

$$g(4) = \dim(\text{Kern}(A - 4I_3)) = 3 - \text{Rang}(A - 4I_3) = 3 - \text{Rang}\begin{pmatrix} -3 & 1 & 1 \\ 0 & -3 & 1 \\ 0 & 0 & 0 \end{pmatrix} = 1$$

Für $\lambda_1 = 1$: $1 = g(1) < a(1) = 2$ (geometrische echt kleiner als algebraische)

Für $\lambda_2 = 4$: $1 = g(4) = a(4) = 1$ (beide gleich)

---

## 7. Lineare Unabhängigkeit von Eigenvektoren

### Satz (Eigenvektoren zu verschiedenen Eigenwerten)

Ist $A \in K^{n,n}$ mit Eigenvektoren $\vec{v}_1, \ldots, \vec{v}_r$ zu den **verschiedenen** Eigenwerten $\lambda_1, \ldots, \lambda_r$ (d.h. $\lambda_i \neq \lambda_j$ für $i \neq j$), so sind $\vec{v}_1, \ldots, \vec{v}_r$ **linear unabhängig**.

### Beweis-Idee (für zwei Eigenvektoren)

Seien $\vec{v}_1, \vec{v}_2$ Eigenvektoren zu verschiedenen Eigenwerten $\lambda_1, \lambda_2$ (mit $\lambda_1 \neq \lambda_2$).

Seien $\alpha_1, \alpha_2 \in K$ mit $\alpha_1\vec{v}_1 + \alpha_2\vec{v}_2 = \vec{0}$.

**Multipliziere mit $\lambda_1$:**

$$\vec{0} = \alpha_1\lambda_1\vec{v}_1 + \alpha_2\lambda_1\vec{v}_2$$

**Multipliziere mit $A$:**

$$\vec{0} = \alpha_1 A\vec{v}_1 + \alpha_2 A\vec{v}_2 = \alpha_1\lambda_1\vec{v}_1 + \alpha_2\lambda_2\vec{v}_2$$

**Differenz:**

$$\vec{0} = \alpha_2(\lambda_1 - \lambda_2)\vec{v}_2$$

Da $\vec{v}_2 \neq \vec{0}$ (Eigenvektor!) und $\lambda_1 \neq \lambda_2$, folgt $\alpha_2 = 0$.

Einsetzen: $\alpha_1\vec{v}_1 = \vec{0}$, also $\alpha_1 = 0$ (da $\vec{v}_1 \neq \vec{0}$).

**Folgerung:** $\vec{v}_1, \vec{v}_2$ sind linear unabhängig. ✓

---

## 📌 Zusammenfassung

### Definitionen

| Begriff | Definition | Bemerkung |
|---------|------------|-----------|
| **Eigenwert** | $A\vec{v} = \lambda\vec{v}$, $\vec{v} \neq \vec{0}$ | Streckungsfaktor |
| **Eigenvektor** | $\vec{v} \neq \vec{0}$ mit $A\vec{v} = \lambda\vec{v}$ | Nie $\vec{0}$! |
| **Eigenraum** | $V_\lambda = \text{Kern}(A - \lambda I)$ | Teilraum |
| **Char. Polynom** | $p_A(z) = \det(A - zI_n)$ | Grad $n$ |

### Vielfachheiten

**Geometrische Vielfachheit:** $g(\lambda) = \dim(V_\lambda) = \dim(\text{Kern}(A - \lambda I))$

**Algebraische Vielfachheit:** $a(\lambda) = $ Vielfachheit der Nullstelle $\lambda$ in $p_A(z)$

**Beziehung:** $$\boxed{1 \leq g(\lambda) \leq a(\lambda)}$$

### Berechnungsschema

1. **Charakteristisches Polynom:** $p_A(z) = \det(A - zI_n)$
2. **Nullstellen berechnen** → **Eigenwerte**
3. **Für jeden Eigenwert $\lambda$:** Löse $(A - \lambda I)\vec{v} = \vec{0}$ → **Eigenvektoren**

### Wichtige Eigenschaften

✅ Dreiecksmatrizen: Eigenwerte = Diagonaleinträge

✅ Eigenvektoren zu **verschiedenen** Eigenwerten sind **linear unabhängig**

✅ $A$ hat höchstens $n$ verschiedene Eigenwerte

✅ Summe aller algebraischen Vielfachheiten = $n$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.14 Gauss-Algorithmus]]: Lösung von $(A - \lambda I)\vec{v} = \vec{0}$
- [[VL.18 Berechnung von Grenzwerten]]: $\det(A - \lambda I) = 0$ für Eigenwerte
- [[VL.20 Sätze über stetige Funktionen]]: Eigenvektoren zu verschiedenen EW
- [[VL.32 Determinante]]: Berechnung des charakteristischen Polynoms