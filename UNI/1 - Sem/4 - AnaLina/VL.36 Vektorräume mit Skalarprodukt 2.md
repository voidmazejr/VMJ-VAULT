**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #OrthogonaleProjektion #GramSchmidt #QRZerlegung #LineareRegression #KleinsteQuadrate

---

## 🎯 Lernziele der Vorlesung

Wichtige Anwendungen von Skalarprodukten: kürzeste Abstände, Orthonormalisierung und lineare Regression.

- **Orthogonale Projektion** und kürzeste Abstände
- **Gram-Schmidt-Verfahren** zur Berechnung von ONB
- **QR-Zerlegung** von Matrizen
- **Lineare Regression** (Methode der kleinsten Quadrate)

---

## 1. Kürzeste Abstände und orthogonale Projektion

### Problem: Abstand eines Punkts zu einer Geraden

**Frage:** Was ist der kürzeste Abstand zwischen einem Punkt $v$ und einer Geraden?

Gesucht: Punkt $v^*$ auf der Geraden, der am nächsten an $v$ liegt.

**Anschaulich:** $v - v^*$ muss **senkrecht** zur Geraden sein!

### Fall: Gerade durch den Ursprung ($k=1$)

Sei $U = \text{span}\{u\}$ mit $\|u\| = 1$ (Richtungsvektor der Ursprungsgeraden).

**Ansatz:** $v^* = \alpha u$ mit $v - v^* \perp u$

Die Bedingung $\langle v - v^*, u \rangle = 0$ ergibt:

$$0 = \langle v, u \rangle - \langle v^*, u \rangle = \langle v, u \rangle - \langle \alpha u, u \rangle = \langle v, u \rangle - \alpha$$

Also: $$\boxed{v^* = \langle v, u \rangle u}$$

**Zerlegung von $v$:**

$$v = \underbrace{v - \langle v, u \rangle u}_{\perp u} + \underbrace{\langle v, u \rangle u}_{v^* \text{ (Projektion)}}$$

### Satz (Kürzester Abstand - eindimensional)

Sei $V$ ein Vektorraum mit Skalarprodukt und $U = \text{span}\{u\}$ mit $\|u\| = 1$. Für $v \in V$ ist:

**Orthogonale Projektion von $v$ auf $U$:**

$$\boxed{v^* = \langle v, u \rangle u}$$

Dann ist $v^*$ der Punkt aus $U$ mit **kleinstem Abstand** zu $v$.

**Abstand von $v$ zu $U$:**

$$\boxed{\|v - \langle v, u \rangle u\| = \sqrt{\|v\|^2 - |\langle v, u \rangle|^2}}$$

### Beweis-Idee

Der Abstand von $v$ zum Punkt $\alpha u \in U$ ist $\|v - \alpha u\|$. Da $v - \langle v, u \rangle u$ und $u$ orthogonal sind, gilt mit Pythagoras:

$$\|v - \alpha u\|^2 = \|v - \langle v, u \rangle u + (\langle v, u \rangle - \alpha)u\|^2$$

$$= \|v - \langle v, u \rangle u\|^2 + \|(\langle v, u \rangle - \alpha)u\|^2$$

$$= \|v - \langle v, u \rangle u\|^2 + |\langle v, u \rangle - \alpha|^2$$

Der zweite Term ist $\geq 0$ und $= 0 \iff \alpha = \langle v, u \rangle$. Also ist $\|v - \alpha u\|^2$ minimal für $\alpha = \langle v, u \rangle$. ✓

### Allgemeiner Fall: Teilraum ($k > 1$)

### Satz (Kürzester Abstand - mehrdimensional)

Sei $V$ ein Vektorraum mit Skalarprodukt und $U = \text{span}\{u_1, \ldots, u_k\}$ mit **Orthonormalbasis** $u_1, \ldots, u_k$ von $U$. Für $v \in V$ ist:

**Orthogonale Projektion von $v$ auf $U$:**

$$\boxed{v^* = \sum_{j=1}^k \langle v, u_j \rangle u_j}$$

Dann ist $v^*$ der Punkt aus $U$ mit **kleinstem Abstand** zu $v$.

**Abstand von $v$ zu $U$:**

$$\boxed{\left\|v - \sum_{j=1}^k \langle v, u_j \rangle u_j\right\| = \sqrt{\|v\|^2 - \|v^*\|^2} = \sqrt{\|v\|^2 - \sum_{j=1}^k |\langle v, u_j \rangle|^2}}$$

**Interpretation:** Die orthogonale Projektion von $v \in V$ auf $U$ sieht fast wie eine "ONB-Entwicklung" von $v$ im Teilraum aus (statt im ganzen Raum).

---

## 2. Das Gram-Schmidt-Verfahren

### Ziel

Aus einer gegebenen **Basis** eine **Orthonormalbasis** berechnen.

### Algorithmus (Gram-Schmidt-Verfahren)

Sei $V$ ein Vektorraum mit Skalarprodukt $\langle \cdot, \cdot \rangle$ und induzierter Norm $\|\cdot\|$. Sei $\mathcal{B} = \{b_1, \ldots, b_n\}$ eine Basis von $V$.

**Schritt 1:** Normiere $b_1$:

$$\boxed{u_1 := \frac{1}{\|b_1\|}b_1}$$

**Schritt 2:** Für $k = 2, \ldots, n$:

**a) Orthogonalisiere $b_k$:** Entferne den Anteil von $b_k$ in die bereits gefundenen Richtungen $u_1, \ldots, u_{k-1}$:

$$\boxed{\tilde{u}_k = b_k - \sum_{j=1}^{k-1} \langle b_k, u_j \rangle u_j}$$

Dann ist $\langle \tilde{u}_k, u_\ell \rangle = 0$ für $\ell = 1, 2, \ldots, k-1$.

**b) Normiere $\tilde{u}_k$:**

$$\boxed{u_k = \frac{1}{\|\tilde{u}_k\|}\tilde{u}_k}$$

**Ergebnis:** $\{u_1, \ldots, u_n\}$ ist eine ONB von $V$ mit:

$$\text{span}\{u_1, \ldots, u_k\} = \text{span}\{b_1, \ldots, b_k\} \quad \text{für } k = 1, 2, \ldots, n$$

### Beispiel: $\mathbb{R}^3$ mit Standardskalarprodukt

Gegeben: Basis $\mathcal{B} = \{b_1, b_2, b_3\}$ mit

$$b_1 = \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, \quad b_2 = \begin{pmatrix} 2 \\ 2 \\ 1 \end{pmatrix}, \quad b_3 = \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix}$$

**Schritt 1:** Normiere $b_1$:

$$\|b_1\| = \sqrt{1 + 1 + 0} = \sqrt{2}$$

$$u_1 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \\ 0 \end{pmatrix}$$

**Schritt 2a:** Orthogonalisiere $b_2$:

$$\langle b_2, u_1 \rangle = \left\langle \begin{pmatrix} 2 \\ 2 \\ 1 \end{pmatrix}, \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \\ 0 \end{pmatrix} \right\rangle = \frac{2}{\sqrt{2}} + \frac{2}{\sqrt{2}} = 2\sqrt{2}$$

$$\tilde{u}_2 = b_2 - \langle b_2, u_1 \rangle u_1 = \begin{pmatrix} 2 \\ 2 \\ 1 \end{pmatrix} - 2\sqrt{2} \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}$$

**Schritt 2b:** Normiere $\tilde{u}_2$:

$$\|\tilde{u}_2\| = 1 \quad \Rightarrow \quad u_2 = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}$$

**Schritt 3a:** Orthogonalisiere $b_3$:

$$\langle b_3, u_1 \rangle = \left\langle \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix}, \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \\ 0 \end{pmatrix} \right\rangle = 0$$

$$\langle b_3, u_2 \rangle = \left\langle \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix}, \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix} \right\rangle = 1$$

$$\tilde{u}_3 = b_3 - \langle b_3, u_1 \rangle u_1 - \langle b_3, u_2 \rangle u_2 = \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix} - 0 - \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 1 \\ -1 \\ 0 \end{pmatrix}$$

**Schritt 3b:** Normiere $\tilde{u}_3$:

$$\|\tilde{u}_3\| = \sqrt{2} \quad \Rightarrow \quad u_3 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \\ 0 \end{pmatrix} = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \\ 0 \end{pmatrix}$$

**Ergebnis:** $\{u_1, u_2, u_3\}$ ist eine ONB von $\mathbb{R}^3$.

---

## 3. QR-Zerlegung

### Satz (QR-Zerlegung)

Sei $A \in \mathbb{R}^{m,n}$ mit $m \geq n$. Dann ist:

$$\boxed{A = QR}$$

mit:
- $Q \in \mathbb{R}^{m,m}$ **orthogonale Matrix**
- $R \in \mathbb{R}^{m,n}$ **obere Dreiecksmatrix**:

$$R = \begin{pmatrix} * & * & \cdots & * \\ 0 & * & \cdots & * \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & * \\ 0 & 0 & \cdots & 0 \\ \vdots & \vdots & & \vdots \\ 0 & 0 & \cdots & 0 \end{pmatrix}$$

**Für komplexe Matrizen:** $A \in \mathbb{C}^{m,n}$ mit $m \geq n$:

$$A = QR$$

mit $Q \in \mathbb{C}^{m,m}$ **unitär** und $R \in \mathbb{C}^{m,n}$ obere Dreiecksmatrix.

### Berechnung der QR-Zerlegung (für invertierbares $A \in K^{n,n}$)

**Schritt 1:** Wende das **Gram-Schmidt-Verfahren** (mit Standardskalarprodukt) auf die **Spalten** $a_1, \ldots, a_n$ von $A$ an, um die ONB $u_1, \ldots, u_n$ zu erhalten.

**Schritt 2:** Setze $Q := [u_1 \ldots u_n]$. Dann ist $Q$ orthogonal (bzw. unitär).

**Probe:** $Q^T Q = I_n$ (bzw. $Q^H Q = I_n$)

**Schritt 3:** Berechnung von $R = [r_{i,j}]$:

**Zwei Möglichkeiten:**

a) Berechne $r_{i,j} = \langle a_j, u_i \rangle$ für $i \leq j$ und $r_{i,j} = 0$ für $i > j$ (wird bei Gram-Schmidt mit berechnet)

b) Berechne $R = Q^T A$ (bzw. $R = Q^H A$)

Dann ist $R$ eine obere Dreiecksmatrix und $A = QR$ eine QR-Zerlegung von $A$.

### Beispiel: QR-Zerlegung

Sei $A = \begin{pmatrix} 1 & 2 & 1 \\ 1 & 2 & -1 \\ 0 & 1 & 1 \end{pmatrix} \in \mathbb{R}^{3,3}$

Die Spalten von $A$ sind genau $b_1, b_2, b_3$ aus dem Gram-Schmidt-Beispiel oben!

Also ist:

$$Q = [u_1 \, u_2 \, u_3] = \begin{pmatrix} \frac{1}{\sqrt{2}} & 0 & \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & 0 & -\frac{1}{\sqrt{2}} \\ 0 & 1 & 0 \end{pmatrix}$$

**Berechnung von $R$:**

**Methode 1:** $R = Q^T A$

$$R = \begin{pmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} & 0 \\ 0 & 0 & 1 \\ \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} & 0 \end{pmatrix} \begin{pmatrix} 1 & 2 & 1 \\ 1 & 2 & -1 \\ 0 & 1 & 1 \end{pmatrix} = \begin{pmatrix} \sqrt{2} & 2\sqrt{2} & 0 \\ 0 & 1 & 1 \\ 0 & 0 & \sqrt{2} \end{pmatrix}$$

**Methode 2:** Aus den berechneten Koeffizienten:

$$R = \begin{pmatrix} \|\tilde{u}_1\| & \langle a_2, u_1 \rangle & \langle a_3, u_1 \rangle \\ 0 & \|\tilde{u}_2\| & \langle a_3, u_2 \rangle \\ 0 & 0 & \|\tilde{u}_3\| \end{pmatrix} = \begin{pmatrix} \sqrt{2} & 2\sqrt{2} & 0 \\ 0 & 1 & 1 \\ 0 & 0 & \sqrt{2} \end{pmatrix}$$

**Probe:** $QQ^T = I_3$ ✓

### Beispiel: Nicht-invertierbare Matrix

Sei $A = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}$

**Gram-Schmidt:** $\|a_1\| = \sqrt{2}$, also $u_1 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$

$$\tilde{u}_2 = a_2 - \langle a_2, u_1 \rangle u_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix} - \frac{2}{\sqrt{2}} \cdot \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Da $\tilde{u}_2 = \vec{0}$, **ergänze** $Q$ zu orthogonaler Matrix:

$$Q = \begin{pmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \end{pmatrix}, \quad R = \begin{pmatrix} \sqrt{2} & \sqrt{2} \\ 0 & 0 \end{pmatrix}$$

Dann ist $A = QR$. ✓

---

## 4. Lineare Regression (Methode der kleinsten Quadrate)

### Problem

**Gegeben:** Messwerte $(t_i, y_i)$, $i = 1, \ldots, m$

**Gesucht:** Gerade $y(t) = a_1 t + a_2$, die diese Punkte "am besten" repräsentiert

Wegen Messfehlern gilt typischerweise $y_i \approx a_1 t_i + a_2$, aber nicht exakt.

### Methode der kleinsten Quadrate

Gesucht sind $a_1, a_2$, so dass:

$$\left\|\begin{pmatrix} t_1 & 1 \\ t_2 & 1 \\ \vdots & \vdots \\ t_m & 1 \end{pmatrix}\begin{pmatrix} a_1 \\ a_2 \end{pmatrix} - \begin{pmatrix} y_1 \\ y_2 \\ \vdots \\ y_m \end{pmatrix}\right\|_2 = \sqrt{\sum_{i=1}^m (a_1 t_i + a_2 - y_i)^2}$$

**möglichst klein** wird.

Setze:

$$A = \begin{pmatrix} t_1 & 1 \\ \vdots & \vdots \\ t_m & 1 \end{pmatrix}, \quad a = \begin{pmatrix} a_1 \\ a_2 \end{pmatrix}, \quad y = \begin{pmatrix} y_1 \\ \vdots \\ y_m \end{pmatrix}$$

Wir wollen $\|Aa - y\|_2$ minimieren.

### Lösung mit QR-Zerlegung

Mit der QR-Zerlegung $A = QR$:

$$\|Aa - y\|_2 = \|QRa - y\|_2 = \|Q(Ra - Q^T y)\|_2 = \|Ra - Q^T y\|_2$$

Da $A$ nur zwei Spalten hat, ist $R$ von der Form:

$$R = \begin{pmatrix} R_e \\ 0 \end{pmatrix} \quad \text{mit} \quad R_e = \begin{pmatrix} r_{1,1} & r_{1,2} \\ 0 & r_{2,2} \end{pmatrix}$$

Teile $b = Q^T y = \begin{pmatrix} b_1 \\ b_2 \end{pmatrix}$ mit $b_1 \in \mathbb{R}^2$, $b_2 \in \mathbb{R}^{m-2}$:

$$\|Aa - y\|_2^2 = \|Ra - b\|_2^2 = \left\|\begin{pmatrix} R_e a - b_1 \\ -b_2 \end{pmatrix}\right\|_2^2 = \|R_e a - b_1\|_2^2 + \|b_2\|_2^2$$

Dies wird **minimal** für $R_e a - b_1 = 0$, also:

$$\boxed{a = R_e^{-1} b_1}$$

Der verbleibende Fehler ist dann $\|Aa - y\|_2 = \|b_2\|_2$.

### Algorithmus

**Gegeben:** Messwerte $(t_i, y_i)$, $i = 1, 2, \ldots, m$

Setze: $A = \begin{pmatrix} t_1 & 1 \\ \vdots & \vdots \\ t_m & 1 \end{pmatrix}$, $y = \begin{pmatrix} y_1 \\ \vdots \\ y_m \end{pmatrix}$

**Schritt 1:** Berechne die QR-Zerlegung $A = QR$

**Schritt 2:** Erhalte $R_e = \begin{pmatrix} r_{1,1} & r_{1,2} \\ 0 & r_{2,2} \end{pmatrix}$ und $b_1 = \begin{pmatrix} q_1^T \\ q_2^T \end{pmatrix} y$

(wobei $q_1^T, q_2^T$ die ersten beiden Zeilen von $Q^T$ sind)

**Schritt 3:** Löse das LGS $R_e \begin{pmatrix} a_1 \\ a_2 \end{pmatrix} = b_1$

**Ergebnis:** $y(t) = a_1 t + a_2$ ist die Gerade mit kleinstem Fehler (in der 2-Norm).

### Beispiel

Datenpunkte:

$$A = \begin{pmatrix} 1 & 1 \\ 2 & 1 \\ 3 & 1 \\ 4 & 1 \\ 5 & 1 \\ 6 & 1 \\ 7 & 1 \end{pmatrix}, \quad y = \begin{pmatrix} 1 \\ 2 \\ 1.8 \\ 1.9 \\ 3 \\ 2.5 \\ 3.2 \end{pmatrix}$$

**Ergebnis:** $a_1 = 0.2714$, $a_2 = 1.0286$ (auf 4 Nachkommastellen)

**Ausgleichsgerade:** $y(t) = 0.2714t + 1.0286$

---

## 📌 Zusammenfassung

### Orthogonale Projektion

**Eindimensional ($U = \text{span}\{u\}$, $\|u\| = 1$):**

$$v^* = \langle v, u \rangle u, \quad \text{Abstand} = \sqrt{\|v\|^2 - |\langle v, u \rangle|^2}$$

**Mehrdimensional ($U = \text{span}\{u_1, \ldots, u_k\}$, ONB):**

$$v^* = \sum_{j=1}^k \langle v, u_j \rangle u_j, \quad \text{Abstand} = \sqrt{\|v\|^2 - \sum_{j=1}^k |\langle v, u_j \rangle|^2}$$

### Gram-Schmidt-Verfahren

**Aus Basis $\{b_1, \ldots, b_n\}$ eine ONB $\{u_1, \ldots, u_n\}$ berechnen:**

1. $u_1 = \frac{b_1}{\|b_1\|}$
2. Für $k = 2, \ldots, n$:
   - Orthogonalisiere: $\tilde{u}_k = b_k - \sum_{j=1}^{k-1} \langle b_k, u_j \rangle u_j$
   - Normiere: $u_k = \frac{\tilde{u}_k}{\|\tilde{u}_k\|}$

**Eigenschaft:** $\text{span}\{u_1, \ldots, u_k\} = \text{span}\{b_1, \ldots, b_k\}$

### QR-Zerlegung

**$A = QR$** mit:
- $Q$ orthogonal (bzw. unitär)
- $R$ obere Dreiecksmatrix

**Berechnung:**
1. Gram-Schmidt auf Spalten von $A$ → ONB $\{u_1, \ldots, u_n\}$
2. $Q = [u_1 \ldots u_n]$
3. $R = Q^T A$ (bzw. $R = Q^H A$)

### Lineare Regression

**Kleinste-Quadrate-Problem:** Minimiere $\|Aa - y\|_2$

**Lösung mit QR:** $A = QR$
1. Berechne $A = QR$
2. Extrahiere $R_e$ (obere $2 \times 2$-Block) und $b_1 = (Q^T y)_{1:2}$
3. Löse $R_e a = b_1$

**Ergebnis:** Ausgleichsgerade $y(t) = a_1 t + a_2$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.11 Basis und Dimension]]: Basis und span
- [[VL.13 Lineare Gleichungssysteme]]: Lösung von LGS in Schritt 3
- [[VL.35 Vektorräume mit Skalarprodukt 1]]: Skalarprodukt, ONB