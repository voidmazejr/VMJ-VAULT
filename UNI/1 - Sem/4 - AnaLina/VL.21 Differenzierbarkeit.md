**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Differenzierbarkeit #Ableitung #Ableitungsregeln #Kettenregel #Tangente

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt den Begriff der Differenzierbarkeit ein und entwickelt die fundamentalen Ableitungsregeln.

- **Definition der Differenzierbarkeit** und der Ableitung
- Geometrische Interpretation: **Tangente** und Sekante
- **Differenzierbarkeit impliziert Stetigkeit**
- **Ableitungsregeln**: Summe, Produkt, Quotient, Kettenregel
- Ableitungen der **elementaren Funktionen**

---

## 1. Definition der Differenzierbarkeit

### Motivation: Von der Sekante zur Tangente

Gegeben: Funktion $f : I \to \mathbb{R}$ und Punkte $x_0, x_1 \in I$

**Sekante** durch $(x_0, f(x_0))$ und $(x_1, f(x_1))$:
$$s(x) = f(x_0) + \frac{f(x_1) - f(x_0)}{x_1 - x_0} (x - x_0)$$

**Steigung der Sekante:** $\frac{f(x_1) - f(x_0)}{x_1 - x_0}$

**Tangente** (Grenzfall für $x_1 \to x_0$):
$$t(x) = f(x_0) + m(x - x_0)$$

**Steigung der Tangente:** $m = \lim_{x_1 \to x_0} \frac{f(x_1) - f(x_0)}{x_1 - x_0}$

### Definition (Differenzierbarkeit)

Sei $f : \mathbb{R} \supseteq D \to \mathbb{R}$ eine Funktion.

**1. Differenzierbarkeit in einem Punkt:** $f$ heißt **differenzierbar in** $x_0 \in D$, falls

$$f'(x_0) := \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}$$

existiert. Der Grenzwert $f'(x_0)$ heißt **Ableitung** von $f$ in $x_0$.

**2. Differenzierbarkeit auf einem Bereich:** $f$ heißt **differenzierbar auf** $D$, falls $f$ in allen $x_0 \in D$ differenzierbar ist. Dann heißt die Abbildung

$$f' : D \to \mathbb{R}, \quad x \mapsto f'(x)$$

die **Ableitung** von $f$.

### Alternative Formulierungen

**Mit** $h := x - x_0$:
$$f'(x_0) = \lim_{h \to 0} \frac{f(x_0 + h) - f(x_0)}{h}$$

**Mit** $\Delta x$ und $\Delta f(x) = f(x + \Delta x) - f(x)$:
$$f'(x) = \lim_{\Delta x \to 0} \frac{f(x + \Delta x) - f(x)}{\Delta x} = \lim_{\Delta x \to 0} \frac{\Delta f(x)}{\Delta x} = \frac{df(x)}{dx} = \frac{df}{dx}(x)$$

**In der Physik** (wenn $t$ die Zeit bezeichnet):
$$\dot{f}(t) = f'(t)$$

### Wichtige Bemerkungen

1. **Isolierte Punkte:** Damit der Grenzwert überhaupt definiert ist, muss es Folgen in $D \setminus \{x_0\}$ geben, die gegen $x_0$ konvergieren. In "isolierten Punkten" kann man nicht ableiten.

   **Beispiel:** Für $D = \,]-3, 2[ \,\cup \{3\}$ ist $3$ ein isolierter Punkt, in dem man nicht ableiten kann.

2. **Differenzenquotient:** $\frac{f(x) - f(x_0)}{x - x_0}$ heißt Differenzenquotient

3. **Differentialquotient:** $f'(x_0)$ heißt Differentialquotient

---

## 2. Beispiele

### Grundlegende Beispiele

**1. Quadratfunktion:** $f : \mathbb{R} \to \mathbb{R}, f(x) = x^2$

$$\frac{f(x) - f(x_0)}{x - x_0} = \frac{x^2 - x_0^2}{x - x_0} = \frac{(x - x_0)(x + x_0)}{x - x_0} = x + x_0$$

Also: $f'(x_0) = \lim_{x \to x_0} (x + x_0) = 2x_0$

Damit: $f'(x) = 2x$

**2. Reziprokfunktion:** $f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, f(x) = \frac{1}{x}$

$$f'(x) = \lim_{h \to 0} \frac{\frac{1}{x+h} - \frac{1}{x}}{h} = \lim_{h \to 0} \frac{x - (x+h)}{hx(x+h)} = \lim_{h \to 0} \frac{-1}{x(x+h)} = -\frac{1}{x^2}$$

**3. Absolutbetrag:** $f : \mathbb{R} \to \mathbb{R}, f(x) = |x|$

$$\frac{f(0 + h) - f(0)}{h} = \frac{|h|}{h} = \begin{cases} 1, & h > 0 \\ -1, & h < 0 \end{cases}$$

Der Grenzwert für $h \to 0$ existiert **nicht**! 

→ $f$ ist in $x_0 = 0$ **nicht differenzierbar**

Aber: $f'(x) = 1$ für $x > 0$ und $f'(x) = -1$ für $x < 0$

---

## 3. Geometrische und physikalische Interpretation

### Geometrische Interpretation: Die Tangente

Der Differenzenquotient $\frac{f(x) - f(x_0)}{x - x_0}$ ist die **Steigung der Sekante** durch die Punkte $(x, f(x))$ und $(x_0, f(x_0))$.

Der Differentialquotient $f'(x_0)$ ist die **Steigung der Tangente** an den Graph von $f$ im Punkt $(x_0, f(x_0))$.

**Tangentengleichung:**
$$t(x) = f(x_0) + f'(x_0)(x - x_0)$$

**Interpretation:** Differenzierbare Funktionen sind solche, deren Graph eine Tangente besitzt und die in diesem Sinne **glatt** sind. Funktionen mit Knickstellen (wie $|x|$ in $0$) sind nicht differenzierbar.

### Analytische Interpretation: Lineare Approximation

Die Tangente approximiert die Funktion nahe bei $x_0$:
$$f(x) \approx t(x) = f(x_0) + f'(x_0)(x - x_0)$$

**Rest/Fehler:**
$$R(x) = f(x) - t(x) = f(x) - f(x_0) - f'(x_0)(x - x_0)$$

Es gilt: $R(x) \to 0$ für $x \to x_0$ und **wichtig:**
$$\lim_{x \to x_0} \frac{R(x)}{x - x_0} = 0$$

Der Fehler wird **schneller klein als** $x - x_0$ (schneller als linear).

**Zentrale Aussage:** Die Tangente ist die **beste lineare Approximation** an $f$ in $x_0$.

### Physikalische Interpretation: Geschwindigkeit

Ein Teilchen bewegt sich entlang einer Geraden: $s = s(t)$ (Position zur Zeit $t$)

**Mittlere Geschwindigkeit** in $[t_0, t_1]$:
$$\Delta v = \frac{\Delta s}{\Delta t} = \frac{s(t_1) - s(t_0)}{t_1 - t_0}$$

**Momentangeschwindigkeit** zum Zeitpunkt $t_0$:
$$v(t_0) = \lim_{t_1 \to t_0} \frac{s(t_1) - s(t_0)}{t_1 - t_0} = s'(t_0)$$

---

## 4. Differenzierbarkeit impliziert Stetigkeit

### Satz

Ist $f$ in $x_0$ differenzierbar, so ist $f$ in $x_0$ **stetig**.

### Beweis

$$f(x) - f(x_0) = \frac{f(x) - f(x_0)}{x - x_0} \cdot (x - x_0) \to f'(x_0) \cdot 0 = 0$$

für $x \to x_0$, also $\lim_{x \to x_0} f(x) = f(x_0)$.

### Wichtige Bemerkung

⚠️ Die **Umkehrung gilt nicht**! Stetige Funktionen müssen nicht differenzierbar sein.

**Gegenbeispiel:** $f : \mathbb{R} \to \mathbb{R}, f(x) = |x|$
- Stetig auf $\mathbb{R}$ ✓
- Nicht differenzierbar in $x_0 = 0$ ✗

---

## 5. Ableitungsregeln

### Satz (Ableitungsregeln)

Seien $f, g : D \to \mathbb{R}$ differenzierbar in $x \in D$. Dann gilt:

**1. Additivität (Summenregel):**
$$(f + g)'(x) = f'(x) + g'(x)$$

**2. Homogenität (Faktorregel):**
$$(cf)'(x) = c \cdot f'(x) \quad \text{für alle } c \in \mathbb{R}$$

**3. Produktregel:**
$$(fg)'(x) = f'(x) \cdot g(x) + f(x) \cdot g'(x)$$

**4. Quotientenregel:** (falls $g(x) \neq 0$)
$$\left(\frac{f}{g}\right)'(x) = \frac{f'(x) \cdot g(x) - f(x) \cdot g'(x)}{g(x)^2}$$

**Spezialfall:**
$$\left(\frac{1}{g}\right)'(x) = -\frac{g'(x)}{g(x)^2}$$

**5. Kettenregel:** Ist $g : D \to \mathbb{R}$ in $x$ differenzierbar und $f : E \to \mathbb{R}$ in $g(x)$ differenzierbar mit $g(D) \subseteq E$, so gilt:
$$(f \circ g)'(x) = f'(g(x)) \cdot g'(x)$$

**Merkhilfe Kettenregel:** "Äußere Ableitung mal innere Ableitung"

### Folgerungen

- Aus (1) und (2) folgt: Differenzierbare Funktionen bilden einen **Vektorraum**
- Dieser ist ein Teilraum des Vektorraums der stetigen Funktionen
- **Ableiten ist eine lineare Abbildung**

### Beweis-Skizzen

**Summenregel:**
$$\frac{f(x+h) + g(x+h) - (f(x) + g(x))}{h} = \frac{f(x+h) - f(x)}{h} + \frac{g(x+h) - g(x)}{h} \to f'(x) + g'(x)$$

**Produktregel:**
$$\frac{f(x+h)g(x+h) - f(x)g(x)}{h} = \frac{f(x+h)g(x+h) - f(x)g(x+h)}{h} + \frac{f(x)g(x+h) - f(x)g(x)}{h}$$
$$\to f'(x)g(x) + f(x)g'(x)$$

**Kettenregel:**
$$\frac{f(g(x+h)) - f(g(x))}{h} = \frac{f(g(x+h)) - f(g(x))}{g(x+h) - g(x)} \cdot \frac{g(x+h) - g(x)}{h} \to f'(g(x)) \cdot g'(x)$$

---

## 6. Ableitungen elementarer Funktionen

### Polynome und rationale Funktionen

**Lineare Funktion:** $f(x) = ax + b$
$$f'(x) = a$$

**Potenzfunktion:** $f(x) = x^n$ für $n \in \mathbb{N}$
$$f'(x) = nx^{n-1}$$

*Beweis per Induktion oder direkt mit binomischer Formel:*
$$\frac{(x+h)^n - x^n}{h} = \frac{x^n + nx^{n-1}h + \sum_{k=2}^n \binom{n}{k} x^{n-k}h^k - x^n}{h} = nx^{n-1} + \sum_{k=2}^n \binom{n}{k} x^{n-k}h^{k-1} \to nx^{n-1}$$

**Polynome:** $p(x) = a_0 + a_1x + \ldots + a_nx^n$

Differenzierbar als Linearkombination differenzierbarer Funktionen:
$$p'(x) = a_1 + 2a_2x + 3a_3x^2 + \ldots + na_nx^{n-1}$$

**Rationale Funktionen:** $f(x) = \frac{p(x)}{q(x)}$

Differenzierbar in $D = \mathbb{R} \setminus \{x \mid q(x) = 0\}$ (Quotientenregel)

### Trigonometrische Funktionen

**Wichtige Grenzwerte** (benötigt für die Ableitungen):
$$\lim_{x \to 0} \frac{\sin(x)}{x} = 1 \quad \text{(bereits in VL.19 gezeigt)}$$

$$\lim_{x \to 0} \frac{\cos(x) - 1}{x} = 0$$

*Beweis für den zweiten Grenzwert:*
$$\frac{\cos(x) - 1}{x} = \frac{(\cos(x) - 1)(\cos(x) + 1)}{x(\cos(x) + 1)} = \frac{\cos^2(x) - 1}{x(\cos(x) + 1)} = \frac{-\sin^2(x)}{x(\cos(x) + 1)}$$
$$= \frac{\sin(x)}{x} \cdot \frac{-\sin(x)}{\cos(x) + 1} \to 1 \cdot \frac{0}{2} = 0$$

**Ableitung des Sinus:**
$$\sin'(x) = \cos(x)$$

*Beweis (mit Additionstheoremen):*
$$\frac{\sin(x+h) - \sin(x)}{h} = \frac{\sin(x)\cos(h) + \sin(h)\cos(x) - \sin(x)}{h}$$
$$= \sin(x) \cdot \frac{\cos(h) - 1}{h} + \frac{\sin(h)}{h} \cdot \cos(x) \to \sin(x) \cdot 0 + 1 \cdot \cos(x) = \cos(x)$$

**Ableitung des Kosinus:**
$$\cos'(x) = -\sin(x)$$

*Beweis:*
$$\frac{\cos(x+h) - \cos(x)}{h} = \frac{\cos(x)\cos(h) - \sin(x)\sin(h) - \cos(x)}{h}$$
$$= \cos(x) \cdot \frac{\cos(h) - 1}{h} - \sin(x) \cdot \frac{\sin(h)}{h} \to \cos(x) \cdot 0 - \sin(x) \cdot 1 = -\sin(x)$$

### Exponentialfunktion

**Exponentialfunktion:** $\exp(x)$
$$\exp'(x) = \exp(x)$$

(Beweis wird in [[VL.26 Elementare Funktionen 2]] nachgeholt)

---

## 7. Beispiele mit Ableitungsregeln

**1. Kettenregel:** $f(x) = \sin(x^2)$
- Äußere Funktion: $\sin(t)$ mit Ableitung $\cos(t)$
- Innere Funktion: $x^2$ mit Ableitung $2x$

$$f'(x) = \cos(x^2) \cdot 2x = 2x\cos(x^2)$$

**2. Kettenregel:** $f(x) = (\sin(x))^2$
- Äußere Funktion: $t^2$ mit Ableitung $2t$
- Innere Funktion: $\sin(x)$ mit Ableitung $\cos(x)$

$$f'(x) = 2\sin(x) \cdot \cos(x)$$

**3. Produktregel:** $f(x) = x \cdot \sin(x)$

$$f'(x) = 1 \cdot \sin(x) + x \cdot \cos(x) = \sin(x) + x\cos(x)$$

**4. Quotientenregel:** $f(x) = \frac{x}{1 + x^2}$

$$f'(x) = \frac{1 \cdot (1 + x^2) - x \cdot 2x}{(1 + x^2)^2} = \frac{1 + x^2 - 2x^2}{(1 + x^2)^2} = \frac{1 - x^2}{(1 + x^2)^2}$$

---

## 📌 Zusammenfassung

### Definition und Eigenschaften

| **Begriff** | **Definition/Aussage** |
|------------|------------------------|
| **Differenzierbarkeit** | $f'(x_0) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}$ existiert |
| **Tangente** | $t(x) = f(x_0) + f'(x_0)(x - x_0)$ |
| **Hauptsatz** | Differenzierbar $\Rightarrow$ stetig (aber nicht umgekehrt!) |

### Ableitungsregeln

| **Regel** | **Formel** |
|-----------|-----------|
| Summe | $(f + g)' = f' + g'$ |
| Faktor | $(cf)' = cf'$ |
| Produkt | $(fg)' = f'g + fg'$ |
| Quotient | $\left(\frac{f}{g}\right)' = \frac{f'g - fg'}{g^2}$ |
| Kette | $(f \circ g)' = f'(g) \cdot g'$ |

### Wichtige Ableitungen

| **Funktion** | **Ableitung** |
|--------------|---------------|
| $x^n$ | $nx^{n-1}$ |
| $\frac{1}{x}$ | $-\frac{1}{x^2}$ |
| $\sin(x)$ | $\cos(x)$ |
| $\cos(x)$ | $-\sin(x)$ |
| $\exp(x)$ | $\exp(x)$ |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.19 Stetigkeit]]: Differenzierbarkeit impliziert Stetigkeit
- [[VL.22 Anwendung Differenzierbarkeit]]: Weitere Ableitungen (ln, tan, Umkehrfunktionen)
- [[VL.23 Mittelwertsatz]]: Anwendungen der Differenzierbarkeit
- [[VL.24 Taylor-Approximation]]: Verallgemeinerung der linearen Approximation
- [[VL.26 Elementare Funktionen 2]]: Ableitung der Exponentialfunktion

