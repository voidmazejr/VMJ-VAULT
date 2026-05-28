**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Umkehrfunktion #NewtonVerfahren #HöhereAbleitungen #LHospital #Logarithmus

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung zeigt wichtige Anwendungen der Differenzierbarkeit und führt neue Werkzeuge ein.

- **Ableitung der Umkehrfunktion** und Anwendungen (ln, Wurzeln)
- **Newton-Verfahren** zur numerischen Nullstellenberechnung
- **Höhere Ableitungen** und ihre Interpretation
- **Regel von Bernoulli/de l'Hospital** für Grenzwerte

---

## 1. Ableitung der Umkehrfunktion

### Satz (Ableitung der Umkehrfunktion)

Seien $I$ und $J$ Intervalle. Sei $f : I \to J$ differenzierbar und umkehrbar mit $f'(x) \neq 0$ für $x \in I$. 

Dann ist auch $f^{-1} : J \to I$ differenzierbar mit

$$(f^{-1})'(x) = \frac{1}{f'(f^{-1}(x))}$$

### Beweis der Formel (nicht der Differenzierbarkeit)

Aus $x = f(f^{-1}(x))$ folgt durch Differentiation mit der Kettenregel:

$$1 = f'(f^{-1}(x)) \cdot (f^{-1})'(x)$$

Also:
$$(f^{-1})'(x) = \frac{1}{f'(f^{-1}(x))}$$

**Wichtig:** Die Differenzierbarkeit von $f^{-1}$ folgt bereits aus den Voraussetzungen (der Beweis ist nicht trivial).

### Anwendung 1: Ableitung des natürlichen Logarithmus

Der natürliche Logarithmus $\ln : \,]0, \infty[ \to \mathbb{R}$ ist die Umkehrfunktion von $\exp : \mathbb{R} \to \,]0, \infty[$.

Es gilt: $\exp'(x) = \exp(x)$

Mit der Formel für die Umkehrfunktion:

$$\ln'(x) = \frac{1}{\exp'(\ln(x))} = \frac{1}{\exp(\ln(x))} = \frac{1}{x}$$

**Ergebnis:**
$$\boxed{\ln'(x) = \frac{1}{x}}$$

### Anwendung 2: Ableitung der n-ten Wurzel

Die Funktion $f : \,]0, \infty[ \to \,]0, \infty[, x \mapsto x^n$ hat die Ableitung $f'(x) = nx^{n-1}$.

Ihre Inverse ist die $n$-te Wurzel: $f^{-1}(x) = \sqrt[n]{x}$

$$(\sqrt[n]{x})' = \frac{1}{f'(\sqrt[n]{x})} = \frac{1}{n(\sqrt[n]{x})^{n-1}} = \frac{1}{n\sqrt[n]{x^{n-1}}}$$

**Spezialfall für die Quadratwurzel** ($n = 2$):

$$\boxed{(\sqrt{x})' = \frac{1}{2\sqrt{x}}}$$

**Wichtig:** Die $n$-te Wurzel ist in $x = 0$ **nicht differenzierbar**, aber stetig.

---

## 2. Newton-Verfahren

### Idee

Das Newton-Verfahren (auch Newton-Raphson-Verfahren) approximiert eine Nullstelle von $f$ durch iterative lineare Approximation.

**Konstruktion:**
1. Wähle Startwert $x_0$ "nahe" der gesuchten Nullstelle $x^*$
2. Approximiere $f$ in $x_n$ durch ihre Tangente:
   $$f(x) \approx f(x_n) + f'(x_n)(x - x_n)$$
3. Bestimme $x_{n+1}$ als Nullstelle der Tangente:
   $$f(x_n) + f'(x_n)(x_{n+1} - x_n) = 0$$

### Iterationsformel

Auflösen nach $x_{n+1}$ ergibt:

$$\boxed{x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}, \quad n = 0, 1, 2, 3, \ldots}$$

### Voraussetzungen

- $f'(x_n) \neq 0$ für alle $n$
- $f'(x^*) \neq 0$ (einfache Nullstelle)
- Startwert $x_0$ "nahe genug" an $x^*$

Unter gewissen Voraussetzungen konvergiert $(x_n)_n$ gegen eine Nullstelle von $f$.

### Beispiel: Wurzelfunktion

Gesucht: Nullstelle von $f(x) = x^2 - a$ (für $a > 0$)

**Nullstellen:** $\pm\sqrt{a}$

**Ableitung:** $f'(x) = 2x$

**Newton-Iteration:**
$$x_{n+1} = x_n - \frac{x_n^2 - a}{2x_n} = \frac{x_n^2 + a}{2x_n} = \frac{1}{2}\left(x_n + \frac{a}{x_n}\right)$$

Dies ist **exakt die Wurzelfolge** aus [[VL.18 Berechnung von Grenzwerten]]!

### Numerisches Beispiel: $\sqrt{3}$

Sei $a = 3$ mit Startwert $x_0 = 2$:

$$x_1 = \frac{1}{2}\left(2 + \frac{3}{2}\right) = 1 + \frac{3}{4} = 1.75$$

Weitere Iterationen:

| $n$ | $x_n$ | Korrekte Stellen |
|-----|-------|------------------|
| 0 | 2.000000000000000 | — |
| 1 | 1.750000000000000 | 1 |
| 2 | 1.732142857142857 | 3 |
| 3 | 1.732050810014727 | 6 |
| 4 | 1.732050807568877 | **15** |

**Vergleich mit $\sqrt{3} = 1.732050807568877...$**

Nach nur 4 Schritten sind 15 Nachkommastellen korrekt! Das Newton-Verfahren konvergiert **quadratisch** (deutlich schneller als Bisektion).

---

## 3. Höhere Ableitungen

### Definition (k-te Ableitung)

Ist $f : \mathbb{R} \supseteq D \to \mathbb{R}$ auf ganz $D$ differenzierbar, so ist $f' : D \to \mathbb{R}$ wieder eine Funktion.

Wir definieren die **k-te Ableitung** per Induktion:

$$f^{(0)} := f, \quad f^{(k)} := (f^{(k-1)})' \quad \text{für } k \geq 1$$

**Notation:**
- $f^{(0)} = f$ (0-te Ableitung = Funktion selbst)
- $f^{(1)} = f'$ (erste Ableitung)
- $f^{(2)} = (f')' = f''$ (zweite Ableitung)
- $f^{(3)} = f'''$ (dritte Ableitung)
- $f^{(k)}$ für $k \geq 4$

**Alternative Schreibweise:**
$$\frac{d^k f}{dx^k} := f^{(k)}$$

Für $k = 1$ schreiben wir nur $\frac{df}{dx}$.

**Wichtig:** Die Ordnung wird in **runden Klammern** geschrieben, um Missverständnisse zu vermeiden!

### Interpretation der zweiten Ableitung

**1. Geometrische Interpretation:**

$f''(x)$ beschreibt die **Krümmung** des Funktionsgraphen von $f$ in $x$.

- $f''(x) > 0$: Graph ist **konvex** (nach oben gekrümmt)
- $f''(x) < 0$: Graph ist **konkav** (nach unten gekrümmt)
- $f''(x) = 0$ und Vorzeichenwechsel: **Wendepunkt**

**2. Physikalische Interpretation:**

$$\begin{align}
s(t) &: \text{Weg (Position)} \\
s'(t) &: \text{Geschwindigkeit} \\
s''(t) &: \text{Beschleunigung}
\end{align}$$

### Wichtige Bemerkung

⚠️ **Nicht jede differenzierbare Funktion ist auch zweimal differenzierbar!**

### Beispiel: Einmal, aber nicht zweimal differenzierbar

$$f : \mathbb{R} \to \mathbb{R}, \quad f(x) = \begin{cases} x^2, & x \geq 0 \\ -x^2, & x < 0 \end{cases}$$

Das ist $f(x) = x|x|$.

**Erste Ableitung:**
$$f'(x) = \begin{cases} 2x, & x \geq 0 \\ -2x, & x < 0 \end{cases} = 2|x|$$

$f$ ist differenzierbar auf ganz $\mathbb{R}$.

**Zweite Ableitung:**

$f'(x) = 2|x|$ ist in $x = 0$ **nicht differenzierbar** (Knick bei 0).

---

## 4. Regel von Bernoulli/de l'Hospital

### Satz (Regel von l'Hospital)

Seien $f, g : \,]a, b[ \to \mathbb{R}$ differenzierbar, wobei $-\infty \leq a < b \leq \infty$. 

Weiter gelte **eine** der folgenden Bedingungen:
1. $\lim_{x \to b} f(x) = \lim_{x \to b} g(x) = 0$ (Typ "$\frac{0}{0}$")
2. $\lim_{x \to b} g(x) \in \{-\infty, \infty\}$ (Typ "$\frac{\text{beliebig}}{\infty}$")

Falls 
$$\lim_{x \to b} \frac{f'(x)}{g'(x)} \in \mathbb{R} \cup \{-\infty, \infty\}$$

existiert (und $g'(x) \neq 0$ für alle $x$ nahe $b$), dann ist

$$\boxed{\lim_{x \to b} \frac{f(x)}{g(x)} = \lim_{x \to b} \frac{f'(x)}{g'(x)}}$$

Gleiches gilt für Grenzwerte $x \to a$.

### Wichtige Bemerkungen

1. **Mehrfache Anwendung:** Man kann die Regel von l'Hospital oft mehrfach hintereinander anwenden, falls der Grenzwert $\lim_{x \to b} \frac{f'(x)}{g'(x)}$ wieder vom Typ "$\frac{0}{0}$" oder "$\frac{\ast}{\infty}$" ist.

2. **Umformung bei** "$0 \cdot \infty$": Bei Produkten "$0 \cdot \infty$" kann man umformen:
   $$f(x) \cdot g(x) = \frac{f(x)}{\frac{1}{g(x)}}$$
   und dann l'Hospital anwenden.

3. **Vorsicht:** Existiert $\lim_{x \to b} \frac{f'(x)}{g'(x)}$ nicht, heißt das **nicht**, dass auch $\lim_{x \to b} \frac{f(x)}{g(x)}$ nicht existiert!

---

## 5. Beispiele zur Regel von l'Hospital

### Beispiel 1: Bekannter Grenzwert

$$\lim_{x \to 0} \frac{\sin(x)}{x}$$

**Typ:** "$\frac{0}{0}$" (da $\sin(0) = 0$ und $0 = 0$)

**Anwendung:**
$$\lim_{x \to 0} \frac{\sin(x)}{x} = \lim_{x \to 0} \frac{\sin'(x)}{(x)'} = \lim_{x \to 0} \frac{\cos(x)}{1} = 1$$

### Beispiel 2: Nicht anwendbar!

$$\lim_{x \to \infty} \frac{\sin(x)}{x}$$

**Typ:** "$\frac{\text{oszilliert}}{\infty}$"

**Problem:** 
$$\lim_{x \to \infty} \frac{\sin'(x)}{(x)'} = \lim_{x \to \infty} \frac{\cos(x)}{1} = \lim_{x \to \infty} \cos(x)$$
existiert nicht!

**Aber:** Der ursprüngliche Grenzwert existiert! Da $|\sin(x)| \leq 1$ und $\frac{1}{x} \to 0$:
$$\lim_{x \to \infty} \frac{\sin(x)}{x} = 0$$

→ Regel von l'Hospital ist **nicht anwendbar**, aber der Grenzwert existiert trotzdem!

### Beispiel 3: Zweimalige Anwendung

$$\lim_{x \to 0} \frac{1 - \cos(x)}{x^2}$$

**Typ:** "$\frac{0}{0}$"

**Erste Anwendung:**
$$\lim_{x \to 0} \frac{1 - \cos(x)}{x^2} = \lim_{x \to 0} \frac{(1 - \cos(x))'}{(x^2)'} = \lim_{x \to 0} \frac{\sin(x)}{2x}$$

Wieder Typ "$\frac{0}{0}$"!

**Zweite Anwendung:**
$$\lim_{x \to 0} \frac{\sin(x)}{2x} = \lim_{x \to 0} \frac{\sin'(x)}{(2x)'} = \lim_{x \to 0} \frac{\cos(x)}{2} = \frac{1}{2}$$

**Ergebnis:**
$$\lim_{x \to 0} \frac{1 - \cos(x)}{x^2} = \frac{1}{2}$$

### Beispiel 4: Umformung bei "$0 \cdot \infty$"

$$\lim_{x \to 0} x \ln(x)$$

**Typ:** "$0 \cdot (-\infty)$" (nicht direkt anwendbar!)

**Umformung:**
$$x \ln(x) = \frac{\ln(x)}{\frac{1}{x}}$$

Jetzt Typ "$\frac{-\infty}{\infty}$"

**Anwendung:**
$$\lim_{x \to 0} \frac{\ln(x)}{\frac{1}{x}} = \lim_{x \to 0} \frac{(\ln(x))'}{(\frac{1}{x})'} = \lim_{x \to 0} \frac{\frac{1}{x}}{-\frac{1}{x^2}} = \lim_{x \to 0} \frac{x^2}{-x} = \lim_{x \to 0} (-x) = 0$$

**Ergebnis:**
$$\lim_{x \to 0} x \ln(x) = 0$$

### Beispiel 5: Allgemeine Exponentialfolge

Zeige: $\lim_{n \to \infty} \left(1 + \frac{a}{n}\right)^n = e^a$ für $a \in \mathbb{R}$

**Trick:** Verwende $\exp$ und $\ln$:
$$\left(1 + \frac{a}{n}\right)^n = \exp\left(n \ln\left(1 + \frac{a}{n}\right)\right)$$

Da $\exp$ stetig:
$$\lim_{n \to \infty} \left(1 + \frac{a}{n}\right)^n = \exp\left(\lim_{n \to \infty} n \ln\left(1 + \frac{a}{n}\right)\right)$$

**Grenzwert berechnen** (ersetze $n \in \mathbb{N}$ durch $x \in \mathbb{R}$):
$$\lim_{x \to \infty} x \ln\left(1 + \frac{a}{x}\right) = \lim_{x \to \infty} \frac{\ln\left(1 + \frac{a}{x}\right)}{\frac{1}{x}}$$

**Typ:** "$\frac{0}{0}$"

**Anwendung l'Hospital:**
$$\lim_{x \to \infty} \frac{\frac{1}{1 + \frac{a}{x}} \cdot \left(-\frac{a}{x^2}\right)}{-\frac{1}{x^2}} = \lim_{x \to \infty} \frac{a}{1 + \frac{a}{x}} = a$$

**Ergebnis:**
$$\lim_{n \to \infty} \left(1 + \frac{a}{n}\right)^n = \exp(a) = e^a$$

---

## 📌 Zusammenfassung

### Wichtige Formeln

| **Funktion/Regel** | **Ableitung/Formel** |
|-------------------|---------------------|
| Umkehrfunktion | $(f^{-1})'(x) = \frac{1}{f'(f^{-1}(x))}$ |
| $\ln(x)$ | $\ln'(x) = \frac{1}{x}$ |
| $\sqrt{x}$ | $(\sqrt{x})' = \frac{1}{2\sqrt{x}}$ |
| $\sqrt[n]{x}$ | $(\sqrt[n]{x})' = \frac{1}{n\sqrt[n]{x^{n-1}}}$ |
| Newton-Verfahren | $x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$ |
| k-te Ableitung | $f^{(k)} = (f^{(k-1)})'$ |
| l'Hospital | $\lim_{x \to b} \frac{f(x)}{g(x)} = \lim_{x \to b} \frac{f'(x)}{g'(x)}$ |

### Physikalische Interpretation

$$\begin{align}
f(t) &: \text{Position/Weg} \\
f'(t) &: \text{Geschwindigkeit} \\
f''(t) &: \text{Beschleunigung} \\
f'''(t) &: \text{Ruck (rate of change of acceleration)}
\end{align}$$

### Wann ist l'Hospital anwendbar?

✅ **Anwendbar bei:**
- Typ "$\frac{0}{0}$": Zähler und Nenner gehen gegen 0
- Typ "$\frac{\ast}{\infty}$": Nenner geht gegen $\pm\infty$

✅ **Nach Umformung bei:**
- Typ "$0 \cdot \infty$": Schreibe als $\frac{f}{\frac{1}{g}}$

❌ **Nicht anwendbar bei:**
- $\frac{\text{konst}}{\infty} = 0$ (direkt ablesen!)
- $\frac{\infty}{\text{konst}} = \infty$ (direkt ablesen!)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.18 Berechnung von Grenzwerten]]: Wurzelfolge ist Spezialfall des Newton-Verfahrens
- [[VL.20 Sätze über stetige Funktionen]]: Bisektionsverfahren (langsamer als Newton)
- [[VL.21 Differenzierbarkeit]]: Grundlagen der Ableitung
- [[VL.23 Mittelwertsatz]]: Beweis der Regel von l'Hospital
- [[VL.24 Taylor-Approximation]]: Höhere Ableitungen für Taylor-Polynome
- [[VL.26 Elementare Funktionen 2]]: Ableitung von $\exp(x)$
