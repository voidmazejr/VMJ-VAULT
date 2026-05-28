**Class:** [[AnaLina]]  
**Date:** 10-01-2026 
**Topics:** #Taylor #Taylorpolynom #Restglied #LagrangeRestglied #ExtremwertkriteriumHöhereAbleitungen

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung verallgemeinert die lineare Approximation zu Polynomen höherer Ordnung und wendet dies auf Extremwertprobleme an.

- **Taylorpolynom** als Approximation durch Polynome
- **Satz von Taylor** (Taylorformel) mit Restglied
- **Lagrange-Restglied** zur Fehlerabschätzung
- **Hinreichendes Extremwertkriterium** mit höheren Ableitungen
- Berechnung von Taylorpolynomen für $e^x$, $\sin(x)$, $\cos(x)$

---

## 1. Motivation: Von der Tangente zum Polynom

### Erinnerung: Lineare Approximation

Aus [[VL.21 Differenzierbarkeit]] wissen wir:

Eine differenzierbare Funktion kann durch ihre **Tangente** approximiert werden:
$$f(x) \approx f(x_0) + f'(x_0)(x - x_0)$$

Dies ist ein Polynom vom Grad $\leq 1$ mit:
- $p(x_0) = f(x_0)$
- $p'(x_0) = f'(x_0)$

Der Fehler $R(x) = f(x) - p(x)$ wird **schneller klein als linear**:
$$\lim_{x \to x_0} \frac{R(x)}{x - x_0} = 0$$

### Idee der Taylor-Approximation

**Hoffnung:** Durch Hinzunahme **weiterer Ableitungen** erhalten wir eine **bessere Approximation**.

Ist $f$ dann $n$-mal differenzierbar, approximieren wir $f$ durch ein Polynom
$$p(x) = a_0 + a_1(x - x_0) + a_2(x - x_0)^2 + \ldots + a_n(x - x_0)^n$$

vom Grad $\leq n$ mit der Eigenschaft:
$$p^{(k)}(x_0) = f^{(k)}(x_0), \quad k = 0, 1, \ldots, n$$

Die **ersten $n$ Ableitungen** von $p$ und $f$ sollen in $x_0$ übereinstimmen!

### Bestimmung der Koeffizienten

Ableiten ergibt:
$$\begin{align}
p(x) &= a_0 + a_1(x - x_0) + a_2(x - x_0)^2 + \ldots + a_n(x - x_0)^n \\
p'(x) &= a_1 + 2a_2(x - x_0) + 3a_3(x - x_0)^2 + \ldots + na_n(x - x_0)^{n-1} \\
p''(x) &= 2!a_2 + 3 \cdot 2a_3(x - x_0) + \ldots + n(n-1)a_n(x - x_0)^{n-2} \\
p'''(x) &= 3!a_3 + \ldots + n(n-1)(n-2)a_n(x - x_0)^{n-3} \\
&\vdots \\
p^{(n)}(x) &= n!a_n
\end{align}$$

Einsetzen von $x = x_0$:
$$p^{(k)}(x_0) = k! \cdot a_k$$

Mit $f^{(k)}(x_0) = p^{(k)}(x_0)$ folgt:
$$\boxed{a_k = \frac{f^{(k)}(x_0)}{k!}}$$

Die Koeffizienten sind **eindeutig bestimmt**!

---

## 2. Taylorpolynom

### Definition (Taylorpolynom)

Sei $f : D \to \mathbb{R}$ **n-mal differenzierbar** und sei $x_0 \in D$. Dann heißt

$$\boxed{T_n(x) = \sum_{k=0}^{n} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k}$$

das **n-te Taylorpolynom** von $f$ im **Entwicklungspunkt** $x_0$.

**Ausgeschrieben:**
$$T_n(x) = f(x_0) + f'(x_0)(x - x_0) + \frac{f''(x_0)}{2!}(x - x_0)^2 + \ldots + \frac{f^{(n)}(x_0)}{n!}(x - x_0)^n$$

### Restglied (Fehler)

Im Allgemeinen ist $f \neq T_n$. Wir schreiben:
$$f(x) = T_n(x) + R_n(x)$$

mit dem **Restglied** (oder **Fehler**):
$$R_n(x) = f(x) - T_n(x)$$

Das Restglied misst den **Abstand** zwischen $f$ und $T_n$ im Punkt $x$.

**Zentrale Frage:** Wie gut approximiert $T_n$ die Funktion $f$? Wie klein ist $R_n$?

---

## 3. Satz von Taylor (Taylorformel)

### Satz (Taylorformel)

Sei $f : I \to \mathbb{R}$ **n-mal differenzierbar** im Intervall $I$, und sei $x_0 \in I$. Dann gilt:

$$\boxed{f(x) = T_n(x) + R_n(x) = \sum_{k=0}^{n} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k + R_n(x)}$$

mit

$$\lim_{x \to x_0} \frac{R_n(x)}{(x - x_0)^n} = 0$$

**Interpretation:** Der Fehler $R_n(x)$ geht für $x \to x_0$ **sehr schnell** gegen $0$ (schneller als $(x - x_0)^n$).

### Lagrange-Restglied

Ist $f$ sogar **(n+1)-mal differenzierbar**, so kann man das Restglied auch schreiben als:

$$\boxed{R_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}(x - x_0)^{n+1}}$$

mit einem $\xi$ **zwischen** $x$ und $x_0$ (d.h. $\xi \in \,]x, x_0[ \,\cup \,]x_0, x[$).

**Wichtig:** Das sieht aus wie der **nächste Summand** im Taylorpolynom, nur dass das Argument der Ableitung die **Zwischenstelle** $\xi$ statt $x_0$ ist!

### Bemerkungen

1. **Polynome:** Für ein Polynom $f$ vom Grad $n$ gilt $f(x) = T_n(x)$, d.h. $f$ stimmt mit seinem Taylorpolynom überein (da $f^{(n+1)}(x) = 0$ und somit $R_n(x) = 0$).

2. **Charakterisierung von Polynomen:** Ist $f$ eine Funktion mit $f^{(n+1)}(x) = 0$ für alle $x \in I$, so ist $R_n(x) = 0$ und $f(x) = T_n(x)$ ist ein Polynom vom Grad höchstens $n$.

3. **Lage von** $\xi$: Die Stelle $\xi$ im Lagrange-Restglied ist im Allgemeinen **unbekannt**, aber sie liegt zwischen $x_0$ und $x$.

---

## 4. Beispiele: Taylorpolynome

### Beispiel 1: Exponentialfunktion $e^x$

**Gegeben:** $f(x) = e^x$ mit Entwicklungspunkt $x_0 = 0$

**Ableitungen:**
$$f^{(k)}(x) = e^x \quad \text{für alle } k \in \mathbb{N}$$

Also: $f^{(k)}(0) = e^0 = 1$ für alle $k$

**Taylorpolynom n-ter Ordnung:**
$$T_n(x) = \sum_{k=0}^{n} \frac{1}{k!}x^k = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \ldots + \frac{x^n}{n!}$$

**Restglied:**
$$R_n(x) = \frac{e^\xi}{(n+1)!}x^{n+1}$$

wobei $\xi$ zwischen $0$ und $x$ liegt.

**Spezielle Taylorpolynome:**
- $T_0(x) = 1$
- $T_1(x) = 1 + x$
- $T_2(x) = 1 + x + \frac{x^2}{2}$
- $T_3(x) = 1 + x + \frac{x^2}{2} + \frac{x^3}{6}$

### Beispiel 2: Sinusfunktion $\sin(x)$

**Gegeben:** $f(x) = \sin(x)$ mit Entwicklungspunkt $x_0 = 0$

**Ableitungen:**
$$\begin{align}
f'(x) &= \cos(x) \\
f''(x) &= -\sin(x) \\
f'''(x) &= -\cos(x) \\
f^{(4)}(x) &= \sin(x) = f(x)
\end{align}$$

Die Ableitungen sind **periodisch** mit Periode 4.

**Muster:**
$$\sin^{(2k)}(x) = (-1)^k\sin(x) \quad \text{und} \quad \sin^{(2k+1)}(x) = (-1)^k\cos(x)$$

Im Entwicklungspunkt $x_0 = 0$:
$$\sin^{(2k)}(0) = 0 \quad \text{und} \quad \sin^{(2k+1)}(0) = (-1)^k$$

**Taylorpolynom:**

Die **geraden Potenzen fallen weg**! Es gilt:
$$T_{2n+1}(x) = T_{2n+2}(x) = \sum_{k=0}^{n} \frac{(-1)^k}{(2k+1)!}x^{2k+1}$$

**Spezielle Taylorpolynome:**
- $T_1(x) = x$
- $T_3(x) = x - \frac{x^3}{3!} = x - \frac{x^3}{6}$
- $T_5(x) = x - \frac{x^3}{6} + \frac{x^5}{120}$
- $T_7(x) = x - \frac{x^3}{6} + \frac{x^5}{120} - \frac{x^7}{5040}$

### Beispiel 3: Kosinusfunktion $\cos(x)$

**Gegeben:** $f(x) = \cos(x)$ mit Entwicklungspunkt $x_0 = 0$

Analog zu $\sin(x)$ erhält man:
$$\cos^{(2k)}(0) = (-1)^k \quad \text{und} \quad \cos^{(2k+1)}(0) = 0$$

Die **ungeraden Potenzen fallen weg**!

**Taylorpolynom:**
$$T_{2n}(x) = T_{2n+1}(x) = \sum_{k=0}^{n} \frac{(-1)^k}{(2k)!}x^{2k}$$

**Spezielle Taylorpolynome:**
- $T_0(x) = 1$
- $T_2(x) = 1 - \frac{x^2}{2}$
- $T_4(x) = 1 - \frac{x^2}{2} + \frac{x^4}{24}$
- $T_6(x) = 1 - \frac{x^2}{2} + \frac{x^4}{24} - \frac{x^6}{720}$

---

## 5. Hinreichendes Extremwertkriterium mit höheren Ableitungen

### Erinnerung: Kriterium mit zweiter Ableitung

Aus [[VL.23 Mittelwertsatz]]:

Sei $f$ auf $[a, b]$ zweimal differenzierbar mit $f'(x_0) = 0$ für $x_0 \in \,]a, b[$. Dann:

1. Wenn $f''(x_0) > 0$, dann hat $f$ in $x_0$ ein **lokales Minimum**
2. Wenn $f''(x_0) < 0$, dann hat $f$ in $x_0$ ein **lokales Maximum**

### Problem: Was wenn auch $f''(x_0) = 0$?

**Beispiel:** $f(x) = x^4$ in $x_0 = 0$
- $f'(0) = 0$ ✓
- $f''(0) = 0$ (keine Aussage!)
- Aber: $f$ hat in $x_0 = 0$ ein **globales Minimum**!

**Lösung:** Untersuche **höhere Ableitungen**!

### Satz (Hinreichendes Extremwertkriterium)

Sei $f : I \to \mathbb{R}$ eine **n-mal differenzierbare** Funktion und sei $x_0$ ein **innerer Punkt** von $I$. Es gelte:

$$f'(x_0) = f''(x_0) = \ldots = f^{(n-1)}(x_0) = 0 \quad \text{und} \quad f^{(n)}(x_0) \neq 0$$

Dann gilt:

**1. n ungerade:** $f$ hat in $x_0$ **kein lokales Extremum**

**2. n gerade:** $f$ hat in $x_0$ ein **lokales Extremum:**
- Ist $f^{(n)}(x_0) < 0$, so hat $f$ ein **lokales Maximum**
- Ist $f^{(n)}(x_0) > 0$, so hat $f$ ein **lokales Minimum**

### Spezialfälle

- **n = 1:** Punkte mit $f'(x_0) \neq 0$ sind keine Extremstellen (bekannt)
- **n = 2:** Dies ist das Kriterium mit der zweiten Ableitung (bekannt)

### Beweis-Idee

Mit der Taylorformel:
$$f(x) = \sum_{k=0}^{n} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k + R_n(x)$$

Da $f'(x_0) = \ldots = f^{(n-1)}(x_0) = 0$:
$$f(x) = f(x_0) + \frac{f^{(n)}(x_0)}{n!}(x - x_0)^n + R_n(x)$$

Also:
$$f(x) = f(x_0) + (x - x_0)^n \left[\underbrace{\frac{f^{(n)}(x_0)}{n!}}_{\neq 0} + \underbrace{\frac{R_n(x)}{(x - x_0)^n}}_{\to 0 \text{ für } x \to x_0}\right]$$

Der Term in Klammern hat nahe genug bei $x_0$ das **gleiche Vorzeichen** wie $\frac{f^{(n)}(x_0)}{n!}$.

**Fall 1: n ungerade**
- $(x - x_0)^n$ **wechselt das Vorzeichen** in $x_0$
- $\Rightarrow$ $f(x)$ ist einmal kleiner und einmal größer als $f(x_0)$
- $\Rightarrow$ **Kein Extremum**

**Fall 2: n gerade**
- $(x - x_0)^n \geq 0$ für alle $x$
- Ist $f^{(n)}(x_0) > 0$: Term $> 0$ $\Rightarrow$ $f(x) \geq f(x_0)$ $\Rightarrow$ **Minimum**
- Ist $f^{(n)}(x_0) < 0$: Term $< 0$ $\Rightarrow$ $f(x) \leq f(x_0)$ $\Rightarrow$ **Maximum**

---

## 6. Beispiele: Extremwertbestimmung

### Beispiel 1: $f(x) = x^3 - 3x$ auf $[-\frac{3}{2}, 3]$

**Schritt 1: Kritische Punkte**
$$f'(x) = 3x^2 - 3 = 3(x^2 - 1) = 3(x-1)(x+1)$$

Nullstellen: $x = -1$ und $x = 1$

**Schritt 2: Zweite Ableitung**
$$f''(x) = 6x$$

**Test:**
- $f''(-1) = -6 < 0$ $\Rightarrow$ **lokales Maximum** mit $f(-1) = 2$
- $f''(1) = 6 > 0$ $\Rightarrow$ **lokales Minimum** mit $f(1) = -2$

**Schritt 3: Randpunkte**
- $f'(-\frac{3}{2}) = 3(\frac{9}{4} - 1) = \frac{15}{4} > 0$ $\Rightarrow$ monoton wachsend nahe $-\frac{3}{2}$
  - **Lokales Minimum** mit $f(-\frac{3}{2}) = -\frac{9}{8}$
- $f'(3) = 3(9 - 1) = 24 > 0$ $\Rightarrow$ monoton wachsend nahe $3$
  - **Lokales Maximum** mit $f(3) = 18$

**Ergebnis:**
- **Globales Maximum:** $f(3) = 18$
- **Globales Minimum:** $f(1) = -2$

### Beispiel 2: $f(x) = x^2 + \cos(x)$ in $x = 0$

**Ableitungen:**
$$\begin{align}
f'(x) &= 2x - \sin(x) &\Rightarrow f'(0) &= 0 \\
f''(x) &= 2 - \cos(x) &\Rightarrow f''(0) &= 1 > 0
\end{align}$$

**Ergebnis:** $f$ hat in $x = 0$ ein **lokales Minimum**

### Beispiel 3: $f(x) = \sin(x) - x$ in $x = 0$

**Ableitungen:**
$$\begin{align}
f'(x) &= \cos(x) - 1 &\Rightarrow f'(0) &= 0 \\
f''(x) &= -\sin(x) &\Rightarrow f''(0) &= 0 \\
f'''(x) &= -\cos(x) &\Rightarrow f'''(0) &= -1 \neq 0
\end{align}$$

**Analyse:** $n = 3$ ist **ungerade** und $f'''(0) \neq 0$

**Ergebnis:** $f$ hat in $x = 0$ **kein lokales Extremum**

### Beispiel 4: $f(x) = x^4$ in $x = 0$

**Ableitungen:**
$$\begin{align}
f'(x) &= 4x^3 &\Rightarrow f'(0) &= 0 \\
f''(x) &= 12x^2 &\Rightarrow f''(0) &= 0 \\
f'''(x) &= 24x &\Rightarrow f'''(0) &= 0 \\
f^{(4)}(x) &= 24 &\Rightarrow f^{(4)}(0) &= 24 > 0
\end{align}$$

**Analyse:** $n = 4$ ist **gerade** und $f^{(4)}(0) > 0$

**Ergebnis:** $f$ hat in $x = 0$ ein **lokales (und globales) Minimum**

---

## 📌 Zusammenfassung

### Taylorpolynom

$$T_n(x) = \sum_{k=0}^{n} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k$$

**Spezielle Taylorpolynome (um $x_0 = 0$):**

| **Funktion** | **Taylorpolynom** |
|-------------|-------------------|
| $e^x$ | $1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \ldots + \frac{x^n}{n!}$ |
| $\sin(x)$ | $x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \ldots$ |
| $\cos(x)$ | $1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \ldots$ |

### Restglied

**Lagrange-Form:**
$$R_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}(x - x_0)^{n+1}$$

mit $\xi$ zwischen $x$ und $x_0$

### Extremwertkriterium mit höheren Ableitungen

Sei $f'(x_0) = \ldots = f^{(n-1)}(x_0) = 0$ und $f^{(n)}(x_0) \neq 0$:

| **n** | **Extremum?** | **Art** |
|-------|---------------|---------|
| ungerade | ❌ Kein Extremum | — |
| gerade, $f^{(n)}(x_0) > 0$ | ✅ Extremum | Minimum |
| gerade, $f^{(n)}(x_0) < 0$ | ✅ Extremum | Maximum |

### Praktische Vorgehensweise

1. **Taylorpolynom berechnen:**
   - Bestimme $f^{(k)}(x_0)$ für $k = 0, 1, \ldots, n$
   - Setze in Formel ein

2. **Extremwertbestimmung:**
   - Finde kritische Punkte: $f'(x) = 0$
   - Teste zweite Ableitung
   - Falls $f''(x_0) = 0$: Teste höhere Ableitungen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.21 Differenzierbarkeit]]: Lineare Approximation als $T_1$
- [[VL.22 Anwendung Differenzierbarkeit]]: Höhere Ableitungen
- [[VL.23 Mittelwertsatz]]: Extremwertkriterium mit erster Ableitung
- [[VL.25 Anwendung Taylor-Approximation]]: Konvergenz und Taylorreihen
- [[VL.26 Elementare Funktionen 2]]: Reihendarstellung von exp, sin, cos

