**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #LineareUnabhängigkeit #Basis #Dimension #Koordinaten #Koordinatenvektor

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt zentrale Konzepte der linearen Algebra ein: lineare Unabhängigkeit, Basis und Dimension. Diese Begriffe ermöglichen es, Vektorräume präzise zu charakterisieren und Vektoren eindeutig durch Koordinaten zu beschreiben.

- **Lineare Unabhängigkeit** und lineare Abhängigkeit von Vektoren
- **Basis** als minimales Erzeugendensystem mit eindeutiger Darstellung
- **Dimension** als Maß für die "Größe" eines Vektorraums
- **Koordinaten** und Koordinatenvektoren bezüglich einer Basis
- Systematische **Konstruktion von Basen**

---

## 1. Lineare Unabhängigkeit

### Definition

Seien $v_1, \ldots, v_k$ Vektoren des $K$-Vektorraums $V$.

**Linear unabhängig:** Die Vektoren $v_1, \ldots, v_k$ heißen **linear unabhängig** genau dann, wenn die Gleichung

$$\lambda_1 v_1 + \lambda_2 v_2 + \ldots + \lambda_k v_k = 0$$

für die Unbekannten $\lambda_1, \lambda_2, \ldots, \lambda_k \in K$ **nur die Lösung** $\lambda_1 = \lambda_2 = \ldots = \lambda_k = 0$ hat.

(D.h. die Lösung $\lambda_1 = \lambda_2 = \ldots = \lambda_k = 0$ ist **eindeutig**.)

**Linear abhängig:** Die Vektoren $v_1, \ldots, v_k$ heißen **linear abhängig**, wenn sie nicht linear unabhängig sind. D.h., die Gleichung

$$\lambda_1 v_1 + \lambda_2 v_2 + \ldots + \lambda_k v_k = 0$$

hat **neben** $\lambda_1 = \ldots = \lambda_k = 0$ **noch weitere Lösungen** (die Lösung ist nicht eindeutig).

### Geometrische Interpretation

**Anschaulich:** Vektoren sind linear unabhängig, wenn jeder Vektor in eine neue eigene "Richtung" zeigt.

**Im $\mathbb{R}^2$:**
- Zwei Vektoren sind linear unabhängig, wenn sie nicht auf der gleichen Geraden liegen
- Drei oder mehr Vektoren im $\mathbb{R}^2$ sind immer linear abhängig

**Im $\mathbb{R}^3$:**
- Drei Vektoren sind linear unabhängig, wenn sie nicht in einer gemeinsamen Ebene liegen
- Vier oder mehr Vektoren im $\mathbb{R}^3$ sind immer linear abhängig

### Praktisches Vorgehen

Um zu prüfen, ob $v_1, \ldots, v_k$ linear unabhängig sind:

1. Stelle die Gleichung $0 = \lambda_1 v_1 + \lambda_2 v_2 + \ldots + \lambda_k v_k$ auf
2. Forme dies zu einem linearen Gleichungssystem für $\lambda_1, \ldots, \lambda_k$ um
3. **Linear unabhängig** ⟺ LGS hat nur die triviale Lösung $\lambda_1 = \ldots = \lambda_k = 0$
4. **Linear abhängig** ⟺ LGS hat nicht-triviale Lösungen

### Beispiele

**Beispiel 1: Linear unabhängig im $K^2$**

Die Vektoren $\vec{v}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ und $\vec{v}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$ sind linear unabhängig, denn aus

$$\begin{bmatrix} 0 \\ 0 \end{bmatrix} = \lambda_1 \vec{v}_1 + \lambda_2 \vec{v}_2 = \begin{bmatrix} \lambda_1 \\ \lambda_2 \end{bmatrix}$$

folgt $\lambda_1 = \lambda_2 = 0$.

Auch $\begin{bmatrix} 1 \\ 0 \end{bmatrix}$ und $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$ sind linear unabhängig.

**Beispiel 2: Linear abhängig im $K^2$**

Die Vektoren $\vec{v}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$, $\vec{v}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$, $\vec{v}_3 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$ sind linear abhängig, da

$$\begin{bmatrix} 0 \\ 0 \end{bmatrix} = 1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + 1 \begin{bmatrix} 0 \\ 1 \end{bmatrix} - 1 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

wobei die Koeffizienten nicht alle Null sind.

**Beispiel 3: Kollineare Vektoren**

$\begin{bmatrix} 1 \\ 0 \end{bmatrix}$ und $\begin{bmatrix} 2 \\ 0 \end{bmatrix}$ sind linear abhängig, denn

$$\begin{bmatrix} 0 \\ 0 \end{bmatrix} = \lambda_1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + \lambda_2 \begin{bmatrix} 2 \\ 0 \end{bmatrix} = \begin{bmatrix} \lambda_1 + 2\lambda_2 \\ 0 \end{bmatrix}$$

gilt z.B. für $\lambda_2 = 1$ und $\lambda_1 = -2$.

Ebenso sind $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$ und $\begin{bmatrix} -1 \\ -1 \end{bmatrix}$ linear abhängig.

**Beispiel 4: Nullvektor**

Der Nullvektor ist **immer linear abhängig**: Sind $v_1, \ldots, v_k \in V$ mit einem $v_j = 0$, so kann man $\lambda_j = 1 \neq 0$ und alle anderen Koeffizienten $= 0$ wählen, so dass $\sum_{i=1}^{k} \lambda_i v_i = 0$ gilt.

**Beispiel 5: Monome**

Sei $V = \mathbb{C}[z]$ der Vektorraum der Polynome. Für $n \in \mathbb{N}$ sind die Polynome $1, z, z^2, \ldots, z^n$ **linear unabhängig**:

Sind $\lambda_0, \lambda_1, \ldots, \lambda_n \in \mathbb{C}$ mit

$$\lambda_0 \cdot 1 + \lambda_1 z + \ldots + \lambda_n z^n = 0 \quad \text{(Nullpolynom)}$$

so sind nach dem Koeffizientenvergleich (Satz 8.12) alle Koeffizienten $\lambda_0 = \lambda_1 = \ldots = \lambda_n = 0$.

### Wichtige Charakterisierung

**Alternative Charakterisierung:** Vektoren $v_1, \ldots, v_k$ sind linear abhängig genau dann, wenn sich mindestens einer von ihnen als Linearkombination der anderen schreiben lässt.

Dies ist gut für die Vorstellung, aber schlecht zum Nachrechnen. Leichter ist es mit der Definition über das LGS.

---

## 2. Basis

### Definition

Sei $V \neq \{0\}$ ein $K$-Vektorraum. Ein endliches linear unabhängiges Erzeugendensystem $\{v_1, \ldots, v_n\}$ von $V$ heißt **Basis** von $V$.

**Ausführlich:** $\{v_1, \ldots, v_n\}$ ist eine Basis von $V$, falls gilt:

1. $v_1, \ldots, v_n$ sind **linear unabhängig**
2. $\{v_1, \ldots, v_n\}$ ist ein **Erzeugendensystem**: $\text{span}\{v_1, \ldots, v_n\} = V$

Für den Nullvektorraum $V = \{0\}$ definiert man die **leere Menge** $\emptyset$ als Basis.

### Wichtige Bemerkungen

1. **Singular:** die Basis, **Plural:** die Basen
2. **Basen sind immer geordnet!** Auch wenn Basen wie Mengen geschrieben werden (Mengen sind ungeordnet), sind Basen immer geordnet. In $B = \{v_1, \ldots, v_n\}$ ist $v_1$ der **erste** Basisvektor, $v_2$ der **zweite** Basisvektor, usw.

### Beispiele für Basen

**Beispiel 1: Basis des $\mathbb{R}^2$**

$\left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 1 \\ 1 \end{bmatrix}\right\}$ ist eine Basis von $\mathbb{R}^2$:

- **Linear unabhängig:** Aus $\begin{bmatrix} 0 \\ 0 \end{bmatrix} = \lambda_1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + \lambda_2 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$ folgt $\lambda_2 = 0$ (zweiter Eintrag) und dann $\lambda_1 = 0$ (erster Eintrag)

- **Erzeugendensystem:** Für beliebiges $\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} \in \mathbb{R}^2$ gilt:
  $$\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = (x_1 - x_2) \begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

**Beispiel 2: Standardbasis des $\mathbb{R}^2$**

$$\left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}\right\}$$

ist eine Basis von $\mathbb{R}^2$ (linear unabhängig und Erzeugendensystem).

**Beispiel 3: Standardbasis des $K^n$**

$$\left\{ \begin{bmatrix} 1 \\ 0 \\ 0 \\ \vdots \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \\ 0 \\ \vdots \\ 0 \end{bmatrix}, \ldots, \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix} \right\}$$

ist die **Standardbasis** von $K^n$.

**Beispiel 4: Kein Basisbeispiel**

$\left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}, \begin{bmatrix} 1 \\ 1 \end{bmatrix}\right\}$ ist **keine Basis**: Dies ist zwar ein Erzeugendensystem, aber die Vektoren sind linear abhängig.

**Beispiel 5: Basis der Polynome**

Der Vektorraum der Polynome vom Grad höchstens $n$,

$$\mathbb{C}[z]_{\leq n} = \text{span}\{1, z, \ldots, z^n\} = \{a_0 + a_1 z + \ldots + a_n z^n \mid a_0, a_1, \ldots, a_n \in \mathbb{C}\}$$

hat die Basis $\{1, z, \ldots, z^n\}$, denn $1, z, \ldots, z^n$ sind linear unabhängig und $\{1, z, \ldots, z^n\}$ ist ein Erzeugendensystem.

---

## 3. Dimension

### Fundamentaler Satz

**Satz:** Alle Basen eines Vektorraums haben die gleiche Anzahl an Elementen.

### Definition

Die **Dimension** eines Vektorraums ist die Anzahl der Elemente einer Basis von $V$ und wird mit $\dim(V)$ bezeichnet.

- Hat $V$ eine endliche Basis, so ist $\dim(V) \in \mathbb{N}$, und wir nennen $V$ **endlichdimensional**
- Hat $V$ keine endliche Basis, so schreiben wir $\dim(V) = \infty$ und nennen $V$ **unendlichdimensional**

### Beispiele

**Beispiel 1:** $\dim(\mathbb{R}^2) = 2$, denn $\left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}\right\}$ ist eine Basis von $\mathbb{R}^2$

**Beispiel 2:** $\dim(K^n) = n$, da die Standardbasis von $K^n$ genau $n$ Elemente hat

**Beispiel 3:** Der Vektorraum $\mathbb{C}[z]_{\leq n}$ der Polynome vom Grad höchstens $n$ hat Dimension
$$\dim(\mathbb{C}[z]_{\leq n}) = n + 1$$
da $\{1, z, \ldots, z^n\}$ eine Basis ist (beachte: $n+1$ Elemente!). Gleiches gilt für reelle Polynome.

**Beispiel 4:** Der Vektorraum aller Polynome
$$\mathbb{C}[z] = \{p(z) = a_0 + a_1 z + \ldots + a_n z^n \mid n \in \mathbb{N}, \, a_0, a_1, \ldots, a_n \in \mathbb{C}\}$$
ist **unendlichdimensional**: $\dim(\mathbb{C}[z]) = \infty$.

Um jedes mögliche Polynom darzustellen, braucht man alle Monome $1, z, z^2, \ldots$ Gleiches gilt für $\mathbb{R}[z]$.

---

## 4. Kriterien für Basen

### Vereinfachte Prüfung bei bekannter Dimension

**Satz:** Sei $V$ ein Vektorraum mit Dimension $n \in \mathbb{N}$, $n \geq 1$. Dann gilt:

1. Sind $v_1, \ldots, v_n \in V$ **linear unabhängig**, so ist $\{v_1, \ldots, v_n\}$ eine **Basis** von $V$

2. Ist $\{v_1, \ldots, v_n\}$ ein **Erzeugendensystem** von $V$, so ist $\{v_1, \ldots, v_n\}$ eine **Basis** von $V$

**Interpretation:** Kennt man die Dimension eines Vektorraums und hat die passende Anzahl Vektoren für eine Basis, braucht man nur noch **eine** der beiden Bedingungen (lineare Unabhängigkeit **oder** Erzeugendensystem) zu prüfen!

---

## 5. Konstruktion von Basen

### Methode 1: Aus Erzeugendensystem

Ist $\{v_1, \ldots, v_k\}$ ein Erzeugendensystem von $V$, aber die Vektoren sind nicht linear unabhängig, so:

**Entferne so lange geeignete Vektoren, bis eine Basis übrig bleibt.**

**Vorgehen:**
1. Sind $v_1, \ldots, v_k$ linear abhängig, gibt es $\lambda_1, \ldots, \lambda_k \in K$ (nicht alle null) mit $\sum_{i=1}^{k} \lambda_i v_i = 0$
2. Ist z.B. $\lambda_k \neq 0$, löse nach $v_k$ auf: $v_k = -\frac{1}{\lambda_k}(\lambda_1 v_1 + \ldots + \lambda_{k-1} v_{k-1})$
3. Dann ist $V = \text{span}\{v_1, \ldots, v_k\} = \text{span}\{v_1, \ldots, v_{k-1}\}$
4. Wiederhole, bis lineare Unabhängigkeit erreicht ist

### Methode 2: Aus linear unabhängigen Vektoren

Sind $v_1, \ldots, v_k$ linear unabhängig, aber $\{v_1, \ldots, v_k\}$ kein Erzeugendensystem, so:

**Nimm geeignete Vektoren $v_{k+1} \notin \text{span}\{v_1, \ldots, v_k\}$ hinzu, bis eine Basis von $V$ entsteht** (falls $\dim(V) < \infty$).

### Zusammenfassung der Basiskonzepte

| Situation | Anzahl Vektoren | Darstellung | Aktion |
|-----------|----------------|-------------|---------|
| Linear unabhängig, aber kein EZS | Zu wenige | Nicht alle Vektoren aus $V$ darstellbar | Vektoren hinzufügen |
| **Basis** | Passend | Alle Vektoren **eindeutig** darstellbar | ✓ Perfekt |
| EZS, aber nicht linear unabhängig | Zu viele | Alle Vektoren **mehrdeutig** darstellbar | Vektoren entfernen |

**Fazit:** Eine Basis enthält die **maximale Anzahl linear unabhängiger Vektoren** und zugleich die **minimale Anzahl von Vektoren**, die den Raum erzeugen.

---

## 6. Koordinaten und Koordinatenvektoren

### Definition

Sei $V$ ein $K$-Vektorraum mit Basis $B = \{v_1, \ldots, v_n\}$. Dann lässt sich jeder Vektor $v \in V$ schreiben als

$$v = \sum_{j=1}^{n} \lambda_j v_j = \lambda_1 v_1 + \lambda_2 v_2 + \ldots + \lambda_n v_n$$

wobei die Koeffizienten $\lambda_1, \ldots, \lambda_n \in K$ **eindeutig bestimmt** sind.

- Die $\lambda_1, \ldots, \lambda_n$ heißen **Koordinaten** von $v$ (bzgl. $B$)
- Der Vektor $\vec{v}_B = \begin{bmatrix} \lambda_1 \\ \vdots \\ \lambda_n \end{bmatrix} \in K^n$ heißt **Koordinatenvektor** von $v$ bzgl. $B$

### Beweis der Eindeutigkeit

Angenommen, $v$ lässt sich auf zwei Arten schreiben:
$$v = \lambda_1 v_1 + \ldots + \lambda_n v_n = \mu_1 v_1 + \ldots + \mu_n v_n$$

Dann:
$$0 = v - v = (\lambda_1 - \mu_1) v_1 + \ldots + (\lambda_n - \mu_n) v_n$$

Da $v_1, \ldots, v_n$ linear unabhängig sind, folgt:
$$\lambda_1 - \mu_1 = 0, \quad \ldots, \quad \lambda_n - \mu_n = 0$$

Also: $\lambda_1 = \mu_1, \ldots, \lambda_n = \mu_n$ ✓

### Interpretation

Die Koordinaten sind eine **"Bauanleitung"**, wie man einen Vektor aus den Basisvektoren (den "Bausteinen") zusammensetzt (linear kombiniert).

**Hat man den Koordinatenvektor** $\vec{v}_B = \begin{bmatrix} \lambda_1 \\ \vdots \\ \lambda_n \end{bmatrix}$, ist die Rekonstruktion einfach:
$$v = \sum_{j=1}^{n} \lambda_j v_j$$

**Hat man den Vektor** $v$ und möchte die Koordinaten finden, ist in der Regel ein **Gleichungssystem zu lösen**.

### Beispiele

**Beispiel 1: Standardbasis des $\mathbb{R}^2$**

Sei $V = \mathbb{R}^2$ mit Standardbasis $B = \left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \end{bmatrix}\right\}$.

Für $\vec{v} = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} \in \mathbb{R}^2$ ist:
$$\vec{v} = x_1 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2 \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

Der Koordinatenvektor ist $\vec{v}_B = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$ (sieht wie $\vec{v}$ selbst aus).

**Allgemein:** $\vec{v}_B = \vec{v}$, falls $B$ die Standardbasis von $K^n$ ist.

**Beispiel 2: Andere Basis des $\mathbb{R}^2$**

Sei $V = \mathbb{R}^2$ mit Basis $B_2 = \left\{\begin{bmatrix} 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 1 \\ 1 \end{bmatrix}\right\}$.

Für $\vec{v} = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$ rechnen wir:
$$\vec{v} = (x_1 - x_2) \begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

Der Koordinatenvektor bzgl. $B_2$ ist:
$$\vec{v}_{B_2} = \begin{bmatrix} x_1 - x_2 \\ x_2 \end{bmatrix}$$

Zum Beispiel: $\vec{v} = \begin{bmatrix} 3 \\ 5 \end{bmatrix} = -2 \begin{bmatrix} 1 \\ 0 \end{bmatrix} + 5 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$, also $\vec{v}_{B_2} = \begin{bmatrix} -2 \\ 5 \end{bmatrix}$.

**Beispiel 3: Polynome**

Sei $V = \mathbb{C}[z]_{\leq 2}$ mit Basis $B = \{1, z, z^2\}$.

Ein Polynom $p(z) = a_0 + a_1 z + a_2 z^2$ hat den Koordinatenvektor:
$$\vec{p}_B = \begin{bmatrix} a_0 \\ a_1 \\ a_2 \end{bmatrix}$$

**Beispiel 4: Koordinatenvektor mit anderer Polynombasis**

Sei $V = \mathbb{R}[z]_{\leq 2}$ und $B = \{z^2, z-1, 2\}$ eine Basis von $V$.

**Gesucht:** Koordinatenvektor $\vec{p}_B$ von $p(z) = a_0 + a_1 z + a_2 z^2$

**Ansatz:**
$$p(z) = a_0 + a_1 z + a_2 z^2 = \lambda_1 z^2 + \lambda_2(z-1) + \lambda_3 \cdot 2$$

**Koeffizientenvergleich:**
- $z^2$: $a_2 = \lambda_1 \implies \lambda_1 = a_2$
- $z^1$: $a_1 = \lambda_2 \implies \lambda_2 = a_1$
- $z^0$: $a_0 = 2\lambda_3 - \lambda_2 \implies \lambda_3 = \frac{a_0 + a_1}{2}$

Also: $\vec{p}_B = \begin{bmatrix} a_2 \\ a_1 \\ \frac{a_0 + a_1}{2} \end{bmatrix}$

Zum Beispiel für $p(z) = 2 - 3z + 2z^2$:
$$\vec{p}_B = \begin{bmatrix} 2 \\ -3 \\ -\frac{1}{2} \end{bmatrix}$$

**Probe:** $2 \cdot z^2 - 3 \cdot (z-1) - \frac{1}{2} \cdot 2 = 2z^2 - 3z + 3 - 1 = 2 - 3z + 2z^2 = p(z)$ ✓

---

## 📌 Zusammenfassung

| Begriff | Definition | Bedeutung |
|---------|------------|-----------|
| **Linear unabhängig** | $\sum \lambda_i v_i = 0 \implies$ alle $\lambda_i = 0$ | Keine Redundanz, jeder Vektor in "neue Richtung" |
| **Linear abhängig** | $\sum \lambda_i v_i = 0$ mit nicht alle $\lambda_i = 0$ | Mindestens ein Vektor als LK der anderen darstellbar |
| **Basis** | Linear unabh. Erzeugendensystem | Minimale Erzeugermenge, eindeutige Darstellung |
| **Dimension** | Anzahl Elemente einer Basis | "Größe" des Vektorraums |
| **Koordinatenvektor** | $\vec{v}_B \in K^n$ für $v \in V$ | Eindeutige Zahlendarstellung bzgl. Basis |

**Wichtigste Eigenschaften:**
- Alle Basen haben die gleiche Anzahl Elemente (= Dimension)
- Bei Basis: $n$ linear unabh. Vektoren in $n$-dim. Raum genügen für Basis
- Bei Basis: $n$ Vektoren als EZS in $n$-dim. Raum genügen für Basis
- Koordinaten bzgl. Basis sind eindeutig bestimmt

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.08 Polynome]]: Koeffizientenvergleich für lineare Unabhängigkeit
- [[VL.10 Vektorräume]]: Grundlagen zu Span und Erzeugendensystemen
- [[VL.13 Lineare Gleichungssysteme]]: Lösung für Koordinatenbestimmung
- [[VL.16 Koordinaten und Matrixdarstellung]]: Transformation zwischen verschiedenen Basen
