**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Koordinatenabbildung #Matrixdarstellung #Basiswechsel #Darstellungsmatrix #Transformationsmatrix

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung zeigt, wie abstrakte Vektoren und lineare Abbildungen durch konkrete Spaltenvektoren und Matrizen dargestellt werden können. Dies ist fundamental für numerische Berechnungen und praktische Anwendungen.

- **Koordinatenabbildung** als Isomorphismus zwischen abstrakten und konkreten Vektorräumen
- **Darstellende Matrix** einer linearen Abbildung
- **Basiswechsel** und Transformation von Koordinaten
- **Basiswechselmatrix** (Transformationsmatrix)
- Zusammenhang zwischen verschiedenen Darstellungen

---

## 1. Koordinatenabbildung

### Wiederholung: Koordinatenvektor

Sei $V$ ein endlichdimensionaler $K$-Vektorraum mit Basis $B = \{b_1, \ldots, b_n\}$. Dann lässt sich jeder Vektor $v \in V$ als **eindeutige** Linearkombination der Basisvektoren schreiben:

$$v = \sum_{j=1}^{n} \lambda_j b_j = \lambda_1 b_1 + \lambda_2 b_2 + \ldots + \lambda_n b_n$$

Der **Koordinatenvektor** von $v \in V$ bzgl. der Basis $B$ ist der Spaltenvektor:

$$\vec{v}_B = \begin{bmatrix} \lambda_1 \\ \lambda_2 \\ \vdots \\ \lambda_n \end{bmatrix} \in K^n$$

### Definition

Sei $V$ ein $K$-Vektorraum mit Basis $B = \{b_1, \ldots, b_n\}$. Die **Koordinatenabbildung** von $V$ bzgl. $B$ ist die Abbildung:

$$K_B : V \to K^n, \quad v = \sum_{j=1}^{n} \lambda_j b_j \mapsto \vec{v}_B = \begin{bmatrix} \lambda_1 \\ \lambda_2 \\ \vdots \\ \lambda_n \end{bmatrix}$$

### Hauptsatz

**Satz:** Sei $V$ ein $K$-Vektorraum mit Basis $B = \{b_1, \ldots, b_n\}$. Die Koordinatenabbildung $K_B$ ist **linear und bijektiv**, also ein **Isomorphismus**.

Die Inverse ist:

$$K_B^{-1} : K^n \to V, \quad \begin{bmatrix} \lambda_1 \\ \vdots \\ \lambda_n \end{bmatrix} \mapsto v = \sum_{j=1}^{n} \lambda_j b_j = \lambda_1 b_1 + \ldots + \lambda_n b_n$$

**Beweis der Linearität:** Für $v = \sum_{j=1}^{n} \lambda_j b_j \in V$ und $w = \sum_{j=1}^{n} \mu_j b_j \in V$ ist $v + w = \sum_{j=1}^{n} (\lambda_j + \mu_j) b_j$, also:

$$K_B(v + w) = \begin{bmatrix} \lambda_1 + \mu_1 \\ \vdots \\ \lambda_n + \mu_n \end{bmatrix} = \begin{bmatrix} \lambda_1 \\ \vdots \\ \lambda_n \end{bmatrix} + \begin{bmatrix} \mu_1 \\ \vdots \\ \mu_n \end{bmatrix} = K_B(v) + K_B(w)$$

Für $\lambda \in K$ ist $\lambda v = \sum_{j=1}^{n} (\lambda \lambda_j) b_j$, also:

$$K_B(\lambda v) = \begin{bmatrix} \lambda \lambda_1 \\ \vdots \\ \lambda \lambda_n \end{bmatrix} = \lambda \begin{bmatrix} \lambda_1 \\ \vdots \\ \lambda_n \end{bmatrix} = \lambda K_B(v)$$

Also ist $K_B$ linear ✓

### Beispiel

Sei $V = \mathbb{C}[z]_{\leq 2} = \{a_0 + a_1 z + a_2 z^2 \mid a_0, a_1, a_2 \in \mathbb{C}\}$ mit Basis $B = \{1, z, z^2\}$.

Für $p(z) = a_0 + a_1 z + a_2 z^2 \in V$ ist:

$$p(z) = a_0 \cdot 1 + a_1 \cdot z + a_2 \cdot z^2$$

Der Koordinatenvektor von $p$ bzgl. $B$ ist:

$$K_B(p) = \vec{p}_B = \begin{bmatrix} a_0 \\ a_1 \\ a_2 \end{bmatrix}$$

Die Koordinatenabbildung ist also:

$$K_B : V \to \mathbb{C}^3, \quad K_B(a_0 + a_1 z + a_2 z^2) = \begin{bmatrix} a_0 \\ a_1 \\ a_2 \end{bmatrix}$$

---

## 2. Matrixdarstellung

### Motivation

**Ziel:** Stelle eine lineare Abbildung $f : V \to W$ durch eine Matrix dar.

Seien:
1. $V$ endlichdimensional mit Basis $B = \{b_1, \ldots, b_n\}$
2. $W$ endlichdimensional mit Basis $C = \{c_1, \ldots, c_m\}$
3. $f : V \to W$ linear

### Herleitung

Für $v = \lambda_1 b_1 + \lambda_2 b_2 + \ldots + \lambda_n b_n \in V$ gilt (da $f$ linear):

$$f(v) = \lambda_1 f(b_1) + \lambda_2 f(b_2) + \ldots + \lambda_n f(b_n)$$

Wende die Koordinatenabbildung $K_C$ an:

$$K_C(f(v)) = K_C(\lambda_1 f(b_1) + \lambda_2 f(b_2) + \ldots + \lambda_n f(b_n))$$

$$= \lambda_1 K_C(f(b_1)) + \lambda_2 K_C(f(b_2)) + \ldots + \lambda_n K_C(f(b_n))$$

$$= [K_C(f(b_1)) \mid K_C(f(b_2)) \mid \cdots \mid K_C(f(b_n))] \begin{bmatrix} \lambda_1 \\ \vdots \\ \lambda_n \end{bmatrix}$$

$$= [K_C(f(b_1)) \mid K_C(f(b_2)) \mid \cdots \mid K_C(f(b_n))] \cdot K_B(v)$$

### Definition

Die Matrix

$$f_{B,C} := [K_C(f(b_1)) \mid K_C(f(b_2)) \mid \cdots \mid K_C(f(b_n))] \in K^{m,n}$$

heißt die **darstellende Matrix** von $f$ bzgl. $B$ und $C$, oder auch **Matrixdarstellung** von $f$ bzgl. $B$ und $C$.

**Konstruktion:** Die $j$-te Spalte der darstellenden Matrix enthält den Koordinatenvektor von $f(b_j)$ bzgl. der Basis $C$.

### Praktische Berechnung

Um $f_{B,C}$ zu berechnen:

1. Berechne $f(b_1), f(b_2), \ldots, f(b_n)$
2. Stelle jedes $f(b_j)$ in der Basis $C$ dar:
   $$f(b_j) = a_{1,j} c_1 + a_{2,j} c_2 + \ldots + a_{m,j} c_m$$
3. Die Koeffizienten bilden die $j$-te Spalte:

$$f_{B,C} = \begin{bmatrix} a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\ a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m,1} & a_{m,2} & \cdots & a_{m,n} \end{bmatrix} \in K^{m,n}$$

### Hauptsatz

**Satz:** Sei $f : V \to W$ linear, wobei $V, W$ endlichdimensionale Vektorräume mit Basen $B$ und $C$ sind. Dann gilt für jeden Vektor $v \in V$:

$$K_C(f(v)) = f_{B,C} \cdot K_B(v)$$

also $K_C \circ f = f_{B,C} \circ K_B$, d.h.

$$\boxed{f_{B,C} = K_C \circ f \circ K_B^{-1}}$$

### Kommutatives Diagramm

![[Screenshot 2026-01-08 at 09.39.12.png]]

### Beispiele

**Beispiel 1: Standardbasen**

Sei $f : \mathbb{R}^2 \to \mathbb{R}^3$, $\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} \mapsto \begin{bmatrix} x_1 \\ 2x_2 + x_1 \\ x_1 - x_2 \end{bmatrix}$.

Betrachte die Standardbasen:
$$B = \left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}\right\}, \quad C = \left\{\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}\right\}$$

Berechne:
$$f(b_1) = f\left(\begin{bmatrix} 1 \\ 0 \end{bmatrix}\right) = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix} = 1c_1 + 1c_2 + 1c_3$$

$$f(b_2) = f\left(\begin{bmatrix} 0 \\ 1 \end{bmatrix}\right) = \begin{bmatrix} 0 \\ 2 \\ -1 \end{bmatrix} = 0c_1 + 2c_2 - 1c_3$$

Darstellende Matrix:
$$f_{B,C} = \begin{bmatrix} 1 & 0 \\ 1 & 2 \\ 1 & -1 \end{bmatrix} \in \mathbb{R}^{3,2}$$

**Beispiel 2: Polynome**

Sei $V = \mathbb{C}[z]_{\leq 2}$ mit Basis $B = \{1, z, z^2\}$ und $f : V \to V$ mit:

$$f(a_0 + a_1 z + a_2 z^2) = (a_0 + a_2) + (a_1 - a_0)z + (2a_1 + a_2)z^2$$

Nehme $C = B$. Berechne:
$$f(1) = 1 - z + 0z^2 = 1 \cdot 1 + (-1) \cdot z + 0 \cdot z^2$$
$$f(z) = 0 + z + 2z^2 = 0 \cdot 1 + 1 \cdot z + 2 \cdot z^2$$
$$f(z^2) = 1 + 0z + z^2 = 1 \cdot 1 + 0 \cdot z + 1 \cdot z^2$$

Darstellende Matrix:
$$f_{B,B} = \begin{bmatrix} 1 & 0 & 1 \\ -1 & 1 & 0 \\ 0 & 2 & 1 \end{bmatrix}$$

---

## 3. Basiswechsel

### Motivation

Die Koordinatenvektoren hängen von der gewählten Basis ab. Wie hängen Koordinatenvektoren bzgl. verschiedener Basen zusammen?

### Koordinatenvektor bei Basiswechsel

**Satz:** Sei $V$ ein endlichdimensionaler Vektorraum mit Basis $B_1$ und Basis $B_2$. Dann gilt für alle $v \in V$:

$$\vec{v}_{B_2} = \text{id}_{B_1,B_2} \cdot \vec{v}_{B_1}$$

Die Matrix $\text{id}_{B_1,B_2}$ heißt **Basiswechselmatrix** oder **Basisübergangsmatrix** oder **Transformationsmatrix**.

**Beweis:** Nach Satz 16.6 gilt:
$$K_{B_2}(v) = K_{B_2}(\text{id}(v)) = \text{id}_{B_1,B_2} \cdot K_{B_1}(v)$$

### Berechnung der Basiswechselmatrix

Die $i$-te Spalte von $\text{id}_{B_1,B_2}$ ist:

$$\text{id}_{B_1,B_2}(e_i) = K_{B_2}(K_{B_1}^{-1}(e_i)) = K_{B_2}(b_i)$$

wobei $e_i \in K^n$ der $i$-te Standardbasisvektor ist und $b_i$ der $i$-te Vektor der Basis $B_1$.

**Formel:**
$$\text{id}_{B_1,B_2} = K_{B_2} \circ K_{B_1}^{-1}$$

### Kommutatives Diagramm

![[Screenshot 2026-01-08 at 09.40.15.png]]

### Beispiel

Sei $V = \mathbb{R}^2$ mit:
- Standardbasis $B_1 = \left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}\right\}$
- Basis $B_2 = \left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 1 \\ 1 \end{bmatrix}\right\}$

**Koordinatenabbildungen:**
$$K_{B_1}\left(\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}\right) = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$$

$$K_{B_2}\left(\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}\right) = \begin{bmatrix} x_1 - x_2 \\ x_2 \end{bmatrix}$$

(da $\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = (x_1 - x_2) \begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$)

**Basiswechselmatrix:**
$$\text{id}_{B_1,B_2} = [K_{B_2}(\text{id}(b_1)) \mid K_{B_2}(\text{id}(b_2))]$$

$$= \left[K_{B_2}\left(\begin{bmatrix} 1 \\ 0 \end{bmatrix}\right) \mid K_{B_2}\left(\begin{bmatrix} 0 \\ 1 \end{bmatrix}\right)\right]$$

$$= \begin{bmatrix} 1 & -1 \\ 0 & 1 \end{bmatrix}$$

**Verifikation:**
$$\text{id}_{B_1,B_2} \cdot K_{B_1}\left(\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}\right) = \begin{bmatrix} 1 & -1 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} x_1 - x_2 \\ x_2 \end{bmatrix} = K_{B_2}\left(\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}\right)$$

---

## 4. Darstellende Matrix bei Basiswechsel

### Hauptsatz

**Satz:** Sei $f : V \to W$ linear, $B_1, B_2$ Basen von $V$ und $C_1, C_2$ Basen von $W$. Dann gilt:

$$\boxed{f_{B_2,C_2} = \text{id}_{C_1,C_2} \cdot f_{B_1,C_1} \cdot \text{id}_{B_2,B_1}}$$

**Interpretation:** Wir erhalten die neue Matrixdarstellung aus der alten, indem wir mit den entsprechenden Basiswechselmatrizen multiplizieren.

**Beweis:** Mit der Formel $f_{B,C} = K_C \circ f \circ K_B^{-1}$:

$$f_{B_2,C_2} = K_{C_2} \circ f \circ K_{B_2}^{-1}$$
$$= K_{C_2} \circ \text{id} \circ f \circ \text{id} \circ K_{B_2}^{-1}$$
$$= K_{C_2} \circ \text{id} \circ K_{C_1}^{-1} \circ K_{C_1} \circ f \circ K_{B_1}^{-1} \circ K_{B_1} \circ \text{id} \circ K_{B_2}^{-1}$$
$$= \text{id}_{C_1,C_2} \cdot f_{B_1,C_1} \cdot \text{id}_{B_2,B_1}$$ 
### Kommutatives Diagramm

![[Screenshot 2026-01-08 at 09.41.22.png]]
### Spezialfall: Gleiche Vektorräume

Besonders wichtig ist der Fall $V = W$ mit $C_1 = B_1$ und $C_2 = B_2$:

$$f_{B_2,B_2} = \text{id}_{B_1,B_2} \cdot f_{B_1,B_1} \cdot \text{id}_{B_2,B_1} = (\text{id}_{B_2,B_1})^{-1} \cdot f_{B_1,B_1} \cdot \text{id}_{B_2,B_1}$$

Mit $A_1 = f_{B_1,B_1}$, $A_2 = f_{B_2,B_2}$ und $S = \text{id}_{B_2,B_1}$:

$$A_2 = S^{-1} A_1 S$$

Diese Transformation heißt **Ähnlichkeitstransformation** und wird in VL.34 (Diagonalisierung) zentral sein.

### Beispiel

Sei $V = \mathbb{R}^2$ mit Basen $B_1, B_2$ aus dem vorherigen Beispiel und Basiswechselmatrizen:

$$\text{id}_{B_1,B_2} = \begin{bmatrix} 1 & -1 \\ 0 & 1 \end{bmatrix}, \quad \text{id}_{B_2,B_1} = \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}$$

Sei $f \in \mathcal{L}(\mathbb{R}^2, \mathbb{R}^2)$ mit $f\left(\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}\right) = \begin{bmatrix} x_1 + x_2 \\ 2x_2 \end{bmatrix}$.

**Berechne** $f_{B_1,B_1}$ (mit $C_1 = B_1$):

$$f_{B_1,B_1} = \left[K_{B_1}(f(b_1)) \mid K_{B_1}(f(b_2))\right]$$

$$= \left[K_{B_1}\left(\begin{bmatrix} 1 \\ 0 \end{bmatrix}\right) \mid K_{B_1}\left(\begin{bmatrix} 1 \\ 2 \end{bmatrix}\right)\right] = \begin{bmatrix} 1 & 1 \\ 0 & 2 \end{bmatrix}$$

**Berechne** $f_{B_2,B_2}$ (mit $C_2 = B_2$) **mittels Basiswechsel:**

$$f_{B_2,B_2} = \text{id}_{B_1,B_2} \cdot f_{B_1,B_1} \cdot \text{id}_{B_2,B_1}$$

$$= \begin{bmatrix} 1 & -1 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 1 & 1 \\ 0 & 2 \end{bmatrix} \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}$$

$$= \begin{bmatrix} 1 & -1 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 1 & 2 \\ 0 & 2 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 2 \end{bmatrix}$$

**Beobachtung:** Die zweite darstellende Matrix ist **diagonal** und damit einfacher! Dies ist das Ziel der Diagonalisierung (VL.34).

---

## 📌 Zusammenfassung

### Koordinatenabbildung

| Konzept | Definition | Eigenschaften |
|---------|------------|---------------|
| **Koordinatenabbildung** | $K_B : V \to K^n$ | Linear, bijektiv (Isomorphismus) |
| **Inverse** | $K_B^{-1} : K^n \to V$ | $K_B^{-1}(\vec{v}_B) = v$ |

### Darstellende Matrix

**Konstruktion:** $f_{B,C} = [K_C(f(b_1)) \mid \ldots \mid K_C(f(b_n))]$

**Formel:** $f_{B,C} = K_C \circ f \circ K_B^{-1}$

**Zusammenhang:** $K_C(f(v)) = f_{B,C} \cdot K_B(v)$

### Basiswechsel

**Koordinatenvektor:** $\vec{v}_{B_2} = \text{id}_{B_1,B_2} \cdot \vec{v}_{B_1}$

**Basiswechselmatrix:** $\text{id}_{B_1,B_2} = K_{B_2} \circ K_{B_1}^{-1}$

**Darstellende Matrix:** $f_{B_2,C_2} = \text{id}_{C_1,C_2} \cdot f_{B_1,C_1} \cdot \text{id}_{B_2,B_1}$

**Spezialfall (Ähnlichkeit):** $A_2 = S^{-1} A_1 S$ mit $S = \text{id}_{B_2,B_1}$

### Kommutative Diagramme

Alle Zusammenhänge lassen sich durch kommutative Diagramme visualisieren, die zeigen, dass verschiedene Wege zum gleichen Ergebnis führen.

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.11 Basis und Dimension]]: Koordinatenvektoren eingeführt
- [[VL.15 Lineare Abbildungen]]: Matrizen als lineare Abbildungen
- [[VL.34 Diagonalisierbarkeit]]: Ähnlichkeitstransformation zur Diagonalisierung

