**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Determinante #Volumenberechnung #Invertierbarkeit #LaplaceEntwicklung

---

## 🎯 Lernziele der Vorlesung

Die Determinante ordnet jeder quadratischen Matrix eine Zahl zu und dient der Volumenberechnung.

- **Determinante** für $n \times n$-Matrizen
- **Geometrische Interpretation** als Volumen
- **Berechnung** von Determinanten (Laplace-Entwicklung, Gauß-Algorithmus)
- **Rechenregeln** für Determinanten
- **Charakterisierung invertierbarer Matrizen** mit der Determinante

---

## 1. Determinante und Volumenberechnung

### Fall $n = 1$

Für $A = [a_{1,1}]$ definiert man: $$\boxed{\det(A) := a_{1,1}}$$

**Geometrische Interpretation:**
- $|\det(A)|$ = Länge von $a_{1,1}$ (Abstand zum Ursprung)
- Vorzeichen: positiv = rechts vom Ursprung, negativ = links vom Ursprung

### Fall $n = 2$

Für eine $2 \times 2$-Matrix $A = \begin{pmatrix} a_{1,1} & a_{1,2} \\ a_{2,1} & a_{2,2} \end{pmatrix}$ ist: $$\boxed{\det(A) = a_{1,1}a_{2,2} - a_{1,2}a_{2,1}}$$

**Geometrische Interpretation in $\mathbb{R}^2$:**

$|\det(A)|$ ist der **Flächeninhalt** des Parallelogramms, aufgespannt von: $$\vec{a}_1 = \begin{pmatrix} a_{1,1} \\ a_{2,1} \end{pmatrix}, \quad \vec{a}_2 = \begin{pmatrix} a_{1,2} \\ a_{2,2} \end{pmatrix}$$

**Vorzeichen:**
- $\det(A) > 0$: Drehung von $\vec{a}_1$ zu $\vec{a}_2$ über kleineren Winkel **entgegen** dem Uhrzeigersinn
- $\det(A) < 0$: Drehung von $\vec{a}_1$ zu $\vec{a}_2$ über kleineren Winkel **im** Uhrzeigersinn

**Herleitung der Flächenformel:**

Betrachte großes Rechteck mit Fläche $(a_{1,1} + a_{1,2})(a_{2,1} + a_{2,2})$:

$$F = (a_{1,1} + a_{1,2})(a_{2,1} + a_{2,2}) - 2F_1 - 2F_2 - 2F_3$$

mit $F_1 = a_{1,2}a_{2,1}$, $F_2 = \frac{1}{2}a_{1,2}a_{2,2}$, $F_3 = \frac{1}{2}a_{1,1}a_{2,1}$.

$$= a_{1,1}a_{2,1} + a_{1,1}a_{2,2} + a_{1,2}a_{2,1} + a_{1,2}a_{2,2} - 2a_{1,2}a_{2,1} - a_{1,2}a_{2,2} - a_{1,1}a_{2,1}$$

$$= a_{1,1}a_{2,2} - a_{1,2}a_{2,1} = \det(A)$$

### Fall $n = 3$

Drei Vektoren $\vec{a}_1, \vec{a}_2, \vec{a}_3 \in \mathbb{R}^3$ erzeugen ein **Parallelotop** (= Parallelepiped = Spat).

**Volumen mit Spatprodukt:** $$V = |\vec{a}_1 \cdot (\vec{a}_2 \times \vec{a}_3)|$$

wobei $\times$ das Vektorprodukt ist: $$\vec{a}_2 \times \vec{a}_3 = \begin{pmatrix} a_{2,2}a_{3,3} - a_{3,2}a_{2,3} \\ a_{3,2}a_{1,3} - a_{1,2}a_{3,3} \\ a_{1,2}a_{2,3} - a_{2,2}a_{1,3} \end{pmatrix}$$

Für $A = [a_{i,j}] \in K^{3,3}$ wird die Determinante formal als Spatprodukt definiert:

$$\det(A) = a_{1,1}(a_{2,2}a_{3,3} - a_{3,2}a_{2,3}) + a_{2,1}(a_{3,2}a_{1,3} - a_{1,2}a_{3,3}) + a_{3,1}(a_{1,2}a_{2,3} - a_{2,2}a_{1,3})$$

Mit Streichungsmatrizen (siehe unten):

$$\det(A) = a_{1,1}\det\begin{pmatrix} a_{2,2} & a_{2,3} \\ a_{3,2} & a_{3,3} \end{pmatrix} - a_{2,1}\det\begin{pmatrix} a_{1,2} & a_{1,3} \\ a_{3,2} & a_{3,3} \end{pmatrix} + a_{3,1}\det\begin{pmatrix} a_{1,2} & a_{1,3} \\ a_{2,2} & a_{2,3} \end{pmatrix}$$

**Vorzeichen (Rechte-Hand-Regel):**
- $\det(A) > 0$: Daumen = $\vec{a}_1$, Zeigefinger = $\vec{a}_2$, Mittelfinger = $\vec{a}_3$ (rechte Hand)
- $\det(A) < 0$: entspricht "linker Hand"

---

## 2. Definition der Determinante

### Definition (Streichungsmatrix)

Sei $A \in K^{n,n}$ mit $n > 1$. Durch **Streichen** der $i$-ten Zeile und $j$-ten Spalte entsteht die Streichungsmatrix:

![[Screenshot 2026-01-21 at 15.29.16.png]]

(durchgestrichene Zeile und Spalte werden entfernt)

### Definition (Determinante)

Die Determinante von $A = [a_{i,j}] \in K^{n,n}$ ist rekursiv definiert:

$$\boxed{\det(A) := \begin{cases} a_{1,1}, & \text{falls } n = 1 \\ \displaystyle\sum_{i=1}^n (-1)^{i+1} a_{i,1} \det(A_{i,1}), & \text{falls } n > 1 \end{cases}}$$

**Interpretation:** Entwicklung nach der **ersten Spalte**.

### Beispiel: $4 \times 4$-Matrix

Für $A = \begin{pmatrix} 1 & 2 & 0 & 1 \\ 4 & -2 & 1 & 0 \\ 0 & 5 & 3 & -1 \\ 2 & 4 & 1 & 3 \end{pmatrix}$:

$$\det(A) = 1 \cdot \det(A_{1,1}) - 4 \cdot \det(A_{2,1}) + 0 \cdot \det(A_{3,1}) - 2 \cdot \det(A_{4,1})$$

mit

$$A_{1,1} = \begin{pmatrix} -2 & 1 & 0 \\ 5 & 3 & -1 \\ 4 & 1 & 3 \end{pmatrix}, \quad A_{2,1} = \begin{pmatrix} 2 & 0 & 1 \\ 5 & 3 & -1 \\ 4 & 1 & 3 \end{pmatrix}, \quad \text{etc.}$$

Nach vollständiger Berechnung: $\det(A) = -65$.

---

## 3. Determinante von Dreiecksmatrizen

### Satz (Dreiecksmatrizen)

Für eine **obere Dreiecksmatrix**

$$A = \begin{pmatrix} a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\ 0 & a_{2,2} & \cdots & a_{2,n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & a_{n,n} \end{pmatrix}$$

ist: $$\boxed{\det(A) = a_{1,1} \cdot a_{2,2} \cdot \ldots \cdot a_{n,n}}$$

**Das gleiche gilt für untere Dreiecksmatrizen.**

**Beweis-Idee:** Durch wiederholte Entwicklung nach der ersten Spalte bleiben nur Diagonalelemente übrig.

---

## 4. Rechenregeln für die Determinante

### Satz (Rechenregeln)

Sei $A = [\vec{a}_1 \ldots \vec{a}_n] \in K^{n,n}$, $\vec{a} \in K^n$ und $\lambda \in K$.

**1. Linearität in jeder Spalte:**

$$\det([\vec{a}_1 \ldots \lambda\vec{a}_j \ldots \vec{a}_n]) = \lambda \det([\vec{a}_1 \ldots \vec{a}_j \ldots \vec{a}_n])$$

$$\det([\vec{a}_1 \ldots (\vec{a}_j + \vec{a}) \ldots \vec{a}_n]) = \det([\vec{a}_1 \ldots \vec{a}_j \ldots \vec{a}_n]) + \det([\vec{a}_1 \ldots \vec{a} \ldots \vec{a}_n])$$

**2. Antisymmetrie:** Vertauschen zweier Spalten ändert das Vorzeichen:

$$\det([\vec{a}_1 \ldots \vec{a}_j \ldots \vec{a}_k \ldots \vec{a}_n]) = -\det([\vec{a}_1 \ldots \vec{a}_k \ldots \vec{a}_j \ldots \vec{a}_n])$$

**3. Gleiche Spalten:** Hat $A$ zwei gleiche Spalten, so ist

$$\det(A) = 0$$

**4. Spaltenaddition:** Addition eines Vielfachen einer Spalte zu einer anderen ändert die Determinante nicht:

$$\det([\vec{a}_1 \ldots (\vec{a}_j + \lambda\vec{a}_k) \ldots \vec{a}_n]) = \det([\vec{a}_1 \ldots \vec{a}_j \ldots \vec{a}_n])$$

**5. Transposition:**

$$\boxed{\det(A) = \det(A^T)}$$

**Wichtig:** Wegen (5) gelten alle Aussagen auch für **Zeilen** der Matrix!

**Achtung:** Die Determinante ist **nicht linear in der Matrix**! Zum Beispiel:

$$\det(2I_2) = 4 \neq 2 = 2\det(I_2)$$

---

## 5. Laplace-Entwicklung

### Satz (Laplacescher Entwicklungssatz)

Für $A \in K^{n,n}$ gilt:

**Entwicklung nach der $j$-ten Spalte:**

$$\boxed{\det(A) = \sum_{i=1}^n (-1)^{i+j} a_{i,j} \det(A_{i,j})}$$

**Entwicklung nach der $i$-ten Zeile:**

$$\boxed{\det(A) = \sum_{j=1}^n (-1)^{i+j} a_{i,j} \det(A_{i,j})}$$

**Vorzeichenmuster ("Schachbrett"):**

$$\begin{pmatrix} + & - & + & - & + & \cdots \\ - & + & - & + & - & \cdots \\ + & - & + & - & + & \cdots \\ - & + & - & + & - & \cdots \\ \vdots & \vdots & \vdots & \vdots & \vdots & \ddots \end{pmatrix}$$

### Beispiel

$$\det\begin{pmatrix} 15 & 2 & 0 \\ 12 & 15 & 4 \\ 1 & 0 & 0 \end{pmatrix}$$

**Entwicklung nach 3. Spalte:**

$$= (-1)^{2+3} \cdot 4 \cdot \det\begin{pmatrix} 15 & 2 \\ 1 & 0 \end{pmatrix} = -4(15 \cdot 0 - 1 \cdot 2) = 8$$

### Strategie zur Berechnung

**Optimales Vorgehen:**

1. Erzeuge möglichst viele Nullen in einer Zeile/Spalte durch elementare Zeilen-/Spaltenoperationen
2. Entwickle nach dieser Zeile/Spalte mit vielen Nullen
3. Wiederhole, bis $2 \times 2$-Matrizen erreicht sind

### Beispiel mit Gauß und Laplace

$$\det\begin{pmatrix} 1 & 2 & 1 & -1 \\ 1 & 5 & 1 & -1 \\ 2 & 5 & 4 & -1 \\ 1 & 2 & 1 & 0 \end{pmatrix} = \det\begin{pmatrix} 1 & 2 & 1 & -1 \\ 0 & 3 & 0 & 0 \\ 0 & 1 & 2 & 1 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$$= 3 \det\begin{pmatrix} 1 & 2 & 1 & -1 \\ 0 & 1 & 0 & 0 \\ 0 & 1 & 2 & 1 \\ 0 & 0 & 0 & 1 \end{pmatrix} = 3 \det\begin{pmatrix} 1 & 2 & 1 & -1 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 2 & 1 \\ 0 & 0 & 0 & 1 \end{pmatrix} = 6$$

---

## 6. Determinantenmultiplikationssatz

### Satz (Multiplikationssatz)

Für quadratische Matrizen $A, B \in K^{n,n}$ gilt:

$$\boxed{\det(AB) = \det(A) \cdot \det(B)}$$

**Achtung:** Es gibt **keinen Determinantenadditionssatz**!

Im Allgemeinen ist: $$\det(A + B) \neq \det(A) + \det(B)$$

**Gegenbeispiel:** Für $A = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}$ und $B = \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix}$:

$$\det(A + B) = \det(I_2) = 1 \neq 0 = \det(A) + \det(B)$$

### Folgerungen aus dem Multiplikationssatz

Für quadratische $A, B \in K^{n,n}$ gilt:

**1. Kommutativität der Determinante:**

$$\det(AB) = \det(BA)$$

(selbst wenn $AB \neq BA$)

**2. Potenzregel:**

$$\det(A^k) = \det(A)^k \quad \text{für } k \in \mathbb{N}$$

**3. Determinante der Inversen:**

$$\det(A^{-1}) = (\det(A))^{-1} = \frac{1}{\det(A)}$$

(falls $A$ invertierbar)

**4. Ähnlichkeitstransformation:**

$$\det(C^{-1}AC) = \det(A)$$

für alle invertierbaren $C \in K^{n,n}$

**5. Blockdreiecksmatrix:**

Für quadratische $B$ und $D$ gilt:

$$\boxed{\det\begin{pmatrix} B & C \\ 0 & D \end{pmatrix} = \det(B) \cdot \det(D)}$$

($C$ muss nicht quadratisch sein)

---

## 7. Charakterisierung invertierbarer Matrizen

### Satz (Äquivalente Aussagen)

Sei $A \in K^{n,n}$. Dann sind **äquivalent:**

1. $A$ ist **invertierbar**
2. $\det(A) \neq 0$
3. $\text{Rang}(A) = n$
4. $A\vec{x} = \vec{0}$ ist eindeutig lösbar (durch $\vec{x} = \vec{0}$)
5. Die **Spalten** von $A$ sind linear unabhängig
6. Die **Zeilen** von $A$ sind linear unabhängig

### Anwendung: Lösbarkeit von LGS

**Beispiel:** Betrachte das LGS

$$\begin{cases} x_1 - 3x_2 + 2x_3 = 9 \\ -2x_1 + 2x_2 = -4 \\ x_1 - 3x_2 = 2 \end{cases}$$

Für $A = \begin{pmatrix} 1 & -3 & 2 \\ -2 & 2 & 0 \\ 1 & -3 & 0 \end{pmatrix}$ und $\vec{b} = \begin{pmatrix} 9 \\ -4 \\ 2 \end{pmatrix}$:

**Entwicklung nach 3. Spalte:**

$$\det(A) = 2 \cdot \det\begin{pmatrix} -2 & 2 \\ 1 & -3 \end{pmatrix} = 2((-2)(-3) - 1 \cdot 2) = 2 \cdot 4 = 8 \neq 0$$

**Folgerung:** Da $\det(A) \neq 0$, ist $A$ invertierbar und das LGS mit $\vec{x} = A^{-1}\vec{b}$ eindeutig lösbar.

### Satz (Nicht-invertierbare Matrizen)

Sei $A \in K^{n,n}$. Dann sind **äquivalent:**

1. $A$ ist **nicht invertierbar**
2. $\det(A) = 0$
3. $\text{Rang}(A) < n$
4. Es existiert $\vec{x} \in K^n$ mit $\vec{x} \neq \vec{0}$ und $A\vec{x} = \vec{0}$
5. Die **Spalten** von $A$ sind linear abhängig
6. Die **Zeilen** von $A$ sind linear abhängig

---

## 📌 Zusammenfassung

### Geometrische Interpretation

| Dimension | Determinante | Geometrische Bedeutung |
|-----------|--------------|------------------------|
| $n=1$ | $\det(A) = a_{1,1}$ | Länge (mit Vorzeichen) |
| $n=2$ | $\det(A) = a_{1,1}a_{2,2} - a_{1,2}a_{2,1}$ | Flächeninhalt des Parallelogramms |
| $n=3$ | Spatprodukt | Volumen des Spats |

### Wichtige Formeln

**Dreiecksmatrix:** $$\det(A) = \prod_{i=1}^n a_{i,i}$$

**Multiplikation:** $$\det(AB) = \det(A) \cdot \det(B)$$

**Inverse:** $$\det(A^{-1}) = \frac{1}{\det(A)}$$

**Transposition:** $$\det(A^T) = \det(A)$$

### Berechnungsmethoden

1. **Dreiecksmatrizen**: Produkt der Diagonalelemente
2. **Gauß-Algorithmus**: Zeilenstufenform erzeugen
3. **Laplace-Entwicklung**: Nach Zeile/Spalte mit vielen Nullen entwickeln
4. **Kombination**: Gauß + Laplace (optimal!)

### Rechenregeln (Spalten)

- ✅ Linearität in jeder Spalte
- ✅ Spaltentausch ändert Vorzeichen
- ✅ Gleiche Spalten ⇒ $\det = 0$
- ✅ Spaltenaddition ändert nichts
- ❌ **Kein** Additionssatz!

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.14 Gauss-Algorithmus]]: Gauß-Algorithmus, Lösbarkeit
- [[VL.18 Berechnung von Grenzwerten]]: Charakterisierung mit Determinante
- [[VL.20 Sätze über stetige Funktionen]]: Spalten/Zeilen linear unabhängig
- [[VL.33 Eigenwerte]]: Charakteristisches Polynom (kommt in VL 33)