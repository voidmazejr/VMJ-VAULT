**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Vektorräume #Teilräume #Linearkombination #Span #Erzeugendensystem

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt die fundamentale Struktur der linearen Algebra ein: Vektorräume. Sie bilden die Grundlage für das Verständnis von Linearität, Dimensionen und linearen Gleichungssystemen.

- **Definition** von Vektorräumen und ihren Axiomen
- **Teilräume** (Untervektorräume) und das Teilraumkriterium
- **Linearkombinationen** von Vektoren
- **Span** (lineare Hülle) und seine Eigenschaften
- **Erzeugendensysteme** von Vektorräumen

---

## 1. Vektorräume

### Definition

Ein **$K$-Vektorraum** ist eine Menge $V$ mit einer Addition $+$ und einer skalaren Multiplikation $\cdot$, so dass

$$v + w \in V \quad \text{und} \quad \lambda \cdot v \in V$$

für alle $v, w \in V$ und $\lambda \in K$ (wobei $K = \mathbb{R}$ oder $K = \mathbb{C}$) gilt und folgende **Rechenregeln** für alle $v, w, x \in V$ und $\lambda, \mu \in K$ gelten:

1. **Assoziativität der Addition:** $(v + w) + x = v + (w + x)$

2. **Kommutativität der Addition:** $v + w = w + v$

3. **Nullvektor:** Es gibt einen Nullvektor $0 \in V$ mit $0 + v = v$

4. **Inverses Element:** Zu jedem Vektor $v \in V$ gibt es $-v \in V$ mit $v + (-v) = 0$

5. **Assoziativität der Skalarmultiplikation:** $(\lambda\mu) \cdot v = \lambda \cdot (\mu \cdot v)$

6. **Distributivgesetz I:** $\lambda \cdot (v + w) = \lambda \cdot v + \lambda \cdot w$

7. **Distributivgesetz II:** $(\lambda + \mu) \cdot v = \lambda \cdot v + \mu \cdot v$

8. **Neutrales Element:** $1 \cdot v = v$

Ein **Vektor** ist ein Element eines Vektorraums.

### Wichtige Bemerkungen

- Die Elemente von $K$ heißen **Skalare**. $K$ steht für einen **Körper** (engl. field)
- Jeder $K$-Vektorraum enthält den Nullvektor und ist somit nicht leer: $V \neq \emptyset$
- Das $K$ bei "$K$-Vektorraum" gibt an, aus welchem Zahlbereich die Skalare kommen
- **Kurzschreibweise:** $\lambda v$ statt $\lambda \cdot v$

### Geometrische Anschauung im $\mathbb{R}^2$

Die Vektorraumoperationen lassen sich geometrisch visualisieren:
- **Addition:** Parallelogrammregel
- **Skalarmultiplikation:** Streckung/Stauchung und ggf. Richtungsumkehr
- **Nullvektor:** Ursprung
- **Inverses:** Spiegelung am Ursprung ($-v = (-1) \cdot v$)

### Beispiele für Vektorräume

**Beispiel 1: Die Ebene $\mathbb{R}^2$**

$$\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} + \begin{bmatrix} y_1 \\ y_2 \end{bmatrix} = \begin{bmatrix} x_1 + y_1 \\ x_2 + y_2 \end{bmatrix}, \quad \lambda \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} \lambda x_1 \\ \lambda x_2 \end{bmatrix}$$

ist ein $\mathbb{R}$-Vektorraum.

**Beispiel 2: Der $K^n$**

Für $n \in \mathbb{N}$, $n \geq 1$ ist die Menge

$$K^n = \left\{ \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix} \, \Bigg| \, x_1, \ldots, x_n \in K \right\}$$

ein $K$-Vektorraum mit **eintragsweiser Addition und Skalarmultiplikation**:

$$\begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix} + \begin{bmatrix} y_1 \\ \vdots \\ y_n \end{bmatrix} := \begin{bmatrix} x_1 + y_1 \\ \vdots \\ x_n + y_n \end{bmatrix}, \quad \lambda \cdot \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} \lambda x_1 \\ \vdots \\ \lambda x_n \end{bmatrix}$$

Der Nullvektor ist $\vec{0} = \begin{bmatrix} 0 \\ \vdots \\ 0 \end{bmatrix}$.

**Beispiel 3: Vektorraum der Polynome**

Die Menge der Polynome

$$\mathbb{C}[z] = \{p(z) = a_0 + a_1 z + \ldots + a_n z^n \mid n \in \mathbb{N}, \, a_0, a_1, \ldots, a_n \in \mathbb{C}\}$$

mit üblicher Addition und Skalarmultiplikation bildet einen $\mathbb{C}$-Vektorraum.

Ebenso ist $\mathbb{R}[z]$ (Polynome mit reellen Koeffizienten) ein $\mathbb{R}$-Vektorraum.

Der Nullvektor ist das Nullpolynom $p_0(z) = 0$.

**Beispiel 4: Funktionenraum**

Ist $D$ eine Menge, so ist die Menge der Funktionen $f : D \to \mathbb{R}$ mit **punktweiser Addition und Skalarmultiplikation**

$$(f + g)(x) := f(x) + g(x), \quad (\lambda f)(x) := \lambda \cdot f(x)$$

ein $\mathbb{R}$-Vektorraum.

Der Nullvektor ist die **Nullfunktion** $f_0 : D \to \mathbb{R}$, $f_0(x) = 0$.

Allgemeiner: Funktionen $f : D \to V$ (wobei $V$ ein beliebiger $K$-Vektorraum ist) bilden einen $K$-Vektorraum.

---

## 2. Teilräume (Untervektorräume)

### Definition

Sei $V$ ein $K$-Vektorraum. Eine Teilmenge $T \subseteq V$ ist ein **Teilraum** (oder **Unterraum** oder **Untervektorraum**) von $V$, falls $T$ selbst ein $K$-Vektorraum ist (mit dem gleichen $+$ und $\cdot$ wie $V$).

### Teilraumkriterium

**Satz:** Sei $V$ ein $K$-Vektorraum. Dann ist $T \subseteq V$ ein Teilraum von $V$ genau dann, wenn:

1. $0 \in T$ (Nullvektor ist enthalten)

2. Für alle $v, w \in T$ ist $v + w \in T$ (abgeschlossen unter Addition)

3. Für alle $v \in T$ und $\lambda \in K$ ist $\lambda v \in T$ (abgeschlossen unter Skalarmultiplikation)

**Intuition:** Eine Teilmenge ist ein Teilraum, wenn wir bei $+$ und $\cdot$ in der Teilmenge bleiben.

### Beispiele für Teilräume

**Beispiel 1: Triviale Teilräume**

Für jeden $K$-Vektorraum $V$ sind $\{0\}$ und $V$ selbst Teilräume von $V$.

**Beispiel 2: Gerade im $\mathbb{R}^2$**

Sei $V = \mathbb{R}^2$. Die Gerade

$$G = \left\{ t \begin{bmatrix} 1 \\ 2 \end{bmatrix} \, \Big| \, t \in \mathbb{R} \right\}$$

ist ein Teilraum von $\mathbb{R}^2$, denn:

- $0 \begin{bmatrix} 1 \\ 2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \in G$

- Sind $\vec{v}, \vec{w} \in G$ mit $\vec{v} = s \begin{bmatrix} 1 \\ 2 \end{bmatrix}$ und $\vec{w} = t \begin{bmatrix} 1 \\ 2 \end{bmatrix}$, dann $\vec{v} + \vec{w} = (s+t) \begin{bmatrix} 1 \\ 2 \end{bmatrix} \in G$

- Ist $\vec{v} = t \begin{bmatrix} 1 \\ 2 \end{bmatrix} \in G$ und $\lambda \in \mathbb{R}$, dann $\lambda\vec{v} = (\lambda t) \begin{bmatrix} 1 \\ 2 \end{bmatrix} \in G$

**Allgemein:** Jede Gerade durch $\vec{0}$ ist ein Teilraum von $\mathbb{R}^2$.

**Beispiel 3: Kein Teilraum**

Der Einheitskreis $K = \{\vec{v} \in \mathbb{R}^2 \mid |\vec{v}| = 1\}$ ist **kein Teilraum**, da $\vec{0} \notin K$.

**Beispiel 4: Geraden und Ebenen im $\mathbb{R}^3$**

In $V = \mathbb{R}^3$ sind Geraden und Ebenen durch $\vec{0}$ Teilräume von $\mathbb{R}^3$.

**Beispiel 5: Polynome beschränkten Grades**

Sei $V = \mathbb{C}[z]$ der $\mathbb{C}$-Vektorraum der Polynome. Die Menge

$$\mathbb{C}[z]_{\leq 2} := \{p \in \mathbb{C}[z] \mid \deg(p) \leq 2\}$$

der Polynome vom Grad höchstens 2 ist ein Teilraum von $V$, denn:

- Das Nullpolynom liegt in $\mathbb{C}[z]_{\leq 2}$ (da $\deg(0) = -\infty \leq 2$)
- Sind $p, q \in \mathbb{C}[z]_{\leq 2}$, so ist $\deg(p + q) \leq 2$
- Ist $p \in \mathbb{C}[z]_{\leq 2}$ und $\lambda \in \mathbb{C}$, so ist $\deg(\lambda \cdot p) \leq 2$

**Allgemein:** Für jedes $n \in \mathbb{N}$ ist

$$\mathbb{C}[z]_{\leq n} = \{p \in \mathbb{C}[z] \mid \deg(p) \leq n\}$$

ein Teilraum von $\mathbb{C}[z]$. Ebenso für reelle Polynome: $\mathbb{R}[z]_{\leq n}$ ist ein Teilraum von $\mathbb{R}[z]$.

---

## 3. Linearkombinationen

### Definition

Sei $V$ ein $K$-Vektorraum. Ein Vektor $v \in V$ heißt **Linearkombination** der Vektoren $v_1, \ldots, v_k \in V$, wenn Zahlen $\lambda_1, \ldots, \lambda_k \in K$ existieren, so dass

$$v = \lambda_1 v_1 + \lambda_2 v_2 + \ldots + \lambda_k v_k = \sum_{j=1}^{k} \lambda_j v_j$$

Man sagt: "$v$ lässt sich aus $v_1, \ldots, v_k$ **linear kombinieren**".

Die $\lambda_1, \ldots, \lambda_k$ heißen **Koeffizienten der Linearkombination**.

### Geometrische Interpretation

Eine Linearkombination von zwei Vektoren $v_1, v_2$ erzeugt alle Vektoren, die durch Skalierung und Addition von $v_1$ und $v_2$ erreichbar sind.

### Beispiele

**Beispiel 1: Linearkombination im $\mathbb{R}^2$**

$$\begin{bmatrix} 2 \\ 1 \end{bmatrix} = 2 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + 1 \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

Also ist $\vec{v} = \begin{bmatrix} 2 \\ 1 \end{bmatrix}$ eine Linearkombination von $\vec{v}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ und $\vec{v}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$.

Auch: $\begin{bmatrix} 2 \\ 1 \end{bmatrix} = 1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + 1 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$

**Beispiel 2: Polynome**

Ein Polynom $p(z) = a_0 + a_1 z + \ldots + a_n z^n$ ist eine Linearkombination der Monome $1, z, \ldots, z^n$.

**Beispiel 3: Trigonometrische Funktionen**

$$\sin\left(x + \frac{\pi}{3}\right) = \sin(x) \cos\left(\frac{\pi}{3}\right) + \cos(x) \sin\left(\frac{\pi}{3}\right) = \frac{1}{2} \sin(x) + \frac{\sqrt{3}}{2} \cos(x)$$

Die Funktion $x \mapsto \sin(x + \frac{\pi}{3})$ ist eine Linearkombination von $\sin$ und $\cos$.

---

## 4. Span (Lineare Hülle)

### Definition

Sei $V$ ein $K$-Vektorraum. Die Menge aller Linearkombinationen von $v_1, \ldots, v_k \in V$ heißt der **Span** (oder die **lineare Hülle** oder das **Erzeugnis**) von $v_1, \ldots, v_k$:

$$\text{span}\{v_1, \ldots, v_k\} := \{\lambda_1 v_1 + \ldots + \lambda_k v_k \mid \lambda_1, \ldots, \lambda_k \in K\}$$

### Wichtiger Satz

**Satz:** Sei $V$ ein $K$-Vektorraum und $v_1, \ldots, v_k \in V$. Dann ist $\text{span}\{v_1, \ldots, v_k\}$ ein Teilraum von $V$.

**Beweis mit Teilraumkriterium:**

1. Mit $\lambda_1 = \ldots = \lambda_k = 0$ ist $0_V = 0v_1 + \ldots + 0v_k \in \text{span}\{v_1, \ldots, v_k\}$

2. Sind $v = \lambda_1 v_1 + \ldots + \lambda_k v_k$ und $w = \mu_1 v_1 + \ldots + \mu_k v_k$, dann
   $$v + w = (\lambda_1 + \mu_1)v_1 + \ldots + (\lambda_k + \mu_k)v_k \in \text{span}\{v_1, \ldots, v_k\}$$

3. Ist $v = \lambda_1 v_1 + \ldots + \lambda_k v_k$ und $\lambda \in K$, dann
   $$\lambda v = (\lambda\lambda_1)v_1 + \ldots + (\lambda\lambda_k)v_k \in \text{span}\{v_1, \ldots, v_k\}$$

### Beispiele

**Beispiel 1: Gerade im $\mathbb{R}^2$**

Sei $V = \mathbb{R}^2$ und $\vec{v}_1 = \begin{bmatrix} 1 \\ 2 \end{bmatrix}$. Dann ist

$$\text{span}\{\vec{v}_1\} = \{\lambda_1 \vec{v}_1 \mid \lambda_1 \in \mathbb{R}\}$$

die Gerade durch $\vec{0}$ mit Richtungsvektor $\vec{v}_1$.

**Beispiel 2: Ebene im $\mathbb{R}^3$**

Sei $V = \mathbb{R}^3$, $\vec{v}_1 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$ und $\vec{v}_2 = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}$. Dann ist

$$\text{span}\{\vec{v}_1, \vec{v}_2\} = \left\{ \begin{bmatrix} \lambda_1 \\ \lambda_2 \\ 0 \end{bmatrix} \, \Bigg| \, \lambda_1, \lambda_2 \in \mathbb{R} \right\}$$

die $x$-$y$-Ebene im $\mathbb{R}^3$.

---

## 5. Erzeugendensysteme

### Definition

Sei $V$ ein $K$-Vektorraum und $T$ ein Teilraum von $V$. Eine Menge $\{v_1, \ldots, v_k\} \subseteq T$ heißt **Erzeugendensystem (EZS)** von $T$, falls ihr Span gleich $T$ ist:

$$\text{span}\{v_1, \ldots, v_k\} = T$$

### Beispiele

**Beispiel 1: Gerade im $\mathbb{R}^2$**

Sei $G = \left\{t \begin{bmatrix} 1 \\ 2 \end{bmatrix} \mid t \in \mathbb{R}\right\}$. Dann ist $G = \text{span}\left\{\begin{bmatrix} 1 \\ 2 \end{bmatrix}\right\}$.

Weitere Erzeugendensysteme von $G$ sind:
- $\left\{\begin{bmatrix} 2 \\ 4 \end{bmatrix}\right\}$
- $\left\{\begin{bmatrix} 1 \\ 2 \end{bmatrix}, \begin{bmatrix} 0 \\ 0 \end{bmatrix}\right\}$
- $\left\{\begin{bmatrix} 2 \\ 4 \end{bmatrix}, \begin{bmatrix} -3 \\ -6 \end{bmatrix}\right\}$

**Beispiel 2: Standardbasis des $\mathbb{R}^2$**

Sei $T = V = \mathbb{R}^2$. Dann ist $\left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}\right\}$ ein Erzeugendensystem von $T$, denn:

$$\vec{x} = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = x_1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2 \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

**Beispiel 3: Standardbasis des $K^n$**

$$\left\{ \begin{bmatrix} 1 \\ 0 \\ 0 \\ \vdots \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \\ 0 \\ \vdots \\ 0 \end{bmatrix}, \ldots, \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix} \right\}$$

ist ein Erzeugendensystem von $K^n$.

**Beispiel 4: Polynome vom Grad höchstens 2**

Sei $T = \mathbb{C}[z]_{\leq 2}$ der Teilraum der Polynome vom Grad höchstens 2. Für $p(z) \in T$ gilt:

$$p(z) = a_0 + a_1 z + a_2 z^2 = a_0 \cdot 1 + a_1 \cdot z + a_2 \cdot z^2$$

Also ist $\{1, z, z^2\}$ ein Erzeugendensystem von $T$.

Hingegen ist $\{1, z\}$ **kein** Erzeugendensystem von $T$, da z.B. $1 + z^2 \in T$ keine Linearkombination von $1$ und $z$ ist.

**Allgemein:**

$$\mathbb{C}[z]_{\leq n} = \text{span}\{1, z, \ldots, z^n\}$$

d.h., $\{1, z, \ldots, z^n\}$ bilden ein Erzeugendensystem der Polynome vom Grad höchstens $n$.

**Wichtig:** $\mathbb{C}[z]$ (und $\mathbb{R}[z]$) haben **kein endliches Erzeugendensystem**, da der Grad beliebig groß werden kann!

**Beispiel 5: Nicht-eindeutige Darstellung**

Sei $T = V = \mathbb{R}^2$. Dann ist $\left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}, \begin{bmatrix} 1 \\ 1 \end{bmatrix}\right\}$ ein Erzeugendensystem von $\mathbb{R}^2$.

Ein Vektor kann unterschiedlich dargestellt werden:

$$\vec{x} = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = x_1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2 \begin{bmatrix} 0 \\ 1 \end{bmatrix} + 0 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

oder

$$\vec{x} = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = (x_1 - x_2) \begin{bmatrix} 1 \\ 0 \end{bmatrix} + 0 \begin{bmatrix} 0 \\ 1 \end{bmatrix} + x_2 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

---

## 📌 Zusammenfassung

**Vektorraum:** Eine Menge mit Addition und Skalarmultiplikation, die 8 Axiome erfüllt

**Teilraum:** Teilmenge eines Vektorraums, die selbst ein Vektorraum ist
- **Teilraumkriterium:** $0 \in T$, abgeschlossen unter $+$ und $\cdot$

**Linearkombination:** $v = \lambda_1 v_1 + \ldots + \lambda_k v_k$

**Span:** Menge aller Linearkombinationen von Vektoren
- Span ist immer ein Teilraum

**Erzeugendensystem:** Vektoren, deren Span den gesamten Raum/Teilraum ergibt
- Darstellung ist im Allgemeinen nicht eindeutig
- Um Eindeutigkeit zu erreichen: Begriff der linearen Unabhängigkeit (VL.11)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.08 Polynome]]: Polynome als Vektorraum
- [[VL.09 Rationale Funktionen]]: Verwendung im Beweis der PBZ-Existenz
- [[VL.11 Basis und Dimension]]: Lineare Unabhängigkeit für eindeutige Darstellung
- [[VL.13 Lineare Gleichungssysteme]]: Lösen von LGS in Vektorräumen
