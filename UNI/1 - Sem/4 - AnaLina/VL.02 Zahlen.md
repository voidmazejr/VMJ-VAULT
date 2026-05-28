**Class:** [[AnaLina]]  
**Date:** 27-12-2025
**Topics:** #Zahlen #Ungleichungen #Absolutbetrag #Summenzeichen #Wurzeln

---
## 🎯 Lernziele der Vorlesung

- Zahlbereiche und ihre Erweiterungen verstehen
- Ungleichungen und Rechenregeln beherrschen
- Absolutbetrag und seine Eigenschaften
- Summen- und Produktzeichen verwenden
- Wurzeln und ihre Definition

---

## 1. Zahlbereiche

### Erweiterung der Zahlmengen

**Motivation:** Lösen von Gleichungen wie $ax + b = 0$, $ax^2 + bx + c = 0$, etc.

| **Zahlmenge**     | **Symbol**   | **Definition**                                 | **Problem gelöst**        |
| ----------------- | ------------ | ---------------------------------------------- | ------------------------- |
| Natürliche Zahlen | $\mathbb{N}$ | ${0, 1, 2, 3, ...}$                            | Zählen                    |
| Ganze Zahlen      | $\mathbb{Z}$ | ${..., -2, -1, 0, 1, 2, ...}$                  | Subtraktion: $x - y$      |
| Rationale Zahlen  | $\mathbb{Q}$ | ${\frac{m}{n} \mid m,n \in \mathbb{Z}, n > 0}$ | Division: $\frac{x}{y}$   |
| Reelle Zahlen     | $\mathbb{R}$ | ${x \mid x \text{ ist Dezimalzahl}}$           | Wurzeln: $x^2 = 2$        |
| Komplexe Zahlen   | $\mathbb{C}$ | ${x+iy \mid x,y \in \mathbb{R}, i^2=-1}$       | Neg. Quadrate: $x^2 = -1$ |

**Zusammenhang:** $\mathbb{N} \subseteq \mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \subseteq \mathbb{C}$

**Körpereigenschaft:** $\mathbb{Q}$, $\mathbb{R}$ und $\mathbb{C}$ sind Körper → alle Grundrechenarten durchführbar

### Dezimaldarstellung

**Rationale Zahlen:** Abbrechende oder periodische Dezimalzahlen

- $\frac{1}{2} = 0.5$ (abbrechend)
- $\frac{1}{3} = 0.\overline{3} = 0.333...$ (periodisch)
- $\frac{22}{7} = 3.\overline{142857}$ (periodisch)

**Irrationale Zahlen:** Nicht abbrechende, nicht periodische Dezimalzahlen

- $\sqrt{2} = 1.414213562373095...$
- $\pi = 3.141592653589793...$
- $e = 2.718281828459045...$

**Wichtig:** $\mathbb{Q}$ hat "Löcher" (z.B. bei $\sqrt{2}$), $\mathbb{R}$ hat keine Löcher!

---

## 2. Ungleichungen

### Ordnungsrelation auf ℝ

**Notation:**

- $x < y$: "x kleiner y"
- $x > y$: "x größer y" ($\Leftrightarrow$ $y < x$)
- $x \leq y$: "x kleiner gleich y" ($\Leftrightarrow$ $x < y$ oder $x = y$)
- $x \geq y$: "x größer gleich y"

### Grundregeln (Axiome)

Für alle $x, y, z \in \mathbb{R}$ und $a, b \in \mathbb{R}$ gilt:

1. **Trichotomie:** Genau einer der drei Fälle gilt: $x < y$ oder $x = y$ oder $x > y$
    
2. **Transitivität:** Aus $x < y$ und $y < z$ folgt $x < z$
    
3. **Additivität:** Aus $x < y$ und $a \leq b$ folgt $x + a < y + b$
    
4. **Multiplikation mit pos. Zahlen:** Aus $x < y$ und $a > 0$ folgt $ax < ay$
    

⚠️ Die Axiome (2)-(4) gelten auch, wenn man überall "<" durch "≤" ersetzt.

### Weitere Rechenregeln

Für alle $x, y, a \in \mathbb{R}$ gilt:

1. **Vorzeichenwechsel:**
    
    - Für $x < 0$ ist $-x > 0$
    - Für $x > 0$ ist $-x < 0$
2. **Multiplikation mit neg. Zahlen:** Aus $x < y$ und $a < 0$ folgt $ax > ay$
    
    - ⚠️ **Richtung kehrt sich um!**
3. **Quadrate sind nichtnegativ:** Für $x \neq 0$ ist $x^2 > 0$
    
4. **Allgemein für Potenzen:**
    
    - Ist $x > 0$, so folgt $x^n > 0$ für alle $n \in \mathbb{N}$
    - Ist $x < 0$, so ist:
        - $x^n > 0$ für gerades $n$
        - $x^n < 0$ für ungerades $n$

**Beispiel:** Für $x = -3$:

- $x^2 = 9 > 0$ (gerade Potenz)
- $x^3 = -27 < 0$ (ungerade Potenz)

### Beispiel: Lösen von Ungleichungen mit Brüchen

**Aufgabe:** Für welche $x \in \mathbb{R}$ gilt $\frac{2x}{x+2} > 1$?

**Lösung:**

1. Definitionsbereich: $x \neq -2$
2. Fallunterscheidung nach Vorzeichen von $x + 2$:

**Fall 1:** $x > -2$ (also $x + 2 > 0$)

- $\frac{2x}{x+2} > 1$ $\Leftrightarrow$ $2x > x + 2$ $\Leftrightarrow$ $x > 2$
- Lösungsmenge: $L_1 = ]2, \infty[$

**Fall 2:** $x < -2$ (also $x + 2 < 0$)

- $\frac{2x}{x+2} > 1$ $\Leftrightarrow$ $2x < x + 2$ $\Leftrightarrow$ $x < 2$ (Richtung kehrt um!)
- Lösungsmenge: $L_2 = ]-\infty, -2[$

**Gesamtlösung:** $L = L_1 \cup L_2 = ]-\infty, -2[ \cup ]2, \infty[ = \mathbb{R} \setminus [-2, 2]$

### Arithmetisches und Geometrisches Mittel

Für $a > 0$ und $b > 0$ gilt:

$$\sqrt{ab} \leq \frac{a+b}{2}$$

_Beweis:_

- $0 \leq (a-b)^2 = a^2 - 2ab + b^2$
- $\Rightarrow$ $4ab \leq a^2 + 2ab + b^2 = (a+b)^2$
- $\Rightarrow$ $ab \leq \left(\frac{a+b}{2}\right)^2$
- $\Rightarrow$ $\sqrt{ab} \leq \frac{a+b}{2}$ ✓

---

## 3. Wurzeln

### Definition

**Quadratwurzel:** Sei $a \geq 0$. Dann ist $\sqrt{a}$ die **nichtnegative** Lösung von $x^2 = a$.

⚠️ **Wichtig:** $\sqrt{4} = 2$ (nicht ±2!), obwohl $x^2 = 4$ die Lösungen $x = \pm 2$ hat.

**n-te Wurzel** $\sqrt[n]{a}$:

1. **Für gerades n ≥ 2 und a ≥ 0:** $\sqrt[n]{a}$ ist die **nichtnegative** Lösung von $x^n = a$
    
2. **Für ungerades n ≥ 1 und a ∈ ℝ:** $\sqrt[n]{a}$ ist die reelle Lösung von $x^n = a$
    
    - Ist $a \geq 0$, so ist $\sqrt[n]{a} \geq 0$
    - Ist $a < 0$, so ist $\sqrt[n]{a} < 0$

**Beispiele:**

- $\sqrt[3]{8} = 2$ (denn $2^3 = 8$)
- $\sqrt[3]{-8} = -2$ (denn $(-2)^3 = -8$)
- $\sqrt{-4}$ ist in $\mathbb{R}$ nicht definiert

---

## 4. Absolutbetrag

### Definition

Für $x \in \mathbb{R}$: $$|x| = \begin{cases} x, & \text{falls } x \geq 0 \ -x, & \text{falls } x < 0 \end{cases}$$

**Geometrische Interpretation:**

- $|x|$ ist der **Abstand von x zum Ursprung** (Nullpunkt)
- $|x - y|$ ist der **Abstand zwischen x und y** auf der Zahlengeraden

**Beispiele:**

- $|7| = 7$
- $|-7| = 7$
- $|3 - 8| = |-5| = 5$

### Eigenschaften des Betrags

Für alle $x, y \in \mathbb{R}$ gilt:

1. $-|x| \leq x \leq |x|$
    
2. $|x| = 0$ $\Leftrightarrow$ $x = 0$
    
3. $|xy| = |x||y|$, insbesondere $|-x| = |x|$
    
4. $|x| = \sqrt{x^2}$
    
5. **Dreiecksungleichung:** $|x + y| \leq |x| + |y|$
    
6. **Umgekehrte Dreiecksungleichung:** $||x| - |y|| \leq |x + y|$
    

### Beispiel: Lösen von Ungleichungen mit Beträgen

**Aufgabe:** Bestimme alle $x \in \mathbb{R}$ mit $|x - 2| \leq 2x + 5$

**Lösung:** Fallunterscheidung nach Vorzeichen von $x - 2$:

**Fall 1:** $x - 2 \geq 0$, also $x \geq 2$

- $x - 2 = |x - 2| \leq 2x + 5$
- $\Leftrightarrow$ $-2 \leq x + 5$
- $\Leftrightarrow$ $x \geq -7$
- Lösungsmenge: $L_1 = [2, \infty[$

**Fall 2:** $x - 2 < 0$, also $x < 2$

- $-x + 2 = -(x - 2) = |x - 2| \leq 2x + 5$
- $\Leftrightarrow$ $2 \leq 3x + 5$
- $\Leftrightarrow$ $-3 \leq 3x$
- $\Leftrightarrow$ $x \geq -1$
- Lösungsmenge: $L_2 = [-1, 2[$

**Gesamtlösung:** $L = L_1 \cup L_2 = [2, \infty[ \cup [-1, 2[ = [-1, \infty[$

---

## 5. Summenzeichen

### Definition

Seien $m, n \in \mathbb{N}$ und $x_0, x_1, ..., x_n \in \mathbb{R}$.

1. **Für m ≤ n:**

$$\sum_{k=m}^{n} x_k := x_m + x_{m+1} + ... + x_n$$

(Lies: "Summe der $x_k$ für $k$ von $m$ bis $n$")

2. **Für m > n:** **Leere Summe**

$$\sum_{k=m}^{n} x_k := 0$$

**Beispiele:**

- $\sum_{k=1}^{10} k = 1 + 2 + ... + 10 = 55$
- $\sum_{k=2}^{5} k^2 = 2^2 + 3^2 + 4^2 + 5^2 = 4 + 9 + 16 + 25 = 54$
- $\sum_{k=0}^{17} 2^k = 2^0 + 2^1 + 2^2 + ... + 2^{17}$

### Wichtige Rechenregeln

1. **Linearität:**
    
    - $\sum_{k=m}^{n} (x_k + y_k) = \sum_{k=m}^{n} x_k + \sum_{k=m}^{n} y_k$
    - $\sum_{k=m}^{n} ax_k = a \cdot \sum_{k=m}^{n} x_k$
2. **Indexverschiebung:** Der Buchstabe für den Index ist beliebig:
    
    - $\sum_{k=m}^{n} x_k = \sum_{j=m}^{n} x_j = \sum_{\ell=m}^{n} x_\ell$
3. **Substitution:** Mit $\ell = k - 1$ (also $k = \ell + 1$):
    
    - $\sum_{k=m}^{n} x_k = \sum_{\ell=m-1}^{n-1} x_{\ell+1}$
4. **Zerlegung:** Für $m \leq p \leq n$:
    
    - $\sum_{k=m}^{n} x_k = \sum_{k=m}^{p} x_k + \sum_{k=p+1}^{n} x_k$
5. **Doppelsummen:**
    
    - $\sum_{k=m}^{n} x_k \cdot \sum_{j=p}^{q} y_j = \sum_{k=m}^{n} \sum_{j=p}^{q} x_k y_j$

### Geometrische Summe

**Satz:** Für $q \in \mathbb{R}$ und $n \in \mathbb{N}$ gilt:

$$\sum_{k=0}^{n} q^k = \begin{cases} n + 1, & \text{falls } q = 1 \\ \frac{1-q^{n+1}}{1-q}, & \text{falls } q \neq 1 \end{cases}$$

_Beweis für q ≠ 1:_ Sei $S = \sum_{k=0}^{n} q^k$

- $qS = q + q^2 + ... + q^{n+1} = \sum_{k=1}^{n+1} q^k$
- $(1-q)S = S - qS = \sum_{k=0}^{n} q^k - \sum_{k=1}^{n+1} q^k = 1 - q^{n+1}$
- $\Rightarrow$ $S = \frac{1-q^{n+1}}{1-q}$ ✓

**Anwendung:** Sparplan mit jährlicher Einzahlung $B$ und Verzinsung $p$%
- Zinsfaktor: $q = 1 + \frac{p}{100}$
- Nach n Jahren: $Bq \cdot \sum_{k=0}^{n-1} q^k = Bq \cdot \frac{1-q^n}{1-q}$

---

## 6. Produktzeichen

### Definition

Seien $m, n \in \mathbb{N}$ und $x_0, ..., x_n \in \mathbb{R}$.

1. **Für m ≤ n:**

$$\prod_{k=m}^{n} x_k := x_m \cdot x_{m+1} \cdot ... \cdot x_n$$

2. **Für m > n:** **Leeres Produkt**

$$\prod_{k=m}^{n} x_k := 1$$

**Beispiele:**

- $\prod_{k=1}^{4} 2^k = 2^1 \cdot 2^2 \cdot 2^3 \cdot 2^4 = 2^{1+2+3+4} = 2^{10} = 1024$
- $\prod_{k=3}^{1} k = 1$ (leeres Produkt)

### Fakultät

**Definition:** Für $n \in \mathbb{N}$ ist die **Fakultät**:

$$n! := \prod_{k=1}^{n} k$$

**Spezialfälle:**

- $0! = 1$ (leeres Produkt per Definition)
- Für $n \geq 1$: $n! = 1 \cdot 2 \cdot 3 \cdot ... \cdot n$

**Beispiele:**

- $1! = 1$
- $3! = 1 \cdot 2 \cdot 3 = 6$
- $4! = 24$
- $5! = 120$
- $10! = 3.628.800$

⚠️ **Wichtig:** Die Fakultät wächst **sehr schnell** für wachsendes $n$!

---

## 📌 Zusammenfassung

| **Konzept**   | **Notation**                                                                                     | **Wichtig**                                 |
| ------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| Zahlbereiche  | $\mathbb{N} \subseteq \mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \subseteq \mathbb{C}$ | Jeder Bereich löst neue Gleichungen         |
| Ungleichungen | $x < y$                                                                                          | Bei Mult. mit neg. Zahl: Richtung kehrt um! |
| Absolutbetrag | $\|x\|$                                                                                          | Abstand zum Ursprung, Dreiecksungl.         |
| Wurzel        | $\sqrt{a}$                                                                                       | Immer nichtnegativ (für gerades n)          |
| Summe         | $\sum_{k=m}^{n} x_k$                                                                             | Geom. Summe: $\frac{1-q^{n+1}}{1-q}$        |
| Produkt       | $\prod_{k=m}^{n} x_k$                                                                            | Fakultät: $n! = \prod_{k=1}^{n} k$          |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Mengen und Logik]] Intervalle als Spezialfall von Mengen
- [[VL.03 Komplexe Zahlen 1]] Erweiterung zu ℂ für $x^2 = -1$
- [[VL.04 Vollständige Induktion]] Beweise mit Summen und Produkten
- [[VL.17 Konvergenz]] Grenzwerte von Folgen und Reihen