**Class:** [[AnaLina]]  
**Date:** 27-12-2025  
**Topics:** #Abbildungen #Funktionen #Injektiv #Surjektiv #Bijektiv #Umkehrfunktion #Monotonie

---
## 🎯 Lernziele der Vorlesung

- Definition von Abbildungen und Funktionen
- Bild und Urbild verstehen
- Komposition von Abbildungen
- Injektivität, Surjektivität und Bijektivität
- Umkehrfunktionen bilden
- Eigenschaften reeller Funktionen (Symmetrie, Monotonie, Beschränktheit)

---

## 1. Definition von Abbildungen

### Grunddefinition

**Definition (Abbildung):** Seien $A, B$ Mengen. Eine **Abbildung** $f$ von $A$ nach $B$ ist eine Vorschrift, die jedem Element $x \in A$ **genau ein** Element $y = f(x) \in B$ zuordnet.

- $A$ heißt **Definitionsbereich** von $f$
- $B$ heißt **Wertebereich** von $f$

**Schreibweisen:**

- $f : A \to B, , x \mapsto y$ (lies: "f von A nach B, x wird auf y abgebildet")
- $f : A \to B, , f(x) = y$

**Funktion:** Wenn $B = \mathbb{R}$ oder $B = \mathbb{C}$, spricht man oft von **Funktion** statt Abbildung.

### Wichtige Beispiele

**1. Quadratfunktion:**

- $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x^2$ oder
- $f : \mathbb{R} \to [0, \infty[, , x \mapsto x^2$ (präziserer Wertebereich!)

**2. Kein Beispiel für Abbildung:**

- $y = \pm x$ ist **keine** Abbildung, da jedem $x$ zwei Werte zugeordnet werden

**3. Konstante Abbildungen:**

- Nullabbildung: $f : \mathbb{R} \to \mathbb{R}, , x \mapsto 0$

**4. Identität:**

- $\text{id}_A : A \to A, , a \mapsto a$ (jedes Element auf sich selbst)
- Für $A = \mathbb{R}$: Graph ist die Winkelhalbierende $y = x$

**5. Diskrete Abbildung:**

![[Screenshot 2025-12-24 at 14.33.56.png]]

---
## 2. Bild und Urbild

### Definitionen

Sei $f : A \to B$ eine Abbildung.

**Bild von X:** Für $X \subseteq A$ ist: $$f(X) := {f(x) \mid x \in X} \subseteq B$$

Speziell: **Bild von f** $$f(A) = {f(x) \mid x \in A}$$ (alle tatsächlich erreichten Werte)

**Urbild von Y:** Für $Y \subseteq B$ ist: $$f^{-1}(Y) := {x \in A \mid f(x) \in Y} \subseteq A$$

### Beispiel: f(x) = x²

Für $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x^2$:

**Bilder:**

- $f(\mathbb{R}) = [0, \infty[$ (alle Quadrate sind nichtnegativ)
- $f([1, 2]) = [1, 4]$
- $f([-1, 0]) = [0, 1]$

**Urbilder:**

- $f^{-1}({4}) = {-2, 2}$ (beide Zahlen ergeben $4$ beim Quadrieren)
- $f^{-1}([1, 4]) = [-2, -1] \cup [1, 2]$
- $f^{-1}([-2, -1]) = \emptyset$ (negative Zahlen werden nie erreicht)

⚠️ **Wichtig:** $f^{-1}(Y)$ bezeichnet das Urbild einer **Menge** $Y$, nicht die Umkehrfunktion!

![[Screenshot 2025-12-24 at 14.34.20.png]]

---

## 3. Komposition von Abbildungen

### Definition

Für Abbildungen $f : A \to B$ und $g : B \to C$ ist die **Komposition** oder **Verkettung**: $$g \circ f : A \to C, \quad x \mapsto g(f(x))$$![[Screenshot 2025-12-24 at 13.58.21.png]]
### Beispiele

**Beispiel 1:**

- $f : \mathbb{R} \to \mathbb{R}, , f(x) = x^2$
- $g : \mathbb{R} \to \mathbb{R}, , g(x) = x + 1$

Dann:

- $(g \circ f)(x) = g(f(x)) = g(x^2) = x^2 + 1$
- $(f \circ g)(x) = f(g(x)) = f(x+1) = (x+1)^2 = x^2 + 2x + 1$

⚠️ **Wichtig:** Im Allgemeinen ist $f \circ g \neq g \circ f$! Die Reihenfolge ist wesentlich!

**Beispiel 2:**

- $f : \mathbb{R} \to [0, \infty[, , x \mapsto x^2$
- $g : [0, \infty[ \to [0, \infty[, , x \mapsto \sqrt{x}$

Dann: $$g \circ f : \mathbb{R} \to [0, \infty[, \quad x \mapsto \sqrt{x^2} = |x|$$

**Beispiel 3:** Eingeschränkte Definitionsbereiche

- $f : \mathbb{R} \to \mathbb{R}, , f(x) = 1 - x^2$
- $g : [0, \infty[ \to \mathbb{R}, , g(y) = \sqrt{y}$

Dann ist $g(f(x)) = \sqrt{1-x^2}$ nur für $x \in [-1, 1]$ definiert! Also: $g \circ f : [-1, 1] \to \mathbb{R}$

---

## 4. Injektiv, Surjektiv, Bijektiv

### Definitionen

Sei $f : A \to B$ eine Abbildung.

**1. Injektiv (eineindeutig):**

$f$ heißt **injektiv**, falls für alle $x_1, x_2 \in A$ gilt: $$f(x_1) = f(x_2) \Rightarrow x_1 = x_2$$

**Äquivalent (Kontraposition):** $$x_1 \neq x_2 \Rightarrow f(x_1) \neq f(x_2)$$

_"Getrenntes bleibt getrennt" – jedes Element aus B wird von **höchstens einem** Punkt erreicht._

**2. Surjektiv (auf):**

$f$ heißt **surjektiv**, falls $f(A) = B$, d.h. zu jedem $y \in B$ existiert ein $x \in A$ mit $y = f(x)$.

_Jeder Punkt in B wird **mindestens einmal** erreicht._

**3. Bijektiv (eineindeutig und auf):**

$f$ heißt **bijektiv**, falls $f$ injektiv **und** surjektiv ist.

_Jedes Element aus B wird **genau einmal** erreicht._

### Visualisierung
![[Screenshot 2025-12-24 at 13.59.13.png]]
### Beispiele

**Beispiel 1:** $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x^2$

- **Nicht injektiv:** $f(2) = 4 = f(-2)$, aber $2 \neq -2$
- **Nicht surjektiv:** negative Zahlen werden nicht erreicht

**Beispiel 2:** $f : [0, \infty[ \to \mathbb{R}, , x \mapsto x^2$

- **Injektiv:** Für $x_1, x_2 \geq 0$ gilt: $x_1^2 = x_2^2$ $\Rightarrow$ $x_1 = x_2$ (Wurzelziehen)
- **Nicht surjektiv:** $f([0, \infty[) = [0, \infty[$ (negative Zahlen nicht erreicht)

**Beispiel 3:** $f : [0, \infty[ \to [0, \infty[, , x \mapsto x^2$

- **Injektiv:** wie oben
- **Surjektiv:** jedes $y \geq 0$ hat Urbild $x = \sqrt{y}$
- **$\Rightarrow$ Bijektiv!**

---

## 5. Umkehrfunktionen

### Definition

Sei $f : A \to B$ **injektiv**. Dann gibt es zu jedem $y \in f(A)$ **genau ein** $x \in A$ mit $f(x) = y$.

Die **Umkehrabbildung** (oder **Inverse**) ist: $$f^{-1} : f(A) \to A, \quad y \mapsto f^{-1}(y)$$

### Eigenschaften

Für die Umkehrfunktion gilt: $$f^{-1}(f(x)) = x \quad \text{für alle } x \in A$$ $$f(f^{-1}(y)) = y \quad \text{für alle } y \in f(A)$$

**Kurzschreibweise:** $$f^{-1} \circ f = \text{id}_A, \quad f \circ f^{-1} = \text{id}_{f(A)}$$

**Berechnung:** Man erhält $f^{-1}(y)$ durch Auflösen von $y = f(x)$ nach $x$.

**Wichtig:** Ist $f$ bijektiv, so ist $f(A) = B$, und $f^{-1}$ ist auf ganz $B$ definiert.

### Verwechslungsgefahr: Urbild vs. Umkehrfunktion

Für $f : A \to B$ und $y \in B$:

- $f^{-1}({y})$ = **Urbild** der Menge ${y}$ (existiert immer, ist eine Menge)
- $f^{-1}(y)$ = **Umkehrfunktion** an der Stelle $y$ (existiert nur bei Injektivität, ist ein Element)

**Beispiel:** $f : [0, \infty[ \to [0, \infty[, , x \mapsto x^2$

- **Umkehrfunktion:** $f^{-1}(4) = 2$ (Zahl)
- **Urbild:** $f^{-1}({4}) = {2}$ (Menge)

### Grafische Konstruktion

Die Umkehrfunktion erhält man durch **Spiegelung des Graphen an der Winkelhalbierenden** $y = x$.

**Beispiel:** $f : [0, \infty[ \to [0, \infty[, , x \mapsto x^2$ und $f^{-1} : [0, \infty[ \to [0, \infty[, , x \mapsto \sqrt{x}$

![[Screenshot 2025-12-24 at 13.59.54.png]]

**Gegenbeispiel:** $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x^2$ ist nicht injektiv

Spiegelt man den Graphen, erhält man **keine Funktion**, da jedem $x > 0$ zwei Werte zugeordnet würden:

```
y = ±√x  (keine Funktion!)
```

**Lösung:** Definitionsbereich einschränken!

- $f : [0, \infty[ \to [0, \infty[$ $\Rightarrow$ $f^{-1}(x) = \sqrt{x}$
- $f : ]-\infty, 0] \to [0, \infty[$ $\Rightarrow$ $f^{-1}(x) = -\sqrt{x}$

---

## 6. Eigenschaften reeller Funktionen

### 6.1 Symmetrie

**Definition (gerade und ungerade Funktionen):**

Die Funktion $f : \mathbb{R} \to \mathbb{R}$ heißt:

1. **gerade**, falls $f(-x) = f(x)$ für alle $x \in \mathbb{R}$
    
    - Graph ist **spiegelsymmetrisch zur y-Achse**
2. **ungerade**, falls $f(-x) = -f(x)$ für alle $x \in \mathbb{R}$
    
    - Graph ist **punktsymmetrisch zum Ursprung**
    - (Drehung um 180° ergibt denselben Graphen)

**Bemerkung:** Dies gilt auch für Funktionen auf $D \subseteq \mathbb{R}$, falls $D$ mit $x$ auch $-x$ enthält (z.B. $D = [-1, 1]$).

**Beispiele:**

|**Funktion**|**Typ**|**Begründung**|
|---|---|---|
|$f(x) = x^2$|gerade|$f(-x) = (-x)^2 = x^2 = f(x)$|
|$f(x) = x^4$|gerade|$f(-x) = (-x)^4 = x^4 = f(x)$|
|$f(x) = \|x\|$|gerade|$\|-x\| = \|x\|$|
|$f(x) = x$|ungerade|$f(-x) = -x = -f(x)$|
|$f(x) = x^3$|ungerade|$f(-x) = (-x)^3 = -x^3 = -f(x)$|

**Allgemein:**

- $f(x) = x^k$ mit **geradem** $k$ ist eine **gerade** Funktion
- $f(x) = x^k$ mit **ungeradem** $k$ ist eine **ungerade** Funktion

### 6.2 Monotonie

**Definition (Monotonie):**

Sei $A \subseteq \mathbb{R}$ und $f : A \to \mathbb{R}$. Dann heißt $f$:

1. **streng monoton wachsend**, wenn aus $x < y$ folgt $f(x) < f(y)$
    
2. **monoton wachsend**, wenn aus $x < y$ folgt $f(x) \leq f(y)$
    
3. **streng monoton fallend**, wenn aus $x < y$ folgt $f(x) > f(y)$
    
4. **monoton fallend**, wenn aus $x < y$ folgt $f(x) \geq f(y)$
    

**Visualisierung:**

![[Screenshot 2025-12-24 at 14.02.34.png]]
### Zusammenhang mit Injektivität

**Satz:** Sei $A \subset \mathbb{R}$ und $f : A \to \mathbb{R}$ streng monoton. Dann ist $f$ **injektiv** und damit umkehrbar.

_Beweis:_ Seien $x \neq y$ aus $A$. Dann gilt entweder $x < y$ oder $x > y$.

- Falls $x < y$ und $f$ streng mon. wachsend: $f(x) < f(y)$ $\Rightarrow$ $f(x) \neq f(y)$
- Falls $x > y$ und $f$ streng mon. wachsend: $f(x) > f(y)$ $\Rightarrow$ $f(x) \neq f(y)$ Also ist $f$ injektiv. ✓

**Beispiele:**

1. $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x + 1$ ist **streng monoton wachsend**
    
    - $x < y$ $\Rightarrow$ $x + 1 < y + 1$ $\Rightarrow$ $f(x) < f(y)$ ✓
2. Konstante Funktion $f : \mathbb{R} \to \mathbb{R}, , x \mapsto 1$ ist sowohl **monoton wachsend** als auch **monoton fallend**
    
3. $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x^2$ ist **weder monoton wachsend noch fallend**
    
    - Aber: streng monoton fallend auf $]-\infty, 0]$
    - Und: streng monoton wachsend auf $[0, \infty[$

### 6.3 Beschränktheit

**Definition (Beschränktheit):**

Eine Funktion $f : A \to \mathbb{R}$ heißt:

1. **nach oben beschränkt**, wenn ein $M \in \mathbb{R}$ existiert mit $f(x) \leq M$ für alle $x \in A$
    
2. **nach unten beschränkt**, wenn ein $m \in \mathbb{R}$ existiert mit $f(x) \geq m$ für alle $x \in A$
    
3. **beschränkt**, wenn $f$ nach oben **und** nach unten beschränkt ist, also wenn $m, M \in \mathbb{R}$ existieren mit: $$m \leq f(x) \leq M \quad \text{für alle } x \in A$$
    

**Äquivalente Charakterisierung:** $f$ ist beschränkt $\Leftrightarrow$ Es gibt $M \geq 0$ mit $|f(x)| \leq M$ für alle $x \in A$

**Beispiele:**

1. $f : \mathbb{R} \to \mathbb{R}, , x \mapsto x^2$
    
    - Nach unten beschränkt durch $m = 0$
    - **Nicht** nach oben beschränkt
2. $f : [0, 4] \to \mathbb{R}, , x \mapsto x^2$
    
    - Beschränkt: $0 \leq x^2 \leq 16$ für alle $x \in [0, 4]$
3. $f : ]-1, 0[ \to \mathbb{R}, , x \mapsto \frac{1}{x}$
    
    - Nach oben beschränkt: $f(x) \leq -1$
    - **Nicht** nach unten beschränkt (geht gegen $-\infty$ für $x \to 0^-$)

---

## 📌 Zusammenfassung

| **Begriff**        | **Definition**                                         | **Wichtig**                                  |
| ------------------ | ------------------------------------------------------ | -------------------------------------------- |
| **Abbildung**      | $f : A \to B$, jedes $x \in A$ auf genau ein $y \in B$ | $A$ = Definitionsbereich, $B$ = Wertebereich |
| **Bild**           | $f(X) = {f(x) \mid x \in X}$                           | Menge der erreichten Werte                   |
| **Urbild**         | $f^{-1}(Y) = {x \mid f(x) \in Y}$                      | Alle Urbilder einer Menge                    |
| **Komposition**    | $(g \circ f)(x) = g(f(x))$                             | Meist $f \circ g \neq g \circ f$             |
| **Injektiv**       | $f(x_1) = f(x_2) \Rightarrow x_1 = x_2$                | Höchstens ein Urbild                         |
| **Surjektiv**      | $f(A) = B$                                             | Jedes Element erreicht                       |
| **Bijektiv**       | Injektiv und surjektiv                                 | Genau ein Urbild                             |
| **Umkehrfunktion** | $f^{-1} : f(A) \to A$                                  | Nur bei Injektivität!                        |
| **Gerade**         | $f(-x) = f(x)$                                         | Spiegelsymmetrie zur y-Achse                 |
| **Ungerade**       | $f(-x) = -f(x)$                                        | Punktsymmetrie zum Ursprung                  |
| **Streng monoton** | $x < y \Rightarrow f(x) < f(y)$ (oder $>$)             | Impliziert Injektivität                      |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Mengen und Logik]] Mengenlehre als Grundlage
- [[VL.06 Elementare Funktionen 1]] Konkrete Funktionen (exp, ln, sin, cos)
- [[VL.19 Stetigkeit]] Stetige Funktionen
- [[VL.21 Differenzierbarkeit]] Monotonie über Ableitung
- [[VL.23 Mittelwertsatz]] Extremwerte und Monotonie

