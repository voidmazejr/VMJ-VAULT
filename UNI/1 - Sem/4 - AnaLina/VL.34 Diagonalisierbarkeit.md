**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Diagonalisierbarkeit #Eigenvektorbasis #Matrixpotenzen #Fibonacci

---

## 🎯 Lernziele der Vorlesung

Diagonalmatrizen sind besonders einfach - wir lernen, wann und wie man allgemeine Matrizen auf Diagonalform bringen kann.

- **Diagonalisierbarkeit** von Matrizen
- **Charakterisierung** diagonalisierbarer Matrizen
- **Berechnung** einer Diagonalisierung
- **Anwendungen**: Matrixpotenzen, Polynome, Funktionen, Rekursionen

---

## 1. Motivation: Diagonalmatrizen

### Warum Diagonalmatrizen?

Eine **Diagonalmatrix** hat die Form:

$$D = \begin{pmatrix} d_{1,1} & 0 & \cdots & 0 \\ 0 & d_{2,2} & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & d_{n,n} \end{pmatrix} =: \text{diag}(d_{1,1}, \ldots, d_{n,n})$$

**Vorteile von Diagonalmatrizen:**

1. Die **Diagonaleinträge** $d_{1,1}, \ldots, d_{n,n}$ sind die **Eigenwerte** von $D$ (nach [[VL.33 Eigenwerte]])
2. Die **Standardbasisvektoren** sind Eigenvektoren:

$$\vec{e}_1 = \begin{pmatrix} 1 \\ 0 \\ \vdots \\ 0 \end{pmatrix}, \quad \vec{e}_2 = \begin{pmatrix} 0 \\ 1 \\ \vdots \\ 0 \end{pmatrix}, \quad \ldots, \quad \vec{e}_n = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 1 \end{pmatrix}$$

mit $D\vec{e}_j = d_{j,j}\vec{e}_j$

3. Für jeden Eigenwert gilt: **algebraische = geometrische Vielfachheit** = Anzahl, wie oft $\lambda_j$ auf der Diagonalen vorkommt

---

## 2. Definition der Diagonalisierbarkeit

### Definition (Diagonalisierbarkeit)

Die Matrix $A \in K^{n,n}$ heißt **diagonalisierbar**, wenn es eine invertierbare Matrix $S \in K^{n,n}$ gibt, so dass

$$\boxed{S^{-1}AS = D = \text{diag}(\lambda_1, \ldots, \lambda_n) = \begin{pmatrix} \lambda_1 & & 0 \\ & \ddots & \\ 0 & & \lambda_n \end{pmatrix}}$$

eine Diagonalmatrix ist.

Die Matrix $D$ nennt man eine **Diagonalisierung** von $A$.

### Äquivalente Schreibweise

$$\boxed{A = SDS^{-1}}$$

### Interpretation

- $S$ ist die **Basiswechselmatrix** von der Basis $\mathcal{B} = \{\vec{s}_1, \ldots, \vec{s}_n\}$ (Spalten von $S$) in die Standardbasis $\mathcal{B}_0$
- $D$ ist die Darstellung von $A$ bezüglich der Basis $\mathcal{B}$

**Wichtig:** Alle Einträge außerhalb der Diagonalen von $D$ sind $0$.

---

## 3. Charakterisierung der Diagonalisierbarkeit

### Satz (Äquivalente Bedingungen)

Für $A \in K^{n,n}$ sind **äquivalent:**

**1.** $A$ ist diagonalisierbar

**2.** Es gibt eine **Basis von $K^n$ aus Eigenvektoren** von $A$

**3.** Das charakteristische Polynom **zerfällt in Linearfaktoren** und $a(\lambda) = g(\lambda)$ für jeden Eigenwert von $A$

**Interpretation von (3):**
- "Zerfällt in Linearfaktoren" = es gibt **genügend Eigenwerte** (klappt immer in $\mathbb{C}$)
- "$a(\lambda) = g(\lambda)$" = es gibt **genügend Eigenvektoren** für eine Basis

### Beweis-Skizze

**1) ⇒ 2)** Sei $S^{-1}AS = D = \text{diag}(\lambda_1, \ldots, \lambda_n)$ mit $S = [\vec{s}_1 \ldots \vec{s}_n]$.

Dann ist:

$$[A\vec{s}_1 \ldots A\vec{s}_n] = AS = SD = [\lambda_1\vec{s}_1 \ldots \lambda_n\vec{s}_n]$$

Also $A\vec{s}_j = \lambda_j\vec{s}_j$ für alle $j$. Da $S$ invertierbar ist, sind $\vec{s}_j \neq \vec{0}$ (Eigenvektoren!) und linear unabhängig → Basis aus Eigenvektoren.

**2) ⇒ 1)** Hat $A$ eine Basis $\vec{s}_1, \ldots, \vec{s}_n$ aus Eigenvektoren mit $A\vec{s}_j = \lambda_j\vec{s}_j$, so ist $S = [\vec{s}_1 \ldots \vec{s}_n]$ invertierbar und:

$$AS = [A\vec{s}_1 \ldots A\vec{s}_n] = [\lambda_1\vec{s}_1 \ldots \lambda_n\vec{s}_n] = S\text{diag}(\lambda_1, \ldots, \lambda_n)$$

Also $S^{-1}AS = \text{diag}(\lambda_1, \ldots, \lambda_n)$.

**2) ⇒ 3)** Es gibt $n$ linear unabhängige Eigenvektoren, also:

$$n \leq \sum g(\lambda_j) \leq \sum a(\lambda_j) \leq n$$

(verwendet: $g(\lambda) \leq a(\lambda)$ und $\sum a(\lambda_j) \leq \deg(p_A) = n$)

Überall gilt "=", also zerfällt $p_A$ in Linearfaktoren und $g(\lambda) = a(\lambda)$ für alle Eigenwerte.

**3) ⇒ 2)** Wähle in jedem Eigenraum eine Basis ($g(\lambda_j)$ Vektoren). Da Eigenvektoren zu verschiedenen Eigenwerten linear unabhängig sind und $\sum g(\lambda_j) = n$, bilden diese $n$ Vektoren eine Basis von $K^n$.

### Wichtige Folgerungen

**Folgerung 1:** Bilden die Spalten von $S$ eine Basis aus Eigenvektoren von $A$, so ist $S^{-1}AS$ diagonal.

**Folgerung 2:** Ist $S^{-1}AS = D$ diagonal, so sind:
- Die **Spalten von $S$** die **Eigenvektoren** von $A$
- Auf der **Diagonalen von $D$** stehen die **Eigenwerte** von $A$

### Satz (Hinreichende Bedingung)

Hat $A \in K^{n,n}$ genau **$n$ verschiedene Eigenwerte**, so ist $A$ **diagonalisierbar**.

**Beweis:** Hat $A$ die $n$ verschiedenen Eigenwerte $\lambda_1, \ldots, \lambda_n$, so ist $a(\lambda_j) = 1$ für alle $j$ (da $p_A$ höchstens $n$ Nullstellen haben kann).

Wegen $1 \leq g(\lambda_j) \leq a(\lambda_j) = 1$ folgt $g(\lambda_j) = a(\lambda_j) = 1$ für alle Eigenwerte.

Also ist $A$ diagonalisierbar. ✓

---

## 4. Berechnung einer Diagonalisierung

### Algorithmus

Sei $A \in K^{n,n}$ gegeben.

**Schritt 1:** Berechne das **charakteristische Polynom** $p_A(z)$

**Schritt 2:** Bestimme die **Nullstellen** $\lambda_1, \ldots, \lambda_k$ von $p_A$ (Eigenwerte von $A$) mit **algebraischen Vielfachheiten** $a(\lambda_j)$

⚠️ Gibt es keine $n$ Nullstellen (d.h. $\sum a(\lambda_j) < n$), so ist $A$ **nicht diagonalisierbar**.

**Schritt 3:** Bestimme für $j = 1, \ldots, k$ die **Eigenräume**:

$$V_{\lambda_j} = \text{Kern}(A - \lambda_j I_n) = \{\vec{x} \in K^n \mid (A - \lambda_j I_n)\vec{x} = \vec{0}\}$$

Bestimme jeweils eine **Basis** $\mathcal{B}_j$ und die **geometrische Vielfachheit** $g(\lambda_j) = \dim(V_{\lambda_j})$

**Schritt 4:** Prüfe: Gilt $g(\lambda_j) = a(\lambda_j)$ für **alle** $j = 1, \ldots, k$?

⚠️ Wenn nicht, ist $A$ **nicht diagonalisierbar**.

**Schritt 5:** $\mathcal{B} := \mathcal{B}_1 \cup \mathcal{B}_2 \cup \ldots \cup \mathcal{B}_k$ ist eine Basis aus Eigenvektoren.

Schreibe $S = [\vec{s}_1 \ldots \vec{s}_n] \in K^{n,n}$ (Spalten = Basisvektoren).

Dann ist:

$$\boxed{S^{-1}AS = D = \text{diag}(\mu_1, \ldots, \mu_n)}$$

wobei $\mu_j$ der Eigenwert zum Eigenvektor $\vec{s}_j$ ist (j-te Spalte von $S$).

**Wichtig:** **Reihenfolge der Eigenwerte = Reihenfolge der Eigenvektoren!**

### Beispiel 1: Untere Dreiecksmatrix

Berechne (wenn möglich) eine Diagonalisierung von

$$A = \begin{pmatrix} 1 & 0 & 0 \\ -2 & 3 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

**Schritt 1:** Charakteristisches Polynom (untere Dreiecksmatrix!):

$$p_A(z) = (1-z)^2(3-z)$$

**Schritt 2:** Eigenwerte: $\lambda_1 = 1$ mit $a(1) = 2$, $\lambda_2 = 3$ mit $a(3) = 1$

**Schritt 3:** Eigenräume:

Für $\lambda_1 = 1$:

$$\text{Kern}(A - I_3) = \text{Kern}\begin{pmatrix} 0 & 0 & 0 \\ -2 & 2 & 0 \\ 0 & 0 & 0 \end{pmatrix} = \text{span}\left\{\begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}\right\}$$

Also $g(1) = 2 = a(1)$ ✓

Für $\lambda_2 = 3$:

$$\text{Kern}(A - 3I_3) = \text{Kern}\begin{pmatrix} -2 & 0 & 0 \\ -2 & 0 & 0 \\ 0 & 0 & -2 \end{pmatrix} = \text{span}\left\{\begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}\right\}$$

Also $g(3) = 1 = a(3)$ ✓

**Schritt 4:** Alle $g(\lambda_j) = a(\lambda_j)$ → $A$ ist diagonalisierbar!

**Schritt 5:** Setze

$$S = \begin{pmatrix} 1 & 0 & 0 \\ 1 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix}, \quad D = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 3 \end{pmatrix}$$

Dann ist $S^{-1}AS = D$.

**Probe:** Am besten $AS = SD$ nachrechnen (dann braucht man $S^{-1}$ nicht zu berechnen):

$$AS = \begin{pmatrix} 1 & 0 & 0 \\ -2 & 3 & 0 \\ 0 & 0 & 1 \end{pmatrix}\begin{pmatrix} 1 & 0 & 0 \\ 1 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix} = \begin{pmatrix} 1 & 0 & 0 \\ 1 & 0 & 3 \\ 0 & 1 & 0 \end{pmatrix}$$

$$SD = \begin{pmatrix} 1 & 0 & 0 \\ 1 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix}\begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 3 \end{pmatrix} = \begin{pmatrix} 1 & 0 & 0 \\ 1 & 0 & 3 \\ 0 & 1 & 0 \end{pmatrix}$$ ✓

### Beispiel 2: Komplexe Matrix

Für $A = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$:

**Charakteristisches Polynom:**

$$p_A(z) = z^2 + 1 = (z-i)(z+i)$$

**Eigenwerte:** $\lambda_1 = i$, $\lambda_2 = -i$

**Eigenräume:**

$$A - iI = \begin{pmatrix} -i & -1 \\ 1 & -i \end{pmatrix} \xrightarrow{i \cdot I} \begin{pmatrix} 1 & -i \\ 1 & -i \end{pmatrix} \xrightarrow{II - I} \begin{pmatrix} 1 & -i \\ 0 & 0 \end{pmatrix}$$

$$\vec{s}_1 = \begin{pmatrix} i \\ 1 \end{pmatrix} \in \text{Kern}(A - iI)$$

$$A + iI = \begin{pmatrix} i & -1 \\ 1 & i \end{pmatrix} \xrightarrow{I - i \cdot II} \begin{pmatrix} 0 & 0 \\ 1 & i \end{pmatrix} \xrightarrow{\text{swap}} \begin{pmatrix} 1 & i \\ 0 & 0 \end{pmatrix}$$

$$\vec{s}_2 = \begin{pmatrix} -i \\ 1 \end{pmatrix} \in \text{Kern}(A + iI)$$

**Diagonalisierung:**

$$S = \begin{pmatrix} i & -i \\ 1 & 1 \end{pmatrix}, \quad D = \begin{pmatrix} i & 0 \\ 0 & -i \end{pmatrix}$$

Also $S^{-1}AS = D$ oder $A = SDS^{-1}$.

### Beispiel 3: Nicht diagonalisierbar

Für $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$:

**Charakteristisches Polynom:** $p_A(z) = (1-z)^2$

**Eigenwert:** $\lambda = 1$ mit $a(1) = 2$

**Eigenraum:**

$$\text{Kern}(A - I_2) = \text{Kern}\begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} = \text{span}\left\{\begin{pmatrix} 1 \\ 0 \end{pmatrix}\right\}$$

**Geometrische Vielfachheit:** $g(1) = 1 < 2 = a(1)$

⚠️ **$A$ ist nicht diagonalisierbar!** Es gibt nur einen eindimensionalen Eigenraum, aber wir bräuchten eine zweidimensionale Basis.

---

## 5. Anwendungen der Diagonalisierung

Im Folgenden sei $A \in K^{n,n}$ diagonalisierbar mit $S^{-1}AS = D = \text{diag}(\lambda_1, \ldots, \lambda_n)$, also $A = SDS^{-1}$.

### Anwendung 1: Potenzen von Matrizen

$$A^2 = AA = SDS^{-1}SDS^{-1} = SD^2S^{-1}$$

$$A^3 = AA^2 = SDS^{-1}SD^2S^{-1} = SD^3S^{-1}$$

Allgemein (per Induktion):

$$\boxed{A^k = SD^kS^{-1} = S\begin{pmatrix} \lambda_1^k & & 0 \\ & \ddots & \\ 0 & & \lambda_n^k \end{pmatrix}S^{-1}}$$

**Vorteil:** Für $A^k$ brauchen wir sonst $k$ Matrixmultiplikationen, mit Diagonalisierung nur **zwei** (plus $n$ Potenzierungen)!

### Anwendung 2: Polynome von Matrizen

Ist $p(z) = a_0 + a_1 z + \ldots + a_m z^m$ ein Polynom, so ist:

$$p(A) = a_0 I_n + a_1 A + \ldots + a_m A^m$$

$$= a_0 SI_n S^{-1} + a_1 SDS^{-1} + \ldots + a_m SD^m S^{-1}$$

$$= S(a_0 I_n + a_1 D + \ldots + a_m D^m)S^{-1}$$

$$\boxed{p(A) = Sp(D)S^{-1} = S\begin{pmatrix} p(\lambda_1) & & 0 \\ & \ddots & \\ 0 & & p(\lambda_n) \end{pmatrix}S^{-1}}$$

**Vorteil:** Wir brauchen nur die $p(\lambda_j)$ berechnen plus zwei Matrixmultiplikationen!

### Anwendung 3: Funktionen von Matrizen

Für eine Funktion $f$, die an allen Eigenwerten definiert ist, schreiben wir:

$$\boxed{f(A) := S\begin{pmatrix} f(\lambda_1) & & 0 \\ & \ddots & \\ 0 & & f(\lambda_n) \end{pmatrix}S^{-1}}$$

**Besonders wichtig:** $f(x) = e^x$ beim Lösen von Differentialgleichungen (siehe [[VL.43 Lineare Differentialgleichung]]).

### Anwendung 4: Rekursionen auflösen (Fibonacci)

**Fibonacci-Folge:** $a_0 = 0$, $a_1 = 1$ und $a_n = a_{n-1} + a_{n-2}$ für $n \geq 2$.

Schreibe als Matrixgleichung:

$$\begin{pmatrix} a_n \\ a_{n-1} \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} a_{n-1} \\ a_{n-2} \end{pmatrix} = A\begin{pmatrix} a_{n-1} \\ a_{n-2} \end{pmatrix}$$

mit $\begin{pmatrix} a_1 \\ a_0 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$.

Dann folgt:

$$\begin{pmatrix} a_n \\ a_{n-1} \end{pmatrix} = A^{n-1}\begin{pmatrix} a_1 \\ a_0 \end{pmatrix} = A^{n-1}\begin{pmatrix} 1 \\ 0 \end{pmatrix}$$

Mit $z_+ = \frac{1+\sqrt{5}}{2}$ (goldener Schnitt) und $z_- = \frac{1-\sqrt{5}}{2}$:

$$A = SDS^{-1} = \begin{pmatrix} z_+ & z_- \\ 1 & 1 \end{pmatrix}\begin{pmatrix} z_+ & 0 \\ 0 & z_- \end{pmatrix}\frac{1}{\sqrt{5}}\begin{pmatrix} 1 & -z_- \\ -1 & z_+ \end{pmatrix}$$

**Explizite Formel für $a_n$:**

$$\boxed{a_n = \frac{1}{\sqrt{5}}(z_+^n - z_-^n) = \frac{1}{\sqrt{5}}\left[\left(\frac{1+\sqrt{5}}{2}\right)^n - \left(\frac{1-\sqrt{5}}{2}\right)^n\right]}$$

**Vorteil:** Direkte Berechnung von $a_n$ **ohne** alle $a_0, a_1, \ldots, a_{n-1}$ vorher zu berechnen!

### Allgemeine lineare Rekursionen

Für $a_n = \alpha_1 a_{n-1} + \ldots + \alpha_k a_{n-k}$ mit gegebenen $a_0, \ldots, a_{k-1}$:

$$\begin{pmatrix} a_n \\ a_{n-1} \\ \vdots \\ a_{n-k+1} \end{pmatrix} = \begin{pmatrix} \alpha_1 & \alpha_2 & \cdots & \alpha_k \\ 1 & 0 & \cdots & 0 \\ 0 & \ddots & \ddots & \vdots \\ 0 & 0 & 1 & 0 \end{pmatrix}\begin{pmatrix} a_{n-1} \\ a_{n-2} \\ \vdots \\ a_{n-k} \end{pmatrix}$$

Lässt sich die Matrix diagonalisieren, kann man wie oben eine explizite Formel für $a_n$ finden.

---

## 📌 Zusammenfassung

### Diagonalisierbarkeit - Äquivalente Bedingungen

Für $A \in K^{n,n}$ sind äquivalent:

| Bedingung | Bedeutung |
|-----------|-----------|
| $A$ ist diagonalisierbar | $\exists S$ invertierbar: $S^{-1}AS$ diagonal |
| Basis aus Eigenvektoren | $K^n$ hat Basis aus EV von $A$ |
| $p_A$ zerfällt in Linearfaktoren & $a(\lambda) = g(\lambda)$ | Genug EW und genug EV |

### Berechnungsschema

1. **Char. Polynom** $p_A(z) = \det(A - zI_n)$
2. **Nullstellen** → Eigenwerte mit $a(\lambda_j)$
3. **Eigenräume** $V_{\lambda_j} = \text{Kern}(A - \lambda_j I)$ → Basen, $g(\lambda_j)$
4. **Prüfe** $g(\lambda_j) = a(\lambda_j)$ für alle $j$
5. **Falls ja:** $S = $ [alle Eigenvektoren], $D = \text{diag}(\text{zugehörige EW})$

### Wichtige Sätze

✅ $n$ verschiedene Eigenwerte ⇒ $A$ diagonalisierbar

✅ Spalten von $S$ = Eigenvektoren, Diagonale von $D$ = Eigenwerte

✅ Reihenfolge beachten: Eigenwert $\mu_j$ gehört zu Eigenvektor $\vec{s}_j$ (j-te Spalte)

### Anwendungen

| Anwendung | Formel | Vorteil |
|-----------|--------|---------|
| **Potenzen** | $A^k = SD^kS^{-1}$ | 2 statt $k$ Multiplikationen |
| **Polynome** | $p(A) = Sp(D)S^{-1}$ | Nur $p(\lambda_j)$ berechnen |
| **Funktionen** | $f(A) = Sf(D)S^{-1}$ | Z.B. $e^A$ für DGLs |
| **Rekursionen** | $a_n$ via $A^n$ | Explizite Formel! |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.12 Matrizen]]: $S$ muss invertierbar sein
- [[VL.33 Eigenwerte]]: Berechnung von Eigenwerten und Eigenvektoren
- [[VL.43 Lineare Differentialgleichung]]: $e^A$ für DGL-Systeme (Anwendung)