**Class:** [[AnaLina]]  
**Date:** 10-01-2026 
**Topics:** #LineareAbbildungen #Kern #Bild #Dimensionsformel #Injektivität #Surjektivität

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt lineare Abbildungen ein – das zentrale Konzept der linearen Algebra. Lineare Abbildungen sind Funktionen zwischen Vektorräumen, die die Vektorraumstruktur respektieren.

- **Definition** linearer Abbildungen (Additivität und Homogenität)
- **Kern und Bild** als fundamentale Charakteristika
- **Dimensionsformel** als zentraler Zusammenhang
- **Berechnung von Basen** für Kern und Bild
- **Injektivität und Surjektivität** charakterisiert durch Kern und Bild
- **Zusammenhang** zwischen Matrizen und linearen Abbildungen

---

## 1. Definition und Grundeigenschaften

### Definition

Seien $V, W$ zwei $K$-Vektorräume. Eine Abbildung $f : V \to W$ heißt **linear**, wenn für alle $v, w \in V$ und $\lambda \in K$ gilt:

1. **Additivität:** $f(v + w) = f(v) + f(w)$

2. **Homogenität:** $f(\lambda v) = \lambda f(v)$

**Notation:** Die Menge aller linearen Abbildungen von $V$ nach $W$ wird mit $\mathcal{L}(V,W)$ oder $\text{Hom}(V,W)$ bezeichnet.

**Alternative Bezeichnung:** Eine lineare Abbildung heißt auch **Homomorphismus**.

### Wichtige Eigenschaften

**Satz:** Seien $V, W, X$ $K$-Vektorräume.

1. Ist $f : V \to W$ linear, so gilt $f(0) = 0$

2. Sind $f : V \to W$ und $g : W \to X$ linear, so ist auch die **Komposition** $g \circ f : V \to X$ linear

3. Ist $f : V \to W$ linear und **bijektiv**, so ist auch die **Umkehrabbildung** $f^{-1} : W \to V$ linear

**Bemerkung zu (3):** Bijektive lineare Abbildungen heißen **Isomorphismus**.

**Bemerkung zu (1):** Ist $f : V \to W$ eine Abbildung mit $f(0) \neq 0$, dann ist $f$ **nicht linear**.

### Beispiele

**Beispiel 1: Spiegelung im $\mathbb{R}^2$**

$$f : \mathbb{R}^2 \to \mathbb{R}^2, \quad \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} \mapsto \begin{bmatrix} x_2 \\ x_1 \end{bmatrix}$$

Dies ist die Spiegelung an der ersten Winkelhalbierenden. Sie ist linear:

$$f(v + w) = f\left(\begin{bmatrix} x_1 + y_1 \\ x_2 + y_2 \end{bmatrix}\right) = \begin{bmatrix} x_2 + y_2 \\ x_1 + y_1 \end{bmatrix} = \begin{bmatrix} x_2 \\ x_1 \end{bmatrix} + \begin{bmatrix} y_2 \\ y_1 \end{bmatrix} = f(v) + f(w)$$

$$f(\lambda v) = f\left(\begin{bmatrix} \lambda x_1 \\ \lambda x_2 \end{bmatrix}\right) = \begin{bmatrix} \lambda x_2 \\ \lambda x_1 \end{bmatrix} = \lambda \begin{bmatrix} x_2 \\ x_1 \end{bmatrix} = \lambda f(v)$$

**Beispiel 2: Von Vektoren zu Matrizen**

$$f : \mathbb{C}^3 \to \mathbb{C}^{2,2}, \quad \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} \mapsto \begin{bmatrix} x_1 & x_2 \\ x_1 & x_3 \end{bmatrix}$$

ist linear (Verifikation analog zu Beispiel 1).

**Beispiel 3: Identität**

Die Identität $\text{id}_V : V \to V$ mit $\text{id}_V(v) = v$ ist linear.

**Beispiel 4: Lineare Funktionen**

$f : \mathbb{R} \to \mathbb{R}$, $x \mapsto ax$ ist linear.

**Aber:** $f(x) = 2x + 1$ ist **nicht linear**, da $f(0) = 1 \neq 0$.

**Beispiel 5: Quadratfunktion**

$f : \mathbb{R} \to \mathbb{R}$, $x \mapsto x^2$ ist **nicht linear**, denn:

$$f(x + y) = (x+y)^2 = x^2 + 2xy + y^2 \neq x^2 + y^2 = f(x) + f(y)$$

(außer für $x = 0$ oder $y = 0$)

---

## 2. Matrizen als lineare Abbildungen

### Hauptsatz

**Satz:** Sei $A \in K^{m,n}$. Dann ist $f : K^n \to K^m$, $x \mapsto Ax$, **linear**, denn nach den Rechenregeln für Matrizen gilt für alle $x, y \in K^n$ und $\lambda \in K$:

$$f(x + y) = A(x + y) = Ax + Ay = f(x) + f(y)$$
$$f(\lambda x) = A(\lambda x) = \lambda Ax = \lambda f(x)$$

**Fazit:** Jede Matrix kann als lineare Abbildung angesehen werden!

### Umkehrung

**Satz:** Ist $f : K^n \to K^m$ linear, dann gibt es eine Matrix $A \in K^{m,n}$ mit $f(x) = Ax$ für alle $x \in K^n$.

**Konstruktion der Matrix:** Dabei enthält $A = [a_1 \mid \ldots \mid a_n]$ die Bilder der **Standardbasisvektoren**:

$$e_1 = \begin{bmatrix} 1 \\ 0 \\ \vdots \\ 0 \end{bmatrix}, \quad \ldots, \quad e_n = \begin{bmatrix} 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}$$

Also: $a_1 = f(e_1), \ldots, a_n = f(e_n)$.

**Beweis:** Für $x = \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix} = \sum_{j=1}^{n} x_j e_j$ gilt:

$$f(x) = f\left(\sum_{j=1}^{n} x_j e_j\right) = \sum_{j=1}^{n} x_j f(e_j) = \sum_{j=1}^{n} x_j a_j = Ax$$

---

## 3. Vektorraumstruktur auf $\mathcal{L}(V,W)$

### Definition

Für $f, g \in \mathcal{L}(V,W)$ und $\lambda \in K$ definieren wir:

$$(f + g)(v) := f(v) + g(v)$$
$$(\lambda f)(v) := \lambda f(v)$$

**Satz:** Mit diesen Operationen ist $\mathcal{L}(V,W)$ selbst wieder ein $K$-Vektorraum.

Die **Nullabbildung** ist die Abbildung, die jeden Vektor auf $0 \in W$ abbildet.

### Rechenregeln

Für lineare Abbildungen $f, g, h$ und $\lambda \in K$ gilt (falls die Verknüpfungen definiert sind):

1. $f \circ (g \circ h) = (f \circ g) \circ h$ (Assoziativität)
2. $f \circ (g + h) = (f \circ g) + (f \circ h)$ (Distributivität)
3. $(f + g) \circ h = (f \circ h) + (g \circ h)$ (Distributivität)
4. $\lambda(f \circ g) = (\lambda f) \circ g = f \circ (\lambda g)$
5. $\text{id} \circ f = f = f \circ \text{id}$

**Beachte:** Diese Regeln entsprechen den Rechenregeln für die Matrizenmultiplikation (Satz 12.12), wobei die Komposition der Matrizenmultiplikation entspricht.

---

## 4. Kern und Bild

### Definitionen

Sei $f : V \to W$ linear.

**Kern von $f$:**
$$\text{Kern}(f) = \{v \in V \mid f(v) = 0\} = f^{-1}(\{0\})$$

**Bild von $f$:**
$$\text{Bild}(f) = f(V) = \{f(v) \mid v \in V\}$$

### Visualisierung

![[Screenshot 2026-01-08 at 13.00.31.png]]
### Hauptsatz

**Satz:** Sei $f : V \to W$ linear. Dann gilt:

1. $\text{Kern}(f)$ ist ein **Teilraum von** $V$
2. $\text{Bild}(f)$ ist ein **Teilraum von** $W$

**Beweis für (1):** Mit dem Teilraumkriterium:
- $f(0) = 0 \implies 0 \in \text{Kern}(f)$
- $v, w \in \text{Kern}(f) \implies f(v+w) = f(v) + f(w) = 0 + 0 = 0 \implies v+w \in \text{Kern}(f)$
- $v \in \text{Kern}(f), \lambda \in K \implies f(\lambda v) = \lambda f(v) = \lambda \cdot 0 = 0 \implies \lambda v \in \text{Kern}(f)$

---

## 5. Berechnung von Basen für Kern und Bild

### Kern einer Matrix

Sei $A \in K^{m,n}$. Dann ist:

$$\text{Kern}(A) = \{x \in K^n \mid Ax = 0\} = L(A,0)$$

die Lösungsmenge des **homogenen linearen Gleichungssystems** $Ax = 0$.

**Algorithmus zur Berechnung einer Basis von Kern$(A)$:**

**Schritt 1:** Bringe $A$ in normierte Zeilenstufenform

**Schritt 2:** Ist $\text{Rang}(A) = r$, so gibt es $n - r$ freie Variablen

**Schritt 3:** Setze jeweils eine freie Variable $= 1$ und alle anderen $= 0$:
- 1. freie Variable $= 1$, andere $= 0$ → 1. Basisvektor
- 2. freie Variable $= 1$, andere $= 0$ → 2. Basisvektor
- usw.

Dies ergibt eine Basis von $\text{Kern}(A)$ mit $n - r$ Basisvektoren.

**Folgerung:**
$$\dim(\text{Kern}(A)) = n - r = n - \text{Rang}(A)$$

### Beispiel: Basis des Kerns

$$A = \begin{bmatrix} 0 & 0 & 1 & -1 \\ 3 & 0 & -6 & -6 \\ 1 & 0 & -2 & -2 \end{bmatrix} \xrightarrow{\text{Gauß}} \begin{bmatrix} 1 & 0 & 0 & -4 \\ 0 & 0 & 1 & -1 \\ 0 & 0 & 0 & 0 \end{bmatrix}$$

$\text{Rang}(A) = 2 \implies n - \text{Rang}(A) = 4 - 2 = 2$ freie Variablen

**Freie Variablen:** $x_2 = s$, $x_4 = t$

**Aus den Zeilen:**
- Zeile I: $x_1 = 4x_4 = 4t$
- Zeile II: $x_3 = x_4 = t$

**Lösungsmenge:**
$$\text{Kern}(A) = \left\{\begin{bmatrix} 4t \\ s \\ t \\ t \end{bmatrix} \, \Bigg| \, s,t \in \mathbb{R}\right\} = s \begin{bmatrix} 0 \\ 1 \\ 0 \\ 0 \end{bmatrix} + t \begin{bmatrix} 4 \\ 0 \\ 1 \\ 1 \end{bmatrix}$$

**Basis von Kern$(A)$:**
$$(i) \, s = 1, t = 0: \quad \begin{bmatrix} 0 \\ 1 \\ 0 \\ 0 \end{bmatrix}$$
$$(ii) \, s = 0, t = 1: \quad \begin{bmatrix} 4 \\ 0 \\ 1 \\ 1 \end{bmatrix}$$

Also: $\left\{\begin{bmatrix} 0 \\ 1 \\ 0 \\ 0 \end{bmatrix}, \begin{bmatrix} 4 \\ 0 \\ 1 \\ 1 \end{bmatrix}\right\}$ ist eine Basis mit $\dim(\text{Kern}(A)) = 2$ ✓

### Bild einer Matrix

Sei $A \in K^{m,n}$ mit Spalten $a_1, \ldots, a_n \in K^m$, also $A = [a_1 \mid \ldots \mid a_n]$.

Für $x \in K^n$ ist:
$$Ax = [a_1 \mid \ldots \mid a_n] \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix} = x_1 a_1 + \ldots + x_n a_n = \sum_{j=1}^{n} x_j a_j$$

Daher:
$$\text{Bild}(A) = \{Ax \mid x \in K^n\} = \text{span}\{a_1, \ldots, a_n\}$$

Die Spalten von $A$ bilden also ein **Erzeugendensystem** von $\text{Bild}(A)$.

**Algorithmus zur Berechnung einer Basis von Bild$(A)$:**

**Schritt 1:** Bringe $A$ in Zeilenstufenform

**Schritt 2:** Die **Spaltenvektoren von** $A$ (nicht der ZSF!), die zu einem **Pivotelement** in der ZSF gehören, bilden eine Basis des Bildes

**Folgerung:**
$$\dim(\text{Bild}(A)) = \text{Rang}(A)$$

### Beispiel: Basis des Bildes

$$A = \begin{bmatrix} 0 & 0 & 1 & -3 \\ 0 & 2 & 1 & 1 \\ 0 & 4 & 3 & -1 \end{bmatrix} \xrightarrow{\text{Gauß}} \begin{bmatrix} 0 & 1 & 0 & 2 \\ 0 & 0 & 1 & -3 \\ 0 & 0 & 0 & 0 \end{bmatrix}$$

**Pivotelemente** in NZSF: 2. und 3. Spalte

**Wähle daher die 2. und 3. Spalte von** $A$ **(nicht der NZSF!) als Basis:**

$$\text{Basis}(\text{Bild}(A)) = \left\{\begin{bmatrix} 0 \\ 2 \\ 4 \end{bmatrix}, \begin{bmatrix} 1 \\ 1 \\ 3 \end{bmatrix}\right\}$$

mit $\dim(\text{Bild}(A)) = \text{Rang}(A) = 2$ ✓

**Wichtig:** Die **Spalten der Originalmatrix** $A$, nicht der ZSF!

---

## 6. Dimensionsformel

### Hauptsatz

**Satz (Dimensionsformel):** Sei $f : V \to W$ linear und $V$ endlichdimensional. Dann gilt:

$$\boxed{\dim(V) = \dim(\text{Kern}(f)) + \dim(\text{Bild}(f))}$$

**Für Matrizen:** Sei $A \in K^{m,n}$. Dann:

$$\dim(K^n) = \dim(\text{Kern}(A)) + \dim(\text{Bild}(A))$$
$$n = (n - \text{Rang}(A)) + \text{Rang}(A)$$

### Interpretation

Die Dimensionsformel sagt:

$V$ ist "aufgeteilt" in:
- **Kern$(f)$:** Diese Vektoren werden auf $0 \in W$ abgebildet
- **Rest:** Wird auf Bild$(f)$ abgebildet

![[Screenshot 2026-01-08 at 13.29.50.png]]

---

## 7. Injektivität und Surjektivität

### Charakterisierung

**Satz:** Sei $f : V \to W$ linear. Dann gilt:

**1. Injektivität:**
$$f \text{ ist injektiv} \iff \text{Kern}(f) = \{0\} \iff \dim(\text{Kern}(f)) = 0$$

**2. Surjektivität:**
$$f \text{ ist surjektiv} \iff \text{Bild}(f) = W \iff \dim(\text{Bild}(f)) = \dim(W)$$

(Letzte Äquivalenz nur falls $\dim(W) < \infty$)

**3. Bijektivität bei gleicher Dimension:**

Wenn $\dim(V) = \dim(W) < \infty$, so gilt:
$$f \text{ ist bijektiv} \iff f \text{ ist injektiv} \iff f \text{ ist surjektiv}$$

### Beweis der Äquivalenzen in (3)

Mit der Dimensionsformel $\dim(V) = \dim(\text{Kern}(f)) + \dim(\text{Bild}(f))$ gilt:

$$\begin{align}
f \text{ injektiv} &\stackrel{(1)}{\iff} \dim(\text{Kern}(f)) = 0 \\
&\stackrel{\text{Dimensionsf.}}{\iff} \dim(V) = \dim(\text{Bild}(f)) \\
&\stackrel{\dim(V)=\dim(W)}{\iff} \dim(\text{Bild}(f)) = \dim(W) \\
&\stackrel{(2)}{\iff} f \text{ surjektiv}
\end{align}$$

Also: Bei gleicher Dimension folgt aus Injektivität die Surjektivität (und umgekehrt), und beides impliziert Bijektivität ✓

### Beispiele

**Beispiel 1:**

$$f : \mathbb{R}^{2,2} \to \mathbb{R}[z]_{\leq 2}, \quad \begin{bmatrix} a & b \\ c & d \end{bmatrix} \mapsto az^2 + b$$

ist linear mit:
- $\dim(\text{Kern}(f)) = 2 \neq 0$ → **nicht injektiv**
- $\dim(\text{Bild}(f)) = 2 \neq 3 = \dim(\mathbb{R}[z]_{\leq 2})$ → **nicht surjektiv**

**Beispiel 2:**

$$f : \mathbb{R}^5 \to \mathbb{R}^3, \quad x \mapsto Ax \text{ mit } A = \begin{bmatrix} 1 & 0 & 0 & 0 & -3 \\ 0 & 1 & 0 & 0 & 1 \\ 0 & 0 & 0 & 1 & 0 \end{bmatrix} \in \mathbb{R}^{3,5}$$

- $\text{Rang}(A) = 3 \implies \dim(\text{Bild}(f)) = 3 = \dim(\mathbb{R}^3)$ → **surjektiv**
- $\dim(\text{Kern}(f)) = n - \text{Rang}(A) = 5 - 3 = 2 \neq 0$ → **nicht injektiv**

---

## 📌 Zusammenfassung

### Lineare Abbildungen

| Konzept | Definition | Bedeutung |
|---------|------------|-----------|
| **Linear** | $f(v+w) = f(v) + f(w)$ und $f(\lambda v) = \lambda f(v)$ | Erhält Vektorraumstruktur |
| **Matrix-Darstellung** | $f(x) = Ax$ mit $A = [f(e_1) \mid \ldots \mid f(e_n)]$ | Jede lin. Abb. $K^n \to K^m$ ist eine Matrix |
| **Homomorphismus** | Lineare Abbildung | Alternative Bezeichnung |
| **Isomorphismus** | Bijektive lineare Abbildung | "Strukturerhaltende" Bijektion |

### Kern und Bild

| Konzept | Definition | Dimension | Berechnung |
|---------|------------|-----------|------------|
| **Kern** | $\{v \in V \mid f(v) = 0\}$ | $n - \text{Rang}(A)$ | Löse $Ax = 0$, freie Variablen → Basis |
| **Bild** | $\{f(v) \mid v \in V\}$ | $\text{Rang}(A)$ | Spalten von $A$ zu Pivots in ZSF |

### Dimensionsformel

$$\boxed{\dim(V) = \dim(\text{Kern}(f)) + \dim(\text{Bild}(f))}$$

### Injektivität und Surjektivität

$$\begin{array}{c|c|c}
\text{Eigenschaft} & \text{Bedingung (Kern)} & \text{Bedingung (Bild)} \\ \hline
\text{Injektiv} & \text{Kern}(f) = \{0\} & \dim(\text{Kern}(f)) = 0 \\
\text{Surjektiv} & - & \text{Bild}(f) = W \\
\text{Bijektiv (bei } \dim(V) = \dim(W)) & \text{Kern}(f) = \{0\} & \text{Bild}(f) = W
\end{array}$$

**Wichtige Folgerung:** Bei $\dim(V) = \dim(W) < \infty$:
$$\text{injektiv} \iff \text{surjektiv} \iff \text{bijektiv}$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Abbildungen]]: Allgemeine Abbildungen
- [[VL.10 Vektorräume]]: Teilräume (Kern, Bild)
- [[VL.11 Basis und Dimension]]: Dimensionsbegriff
- [[VL.12 Matrizen]]: Matrizen als lineare Abbildungen
- [[VL.13 Lineare Gleichungssysteme]]: Kern als Lösungsmenge von $Ax = 0$
- [[VL.14 Gauss-Algorithmus]]: Zusammenhang Rang-Dimension
- [[VL.16 Koordinaten und Matrixdarstellung]]: Matrizen für allgemeine lineare Abbildungen
