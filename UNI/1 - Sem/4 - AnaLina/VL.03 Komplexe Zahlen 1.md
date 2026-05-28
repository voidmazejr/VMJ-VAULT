**Class:** [[AnaLina]]  
**Date:** 27-12-2025 
**Topics:** #KomplexeZahlen #ImaginäreEinheit #Konjugierte #Absolutbetrag #QuadratischeGleichungen

---
## 🎯 Lernziele der Vorlesung

- Definition der komplexen Zahlen und imaginären Einheit
- Grundrechenarten mit komplexen Zahlen
- Gaußsche Zahlenebene verstehen
- Realteil, Imaginärteil, Konjugierte und Betrag
- Lösen quadratischer Gleichungen in ℂ

---

## 1. Definition und Motivation

### Problem und Lösung

**Problem:** In $\mathbb{R}$ hat die Gleichung $x^2 = -1$ keine Lösung, da $x^2 \geq 0$ für alle $x \in \mathbb{R}$.

**Lösung:** Einführung der **imaginären Einheit** $i$ mit $i^2 = -1$

### Definition der komplexen Zahlen

$$\mathbb{C} := {x + iy \mid x, y \in \mathbb{R}}$$

Die Menge der komplexen Zahlen heißt $\mathbb{C}$.

**Zahlbereiche:** $\mathbb{N} \subseteq \mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \subseteq \mathbb{C}$

Da $z = x + i \cdot 0 = x$, gilt $\mathbb{R} \subseteq \mathbb{C}$ (jede reelle Zahl ist auch komplex).

### Grundrechenarten

Für $a + ib, c + id \in \mathbb{C}$ mit $a, b, c, d \in \mathbb{R}$:

**Addition:** $$(a + ib) + (c + id) := (a + c) + i(b + d)$$

**Multiplikation:** $$(a + ib) \cdot (c + id) = ac + iad + ibc + i^2bd = (ac - bd) + i(ad + bc)$$

wobei $i^2 = -1$ verwendet wird.

⚠️ **Wichtig:** Man rechnet wie mit reellen Zahlen, beachtet aber $i^2 = -1$!

### Schreibweisen

- $x + iy = x + yi$ (beide Schreibweisen üblich)
- $x + i \cdot 0 = x$ (reelle Zahl)
- $0 + iy = iy$ (rein imaginäre Zahl)
- $2 + 1i = 2 + i$
- $3 + (-2)i = 3 - 2i$

### Rechenbeispiele

**Addition:** $$(2 + 4i) + (1 - 3i) = (2+1) + i(4-3) = 3 + i$$

**Subtraktion:** $$(2 + 4i) - (1 - 3i) = 2 + 4i - 1 + 3i = 1 + 7i$$

**Multiplikation:** $$(2 + 4i) \cdot (1 - 3i) = 2 - 6i + 4i - 12i^2 = 2 - 2i + 12 = 14 - 2i$$

**Division:** Erweitern mit konjugiert Komplexem $$\frac{2 + 4i}{1 - 3i} = \frac{(2 + 4i)(1 + 3i)}{(1 - 3i)(1 + 3i)} = \frac{2 + 6i + 4i + 12i^2}{1 - 9i^2} = \frac{-10 + 10i}{10} = -1 + i$$

**Potenzen von i:**

- $i^1 = i$
- $i^2 = -1$
- $i^3 = i^2 \cdot i = -i$
- $i^4 = i^2 \cdot i^2 = 1$
- $i^5 = i^4 \cdot i = i$ (Periode 4!)
- $i^{101} = i^{100} \cdot i = (i^4)^{25} \cdot i = 1^{25} \cdot i = i$

**Trick:** $i^n$ berechnen: $n \bmod 4$ rechnen!

---

## 2. Gaußsche Zahlenebene

### Geometrische Darstellung

Benannt nach **Carl Friedrich Gauß (1777-1855)**

Komplexe Zahlen werden als Punkte in der Ebene dargestellt:

- **Reelle Achse:** horizontale Achse
- **Imaginäre Achse:** vertikale Achse
- $z = x + iy$ entspricht dem Punkt $(x, y)$

![[Screenshot 2025-12-24 at 14.05.19.png]]

**Kartesische Koordinaten:** Für $z = x + iy$ ist $(x, y)$ die Position in der Ebene.

### Addition in der Ebene

Die Addition komplexer Zahlen entspricht der **Vektoraddition**:

$$(x_1 + iy_1) + (x_2 + iy_2) = (x_1 + x_2) + i(y_1 + y_2)$$

Geometrisch: Parallelogramm-Regel für Vektoren!

---

## 3. Realteil, Imaginärteil, Konjugierte

### Definitionen

Sei $z = x + iy \in \mathbb{C}$ mit $x, y \in \mathbb{R}$.

|**Begriff**|**Notation**|**Definition**|**Typ**|
|---|---|---|---|
|**Realteil**|$\text{Re}(z)$|$x$|$\in \mathbb{R}$|
|**Imaginärteil**|$\text{Im}(z)$|$y$|$\in \mathbb{R}$|
|**Konjugierte**|$\overline{z}$|$x - iy$|$\in \mathbb{C}$|
|**Betrag**|$\|z\|$|$\sqrt{x^2 + y^2}$|$\in \mathbb{R}$|

⚠️ **Wichtig:** $\text{Im}(z) = y$ ist reell, nicht $iy$!

**Beispiel:** Für $z = 2 + 3i$:

- $\text{Re}(z) = 2$
- $\text{Im}(z) = 3$
- $\overline{z} = 2 - 3i$
- $|z| = \sqrt{4 + 9} = \sqrt{13}$

### Geometrische Interpretation

**Konjugierte:** Spiegelung an der reellen Achse

- $z = x + iy$ → $\overline{z} = x - iy$
- Beispiele:
    - $\overline{2 - 3i} = 2 + 3i$
    - $\overline{-1 + 2i} = -1 - 2i$
    - $\overline{-2i - 1} = 2i - 1$

```
       Im
        ↑
        |  z = x + iy
        |  ●
────────┼────────→ Re
        |  ●
        |  z̄ = x - iy
```

### Rechenregeln für die Konjugierte

Für $z = x + iy$ mit $x, y \in \mathbb{R}$ gilt:

1. $\overline{\overline{z}} = z$ (zweimal konjugieren gibt Original zurück)
    
2. $z \cdot \overline{z} = x^2 + y^2 = |z|^2$
    
3. $\overline{z_1 + z_2} = \overline{z_1} + \overline{z_2}$ (Konjugation ist linear)
    
4. $\overline{z_1 \cdot z_2} = \overline{z_1} \cdot \overline{z_2}$ (Konjugation verträgt sich mit Multiplikation)
    
5. $\overline{\left(\frac{1}{z}\right)} = \frac{1}{\overline{z}}$ für $z \neq 0$
    
6. $\text{Re}(z) = \frac{z + \overline{z}}{2}$
    
7. $\text{Im}(z) = \frac{z - \overline{z}}{2i}$
    

**Beweis von (2):** $$z \cdot \overline{z} = (x + iy)(x - iy) = x^2 - ixy + ixy - i^2y^2 = x^2 + y^2$$

**Beweis von (6):** $$z + \overline{z} = (x + iy) + (x - iy) = 2x = 2\text{Re}(z)$$ $$\Rightarrow \text{Re}(z) = \frac{z + \overline{z}}{2}$$

---

## 4. Absolutbetrag (Betrag)

### Definition

Für $z = x + iy \in \mathbb{C}$: $$|z| := \sqrt{x^2 + y^2} \in \mathbb{R}$$

### Geometrische Interpretation

Der Betrag $|z|$ ist der **Abstand von z zum Ursprung** in der Gaußschen Zahlenebene.

Nach dem **Satz des Pythagoras** im rechtwinkligen Dreieck mit Ecken $0, x, z$:

![[Screenshot 2025-12-24 at 14.06.41.png]]

**Abstand zweier komplexer Zahlen:** $$|z - w| = \text{Abstand zwischen } z \text{ und } w$$

### Rechenregeln für den Betrag

Für komplexe Zahlen $z, z_1, z_2$ gilt:

1. $|z| = \sqrt{z \cdot \overline{z}} \geq 0$
    
2. $|z_1 \cdot z_2| = |z_1| \cdot |z_2|$ (Betrag von Produkten)
    
3. $\left|\frac{z_1}{z_2}\right| = \frac{|z_1|}{|z_2|}$ für $z_2 \neq 0$
    
4. **Dreiecksungleichung:** $|z_1 + z_2| \leq |z_1| + |z_2|$
    

**Geometrische Interpretation der Dreiecksungleichung:**

In einem Dreieck ist die direkte Verbindung kürzer als der Umweg:

```
        z₁ + z₂
       ●
      /│
     / │ |z₂|
    /  │
   ●───●
  0    z₁
  
  |z₁ + z₂| ≤ |z₁| + |z₂|
```

---

## 5. Quadratische Gleichungen in ℂ

### Allgemeine Form

Gegeben: $az^2 + bz + c = 0$ mit $a, b, c \in \mathbb{R}$ und $a \neq 0$

**Lösungsformel (abc-Formel):** $$z_{1,2} = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

**Diskriminante:** $d := b^2 - 4ac$

### Fallunterscheidung nach Diskriminante

|**Fall**|**Diskriminante**|**Wurzel**|**Lösungen**|
|---|---|---|---|
|1|$d > 0$|$\sqrt{d} \in \mathbb{R}$|2 verschiedene reelle Lösungen|
|2|$d = 0$|$\sqrt{0} = 0$|1 doppelte reelle Lösung|
|3|$d < 0$|$\sqrt{d} = i\sqrt{-d}$|2 verschiedene komplexe Lösungen|

**Für Fall 3:** $d < 0$ $\Rightarrow$ $\sqrt{d} = \pm i\sqrt{|d|}$

### pq-Formel

Durch Division durch $a$ erhält man $z^2 + pz + q = 0$ mit $p = \frac{b}{a}$, $q = \frac{c}{a}$:

$$z_{1,2} = -\frac{p}{2} \pm \sqrt{\left(\frac{p}{2}\right)^2 - q}$$

### Beispiel

**Aufgabe:** Löse $z^2 + 2z + 5 = 0$

**Lösung mit pq-Formel:** $p = 2$, $q = 5$ $$z_{1,2} = -1 \pm \sqrt{1 - 5} = -1 \pm \sqrt{-4} = -1 \pm i\sqrt{4} = -1 \pm 2i$$

**Lösungen:**

- $z_1 = -1 + 2i$
- $z_2 = -1 - 2i$

**Probe für** $z_1$: $$(-1 + 2i)^2 + 2(-1 + 2i) + 5$$ $$= (1 - 4i + 4i^2) + (-2 + 4i) + 5$$ $$= (1 - 4i - 4) + (-2 + 4i) + 5$$ $$= -3 - 4i - 2 + 4i + 5 = 0 ,\checkmark$$

---

## 📌 Zusammenfassung

| **Konzept**    | **Definition**                         | **Wichtig**                                  |
| -------------- | -------------------------------------- | -------------------------------------------- |
| $\mathbb{C}$   | ${x + iy \mid x,y \in \mathbb{R}}$     | $i^2 = -1$                                   |
| $\text{Re}(z)$ | Realteil $x$                           | $\text{Re}(z) = \frac{z + \overline{z}}{2}$  |
| $\text{Im}(z)$ | Imaginärteil $y$                       | $\text{Im}(z) = \frac{z - \overline{z}}{2i}$ |
| $\overline{z}$ | Konjugierte $x - iy$                   | Spiegelung an reeller Achse                  |
| $\|z\|$        | Betrag $\sqrt{x^2 + y^2}$              | Abstand zum Ursprung                         |
| Dreiecksungl.  | $\|z_1 + z_2\| \leq \|z_1\| + \|z_2\|$ | Gilt auch in ℂ                               |

**Wichtige Formeln:**

- $z \cdot \overline{z} = |z|^2$
- Division: $\frac{a+ib}{c+id}$ → mit $(c-id)$ erweitern
- Quadr. Gl.: $z_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2a}$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Zahlen]] Erweiterung von ℝ zu ℂ
- [[VL.07 Komplexe Zahlen 2]] Polardarstellung und Eulersche Formel
- [[VL.08 Polynome]] Nullstellen von Polynomen in ℂ
- [[VL.26 Elementare Funktionen 2]] Komplexe Exponentialfunktion

