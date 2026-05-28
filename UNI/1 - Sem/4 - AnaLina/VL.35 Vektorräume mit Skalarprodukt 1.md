**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Norm #Skalarprodukt #Orthogonalität #Orthonormalbasis #OrthogonaleMatrizen

---

## 🎯 Lernziele der Vorlesung

Wir verallgemeinern Längen- und Winkelbegriffe auf allgemeine Vektorräume über $\mathbb{R}$ oder $\mathbb{C}$.

- **Norm** als Verallgemeinerung der Länge
- **Skalarprodukt** und euklidische/unitäre Vektorräume
- **Orthogonale und orthonormale Vektoren**
- **Orthonormalbasen** und ihre Eigenschaften
- **Orthogonale und unitäre Matrizen**

---

## 1. Norm

### Motivation: Länge in $\mathbb{R}^2$

In $\mathbb{R}^2$ ist die "übliche" Länge eines Vektors:

$$\left\|\begin{pmatrix} x_1 \\ x_2 \end{pmatrix}\right\|_2 = \sqrt{x_1^2 + x_2^2}$$

**Eigenschaften der Länge:**

1. ✅ Längen sind immer positiv (nichtnegativ): $\|\vec{x}\|_2 \geq 0$, und $\|\vec{x}\|_2 = 0 \iff \vec{x} = \vec{0}$
2. ✅ Bei Streckung um $\lambda$ wird Länge mit $|\lambda|$ multipliziert: $\|\lambda\vec{x}\|_2 = |\lambda|\|\vec{x}\|_2$
3. ✅ **Dreiecksungleichung:** $\|\vec{x} + \vec{y}\|_2 \leq \|\vec{x}\|_2 + \|\vec{y}\|_2$

### Definition (Norm)

Sei $V$ ein $K$-Vektorraum. Eine **Norm** auf $V$ ist eine Abbildung $\|\cdot\| : V \to \mathbb{R}$ mit:

**1. Positive Definitheit:**

$$\boxed{\|\vec{v}\| \geq 0 \text{ für alle } \vec{v} \in V, \quad \text{und} \quad \|\vec{v}\| = 0 \iff \vec{v} = \vec{0}}$$

**2. Homogenität:**

$$\boxed{\|\lambda\vec{v}\| = |\lambda|\|\vec{v}\| \quad \text{für alle } \vec{v} \in V, \lambda \in K}$$

**3. Dreiecksungleichung:**

$$\boxed{\|\vec{v} + \vec{w}\| \leq \|\vec{v}\| + \|\vec{w}\| \quad \text{für alle } \vec{v}, \vec{w} \in V}$$

### Beispiele von Normen

**Beispiel 1:** Absolutbetrag auf $V = \mathbb{R}$ oder $V = \mathbb{C}$ ist eine Norm.

**Beispiel 2:** Die **2-Norm** (Standardnorm, euklidische Norm) auf $K^n$:

$$\boxed{\|\vec{x}\|_2 = \sqrt{\sum_{j=1}^n |x_j|^2}}$$

In $\mathbb{R}^2$ oder $\mathbb{R}^3$ ist das genau die "übliche Länge" von Vektoren.

**Beispiel 3:** Allgemeine **$p$-Norm** für $1 \leq p < \infty$:

$$\|\vec{x}\|_p = \left(\sum_{j=1}^n |x_j|^p\right)^{\frac{1}{p}}$$

**Beispiel 4:** **Maximumsnorm** ($\infty$-Norm):

$$\boxed{\|\vec{x}\|_\infty = \max_{j=1,\ldots,n} |x_j| = \max\{|x_1|, \ldots, |x_n|\}}$$

Man kann zeigen: $\lim_{p \to \infty} \|\vec{x}\|_p = \|\vec{x}\|_\infty$ für jedes $\vec{x} \in K^n$.

**Beispiel 5:** **Maximumsnorm von Funktionen**:

$$\|f\|_\infty = \max_{x \in [a,b]} |f(x)|$$

---

## 2. Skalarprodukte

### Definition (Skalarprodukt)

Sei $V$ ein Vektorraum über $K$. Eine Abbildung $\langle \cdot, \cdot \rangle : V \times V \to K$ heißt **Skalarprodukt** auf $V$, falls für alle $u, v, w \in V$ und $\lambda \in K$ gilt:

**1. Linearität im ersten Argument:**

$$\langle u + v, w \rangle = \langle u, w \rangle + \langle v, w \rangle$$

$$\langle \lambda v, w \rangle = \lambda \langle v, w \rangle$$

**2. Symmetrie:**

$$\boxed{\langle v, w \rangle = \overline{\langle w, v \rangle}}$$

**3. Positive Definitheit:**

$$\boxed{\langle v, v \rangle \geq 0 \text{ für alle } v, \quad \text{und} \quad \langle v, v \rangle = 0 \iff v = 0}$$

### Terminologie

- Ist $K = \mathbb{R}$: $V$ heißt **euklidischer Vektorraum**
- Ist $K = \mathbb{C}$: $V$ heißt **unitärer Vektorraum**

### Wichtige Bemerkungen zum zweiten Argument

Für das zweite Argument gilt:

$$\langle v, u + w \rangle = \langle u + w, v \rangle = \overline{\langle u, v \rangle + \langle w, v \rangle} = \overline{\langle u, v \rangle} + \overline{\langle w, v \rangle} = \langle v, u \rangle + \langle v, w \rangle$$

$$\langle v, \lambda w \rangle = \langle \lambda w, v \rangle = \overline{\lambda \langle w, v \rangle} = \overline{\lambda} \cdot \overline{\langle w, v \rangle} = \overline{\lambda}\langle v, w \rangle$$

**Folgerungen:**

1. Für $K = \mathbb{R}$ ist $\overline{\lambda} = \lambda$ → Skalarprodukt ist auch **linear im zweiten Argument**
2. Für $K = \mathbb{C}$ ist das Skalarprodukt **nicht linear im zweiten Argument** (Skalare werden komplex konjugiert herausgezogen)

Man sagt: Das Skalarprodukt ist **semilinear** oder **antilinear** im zweiten Argument.

3. In einem **reellen** Vektorraum ist $\langle w, v \rangle \in \mathbb{R}$, also kann man das Konjugieren weglassen: $\langle v, w \rangle = \langle w, v \rangle$

⚠️ **Achtung:** In manchen Büchern (insbesondere Physik) ist das Skalarprodukt linear im zweiten Argument statt im ersten!

### Beispiele von Skalarprodukten

**Beispiel 1:** **Standardskalarprodukt** in $K^n$:

$$\boxed{\langle \vec{x}, \vec{y} \rangle = \sum_{j=1}^n x_j \overline{y_j} = \vec{y}^H \vec{x}}$$

Speziell in $\mathbb{R}^2$: $\langle \vec{x}, \vec{y} \rangle = x_1 y_1 + x_2 y_2$

**Nachweis der Eigenschaften:**

a) Linearität im ersten Argument:

$$\langle \vec{x} + \vec{y}, \vec{z} \rangle = \sum_{j=1}^n (x_j + y_j)\overline{z_j} = \sum_{j=1}^n x_j\overline{z_j} + \sum_{j=1}^n y_j\overline{z_j} = \langle \vec{x}, \vec{z} \rangle + \langle \vec{y}, \vec{z} \rangle$$

$$\langle \lambda\vec{x}, \vec{y} \rangle = \sum_{j=1}^n \lambda x_j \overline{y_j} = \lambda \sum_{j=1}^n x_j\overline{y_j} = \lambda\langle \vec{x}, \vec{y} \rangle$$

b) Symmetrie:

$$\langle \vec{x}, \vec{y} \rangle = \sum_{j=1}^n x_j\overline{y_j} = \overline{\sum_{j=1}^n \overline{x_j}y_j} = \overline{\sum_{j=1}^n y_j\overline{x_j}} = \overline{\langle \vec{y}, \vec{x} \rangle}$$

c) Positive Definitheit:

$$\langle \vec{x}, \vec{x} \rangle = \sum_{j=1}^n x_j\overline{x_j} = \sum_{j=1}^n |x_j|^2 \geq 0$$

Aus $\langle \vec{x}, \vec{x} \rangle = 0$ folgt: alle Summanden $|x_j|^2 \geq 0$ sind auch $= 0$, also $x_j = 0$ für alle $j$, d.h. $\vec{x} = \vec{0}$.

**Beispiel 2:** **Gewichtetes Skalarprodukt** auf $K^n$:

Sind $w_1, \ldots, w_n > 0$, so definiert

$$\langle \vec{x}, \vec{y} \rangle_w = \sum_{j=1}^n w_j x_j \overline{y_j}$$

ein Skalarprodukt. Für alle $w_j = 1$ erhält man das Standardskalarprodukt.

**Beispiel 3:** **$L^2$-Skalarprodukt** auf dem Vektorraum der stetigen Funktionen $V = C([a,b])$:

$$\boxed{\langle f, g \rangle = \int_a^b f(x)\overline{g(x)}\,dx}$$

Linearität und Symmetrie rechnen sich wie beim Standardskalarprodukt nach.

---

## 3. Induzierte Norm

### Satz (Vom Skalarprodukt induzierte Norm)

Ist $V$ ein $K$-Vektorraum mit Skalarprodukt $\langle \cdot, \cdot \rangle$, so ist

$$\boxed{\|\cdot\| : V \to \mathbb{R}, \quad \|\vec{v}\| := \sqrt{\langle \vec{v}, \vec{v} \rangle}}$$

eine Norm auf $V$. Diese heißt **vom Skalarprodukt induzierte Norm** (= zum Skalarprodukt zugehörige Norm).

### Beweis (Skizze)

**1. Positive Definitheit:** Wegen $\langle v, v \rangle \geq 0$ und $= 0 \iff v = 0$ folgt $\|\vec{v}\| = \sqrt{\langle \vec{v}, \vec{v} \rangle} \geq 0$ und $\|\vec{v}\| = 0 \iff \vec{v} = \vec{0}$.

**2. Homogenität:**

$$\|\lambda\vec{v}\| = \sqrt{\langle \lambda\vec{v}, \lambda\vec{v} \rangle} = \sqrt{\lambda\langle \vec{v}, \lambda\vec{v} \rangle} = \sqrt{\lambda\overline{\lambda}\langle \vec{v}, \vec{v} \rangle} = \sqrt{|\lambda|^2}\sqrt{\langle \vec{v}, \vec{v} \rangle} = |\lambda|\|\vec{v}\|$$

**3. Dreiecksungleichung:** Benötigt die **Cauchy-Schwarz-Ungleichung**: $|\langle \vec{v}, \vec{w} \rangle| \leq \|\vec{v}\|\|\vec{w}\|$

Dann:

$$\|\vec{v} + \vec{w}\|^2 = \langle \vec{v} + \vec{w}, \vec{v} + \vec{w} \rangle = \|\vec{v}\|^2 + \langle \vec{v}, \vec{w} \rangle + \overline{\langle \vec{v}, \vec{w} \rangle} + \|\vec{w}\|^2$$

$$= \|\vec{v}\|^2 + 2\text{Re}(\langle \vec{v}, \vec{w} \rangle) + \|\vec{w}\|^2 \leq \|\vec{v}\|^2 + 2|\langle \vec{v}, \vec{w} \rangle| + \|\vec{w}\|^2$$

$$\leq \|\vec{v}\|^2 + 2\|\vec{v}\|\|\vec{w}\| + \|\vec{w}\|^2 = (\|\vec{v}\| + \|\vec{w}\|)^2$$

Durch Wurzelziehen folgt die Dreiecksungleichung.

### Beispiele induzierter Normen

**Beispiel 1:** Die **2-Norm** wird vom Standardskalarprodukt induziert:

$$\|\vec{x}\|_2 = \sqrt{\sum_{j=1}^n |x_j|^2} = \sqrt{\langle \vec{x}, \vec{x} \rangle}$$

**Beispiel 2:** Die **$L^2$-Norm** wird vom $L^2$-Skalarprodukt induziert:

$$\|f\|_{L^2} = \sqrt{\langle f, f \rangle} = \sqrt{\int_a^b f(x)\overline{f(x)}\,dx} = \sqrt{\int_a^b |f(x)|^2\,dx}$$

**Beispiel 3:** **Nicht** von einem Skalarprodukt induziert sind:
- Die $p$-Norm für $p \neq 2$
- Die Maximumsnorm $\|\cdot\|_\infty$

---

## 4. Orthogonale Vektoren

### Motivation aus $\mathbb{R}^2$

Zwei Vektoren im $\mathbb{R}^2$ (mit Standardskalarprodukt) sind **senkrecht zueinander** $\iff$ ihr Skalarprodukt ist Null.

**Beispiel:** $\vec{x} = \begin{pmatrix} 2 \\ -1 \end{pmatrix}$ und $\vec{y} = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$ sind senkrecht:

$$\langle \vec{x}, \vec{y} \rangle = 2 \cdot 1 + (-1) \cdot 2 = 0$$

### Definition (Orthogonale und orthonormale Vektoren)

Sei $V$ ein Vektorraum mit Skalarprodukt $\langle \cdot, \cdot \rangle$. Die Vektoren $v_1, \ldots, v_k \in V$ heißen:

**1. Orthogonal** (= senkrecht), falls:

$$\boxed{\langle v_i, v_j \rangle = 0 \quad \text{für } i \neq j}$$

**2. Orthonormal**, falls:

$$\boxed{\langle v_i, v_j \rangle = \begin{cases} 1, & i = j \\ 0, & i \neq j \end{cases}}$$

d.h. sie sind **orthogonal** und **normiert** (Länge 1): $\|v_i\| = \sqrt{\langle v_i, v_i \rangle} = 1$

**Bemerkung:** Zwei Vektoren $u, v$ sind orthogonal $\iff \langle u, v \rangle = 0$.

### Satz des Pythagoras

Sei $V$ ein Vektorraum mit Skalarprodukt $\langle \cdot, \cdot \rangle$ und induzierter Norm $\|\cdot\|$. Sind $u, v \in V$ orthogonal, so gilt:

$$\boxed{\|u + v\|^2 = \|u\|^2 + \|v\|^2}$$

Allgemeiner: Sind $v_1, \ldots, v_k \in V$ orthogonal, so gilt:

$$\boxed{\|v_1 + \ldots + v_k\|^2 = \|v_1\|^2 + \ldots + \|v_k\|^2}$$

**Beweis:**

$$\|u + v\|^2 = \langle u + v, u + v \rangle = \langle u, u + v \rangle + \langle v, u + v \rangle$$

$$= \langle u, u \rangle + \underbrace{\langle u, v \rangle}_{=0} + \underbrace{\langle v, u \rangle}_{=0} + \langle v, v \rangle = \|u\|^2 + \|v\|^2$$

---

## 5. Orthonormalbasen

### Motivation: Kartesische Koordinatensysteme

Kartesische Koordinatensysteme sind besonders einfach, weil die Basisvektoren orthonormal sind.

In einer ONB lassen sich Vektoren einfacher als Linearkombination schreiben als in einer beliebigen Basis.

### Definition (Orthonormalbasis)

Sei $V$ ein Vektorraum mit Skalarprodukt $\langle \cdot, \cdot \rangle$. Eine Basis $\{u_1, u_2, \ldots, u_n\}$ von $V$ heißt **Orthonormalbasis** (kurz: **ONB**), falls die Vektoren orthonormal sind.

### Satz (Eigenschaften von ONB)

**1. Orthonormale Vektoren sind linear unabhängig.**

**2.** Sind $u_1, \ldots, u_n$ orthonormal und ist $n = \dim(V)$, so ist $\{u_1, \ldots, u_n\}$ eine ONB von $V$.

**Beweis von (1):** Seien $u_1, \ldots, u_n$ orthonormal und $\lambda_1, \ldots, \lambda_n \in K$ mit $0 = \sum_{j=1}^n \lambda_j u_j$.

Dann für jedes $k$:

$$0 = \langle 0, u_k \rangle = \left\langle \sum_{j=1}^n \lambda_j u_j, u_k \right\rangle = \sum_{j=1}^n \lambda_j \underbrace{\langle u_j, u_k \rangle}_{= 0 \text{ für } j \neq k} = \lambda_k \underbrace{\langle u_k, u_k \rangle}_{=1} = \lambda_k$$

Also $\lambda_1 = \ldots = \lambda_n = 0$ → linear unabhängig. ✓

### Satz (Koordinaten in ONB)

Sei $V$ ein Vektorraum mit Skalarprodukt $\langle \cdot, \cdot \rangle$ und einer Orthonormalbasis $\mathcal{B} = \{u_1, \ldots, u_n\}$. Dann gilt für jeden Vektor $v \in V$:

$$\boxed{v = \sum_{j=1}^n \langle v, u_j \rangle u_j}$$

**Interpretation:** Die **Koordinaten** von $v$ in der ONB $\mathcal{B}$ sind einfach die Skalarprodukte $\langle v, u_j \rangle$!

**Beweis:** Da $\mathcal{B}$ eine Basis ist, lässt sich $v$ darstellen als $v = \sum_{j=1}^n \alpha_j u_j$. Dann:

$$\langle v, u_k \rangle = \left\langle \sum_{j=1}^n \alpha_j u_j, u_k \right\rangle = \sum_{j=1}^n \alpha_j \underbrace{\langle u_j, u_k \rangle}_{= 0 \text{ für } j \neq k} = \alpha_k \underbrace{\langle u_k, u_k \rangle}_{=1} = \alpha_k$$

### Beispiele von ONB

**Beispiel 1:** Die **Standardbasis** im $K^2$ ist eine ONB bzgl. des Standardskalarprodukts:

$$\left\langle \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 0 \end{pmatrix} \right\rangle = 1, \quad \left\langle \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \end{pmatrix} \right\rangle = 0$$

$$\left\langle \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \begin{pmatrix} 1 \\ 0 \end{pmatrix} \right\rangle = 0, \quad \left\langle \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \end{pmatrix} \right\rangle = 1$$

**Beispiel 2:** Allgemein ist die **Standardbasis** im $K^n$ eine ONB bzgl. des Standardskalarprodukts.

**Beispiel 3:** In $V = \mathbb{R}^2$ mit Standardskalarprodukt sind:

$$\vec{u}_1 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}, \quad \vec{u}_2 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix}$$

orthonormal:

$$\langle \vec{u}_1, \vec{u}_1 \rangle = \frac{1}{2}(1 + 1) = 1$$

$$\langle \vec{u}_2, \vec{u}_2 \rangle = \frac{1}{2}(1 + 1) = 1$$

$$\langle \vec{u}_1, \vec{u}_2 \rangle = \langle \vec{u}_2, \vec{u}_1 \rangle = \frac{1}{2}(1 - 1) = 0$$

Daher ist $\{\vec{u}_1, \vec{u}_2\}$ eine ONB von $\mathbb{R}^2$.

---

## 6. Orthogonale Matrizen

### Definition (Orthogonale Matrix)

Eine Matrix $Q \in \mathbb{R}^{n,n}$ heißt **orthogonal**, falls:

$$\boxed{Q^T Q = I_n}$$

### Charakterisierung

Schreibe $Q = [q_1 \ldots q_n]$ mit Spalten $q_1, \ldots, q_n \in \mathbb{R}^n$. Dann:

$$Q^T Q = \begin{pmatrix} q_1^T \\ \vdots \\ q_n^T \end{pmatrix}[q_1 \ldots q_n] = \begin{pmatrix} q_1^T q_1 & \cdots & q_1^T q_n \\ \vdots & \ddots & \vdots \\ q_n^T q_1 & \cdots & q_n^T q_n \end{pmatrix}$$

Also:

$$\boxed{Q^T Q = I_n \iff q_i^T q_j = \begin{cases} 1, & i = j \\ 0, & i \neq j \end{cases}}$$

**Folgerung:** $Q$ ist orthogonal $\iff$ die **Spalten von $Q$** bilden eine **ONB** von $\mathbb{R}^n$ (bzgl. Standardskalarprodukt).

### Beispiele orthogonaler Matrizen

**Beispiel 1:** Die **Einheitsmatrix** ist orthogonal: $I_n^T I_n = I_n I_n = I_n$

**Beispiel 2:** **Drehmatrix** in $\mathbb{R}^2$:

$$Q = \begin{pmatrix} \cos(\alpha) & -\sin(\alpha) \\ \sin(\alpha) & \cos(\alpha) \end{pmatrix}$$

ist orthogonal:

$$Q^T Q = \begin{pmatrix} \cos(\alpha) & \sin(\alpha) \\ -\sin(\alpha) & \cos(\alpha) \end{pmatrix}\begin{pmatrix} \cos(\alpha) & -\sin(\alpha) \\ \sin(\alpha) & \cos(\alpha) \end{pmatrix}$$

$$= \begin{pmatrix} \cos^2(\alpha) + \sin^2(\alpha) & 0 \\ 0 & \sin^2(\alpha) + \cos^2(\alpha) \end{pmatrix} = I_2$$

**Geometrische Bedeutung:** Multiplikation mit $Q$ führt eine **Drehung um Winkel $\alpha$** aus (entgegen dem Uhrzeigersinn).

**Beispiel 3:**

$$Q = \begin{pmatrix} \frac{\sqrt{2}}{2} & -\frac{\sqrt{2}}{2} \\ \frac{\sqrt{2}}{2} & \frac{\sqrt{2}}{2} \end{pmatrix}$$

ist orthogonal (Drehung um $45°$).

### Satz (Eigenschaften orthogonaler Matrizen)

Sei $Q \in \mathbb{R}^{n,n}$ orthogonal. Dann gilt:

**1.** $\det(Q) = \pm 1$

**2.** $Q$ ist invertierbar und $Q^{-1} = Q^T$. Insbesondere gilt auch $QQ^T = I_n$

**3.** Für alle $\vec{x}, \vec{y} \in \mathbb{R}^n$ gilt: $\langle Q\vec{x}, Q\vec{y} \rangle = \langle \vec{x}, \vec{y} \rangle$ (Standardskalarprodukt)

**4.** Für alle $\vec{x} \in \mathbb{R}^n$ gilt: $\|Q\vec{x}\|_2 = \|\vec{x}\|_2$

**Interpretation:** Multiplikation mit orthogonaler Matrix erhält **Winkel** und **euklidische Länge**.

**Beweis-Skizzen:**

**1.** Übungsaufgabe.

**2.** Da $\det(Q) \neq 0$ ist $Q$ invertierbar. Da $Q^T Q = I_n$ ist $Q^T = Q^{-1}$.

**3.**

$$\langle Q\vec{x}, Q\vec{y} \rangle = (Q\vec{y})^T Q\vec{x} = \vec{y}^T \underbrace{Q^T Q}_{=I_n} \vec{x} = \vec{y}^T \vec{x} = \langle \vec{x}, \vec{y} \rangle$$

**4.**

$$\|Q\vec{x}\|_2 = \sqrt{\langle Q\vec{x}, Q\vec{x} \rangle} = \sqrt{\langle \vec{x}, \vec{x} \rangle} = \|\vec{x}\|_2$$

### Anwendung: Householder-Matrix (Spiegelung)

Sei $\vec{u} \in \mathbb{R}^n$, $\vec{u} \neq \vec{0}$. Die **Householder-Matrix**

$$\boxed{H(\vec{u}) = I_n - 2\frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}}}$$

beschreibt die **Spiegelung** an der zu $\vec{u}$ orthogonalen Hyperebene $U = \{\vec{v} \in \mathbb{R}^n \mid \langle \vec{v}, \vec{u} \rangle = 0\}$.

Für $\vec{u} \in \mathbb{R}^2$ ist dies die Spiegelung an der Ursprungsgeraden senkrecht zu $\vec{u}$.

---

## 7. Unitäre Matrizen

### Definition (Unitäre Matrix)

Eine Matrix $U \in \mathbb{C}^{n,n}$ heißt **unitär**, falls:

$$\boxed{U^H U = I_n}$$

(wobei $U^H = \overline{U^T}$ die **hermitesche Transponierte** ist)

**Charakterisierung:** $U$ ist unitär $\iff$ die Spalten von $U$ bilden eine ONB von $\mathbb{C}^n$ (bzgl. Standardskalarprodukt).

### Satz (Eigenschaften unitärer Matrizen)

Sei $U \in \mathbb{C}^{n,n}$ unitär. Dann gilt:

**1.** $|\det(U)| = 1$, d.h. $\det(U) = e^{i\varphi}$ für $\varphi \in \mathbb{R}$

**2.** $U$ ist invertierbar und $U^{-1} = U^H$. Insbesondere gilt auch $UU^H = I_n$

**3.** Für alle $\vec{x}, \vec{y} \in \mathbb{C}^n$ gilt: $\langle U\vec{x}, U\vec{y} \rangle = \langle \vec{x}, \vec{y} \rangle$ (Standardskalarprodukt)

**4.** Für alle $\vec{x} \in \mathbb{C}^n$ gilt: $\|U\vec{x}\|_2 = \|\vec{x}\|_2$

**5.** Die **Eigenwerte von $U$ liegen auf dem Einheitskreis**: $|\lambda| = 1$

**Beweis von (5):** Da $U \in \mathbb{C}^{n,n}$ eine komplexe Matrix ist, hat $U$ Eigenwerte, etwa $U\vec{x} = \lambda\vec{x}$ mit $\lambda \in \mathbb{C}$ und $\vec{x} \in \mathbb{C}^n$, $\vec{x} \neq \vec{0}$.

Mit (4):

$\|\vec{x}\|_2 = \|U\vec{x}\|_2 = \|\lambda\vec{x}\|_2 = |\lambda|\|\vec{x}\|_2$

Da $\vec{x} \neq \vec{0}$ ist auch $\|\vec{x}\|_2 \neq 0$, also folgt $|\lambda| = 1$. ✓

### Beispiel unitärer Matrix

$U = \frac{1}{2}\begin{pmatrix} 1+i & 1-i \\ 1-i & 1+i \end{pmatrix}$

ist unitär:

$U^H U = \frac{1}{2}\begin{pmatrix} 1-i & 1+i \\ 1+i & 1-i \end{pmatrix} \cdot \frac{1}{2}\begin{pmatrix} 1+i & 1-i \\ 1-i & 1+i \end{pmatrix}$

$= \frac{1}{4}\begin{pmatrix} 2(1-i)(1+i) & (1-i)^2 + (1+i)^2 \\ (1+i)^2 + (1-i)^2 & 2(1+i)(1-i) \end{pmatrix}$

$= \frac{1}{4}\begin{pmatrix} 2(1-i^2) & 1-2i+i^2 + 1+2i+i^2 \\ 1+2i+i^2 + 1-2i+i^2 & 2(1-i^2) \end{pmatrix}$

$= \frac{1}{4}\begin{pmatrix} 2 \cdot 2 & 0 \\ 0 & 2 \cdot 2 \end{pmatrix} = I_2$

---

## 📌 Zusammenfassung

### Definitionen

| Begriff | Definition | K-Werte |
|---------|------------|---------|
| **Norm** | $\\\|\\cdot\\\| : V \to \mathbb{R}$ mit pos. Definitheit, Homogenität, Dreiecksungl. | $\mathbb{R}, \mathbb{C}$ |
| **Skalarprodukt** | $\langle \cdot, \cdot \rangle : V \times V \to K$ mit Linearität, Symmetrie, pos. Definitheit | $\mathbb{R}, \mathbb{C}$ |
| **Euklidischer VR** | VR mit Skalarprodukt über $\mathbb{R}$ | $\mathbb{R}$ |
| **Unitärer VR** | VR mit Skalarprodukt über $\mathbb{C}$ | $\mathbb{C}$ |

### Wichtige Normen

**2-Norm (Standardnorm):** $\\\|\vec{x}\\\|_2 = \sqrt{\sum_{j=1}^n |x_j|^2}$

**p-Norm:** $\\\|\vec{x}\\\|_p = \left(\sum_{j=1}^n |x_j|^p\right)^{1/p}$

**Maximumsnorm:** $\\\|\vec{x}\\\|_\infty = \max_{j=1,\ldots,n} |x_j|$

### Standardskalarprodukt

$\langle \vec{x}, \vec{y} \rangle = \sum_{j=1}^n x_j \overline{y_j} = \vec{y}^H \vec{x}$

**Eigenschaften im zweiten Argument:**

- $K = \mathbb{R}$: linear
- $K = \mathbb{C}$: semilinear (antilinear)

### Induzierte Norm

Jedes Skalarprodukt induziert eine Norm:

$\\\|\vec{v}\\\| = \sqrt{\langle \vec{v}, \vec{v} \rangle}$

Die 2-Norm wird vom Standardskalarprodukt induziert.

### Orthogonalität

**Orthogonal:** $\langle v_i, v_j \rangle = 0$ für $i \neq j$

**Orthonormal:** $\langle v_i, v_j \rangle = \delta_{ij} = \begin{cases} 1, & i=j \\\\ 0, & i \neq j \end{cases}$

**Satz des Pythagoras:** Sind $v_1, \ldots, v_k$ orthogonal, so:

$\\\|v_1 + \ldots + v_k\\\|^2 = \\\|v_1\\\|^2 + \ldots + \\\|v_k\\\|^2$

### Orthonormalbasen (ONB)

✅ Orthonormale Vektoren sind linear unabhängig

✅ Koordinaten in ONB: $v = \sum_{j=1}^n \langle v, u_j \rangle u_j$

### Orthogonale/Unitäre Matrizen

| Eigenschaft         | Orthogonal ($Q \in \mathbb{R}^{n,n}$)                                   | Unitär ($U \in \mathbb{C}^{n,n}$)                                       |
| ------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Definition**      | $Q^T Q = I_n$                                                           | $U^H U = I_n$                                                           |
| **Spalten**         | ONB von $\mathbb{R}^n$                                                  | ONB von $\mathbb{C}^n$                                                  |
| **Inverse**         | $Q^{-1} = Q^T$                                                          | $U^{-1} = U^H$                                                          |
| **Determinante**    | $\det(Q) = \pm 1$                                                       | $\det(U)= 1$                                                            |
| **Längenerhaltung** | $\\\|Q\vec{x}\\\|_2 = \\\|\vec{x}\\\|_2$                                | $\\\|U\vec{x}\\\|_2 = \\\|\vec{x}\\\|_2$                                |
| **Skalarprodukt**   | $\langle Q\vec{x}, Q\vec{y} \rangle = \langle \vec{x}, \vec{y} \rangle$ | $\langle U\vec{x}, U\vec{y} \rangle = \langle \vec{x}, \vec{y} \rangle$ |
| **Eigenwerte**      | —                                                                       | $\|\lambda\|= 1$                                                        |

**Wichtig:** Orthogonale/unitäre Matrizen erhalten Winkel und Längen!

### Geometrische Anwendungen

**Drehmatrix (2D):** $Q = \begin{pmatrix} \cos(\alpha) & -\sin(\alpha) \\\\ \sin(\alpha) & \cos(\alpha) \end{pmatrix}$ (Drehung um $\alpha$)

**Householder-Matrix:** $H(\vec{u}) = I - 2\frac{\vec{u}\vec{u}^T}{\vec{u}^T\vec{u}}$ (Spiegelung an Hyperebene $\perp \vec{u}$)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.10 Vektorräume]]: Grundlagen von Vektorräumen
- [[VL.11 Basis und Dimension]]: Basiswechsel
- [[VL.33 Eigenwerte]]: Eigenwerte unitärer Matrizen
- [[VL.36 Vektorräume mit Skalarprodukt 2]]: Gram-Schmidt, symmetrische Matrizen (nächste VL)