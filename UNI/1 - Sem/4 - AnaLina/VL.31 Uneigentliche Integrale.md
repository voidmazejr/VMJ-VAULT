**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #UneigentlicheIntegrale #RationaleFunktionen #Partialbruchzerlegung #Konvergenz

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung erweitert die Integration auf unbeschränkte Definitionsbereiche und unbeschränkte Funktionen.

- **Uneigentliche Integrale** über unbeschränkten Definitionsbereich
- **Uneigentliche Integrale** von unbeschränkten Funktionen
- Konvergenz und Divergenz von uneigentlichen Integralen
- **Integration rationaler Funktionen** mit Partialbruchzerlegung

---

## 1. Uneigentliche Integrale - Unbeschränkter Definitionsbereich

### Motivation

Integrierbare Funktionen sind immer beschränkt und auf einem kompakten Intervall $[a,b]$ gegeben. Aber wie integriert man Funktionen auf $[a, \infty[$?

**Beispiel:** Hat die Fläche zwischen $f(x) = \frac{1}{1+x^2}$ und der $x$-Achse auf $[0, \infty[$ endlichen Inhalt?

### Definition (Integral über $[a, \infty[$)

Sei $f : [a, \infty[ \to \mathbb{R}$ integrierbar über jedem Intervall $[a,b]$ mit $b > a$. Dann heißt

$$\boxed{\int_a^\infty f(x)\,dx := \lim_{b \to \infty} \int_a^b f(x)\,dx}$$

das **uneigentliche Integral** von $f$ über $[a, \infty[$.

**Terminologie:**
- Falls der Grenzwert **existiert**: $f$ ist **uneigentlich integrierbar** auf $[a, \infty[$, das Integral **konvergiert**
- Falls der Grenzwert **nicht existiert**: das Integral **divergiert**

### Definition (Integral über $]-\infty, b]$)

Sei $f : ]-\infty, b] \to \mathbb{R}$ integrierbar über jedem Intervall $[a,b]$ mit $a < b$. Dann heißt

$$\boxed{\int_{-\infty}^b f(x)\,dx := \lim_{a \to -\infty} \int_a^b f(x)\,dx}$$

das **uneigentliche Integral** von $f$ über $]-\infty, b]$.

### Beispiele

**Beispiel 1:** $\int_0^\infty \frac{1}{1+x^2}\,dx$

$$\int_0^\infty \frac{1}{1+x^2}\,dx = \lim_{b \to \infty} \int_0^b \frac{1}{1+x^2}\,dx = \lim_{b \to \infty} \arctan(x)\bigg|_0^b = \lim_{b \to \infty} \arctan(b) = \frac{\pi}{2}$$

**Das Integral konvergiert!**

⚠️ **Achtung:** Schreibe **nicht** $\arctan(x)\big|_0^\infty$, sondern $\lim_{b \to \infty} \arctan(x)\big|_0^b$.

Genauso:

$$\int_{-\infty}^0 \frac{1}{1+x^2}\,dx = \lim_{a \to -\infty} \arctan(x)\bigg|_a^0 = \lim_{a \to -\infty} -\arctan(a) = \frac{\pi}{2}$$

**Beispiel 2:** $\int_0^\infty e^{-\alpha x}\,dx$ für $\alpha > 0$

$$\int_0^\infty e^{-\alpha x}\,dx = \lim_{b \to \infty} \int_0^b e^{-\alpha x}\,dx = \lim_{b \to \infty} \left(-\frac{1}{\alpha}e^{-\alpha x}\right)\bigg|_0^b$$

$$= \lim_{b \to \infty} \left(-\frac{1}{\alpha}e^{-\alpha b} + \frac{1}{\alpha}\right) = \frac{1}{\alpha}$$

**Das Integral konvergiert.**

**Beispiel 3:** $\int_1^\infty \frac{1}{x}\,dx$ (divergiert!)

$$\int_1^\infty \frac{1}{x}\,dx = \lim_{b \to \infty} \int_1^b \frac{1}{x}\,dx = \lim_{b \to \infty} \ln(x)\bigg|_1^b = \lim_{b \to \infty} \ln(b) = \infty$$

**Das Integral existiert nicht (divergiert).**

**Beispiel 4:** $\int_1^\infty \frac{1}{x^\alpha}\,dx$ für $\alpha > 0$, $\alpha \neq 1$

Stammfunktion: $\frac{1}{1-\alpha}x^{1-\alpha}$

$$\int_1^\infty \frac{1}{x^\alpha}\,dx = \lim_{b \to \infty} \frac{1}{1-\alpha}x^{1-\alpha}\bigg|_1^b = \lim_{b \to \infty} \left(\frac{1}{1-\alpha}b^{1-\alpha} + \frac{1}{\alpha - 1}\right)$$

**Fallunterscheidung:**
- Für $0 < \alpha < 1$: $\lim_{b \to \infty} b^{1-\alpha} = \infty$ → **divergiert**
- Für $\alpha > 1$: $\lim_{b \to \infty} b^{1-\alpha} = 0$ → **konvergiert**

$$\boxed{\int_1^\infty \frac{1}{x^\alpha}\,dx = \begin{cases} \frac{1}{\alpha - 1}, & \alpha > 1 \\ \text{existiert nicht}, & 0 < \alpha < 1 \end{cases}}$$

### Definition (Integral über ganz $\mathbb{R}$)

Ist $f : \mathbb{R} \to \mathbb{R}$, so setzen wir

$$\boxed{\int_{-\infty}^\infty f(x)\,dx := \int_{-\infty}^0 f(x)\,dx + \int_0^\infty f(x)\,dx}$$

falls **beide** uneigentlichen Integrale existieren.

**Bemerkung:** Existiert $\int_{-\infty}^\infty f(x)\,dx$, so gilt für jedes $c \in \mathbb{R}$:

$$\int_{-\infty}^\infty f(x)\,dx = \int_{-\infty}^c f(x)\,dx + \int_c^\infty f(x)\,dx$$

### Beispiel über ganz $\mathbb{R}$

$$\int_{-\infty}^\infty \frac{1}{1+x^2}\,dx = \int_{-\infty}^0 \frac{1}{1+x^2}\,dx + \int_0^\infty \frac{1}{1+x^2}\,dx = \frac{\pi}{2} + \frac{\pi}{2} = \pi$$

⚠️ **Achtung - Wichtiger Fall!**

Für $f(x) = x$ existiert der Grenzwert

$$\lim_{b \to \infty} \int_{-b}^b x\,dx = \lim_{b \to \infty} \frac{1}{2}x^2\bigg|_{-b}^b = 0$$

**Aber:** Das uneigentliche Integral $\int_{-\infty}^\infty x\,dx$ existiert **nicht**, da

$$\int_0^\infty x\,dx = \lim_{b \to \infty} \frac{1}{2}x^2\bigg|_0^b = \infty$$

nicht existiert! (Auch $\int_{-\infty}^0 x\,dx$ existiert nicht.)

---

## 2. Uneigentliche Integrale - Unbeschränkte Funktionen

### Definition (Unbeschränkte Funktion an unterer Grenze)

Sei $f : ]a, b] \to \mathbb{R}$ integrierbar auf $[c, b]$ für alle $c \in ]a, b]$. Dann heißt

$$\boxed{\int_a^b f(x)\,dx = \lim_{c \searrow a} \int_c^b f(x)\,dx}$$

das **uneigentliche Integral** von $f$ über $]a, b]$.

Falls dieser Grenzwert existiert, heißt $f$ **uneigentlich integrierbar** auf $]a, b]$.

### Definition (Unbeschränkte Funktion an oberer Grenze)

Ist $f : [a, b[ \to \mathbb{R}$ integrierbar auf $[a, c]$ für jedes $c \in [a, b[$, so definiert man genauso

$$\boxed{\int_a^b f(x)\,dx = \lim_{c \nearrow b} \int_a^c f(x)\,dx}$$

### Beispiele

**Beispiel 1:** $\int_0^1 \frac{1}{x}\,dx$ (divergiert!)

$$\int_0^1 \frac{1}{x}\,dx = \lim_{c \searrow 0} \int_c^1 \frac{1}{x}\,dx = \lim_{c \searrow 0} \ln(x)\bigg|_c^1 = \lim_{c \searrow 0} -\ln(c) = \infty$$

**Das Integral existiert nicht.**

**Beispiel 2:** $\int_0^1 \frac{1}{x^\alpha}\,dx$ für $\alpha > 0$, $\alpha \neq 1$

$$\int_0^1 \frac{1}{x^\alpha}\,dx = \lim_{c \searrow 0} \int_c^1 \frac{1}{x^\alpha}\,dx = \lim_{c \searrow 0} \frac{1}{1-\alpha}x^{1-\alpha}\bigg|_c^1 = \lim_{c \searrow 0} \frac{1}{1-\alpha}(1 - c^{1-\alpha})$$

**Fallunterscheidung:**
- Für $0 < \alpha < 1$: $\lim_{c \searrow 0} c^{1-\alpha} = 0$ → **konvergiert zu** $\frac{1}{1-\alpha}$
- Für $\alpha > 1$: $\lim_{c \searrow 0} c^{1-\alpha} = \infty$ → **divergiert**

$$\boxed{\int_0^1 \frac{1}{x^\alpha}\,dx = \begin{cases} \frac{1}{1-\alpha}, & 0 < \alpha < 1 \\ \text{existiert nicht}, & \alpha > 1 \end{cases}}$$

### Wichtige Beobachtung

Insbesondere existiert

$$\int_0^\infty \frac{1}{x^\alpha}\,dx := \int_0^1 \frac{1}{x^\alpha}\,dx + \int_1^\infty \frac{1}{x^\alpha}\,dx$$

für **kein** $\alpha > 0$, denn:

- $\int_0^1 \frac{1}{x^\alpha}\,dx$ existiert nur für $\alpha < 1$
- $\int_1^\infty \frac{1}{x^\alpha}\,dx$ existiert nur für $\alpha > 1$

**Kritischer Parameter:** $\alpha = 1$ ist der Grenzfall für beide Integrale!

---

## 3. Integration rationaler Funktionen

### Ziel

Bestimmung von Stammfunktionen von rationalen Funktionen

$$f(x) = \frac{p(x)}{q(x)}$$

mit reellen Polynomen $p$ und $q$.

### Methode: Partialbruchzerlegung

Eine **(komplexe) Polynomdivision** und **Partialbruchzerlegung** (siehe [[VL.09 Polynome]]) liefert $\frac{p}{q}$ als Summe von Bestandteilen der Form:

1. **Polynom**
2. $\frac{A}{x-z}$ mit Nullstellen $z \in \mathbb{C}$ des Nenners $q$
3. $\frac{A}{(x-z)^{k+1}}$ mit $k \geq 1$, falls $z \in \mathbb{C}$ mehrfache Nullstelle ist

Die Stammfunktion eines Polynoms ist bekannt. Für Partialbrüche:

### Satz (Stammfunktion von Partialbrüchen)

**1. Mehrfache Polstellen:** Für $k \geq 1$ gilt wie im Reellen:

$$\boxed{\int \frac{1}{(x-z)^{k+1}}\,dx = -\frac{1}{k} \cdot \frac{1}{(x-z)^k} + c, \quad c \in \mathbb{C}}$$

**2. Einfache Polstellen:** Für $z = a + ib \in \mathbb{C}$ mit $a, b \in \mathbb{R}$ ist:

$$\boxed{\int \frac{1}{x-z}\,dx = \begin{cases} \ln|x-z| + c, & b = 0 \\ \ln|x-z| + i\arctan\left(\frac{x-a}{b}\right) + c, & b \neq 0 \end{cases}}$$

mit $c \in \mathbb{C}$.

### Beweis-Idee für Fall 2 ($b \neq 0$)

Für $z = a + ib$ ist $|x-z|^2 = (x-a)^2 + b^2$ und

$$\frac{1}{x-z} = \frac{\overline{x-z}}{(x-z)\overline{(x-z)}} = \frac{x-a}{(x-a)^2 + b^2} + i\frac{b}{(x-a)^2 + b^2}$$

**Erster Term:**

$$\int \frac{x-a}{(x-a)^2 + b^2}\,dx = \frac{1}{2}\ln((x-a)^2 + b^2) = \ln|x-z| + c_1$$

**Zweiter Term:** Mit Substitution $t = \frac{x-a}{b}$:

$$\int \frac{b}{(x-a)^2 + b^2}\,dx = \int \frac{1}{1+t^2}\,dt = \arctan(t) = \arctan\left(\frac{x-a}{b}\right) + c_2$$

Zusammen: $\ln|x-z| + i\arctan\left(\frac{x-a}{b}\right) + c$

### Beispiel 1: Reelle Nullstellen

Berechne $\int \frac{1}{x^2-9}\,dx$.

Wegen $x^2 - 9 = (x-3)(x+3)$ setzen wir an:

$$\frac{1}{x^2-9} = \frac{A}{x-3} + \frac{B}{x+3}$$

Multiplikation mit Nenner: $1 = A(x+3) + B(x-3)$

Einsetzen $x = 3$: $A = \frac{1}{6}$

Einsetzen $x = -3$: $B = -\frac{1}{6}$

Also:

$$\int \frac{1}{x^2-9}\,dx = \frac{1}{6}\int \frac{1}{x-3}\,dx - \frac{1}{6}\int \frac{1}{x+3}\,dx$$

$$= \frac{1}{6}\ln|x-3| - \frac{1}{6}\ln|x+3| + c = \boxed{\frac{1}{6}\ln\left|\frac{x-3}{x+3}\right| + c}$$

### Beispiel 2: Komplexe Nullstellen

Berechne $\int \frac{4x^2 - 4x}{(x^2+1)^2}\,dx$.

Mit $x^2 + 1 = (x-i)(x+i)$:

$$\frac{4x^2 - 4x}{(x^2+1)^2} = \frac{i}{x+i} + \frac{1-i}{(x+i)^2} + \frac{-i}{x-i} + \frac{1+i}{(x-i)^2}$$

Fasse Pole erster Ordnung zusammen:

$$= \frac{2}{1+x^2} + \frac{1-i}{(x+i)^2} + \frac{1+i}{(x-i)^2}$$

Integration:

$$\int f(x)\,dx = 2\arctan(x) - \frac{1-i}{x+i} - \frac{1+i}{x-i} + c$$

$$= 2\arctan(x) - \frac{(1-i)(x-i) + (1+i)(x+i)}{x^2+1} + c$$

$$= \boxed{2\arctan(x) - \frac{2x-2}{x^2+1} + c}$$

### Wichtige Bemerkung zu konjugiert komplexen Nullstellen

Ist $f(x) = \frac{p(x)}{q(x)}$ mit **reellen** Polynomen $p, q$, und ist $z = a + ib$ eine nichtreelle Nullstelle von $q$ (mit $b \neq 0$), so ist auch $\overline{z} = a - ib$ eine Nullstelle von $q$.

In der PBZ haben wir dann Terme:

$$\frac{A}{x-z} + \frac{B}{x-\overline{z}}$$

**Zwei Möglichkeiten:**

1. Verwende komplexe Stammfunktion aus Satz (liefert reelles Ergebnis)
2. Fasse beide Terme zu einem Bruch zusammen → typischerweise ein $\ln$ und ein $\arctan$

---

## 📌 Zusammenfassung

### Uneigentliche Integrale - Übersicht

| Typ | Definition | Existiert wenn |
|-----|------------|----------------|
| $\int_a^\infty f(x)\,dx$ | $\lim_{b \to \infty} \int_a^b f(x)\,dx$ | Grenzwert existiert |
| $\int_{-\infty}^b f(x)\,dx$ | $\lim_{a \to -\infty} \int_a^b f(x)\,dx$ | Grenzwert existiert |
| $\int_a^b f(x)\,dx$ (unbeschränkt bei $a$) | $\lim_{c \searrow a} \int_c^b f(x)\,dx$ | Grenzwert existiert |
| $\int_a^b f(x)\,dx$ (unbeschränkt bei $b$) | $\lim_{c \nearrow b} \int_a^c f(x)\,dx$ | Grenzwert existiert |

### Wichtige Integrale

**Unbeschränkter Definitionsbereich:**

$$\int_1^\infty \frac{1}{x^\alpha}\,dx = \begin{cases} \frac{1}{\alpha-1}, & \alpha > 1 \\ \text{divergiert}, & 0 < \alpha \leq 1 \end{cases}$$

**Unbeschränkte Funktion:**

$$\int_0^1 \frac{1}{x^\alpha}\,dx = \begin{cases} \frac{1}{1-\alpha}, & 0 < \alpha < 1 \\ \text{divergiert}, & \alpha \geq 1 \end{cases}$$

**Wichtig:** $\alpha = 1$ ist jeweils der kritische Parameter!

### Stammfunktionen von Partialbrüchen

**Mehrfache Pole:**

$$\int \frac{1}{(x-z)^{k+1}}\,dx = -\frac{1}{k(x-z)^k} + c$$

**Einfache Pole (reell):**

$$\int \frac{1}{x-a}\,dx = \ln|x-a| + c$$

**Einfache Pole (komplex, $z = a + ib$, $b \neq 0$):**

$$\int \frac{1}{x-z}\,dx = \ln|x-z| + i\arctan\left(\frac{x-a}{b}\right) + c$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.09 Rationale Funktionen]]: Partialbruchzerlegung
- [[VL.26 Elementare Funktionen 2]]: Komplexe Exponentialfunktion
- [[VL.28 Das Integral]]: Hauptsatz der Differential- und Integralrechnung
- [[VL.29 Integrationsregeln 1]]: Grundintegrale
- [[VL.30 Integrationsregeln 2]]: Komplexe Integration