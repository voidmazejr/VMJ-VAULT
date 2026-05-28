**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Zwischenwertsatz #Nullstellensatz #Extremwerte #Supremum #Infimum #Bisektionsverfahren

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt die fundamentalen Sätze über stetige Funktionen, insbesondere die Existenz von Nullstellen und Extremwerten.

- **Nullstellensatz von Bolzano** und seine Anwendung
- **Zwischenwertsatz** als Verallgemeinerung
- **Intervallhalbierungsverfahren** (Bisektionsverfahren) zur numerischen Nullstellenberechnung
- Definitionen von **Maximum, Minimum, Supremum und Infimum**
- **Satz vom Minimum und Maximum** für stetige Funktionen

---

## 1. Nullstellensatz von Bolzano

### Satz (Nullstellensatz von Bolzano)

Sei $f : I \to \mathbb{R}$ stetig auf einem Intervall $I \subseteq \mathbb{R}$. Sind dann $a, b \in I$ mit $a < b$ und

- $f(a) < 0$ und $f(b) > 0$ (oder umgekehrt $f(a) > 0$ und $f(b) < 0$),

dann hat $f$ **mindestens eine Nullstelle** in $\,]a, b[$.

### Grafische Interpretation

Wenn eine stetige Funktion auf einem Intervall das Vorzeichen wechselt, muss sie die $x$-Achse schneiden.

**Wichtig:** Der Definitionsbereich muss ein **Intervall** sein!

### Gegenbeispiel

$f : \mathbb{R} \setminus \{0\} \to \mathbb{R}, f(x) = \frac{1}{x}$

- $f(-1) = -1 < 0$ und $f(1) = 1 > 0$
- Aber: Keine Nullstelle, da $\mathbb{R} \setminus \{0\}$ **kein Intervall** ist!

---

## 2. Intervallhalbierungsverfahren (Bisektionsverfahren)

### Idee des Beweises

Das Intervallhalbierungsverfahren konstruiert zwei Folgen $(a_k)_k$ und $(b_k)_k$, die gegen eine Nullstelle konvergieren.

### Algorithmus

Gegeben: $f : [a, b] \to \mathbb{R}$ stetig mit $f(a) < 0$ und $f(b) > 0$

**Initialisierung:** $a_0 = a$, $b_0 = b$

**Iteration für** $k = 0, 1, 2, 3, \ldots$:

1. Berechne Mittelpunkt: $x_k = \frac{a_k + b_k}{2}$

2. Berechne $f(x_k)$ und entscheide:
   - Falls $f(x_k) = 0$: Nullstelle gefunden! ✓
   - Falls $f(x_k) < 0$: Setze $a_{k+1} = x_k$, $b_{k+1} = b_k$
   - Falls $f(x_k) > 0$: Setze $a_{k+1} = a_k$, $b_{k+1} = x_k$

### Eigenschaften

**Konvergenz der Folgen:**
- $(a_k)_k$ ist monoton wachsend und beschränkt
- $(b_k)_k$ ist monoton fallend und beschränkt
- Beide konvergieren gegen dieselbe Nullstelle $x^* \in [a, b]$

**Intervalllänge:**
$$b_k - a_k = \frac{b - a}{2^k}$$

**Fehlerabschätzung:**
$$|x_k - x^*| \leq \frac{b_k - a_k}{2} = \frac{b - a}{2^{k+1}}$$

Zu vorgegebener Genauigkeit $\varepsilon$ wähle $k$ so groß, dass $\frac{b - a}{2^{k+1}} < \varepsilon$.

### Beispiel: Berechnung von $\sqrt{2}$

Betrachte $f : [0, 2] \to \mathbb{R}, f(x) = x^2 - 2$

- $f(0) = -2 < 0$ und $f(2) = 2 > 0$
- Nullstelle ist $\sqrt{2} \approx 1.41421356...$

**Intervallhalbierung:**

| $k$ | $a_k$ | $b_k$ |
|-----|-------|-------|
| 0 | 0.0000000 | 2.0000000 |
| 1 | 1.0000000 | 2.0000000 |
| 2 | 1.0000000 | 1.5000000 |
| 3 | 1.2500000 | 1.5000000 |
| 4 | 1.3750000 | 1.5000000 |
| 5 | 1.3750000 | 1.4375000 |
| 10 | 1.4140625 | 1.4160156 |
| 20 | 1.4142132 | 1.4142151 |

Nach 20 Schritten: $x_{20} \approx 1.414214134$ (Fehler $\approx 5.7 \times 10^{-7}$)

**Vergleich:** Die Wurzelfolge aus [[VL.18 Berechnung von Grenzwerten]] konvergiert **deutlich schneller**:
- Nach 4 Iterationen bereits $x_4 = 1.4142135...$

---

## 3. Zwischenwertsatz

### Satz (Zwischenwertsatz, ZWS)

Sei $f : I \to \mathbb{R}$ stetig auf einem Intervall $I \subseteq \mathbb{R}$. Seien $a, b \in I$ und $c$ ein Wert zwischen $f(a)$ und $f(b)$. 

Dann gibt es **mindestens ein** $\xi \in [a, b]$ mit $f(\xi) = c$.

### Interpretation

Eine stetige Funktion $f : [a, b] \to \mathbb{R}$ nimmt **alle Werte** zwischen $f(a)$ und $f(b)$ an.

### Zusammenhang mit dem Nullstellensatz

Für $c = 0$ ist der Zwischenwertsatz genau der **Nullstellensatz von Bolzano**.

### Beweis-Skizze

Betrachte die Hilfsfunktion $g(x) = f(x) - c$:
- $g(a) = f(a) - c < 0$ (falls $f(a) < c < f(b)$)
- $g(b) = f(b) - c > 0$
- Nach Bolzano hat $g$ eine Nullstelle $\xi \in \,]a, b[$
- Also: $g(\xi) = 0 \iff f(\xi) = c$

---

## 4. Maximum und Minimum

### Definition (Maximum und Minimum)

Sei $f : D \to \mathbb{R}$ mit $D \subseteq \mathbb{R}$. Dann heißt $x_0 \in D$ eine

**1. Maximalstelle** (oder Stelle eines Maximums), wenn
$$f(x_0) \geq f(x) \quad \text{für alle } x \in D$$

Der Wert $f(x_0)$ heißt das **Maximum** von $f$.

**Bezeichnung:** $\max_{x \in D} f(x)$ oder $\max f$

**2. Minimalstelle** (oder Stelle eines Minimums), wenn
$$f(x_0) \leq f(x) \quad \text{für alle } x \in D$$

Der Wert $f(x_0)$ heißt das **Minimum** von $f$.

**Bezeichnung:** $\min_{x \in D} f(x)$ oder $\min f$

**Extremum:** Bezeichnet ein Maximum oder Minimum  
**Extremalstelle:** Zugehörige Maximal- oder Minimalstelle

**Plural:** Maxima, Minima, Extrema

### Wichtige Bemerkungen

- Es kann **mehrere** Maximal- oder Minimalstellen geben
- Es gibt aber immer nur **ein** Maximum und **ein** Minimum (falls existent)
- Nicht jede Funktion besitzt ein Maximum oder Minimum!

### Beispiele

**1. Existenz von Min und Max:** $f : [-2, 2] \to \mathbb{R}, f(x) = x^2 - 1$

- Maximum: $3$ bei den Maximalstellen $x = -2$ und $x = 2$
- Minimum: $-1$ bei der Minimalstelle $x = 0$

**2. Kein Maximum:** $f : [0, 1[ \to \mathbb{R}, f(x) = x$

- Minimum: $0$ bei $x = 0$
- Kein Maximum: Funktion nähert sich $1$ an, erreicht diesen Wert aber nicht

**3. Weder Min noch Max:** $f : \,]0, \infty[ \to \mathbb{R}, f(x) = \frac{1}{x}$

- $\lim_{x \searrow 0} f(x) = +\infty$ → kein Maximum
- $\lim_{x \to \infty} f(x) = 0$, aber $f(x) \neq 0$ für alle $x$ → kein Minimum

**4. Arcus Tangens:** $\arctan : \mathbb{R} \to \,]-\frac{\pi}{2}, \frac{\pi}{2}[$

- $\lim_{x \to +\infty} \arctan(x) = \frac{\pi}{2}$, aber dieser Wert wird nicht angenommen
- Weder Maximum noch Minimum

---

## 5. Infimum und Supremum

### Motivation

In den Beispielen nähert sich die Funktion oft einem Wert beliebig nahe an, ohne ihn zu erreichen. Dies führt zu den Begriffen **Supremum** und **Infimum**.

### Definition (Infimum und Supremum)

Sei $f : D \to \mathbb{R}$ mit $D \subseteq \mathbb{R}$.

**1. Supremum:** $y^* \in \mathbb{R} \cup \{+\infty\}$ ist das **Supremum** von $f$, geschrieben
$$y^* = \sup_{x \in D} f(x) = \sup f,$$

wenn gilt:
- (a) $f(x) \leq y^*$ für alle $x \in D$ (d.h. $y^*$ ist eine **obere Schranke**)
- (b) Es gibt eine Folge $(x_n)_n$ in $D$ mit $\lim_{n \to \infty} f(x_n) = y^*$

**2. Infimum:** $y_* \in \mathbb{R} \cup \{-\infty\}$ ist das **Infimum** von $f$, geschrieben
$$y_* = \inf_{x \in D} f(x) = \inf f,$$

wenn gilt:
- (a) $f(x) \geq y_*$ für alle $x \in D$ (d.h. $y_*$ ist eine **untere Schranke**)
- (b) Es gibt eine Folge $(x_n)_n$ in $D$ mit $\lim_{n \to \infty} f(x_n) = y_*$

### Interpretation

- **Supremum** = kleinste obere Schranke
- **Infimum** = größte untere Schranke

**Wichtig:** Die Folge $(x_n)_n$ braucht **nicht zu konvergieren**!

### Eigenschaften

1. **Jede Funktion** $f : D \to \mathbb{R}$ hat ein Supremum und ein Infimum

2. Wird das Supremum angenommen (d.h. $\exists x_0 \in D: f(x_0) = \sup f$), so ist das Supremum auch ein **Maximum**

3. Wird das Infimum angenommen (d.h. $\exists x_0 \in D: f(x_0) = \inf f$), so ist das Infimum auch ein **Minimum**

### Beispiele

**1. Reziprokfunktion:**
- $\sup_{x \in \,]0, \infty[} \frac{1}{x} = +\infty$
- $\inf_{x \in \,]0, \infty[} \frac{1}{x} = 0$ (nicht angenommen)

**2. Eingeschränkte Reziprokfunktion:**
- $\sup_{x \in \,]0, 1]} \frac{1}{x} = +\infty$
- $\inf_{x \in \,]0, 1]} \frac{1}{x} = 1 = \min_{x \in \,]0, 1]} \frac{1}{x}$ (angenommen!)

**3. Arcus Tangens:**
- $\sup_{x \in \mathbb{R}} \arctan(x) = \frac{\pi}{2}$ (nicht angenommen)
- $\inf_{x \in \mathbb{R}} \arctan(x) = -\frac{\pi}{2}$ (nicht angenommen)

---

## 6. Satz vom Minimum und Maximum

### Satz (Existenz vom Minimum und Maximum)

Sei $f : [a, b] \to \mathbb{R}$ stetig. Dann gibt es Stellen $x_{\min}, x_{\max} \in [a, b]$ mit

$$f(x_{\min}) \leq f(x) \leq f(x_{\max}) \quad \text{für alle } x \in [a, b],$$

d.h. $f$ nimmt auf $[a, b]$ **Minimum und Maximum** an.

### Kurzform

**Stetige Funktionen auf kompakten Intervallen besitzen ein Minimum und ein Maximum.**

### Folgerungen

1. Stetige Funktionen auf $[a, b]$ sind **beschränkt**

2. Es gilt:
   $$\inf_{x \in [a,b]} f(x) = \min_{x \in [a,b]} f(x)$$
   $$\sup_{x \in [a,b]} f(x) = \max_{x \in [a,b]} f(x)$$

### Wichtige Voraussetzungen

Der Satz gilt NUR wenn:
- ✓ Die Funktion ist **stetig**
- ✓ Das Intervall ist **kompakt** (= abgeschlossen und beschränkt, d.h. $[a, b]$)

**Gegenbeispiele:**
- $f : \,]0, 1] \to \mathbb{R}, f(x) = \frac{1}{x}$ (Intervall nicht abgeschlossen)
- $f : [0, \infty) \to \mathbb{R}, f(x) = x$ (Intervall nicht beschränkt)
- $f : [0, 1] \to \mathbb{R}, f(x) = \begin{cases} x, & 0 \leq x < 1 \\ 0, & x = 1 \end{cases}$ (nicht stetig)

---

## 📌 Zusammenfassung

| **Satz/Begriff** | **Aussage** | **Voraussetzung** |
|-----------------|-------------|-------------------|
| **Nullstellensatz von Bolzano** | Vorzeichenwechsel → Nullstelle | Stetig, Intervall |
| **Zwischenwertsatz** | Nimmt alle Zwischenwerte an | Stetig, Intervall |
| **Bisektionsverfahren** | Fehler: $\leq \frac{b-a}{2^{k+1}}$ | — |
| **Supremum** | Kleinste obere Schranke | Jede Funktion hat eins |
| **Infimum** | Größte untere Schranke | Jede Funktion hat eins |
| **Maximum** | Angenommenes Supremum | — |
| **Minimum** | Angenommenes Infimum | — |
| **Satz Min/Max** | Min und Max existieren | Stetig + kompaktes Intervall |

### Wichtige Unterscheidungen

**Maximum vs. Supremum:**
- Maximum: Wird **angenommen** (es gibt $x_0$ mit $f(x_0) = \max f$)
- Supremum: Wird **eventuell nicht** angenommen (kleinste obere Schranke)
- Jedes Maximum ist ein Supremum, aber nicht umgekehrt!

**Kompaktes Intervall:** $[a, b]$ (abgeschlossen und beschränkt)
- Offene Intervalle: $\,]a, b[$, $\,]a, b]$, $[a, b[$
- Unbeschränkte Intervalle: $[a, \infty)$, $\mathbb{R}$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.18 Berechnung von Grenzwerten]]: Wurzelfolge (schnellere Alternative zur Bisektion)
- [[VL.19 Stetigkeit]]: Definition und Eigenschaften stetiger Funktionen
- [[VL.21 Differenzierbarkeit]]: Lokale Extrema (notwendige Bedingung)
- [[VL.23 Mittelwertsatz]]: Weitere Sätze über stetige/differenzierbare Funktionen

