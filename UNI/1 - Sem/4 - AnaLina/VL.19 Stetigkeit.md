**Class:** [[AnaLina]]  
**Date:** 10-01-2026 
**Topics:** #Grenzwerte #Stetigkeit #StetigeFunktionen #EinseitigeGrenzwerte

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt den Begriff der Stetigkeit über Grenzwerte von Funktionen ein und etabliert die fundamentalen Rechenregeln für stetige Funktionen.

- Definition von **Grenzwerten von Funktionen** mittels Folgenkriterium
- **Einseitige Grenzwerte** (linksseitig und rechtsseitig)
- Präzise Definition der **Stetigkeit** einer Funktion
- **Rechenregeln** für stetige Funktionen
- Konzept der **stetigen Fortsetzbarkeit**

---

## 1. Grenzwerte von Funktionen

### Definition

Sei $f : D \to \mathbb{R}$ eine Funktion ($D \subseteq \mathbb{R}$) und sei $a \in \mathbb{R} \cup \{-\infty, +\infty\}$. 

Wir sagen, $f$ hat für $x$ gegen $a$ den **Grenzwert** $c \in \mathbb{R} \cup \{-\infty, +\infty\}$, in Zeichen

$$\lim_{x \to a} f(x) = c,$$

falls gilt:

1. Für jede Folge $(x_n)_{n \in \mathbb{N}}$ mit
   - (a) $x_n \in D$
   - (b) $x_n \neq a$
   - (c) $\lim_{n \to \infty} x_n = a$
   
   ist $\lim_{n \to \infty} f(x_n) = c$.

2. Es gibt mindestens eine Folge $(x_n)_{n \in \mathbb{N}}$ mit (a)–(c).

### Wichtige Bemerkungen

- $a$ kann im Definitionsbereich von $f$ sein, muss aber nicht
- Der Punkt $a$ muss von $D \setminus \{a\}$ **"erreichbar"** sein
- **Beispiel:** $a = 3$ für $D = [0, 2] \cup \{3\}$ ist nicht aus $D \setminus \{3\} = [0, 2]$ erreichbar

### Beispiele

**1. Polynom:** Für $f : \mathbb{R} \to \mathbb{R}, x \mapsto x^2$ gilt:
$$\lim_{x \to a} f(x) = a^2$$

**2. Oszillierende Funktion:** Für $f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, f(x) = x \sin\left(\frac{1}{x}\right)$ gilt:
$$\lim_{x \to 0} f(x) = 0$$

*Beweis:* $|f(x)| = |x| \cdot \left|\sin\left(\frac{1}{x}\right)\right| \leq |x| \to 0$

**3. Heaviside-Funktion:** $H : \mathbb{R} \to \mathbb{R}, H(x) = \begin{cases} 0 & x < 0 \\ 1 & x \geq 0 \end{cases}$

Der Grenzwert $\lim_{x \to 0} H(x)$ existiert **nicht**, denn:
- $\lim_{n \to \infty} H\left(-\frac{1}{n}\right) = 0$
- $\lim_{n \to \infty} H\left(\frac{1}{n}\right) = 1$

### Grenzwertsätze für Funktionen

Sind $\lim_{x \to a} f(x) = c$ und $\lim_{x \to a} g(x) = d$ mit $c, d \in \mathbb{R}$, so gilt:

1. **Summe:** $\lim_{x \to a} (f(x) + g(x)) = c + d$

2. **Produkt:** $\lim_{x \to a} (f(x) \cdot g(x)) = c \cdot d$

3. **Skalarmultiplikation:** $\lim_{x \to a} (\alpha f(x)) = \alpha c$ für alle $\alpha \in \mathbb{R}$

4. **Quotient:** $\lim_{x \to a} \frac{f(x)}{g(x)} = \frac{c}{d}$, falls $d \neq 0$

**Wichtig:**
- Aus (1) und (3) folgt: Grenzwertbildung ist **linear**
- Das **Sandwich-Prinzip** gilt auch für Grenzwerte von Funktionen
- $a = \pm\infty$ ist erlaubt, aber $c, d \in \mathbb{R}$ müssen endlich sein

### Beispiel: Wichtiger Grenzwert

Mit dem Sandwich-Prinzip zeigt man:

$$\lim_{x \to 0} \frac{\sin(x)}{x} = 1$$

*Beweis-Skizze:* Für $0 < x < \frac{\pi}{2}$ betrachtet man Flächeninhalte und erhält:
$$\cos(x) \leq \frac{\sin(x)}{x} \leq \frac{1}{\cos(x)}$$

Mit $\lim_{x \to 0} \cos(x) = 1$ folgt die Behauptung aus dem Sandwich-Theorem.

---

## 2. Einseitige Grenzwerte

### Linksseitiger Grenzwert

Sei $f : D \to \mathbb{R}$ und $a \in \mathbb{R} \cup \{-\infty, +\infty\}$. 

Wir sagen, $f$ hat für $x$ gegen $a$ den **linksseitigen Grenzwert** $c$, in Zeichen

$$\lim_{x \nearrow a} f(x) = c \quad \text{oder} \quad \lim_{x \to a^-} f(x) = c,$$

falls für jede Folge $(x_n)_n$ mit $x_n \in D$, $x_n < a$ und $\lim_{n \to \infty} x_n = a$ gilt:
$$\lim_{n \to \infty} f(x_n) = c$$

### Rechtsseitiger Grenzwert

Analog definiert man den **rechtsseitigen Grenzwert** mit der Bedingung $x_n > a$:

$$\lim_{x \searrow a} f(x) = c \quad \text{oder} \quad \lim_{x \to a^+} f(x) = c$$

### Zusammenhang mit dem Grenzwert

**Charakterisierung:**
$$\lim_{x \to a} f(x) = c \iff \lim_{x \nearrow a} f(x) = c = \lim_{x \searrow a} f(x)$$

Der Grenzwert existiert genau dann, wenn beide einseitigen Grenzwerte existieren und übereinstimmen.

### Beispiele

**1. Vorzeichenfunktion:** $f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, f(x) = \frac{x}{|x|} = \begin{cases} 1, & x > 0 \\ -1, & x < 0 \end{cases}$

- $\lim_{x \nearrow 0} f(x) = -1$
- $\lim_{x \searrow 0} f(x) = 1$
- $\lim_{x \to 0} f(x)$ existiert **nicht**

**2. Logarithmus:** $\lim_{x \searrow 0} \ln(x) = -\infty$

---

## 3. Stetigkeit

### Definition

Sei $f : D \to \mathbb{R}$ und $a \in D$. Die Funktion $f$ heißt **stetig in** $a$, falls

$$\lim_{x \to a} f(x) = f(a)$$

Die Funktion heißt **stetig auf** $D$, falls $f$ in allen $a \in D$ stetig ist.

**Bedeutung:** Dies beinhaltet zwei Bedingungen:
1. Der Grenzwert existiert
2. Der Grenzwert ist gleich dem Funktionswert

**Alternative Formulierung:** Stetigkeit bedeutet "Vertauschung von Funktion und Grenzwert":
$$\lim_{x \to a} f(x) = f(a) = f\left(\lim_{x \to a} x\right)$$

### Grafische Interpretation

- **Stetig:** Keine Sprünge, Graph kann ohne Absetzen gezeichnet werden
- **Unstetig:** Sprünge oder fehlende Grenzwerte

### Rechenregeln für stetige Funktionen

Seien $f, g : D \to \mathbb{R}$ stetig. Dann sind auch stetig:

1. **Summe und Differenz:** $f + g$ und $f - g$ in $D$

2. **Skalarmultiplikation:** $\alpha f$ für alle $\alpha \in \mathbb{R}$ in $D$

3. **Produkt:** $f \cdot g$ in $D$

4. **Quotient:** $\frac{f}{g}$ in $D \setminus \{x \mid g(x) = 0\}$ (überall wo $\frac{f}{g}$ definiert ist)

5. **Komposition:** Sind $f : D \to \mathbb{R}$ und $g : E \to \mathbb{R}$ stetig mit $g(E) \subseteq D$, so ist auch $f \circ g : E \to \mathbb{R}, x \mapsto f(g(x))$ stetig

**Folgerung:** Die stetigen Funktionen bilden einen **Vektorraum** (Teilraum von $\{f : D \to \mathbb{R}\}$).

---

## 4. Beispiele zur Stetigkeit

### Stetige Funktionen

**1. Polynome:** $p : \mathbb{R} \to \mathbb{R}, x \mapsto a_0 + a_1 x + \ldots + a_k x^k$

Polynome sind **stetig auf ganz** $\mathbb{R}$ als Summe von Produkten stetiger Funktionen.

**2. Wurzelfunktionen:** $f : [0, \infty) \to [0, \infty), x \mapsto \sqrt[k]{x}$ (mit $k \in \mathbb{N}, k \geq 2$)

Wurzelfunktionen sind stetig.

**3. Rationale Funktionen:** $f : D \subseteq \mathbb{R} \to \mathbb{R}, x \mapsto \frac{p(x)}{q(x)}$

Stetig auf $D = \mathbb{R} \setminus \{x \mid q(x) = 0\}$ als Quotient stetiger Funktionen.

**Beispiel:** $f(x) = \frac{x^3 - 5x + 4}{x^2 - 4}$ ist stetig auf $\mathbb{R} \setminus \{-2, 2\}$

**4. Absolutbetrag:** $f : \mathbb{R} \to \mathbb{R}, f(x) = |x|$

Stetig auf ganz $\mathbb{R}$.

### Unstetige Funktionen

**1. Reziprokfunktion:** $f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, x \mapsto \frac{1}{x}$

Stetig auf $\mathbb{R} \setminus \{0\}$, aber $\lim_{x \to 0} f(x)$ existiert nicht.

→ **Nicht hebbare Polstelle** in $x = 0$

**2. Erweiterte Reziprokfunktion:** $f : \mathbb{R} \to \mathbb{R}, f(x) = \begin{cases} \frac{1}{x}, & x \neq 0 \\ 0, & x = 0 \end{cases}$

**Nicht stetig** in $x = 0$, da $\lim_{x \to 0} f(x)$ nicht existiert.

**3. Vorzeichenfunktion:** $f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, f(x) = \begin{cases} 1, & x > 0 \\ -1, & x < 0 \end{cases}$

Stetig auf $\mathbb{R} \setminus \{0\}$, aber $\lim_{x \to 0} f(x)$ existiert nicht.

→ **Sprungstelle** in $x = 0$

**4. Erweiterte Vorzeichenfunktion:** $f : \mathbb{R} \to \mathbb{R}, f(x) = \begin{cases} 1, & x \geq 0 \\ -1, & x < 0 \end{cases}$

**Nicht stetig** in $x = 0$, da $\lim_{x \to 0} f(x)$ nicht existiert.

**5. Oszillierende Funktion:** $f : \mathbb{R} \to \mathbb{R}, f(x) = \begin{cases} \sin\left(\frac{1}{x}\right), & x \neq 0 \\ 0, & x = 0 \end{cases}$

**Nicht stetig** in $x = 0$, da $\lim_{x \to 0} f(x)$ nicht existiert (Funktion oszilliert unendlich oft zwischen $-1$ und $1$).

---

## 5. Stetige Fortsetzbarkeit

### Definition

Sei $f : I \setminus \{a\} \to \mathbb{R}$ stetig, wobei $I$ ein Intervall ist und $a \in I$. 

Wenn der Grenzwert $\lim_{x \to a} f(x) = c \in \mathbb{R}$ existiert, so können wir die Funktion

$$g : I \to \mathbb{R}, \quad g(x) = \begin{cases} f(x), & x \neq a \\ c, & x = a \end{cases}$$

definieren, die dann **stetig auf ganz** $I$ ist.

Diese Funktion heißt **stetige Fortsetzung** von $f$ (oft nennt man $g$ auch wieder $f$).

### Beispiele

**1. Hebbare Polstelle:** $f : \mathbb{R} \setminus \{1\} \to \mathbb{R}, f(x) = \frac{x^2 - 1}{x - 1}$

$$\lim_{x \to 1} f(x) = \lim_{x \to 1} \frac{(x-1)(x+1)}{x-1} = \lim_{x \to 1} (x+1) = 2$$

Stetige Fortsetzung:
$$f : \mathbb{R} \to \mathbb{R}, \quad f(x) = \begin{cases} \frac{x^2 - 1}{x - 1}, & x \neq 1 \\ 2, & x = 1 \end{cases}$$

**Vereinfachung:** $f(x) = \frac{x^2-1}{x-1} = x + 1$ (für $x \neq 1$)

**2. Oszillierende Funktion:** $f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, f(x) = x \sin\left(\frac{1}{x}\right)$

Da $\lim_{x \to 0} f(x) = 0$, ist
$$f : \mathbb{R} \to \mathbb{R}, \quad f(x) = \begin{cases} x \sin\left(\frac{1}{x}\right), & x \neq 0 \\ 0, & x = 0 \end{cases}$$

stetig auf ganz $\mathbb{R}$.

**3. Nicht fortsetzbar:**
- $f(x) = \frac{1}{x}$: $\lim_{x \to 0} f(x)$ existiert nicht
- $f(x) = \frac{x}{|x|}$: $\lim_{x \to 0} f(x)$ existiert nicht
- $f(x) = \frac{1}{x^2}$: $\lim_{x \to 0} f(x) = \infty$ ist nicht endlich

---

## 📌 Zusammenfassung

| **Begriff** | **Definition/Eigenschaft** |
|------------|---------------------------|
| Grenzwert | $\lim_{x \to a} f(x) = c$ ⟺ Für alle Folgen $(x_n)$ mit $x_n \to a, x_n \neq a$ gilt $f(x_n) \to c$ |
| Linksseitiger Grenzwert | $\lim_{x \nearrow a} f(x) = c$ mit $x_n < a$ |
| Rechtsseitiger Grenzwert | $\lim_{x \searrow a} f(x) = c$ mit $x_n > a$ |
| Stetigkeit | $\lim_{x \to a} f(x) = f(a)$ |
| Stetige Fortsetzung | Wenn $\lim_{x \to a} f(x) = c$ existiert, kann $f$ stetig fortgesetzt werden |

**Wichtige stetige Funktionen:**
- Polynome
- Wurzelfunktionen
- Rationale Funktionen (auf ihrem Definitionsbereich)
- Absolutbetrag
- Elementare Funktionen: $\exp, \ln, \sin, \cos, \tan$

**Typen von Unstetigkeiten:**
- **Hebbare Polstelle:** Grenzwert existiert und ist endlich
- **Nicht hebbare Polstelle:** Grenzwert ist $\pm\infty$
- **Sprungstelle:** Links- und rechtsseitiger Grenzwert verschieden
- **Oszillation:** Grenzwert existiert nicht wegen Schwingungen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.06 Elementare Funktionen 1]]: Elementare Funktionen sind stetig
- [[VL.20 Sätze über stetige Funktionen]]: Zwischenwertsatz, Extremwertsatz
- [[VL.21 Differenzierbarkeit]]: Differenzierbarkeit impliziert Stetigkeit


