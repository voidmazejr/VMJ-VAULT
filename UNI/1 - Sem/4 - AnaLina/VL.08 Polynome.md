**Class:** [[AnaLina]]  
**Date:** 27-12-2025  
**Topics:** #Polynome #Nullstellen #Fundamentalsatz #Polynomdivision #Linearfaktorzerlegung

---
## 🎯 Lernziele der Vorlesung

- Polynome als komplexe Funktionen verstehen
- Rechenoperationen mit Polynomen (Addition, Multiplikation, Division mit Rest)
- Nullstellen finden und abspalten
- Fundamentalsatz der Algebra kennen
- Linearfaktorzerlegung verstehen
- Reelle Polynome und konjugierte Nullstellen
- Methoden zur Nullstellenberechnung

---

## 1. Definition und Grundlagen

### Definition eines Polynoms

**Definition (Polynom):** Ein **Polynom** $p$ hat die Form: $$p(z) := a_0 + a_1 z + a_2 z^2 + ... + a_n z^n = \sum_{k=0}^{n} a_k z^k$$

wobei $a_0, a_1, ..., a_n \in \mathbb{C}$ und $n \in \mathbb{N}$.

- Die $a_k$ heißen die **Koeffizienten** des Polynoms
- Dadurch wird eine Funktion $p : \mathbb{C} \to \mathbb{C}$, $z \mapsto p(z)$ definiert

**Reelles Polynom:** Sind alle $a_k \in \mathbb{R}$, so nennt man $p$ ein **reelles Polynom**. Dann betrachten wir wahlweise $p : \mathbb{C} \to \mathbb{C}$ oder $p : \mathbb{R} \to \mathbb{R}$.

### Grad eines Polynoms

**Definition (Grad):** Ist der höchste Koeffizient $a_n \neq 0$, so heißt $n$ der **Grad** von $p$: $$n = \deg(p)$$

**Spezialfälle:**

- Sind alle Koeffizienten null (Nullpolynom), so setzt man $\deg(p) = -\infty$
- Polynome vom Grad 0 sind konstante Funktionen $p(z) = a_0 \neq 0$

**Konvention für Rechnen mit** $-\infty$:

- $-\infty < n$ für jedes $n \in \mathbb{N}$
- $-\infty + n = -\infty$

### Beispiele

1. $p(z) = 1 + i + 3z + (5i - 1)z^2$ ist ein Polynom vom Grad 2
    
2. $p(z) = 1 + 3z - 5z^2 + z^{42}$ ist ein reelles Polynom vom Grad 42
    
3. $p(z) = 3$ ist ein konstantes Polynom vom Grad 0
    
4. $p(z) = 0$ ist das Nullpolynom mit Grad $-\infty$
    

---

## 2. Rechenoperationen

### Addition

Bei der Addition $p + q$ werden die Koeffizienten vor gleichen Potenzen von $z$ addiert:

**Beispiel:** $$p(z) = 2 + 3z + 4z^3, \quad q(z) = 1 + z$$ $$p(z) + q(z) = (2+1) + (3+1)z + 4z^3 = 3 + 4z + 4z^3$$

**Weitere Beispiele:**

- $(z^2 + z + 1) + (3z^4 + 5z^2 + 2z - 4) = 3z^4 + 6z^2 + 3z - 3$
- $(z^2 + z + 1) + (-z^2 + 2z - 5) = 3z - 4$

### Skalarmultiplikation

Bei der Skalarmultiplikation $\lambda p$ mit $\lambda \in \mathbb{C}$ (oder $\lambda \in \mathbb{R}$) werden alle Koeffizienten mit $\lambda$ multipliziert:

**Beispiel:** $$2(z^2 + 3z - 1) = 2z^2 + 6z - 2$$

### Multiplikation

Die Multiplikation $pq$ erfolgt durch Ausmultiplizieren (Distributivgesetz) und Sortieren nach Potenzen:

**Beispiel:** $$p(z) = 2 + 3z + 4z^3, \quad q(z) = 1 + z$$ $$p(z)q(z) = (2 + 3z + 4z^3)(1 + z)$$ $$= 2 + 2z + 3z + 3z^2 + 4z^3 + 4z^4$$ $$= 2 + 5z + 3z^2 + 4z^3 + 4z^4$$

**Weitere Beispiele:**

- $(1 + z)(2 + 3z) = 2 + 3z + 2z + 3z^2 = 2 + 5z + 3z^2$
- $(2z^2 + 3z)(z^3 - z + 2) = 2z^5 + 3z^4 - 2z^3 + z^2 + 6z$

### Gradformel

Bei der Multiplikation gilt die **Gradformel**: $$\deg(pq) = \deg(p) + \deg(q)$$

Diese Formel gilt auch für das Nullpolynom mit der Konvention $-\infty + n = -\infty$.

### Division mit Rest (Polynomdivision)

Dividiert man zwei Polynome, erhält man im Allgemeinen kein Polynom, sondern eine rationale Funktion (siehe [[VL.09 Rationale Funktionen]]).

**Satz (Division mit Rest):** Sind $p, q$ zwei Polynome und $q \neq 0$, so existieren Polynome $r, s$ mit: $$p = sq + r \quad \text{und} \quad \deg(r) < \deg(q)$$

Dabei heißt $r$ der **Divisionsrest** oder kurz **Rest**.

**Spezialfall:** Ist der Rest $r = 0$, so ist $\frac{p}{q} = s$ ein Polynom. Man sagt:

- Die Division **geht auf**
- $q$ **teilt** $p$

### Beispiel: Polynomdivision

**Aufgabe:** Dividiere $p(z) = 2z^3 + z^2 + 3$ durch $q(z) = z + 1$

![[Screenshot 2025-12-26 at 21.30.34.png]]

**Ergebnis:** $$2z^3 + z^2 + 3 = (2z^2 - z + 1)(z + 1) + 2$$

oder

$$\frac{2z^3 + z^2 + 3}{z + 1} = 2z^2 - z + 1 + \frac{2}{z + 1}$$

mit $s(z) = 2z^2 - z + 1$ und Rest $r(z) = 2$ mit $\deg(r) = 0 < 1 = \deg(q)$.

---

## 3. Nullstellen von Polynomen

### Definition

Eine **Nullstelle** von $p$ ist eine Zahl $z_0 \in \mathbb{C}$ mit $p(z_0) = 0$.

### Abspalten von Nullstellen

**Satz:** Ist $p$ ein Polynom vom Grad $n \geq 1$ mit Nullstelle $z_0 \in \mathbb{C}$, so gibt es ein Polynom $s$ vom Grad $n - 1$ mit: $$p(z) = (z - z_0)s(z)$$

**Beweis:** Division mit Rest für $p$ und $q(z) = z - z_0$ ergibt: $$p(z) = (z - z_0)s(z) + r(z)$$

mit $\deg(r) < \deg(q) = 1$, also $r(z) = c$ konstant.

Einsetzen von $z_0$: $$0 = p(z_0) = (z_0 - z_0)s(z_0) + c = c$$

Also $r = 0$ und damit $p(z) = (z - z_0)s(z)$.

Mit der Gradformel folgt: $\deg(s) = \deg(p) - 1 = n - 1$. ✓

### Beispiel

**Gegeben:** $p(z) = 2z^3 - 16$

**Nullstelle:** $p(2) = 2 \cdot 8 - 16 = 0$, also ist $z_0 = 2$ eine Nullstelle.

**Polynomdivision:**

![[Screenshot 2025-12-26 at 21.31.10.png]]

**Ergebnis:** $$p(z) = (z - 2)(2z^2 + 4z + 8)$$

### Vielfachheit von Nullstellen

**Definition (Vielfachheit):** Die **Vielfachheit** der Nullstelle $z_0$ ist die Zahl $k \in \mathbb{N}$, sodass: $$p(z) = (z - z_0)^k q(z)$$

wobei $q$ ein Polynom mit $q(z_0) \neq 0$ ist.

**Terminologie:**

- **Einfache Nullstelle:** Vielfachheit 1
- **Mehrfache Nullstelle:** Vielfachheit $k \geq 2$
- **Doppelte Nullstelle:** Vielfachheit 2

**Beispiel:** $$p(z) = z^3 + z^2 = z^2(z + 1)$$

hat:

- Nullstelle 0 mit Vielfachheit 2 (mehrfach)
- Nullstelle -1 mit Vielfachheit 1 (einfach)

---

## 4. Fundamentalsatz der Algebra

### Satz

**Fundamentalsatz der Algebra:** Sei $p(z) = \sum_{k=0}^{n} a_k z^k$ ein Polynom vom Grad $n \geq 1$. Dann gibt es eine bis auf die Reihenfolge eindeutige **Linearfaktorzerlegung**: $$p(z) = a_n(z - z_1)(z - z_2) \cdots (z - z_n) = a_n \prod_{k=1}^{n} (z - z_k)$$

mit $z_1, z_2, ..., z_n \in \mathbb{C}$.

**Folgerung:** $p$ hat genau $n$ Nullstellen (mehrfache Nullstellen werden entsprechend ihrer Vielfachheit gezählt).

⚠️ **Wichtig:** Die Nullstellen müssen nicht voneinander verschieden sein!

### Beispiel

**Gegeben:** $p(z) = 2z^3 - 16 = 2(z - 2)(z^2 + 2z + 4)$

**Nullstellen von** $z^2 + 2z + 4$ (pq-Formel): $$z_{2,3} = -1 \pm \sqrt{1 - 4} = -1 \pm \sqrt{-3} = -1 \pm i\sqrt{3}$$

**Alle Nullstellen:**

- $z_1 = 2$
- $z_2 = -1 + i\sqrt{3}$
- $z_3 = -1 - i\sqrt{3}$

**Linearfaktorzerlegung:** $$p(z) = 2(z - 2)(z - (-1 + i\sqrt{3}))(z - (-1 - i\sqrt{3}))$$

### Zwei Darstellungen von Polynomen

**1. Summenform** (gut zum Rechnen): $$p(z) = \sum_{k=0}^{n} a_k z^k$$

- Gut für Addition, Subtraktion, Polynomdivision

**2. Produktform** (Nullstellen ablesbar): $$p(z) = a_n \prod_{k=1}^{n} (z - z_k)$$

- Nullstellen sind sofort sichtbar

⚠️ **Tipp:** Wenn Sie Nullstellen suchen und bereits einen Faktor $(z - z_0)$ ausgeklammert haben, **multiplizieren Sie diesen auf keinen Fall aus!**

### Koeffizientenvergleich

**Satz (Koeffizientenvergleich):** Seien $p(z) = \sum_{k=0}^{n} a_k z^k$ und $q(z) = \sum_{k=0}^{m} b_k z^k$ mit $p(z) = q(z)$ für alle $z$.

Dann sind die Koeffizienten gleich: $a_k = b_k$ für alle $k$.

**Bemerkung:** Es genügt Gleichheit in $N + 1$ Stellen, wobei $N = \max{n, m}$.

**Begründung:** Das Polynom $p(z) - q(z)$ hat Grad $\leq N$. Stimmt es an $N + 1$ Stellen überein, muss es das Nullpolynom sein.

---

## 5. Reelle Polynome

### Konjugierte Nullstellen

**Satz:** Sei $p$ ein reelles Polynom (alle Koeffizienten in $\mathbb{R}$). Dann treten die **nichtreellen Nullstellen in komplex konjugierten Paaren** auf.

D.h.: Ist $z_0 \in \mathbb{C} \setminus \mathbb{R}$ eine Nullstelle mit $p(z_0) = 0$, dann ist auch $\overline{z_0}$ eine Nullstelle: $p(\overline{z_0}) = 0$

**Beweis:** Für ein reelles Polynom gilt $\overline{a_k} = a_k$. Damit: $$p(\overline{z_0}) = \sum_{k=0}^{n} a_k \overline{z_0}^k = \sum_{k=0}^{n} \overline{a_k} \cdot \overline{z_0^k} = \overline{\sum_{k=0}^{n} a_k z_0^k} = \overline{p(z_0)} = \overline{0} = 0$$

### Beispiele

**Beispiel 1:** $p(z) = z^2 + 1$

- Nullstellen: $i$ und $-i = \overline{i}$ ✓

**Beispiel 2:** $p(z) = z^2 + z + 1$

- Nullstellen: $z_{1,2} = \frac{-1 \pm i\sqrt{3}}{2}$
- Also: $z_2 = \overline{z_1}$ ✓

**Gegenbeispiel (nicht reell):** $p(z) = (z - i)(z + 2i) = z^2 + iz - 2$

- Koeffizienten nicht reell!
- Nullstellen: $i$ und $-2i$ (nicht konjugiert)

### Reelle Faktorzerlegung

Für konjugierte Nullstellen $z_0 = \alpha + i\beta$ und $\overline{z_0} = \alpha - i\beta$ gilt: $$(z - z_0)(z - \overline{z_0}) = z^2 - (z_0 + \overline{z_0})z + |z_0|^2$$ $$= z^2 - 2\alpha z + (\alpha^2 + \beta^2) = (z - \alpha)^2 + \beta^2$$

Dies ist ein **reelles quadratisches Polynom ohne reelle Nullstellen**.

**Satz (Reelle Zerlegung):** Sei $p(z) = \sum_{k=0}^{n} a_k z^k$ ein Polynom mit reellen Koeffizienten vom Grad $n \geq 1$. Dann gibt es eine bis auf die Reihenfolge eindeutige Zerlegung: $$p(z) = a_n(z - x_1) \cdots (z - x_k) \cdot ((z - \alpha_1)^2 + \beta_1^2) \cdots ((z - \alpha_m)^2 + \beta_m^2)$$

mit reellen $a_n, x_1, ..., x_k, \alpha_1, ..., \alpha_m$ und $\beta_1, ..., \beta_m \neq 0$.

**Interpretation:**

- **Linearfaktoren** $(z - x_j)$: reelle Nullstellen
- **Quadratische Faktoren** $((z - \alpha_j)^2 + \beta_j^2)$: Paare konjugiert komplexer Nullstellen

### Beispiel

**Komplexe Linearfaktorzerlegung:** $$z^4 - 1 = (z - 1)(z + 1)(z - i)(z + i)$$

**Reelle Zerlegung:** $$z^4 - 1 = (z - 1)(z + 1)(z^2 + 1)$$

wobei $z^2 + 1 = (z - 0)^2 + 1^2$ keine reellen Nullstellen hat.

### Folgerung

**Satz:** Ein reelles Polynom mit **ungeradem Grad** hat mindestens eine **reelle Nullstelle**.

**Begründung:**

- Komplexe Nullstellen treten paarweise auf (Vielfachheit 2)
- Bei ungeradem Grad bleibt mindestens eine Nullstelle übrig
- Diese muss reell sein!

---

## 6. Nullstellen berechnen

### Methoden nach Grad

|**Grad**|**Methode**|**Bemerkung**|
|---|---|---|
|$n = 1$|$p(z) = a_1 z + a_0$|Nullstelle: $z = -\frac{a_0}{a_1}$|
|$n = 2$|Quadratische Gleichung|pq-Formel oder abc-Formel|
|$n = 3$|Kubische Gleichung|Cardanische Formeln (sehr kompliziert!)|
|$n = 4$|Quartische Gleichung|Formeln von Ferrari, Cardano, Euler (sehr kompliziert!)|
|$n \geq 5$|**Keine allgemeine Formel!**|Satz von Abel-Ruffini|

### Spezialfälle für n ≥ 5

**Trotzdem lösbar:**

1. **Spezielle Form:** $z^n = a$ (siehe [[VL.07 Komplexe Zahlen 2]])
2. **Nullstelle raten:** Eine Nullstelle erraten und abspalten (dann Grad reduziert!)

**Beispiel:** $p(z) = z^3 - 1$

- Offensichtlich: $p(1) = 0$, also ist $z_0 = 1$ eine Nullstelle
- Abspalten: $p(z) = (z - 1)q(z)$ mit $q$ vom Grad 2
- $q$ mit pq-Formel lösen

### Numerische Verfahren

Für allgemeine Polynome hohen Grades:

1. **Bisektionsverfahren** (siehe [[VL.20 Sätze über stetige Funktionen]])
    
    - Für reelle Nullstellen
    - Funktioniert bei Vorzeichenwechsel
2. **Newtonverfahren** (siehe [[VL.22 Anwendung Differenzierbarkeit]])
    
    - Sehr schnelle Konvergenz
    - Benötigt Ableitung

---

## 📌 Zusammenfassung

|**Begriff**|**Definition/Aussage**|**Wichtig**|
|---|---|---|
|**Polynom**|$p(z) = \sum_{k=0}^{n} a_k z^k$|Funktion $\mathbb{C} \to \mathbb{C}$|
|**Grad**|$\deg(p) = n$ falls $a_n \neq 0$|Gradformel: $\deg(pq) = \deg(p) + \deg(q)$|
|**Division mit Rest**|$p = sq + r$ mit $\deg(r) < \deg(q)$|Polynomdivision|
|**Nullstelle**|$p(z_0) = 0$|Abspalten: $p(z) = (z - z_0)s(z)$|
|**Fundamentalsatz**|$p(z) = a_n \prod_{k=1}^{n} (z - z_k)$|Jedes Polynom hat n Nullstellen in ℂ|
|**Reelle Polynome**|Konjugierte Nullstellen|$z_0$ Nullstelle $\Rightarrow$ $\overline{z_0}$ Nullstelle|
|**Ungerade Grad**|Mindestens 1 reelle Nullstelle|Folgt aus konjugierten Paaren|

**Wichtige Formeln:**

- **Linearfaktorzerlegung:** $p(z) = a_n \prod_{k=1}^{n} (z - z_k)$
- **Reelle Zerlegung:** Linearfaktoren $\times$ quadratische Faktoren
- **Für n ≥ 5:** Keine allgemeine Lösungsformel (Abel-Ruffini)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.03 Komplexe Zahlen 1]] Quadratische Gleichungen
- [[VL.04 Vollständige Induktion]] Binomischer Lehrsatz
- [[VL.07 Komplexe Zahlen 2]] Quadratische Gleichungen
- [[VL.09 Rationale Funktionen]] Quotient von Polynomen
- [[VL.20 Sätze über stetige Funktionen]] Bisektionsverfahren
- [[VL.22 Anwendung Differenzierbarkeit]] Newtonverfahren