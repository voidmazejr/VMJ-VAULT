**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Exponentialfunktion #Logarithmusfunktion #AllgemeinePotenz #KomplexeExponentialfunktion #EulerscheZahl

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung gibt eine rigorose Definition der Exponentialfunktion über ihre Reihendarstellung und leitet daraus systematisch weitere elementare Funktionen ab.

- **Exakte Definition** der Exponentialfunktion durch die Exponentialreihe
- Herleitung der **Eigenschaften** von exp(x) aus der Reihendarstellung
- Definition und Eigenschaften der **Logarithmusfunktion** als Umkehrfunktion
- **Allgemeine Potenz** $a^b$ für beliebige reelle Exponenten
- Einführung in die **komplexe Exponentialfunktion**

---

## 1. Exponentialfunktion

### Definition über die Exponentialreihe

**Ausgangspunkt:** Für beliebiges $x \in \mathbb{R}$ ist die Reihe

$$\sum_{k=0}^{\infty} \frac{x^k}{k!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \ldots$$

konvergent (gezeigt in [[VL.25 Anwendung Taylor-Approximation]]).

### Definition (Exponentialfunktion, Eulersche Zahl)

Die durch diesen Grenzwert definierte Funktion heißt **Exponentialfunktion**:

$$\boxed{\exp(x) := \sum_{k=0}^{\infty} \frac{x^k}{k!} := \lim_{n \to \infty} \sum_{k=0}^{n} \frac{x^k}{k!}}$$

Die Zahl $e := \exp(1)$ heißt die **Eulersche Zahl**.

**Numerischer Wert:** $e \approx 2.71828182845904...$

### Eigenschaften der Exponentialfunktion

Für alle $x, x_1, x_2 \in \mathbb{R}$ gilt:

**1. Differenzierbarkeit:**
$$(\exp(x))' = \exp(x)$$

*Beweis-Skizze:* Gliedweise Differentiation der Reihe ergibt:
$$\frac{d}{dx}\left(\sum_{k=0}^{\infty} \frac{x^k}{k!}\right) = \sum_{k=1}^{\infty} \frac{kx^{k-1}}{k!} = \sum_{k=1}^{\infty} \frac{x^{k-1}}{(k-1)!} = \sum_{k=0}^{\infty} \frac{x^k}{k!} = \exp(x)$$

**2. Funktionswert bei Null:**
$$\exp(0) = 1$$

**3. Funktionalgleichung:**
$$\exp(x_1 + x_2) = \exp(x_1) \cdot \exp(x_2)$$

*Folgerung:* 
$$\exp(x) \cdot \exp(-x) = \exp(0) = 1 \quad \Rightarrow \quad \exp(-x) = \frac{1}{\exp(x)}$$

Insbesondere: $\exp(x) \neq 0$ für alle $x \in \mathbb{R}$

**4. Positivität:**
$$\exp(x) > 0 \quad \text{für alle } x \in \mathbb{R}$$

*Beweis durch Widerspruch:* Wäre $\exp(x_0) < 0$ für ein $x_0$, hätte exp nach dem Zwischenwertsatz eine Nullstelle zwischen $x_0$ und $0$ (da $\exp(0) = 1 > 0$), im Widerspruch zur Funktionalgleichung.

**5. Strenge Monotonie:**
$$\exp'(x) = \exp(x) > 0 \quad \Rightarrow \quad \text{exp ist streng monoton wachsend}$$

**6. Wachstumsverhalten:**
$$\begin{align}
\lim_{x \to +\infty} \exp(x) &= +\infty \\
\lim_{x \to -\infty} \exp(x) &= 0 \\
\lim_{x \to +\infty} \frac{\exp(x)}{x^n} &= +\infty \quad \text{für alle } n \in \mathbb{N}
\end{align}$$

*Interpretation:* Die Exponentialfunktion wächst **schneller als jede Potenz** $x^n$.

**7. Bijektivität:**
$$\exp : \mathbb{R} \to \,]0, \infty[$$

ist bijektiv (injektiv wegen Monotonie, surjektiv wegen Grenzwertverhalten und Zwischenwertsatz), also **umkehrbar**.

---

## 2. Logarithmusfunktion

### Definition

Die **(natürliche) Logarithmusfunktion** $\ln : \,]0, \infty[ \,\to \mathbb{R}$ ist die **Umkehrfunktion** von exp.

**Umkehreigenschaften:**
$$\begin{align}
\exp(\ln(x)) &= x \quad \text{für alle } x > 0 \\
\ln(\exp(x)) &= x \quad \text{für alle } x \in \mathbb{R}
\end{align}$$

### Grafische Darstellung

![[Screenshot 2026-01-10 at 00.42.41.png]]

Die Graphen von exp und ln sind **symmetrisch bezüglich der Winkelhalbierenden** $y = x$.

### Eigenschaften des Logarithmus

Für alle $x, y > 0$ und $n \in \mathbb{Z}$ gilt:

**1. Funktionswert bei 1:**
$$\ln(1) = 0$$

**2. Funktionalgleichung:**
$$\ln(xy) = \ln(x) + \ln(y)$$

**3. Reziproke:**
$$\ln\left(\frac{1}{x}\right) = -\ln(x)$$

**4. Quotientenregel:**
$$\ln\left(\frac{x}{y}\right) = \ln(x) - \ln(y)$$

**5. Potenzregel:**
$$\ln(x^n) = n \cdot \ln(x)$$

**6. Bijektivität:**
$$\ln : \,]0, \infty[ \,\to \mathbb{R} \text{ ist bijektiv}$$

**7. Ableitung:**
$$\ln'(x) = \frac{1}{x}$$

**8. Monotonie:** ln ist streng monoton wachsend mit
$$\begin{align}
\lim_{x \to 0^+} \ln(x) &= -\infty \\
\lim_{x \to +\infty} \ln(x) &= +\infty
\end{align}$$

### Taylorreihe des Logarithmus

Da ln(x) bei $x = 0$ nicht definiert ist, betrachtet man $f(x) = \ln(1+x)$ um $x_0 = 0$:

**Ableitungen:**
$$\begin{align}
f'(x) &= (1+x)^{-1} &\Rightarrow f'(0) &= 1 \\
f''(x) &= -(1+x)^{-2} &\Rightarrow f''(0) &= -1 \\
f'''(x) &= 2(1+x)^{-3} &\Rightarrow f'''(0) &= 2
\end{align}$$

Allgemein: $f^{(k)}(x) = (-1)^{k-1}(k-1)!(1+x)^{-k}$, also $f^{(k)}(0) = (-1)^{k-1}(k-1)!$

**Taylorreihe für** $|x| < 1$:

$$\boxed{\ln(1+x) = \sum_{k=1}^{\infty} \frac{(-1)^{k-1}}{k} x^k = x - \frac{x^2}{2} + \frac{x^3}{3} - \frac{x^4}{4} \pm \ldots}$$

---

## 3. Allgemeine Potenzfunktion

### Motivation

**Bisher:** $a^n$ für $n \in \mathbb{N}$ als $n$-faches Produkt definiert.  
**Frage:** Was bedeutet z.B. $5^\pi$ oder $e^x$?

### Definition (Allgemeine Potenz)

Für $a > 0$ und $b \in \mathbb{R}$ definieren wir die **allgemeine Potenz**:

$$\boxed{a^b := \exp(b \ln(a))}$$

- $a$ heißt **Basis**
- $b$ heißt **Exponent**

Dies ergibt zwei wichtige Funktionen:
1. **Allgemeine Potenz:** $x \mapsto a^x$ (Basis fest, Exponent variabel)
2. **Potenzfunktion:** $x \mapsto x^b$ (Basis variabel, Exponent fest)

### Rechenregeln für die allgemeine Potenz

Für $a > 0$ und alle $x, y \in \mathbb{R}$ gilt:

**1. Stetig und differenzierbar:**
$$x \mapsto a^x \text{ ist stetig und beliebig oft differenzierbar}$$

**2. Funktionswert bei 0:**
$$a^0 = 1$$

**3. Produktregel:**
$$a^{x+y} = a^x \cdot a^y$$

**4. Reziproke:**
$$a^{-x} = \frac{1}{a^x}$$

**5. Positivität:**
$$a^x > 0$$

**6. Logarithmus:**
$$\ln(a^x) = x \ln(a)$$

**7. Potenzregel:**
$$(a^x)^y = a^{xy}$$

**Wichtige Spezialfälle:**
- Für $n \in \mathbb{N}$: $a^n = \underbrace{a \cdot a \cdot \ldots \cdot a}_{n\text{ mal}}$ (konsistent mit alter Definition)
- $a^{1/n} = \sqrt[n]{a}$ (denn $(a^{1/n})^n = a^{n/n} = a^1 = a$)
- $a^{p/q} = \sqrt[q]{a^p}$ für $p \in \mathbb{Z}, q \in \mathbb{N} \setminus \{0\}$
- **Natürliche Basis:** $e^x = \exp(x \ln(e)) = \exp(x)$

### Wichtige Hinweise

**1. Vorsicht bei Klammern:**

Für $a > 0$ und $x, y \in \mathbb{R}$ gilt im Allgemeinen:
$$(a^x)^y \neq a^{(x^y)}$$

**2. Einschränkung auf positive Basen:**

$x \mapsto a^x$ ist nur für $a > 0$ definiert. Für $a < 0$ wäre z.B. $a^{1/2} = \sqrt{a}$ nicht definiert.

### Ableitung und Monotonie

**Ableitung der allgemeinen Potenz:** Für $a > 0$:

$$\boxed{\frac{d}{dx} a^x = \ln(a) \cdot a^x}$$

*Beweis mit Kettenregel:*
$$\frac{d}{dx} a^x = \frac{d}{dx} \exp(x \ln(a)) = \exp(x \ln(a)) \cdot \ln(a) = a^x \ln(a)$$

**Monotonieverhalten:**
- $a > 1$: $\ln(a) > 0$ → $a^x$ **streng monoton wachsend** (Wachstumsprozesse)
- $a = 1$: $\ln(a) = 0$ → $a^x = 1$ **konstant**
- $0 < a < 1$: $\ln(a) < 0$ → $a^x$ **streng monoton fallend** (Zerfallsprozesse)

**Ableitung der Potenzfunktion:** Für $b \in \mathbb{R}$ und $x > 0$:

$$\boxed{\frac{d}{dx} x^b = b \cdot x^{b-1}}$$

*Beweis:*
$$\frac{d}{dx} x^b = \frac{d}{dx} \exp(b \ln(x)) = \exp(b \ln(x)) \cdot b \cdot \frac{1}{x} = x^b \cdot b \cdot x^{-1} = bx^{b-1}$$

**Spezialfall:** Für $x > 0$:
$$\frac{d}{dx} x^x = x^x(\ln(x) + 1)$$

### Grafische Darstellung

![[Screenshot 2026-01-10 at 00.43.25.png]]
Funktionen $2^x$ (Wachstum), $1^x$ (konstant), $\left(\frac{1}{2}\right)^x$ (Zerfall)

---

## 4. Logarithmus zur Basis a

### Definition

Für $a > 0, a \neq 1$ ist $a^x$ bijektiv und damit umkehrbar. Die Umkehrfunktion heißt **Logarithmus zur Basis a**:

$$\log_a : \,]0, \infty[ \,\to \mathbb{R}$$

**Umkehreigenschaft:**
$$a^y = x \quad \Leftrightarrow \quad \log_a(x) = y$$

**Spezialfall:** $\log_e(x) = \ln(x)$ (natürlicher Logarithmus)

### Darstellung durch den natürlichen Logarithmus

Aus $a^{\log_a(x)} = x$ folgt:
$$\ln(x) = \ln(a^{\log_a(x)}) = \log_a(x) \cdot \ln(a)$$

Also:
$$\boxed{\log_a(x) = \frac{\ln(x)}{\ln(a)}}$$

### Rechenregeln

Für $a, x, y > 0$ und $b \in \mathbb{R}$ gilt:

**1. Produktregel:**
$$\log_a(xy) = \log_a(x) + \log_a(y)$$

**2. Potenzregel:**
$$\log_a(x^b) = b \cdot \log_a(x)$$

**3. Reziproke:**
$$\log_a\left(\frac{1}{x}\right) = -\log_a(x)$$

**4. Quotientenregel:**
$$\log_a\left(\frac{x}{y}\right) = \log_a(x) - \log_a(y)$$

### Grafischer Vergleich


![[Screenshot 2026-01-10 at 00.43.52.png]]

---

## 5. Komplexe Exponentialfunktion

### Definition

Die Exponentialreihe konvergiert für **alle komplexen Zahlen** $z \in \mathbb{C}$:

$$\boxed{\exp(z) = \sum_{k=0}^{\infty} \frac{z^k}{k!} = 1 + z + \frac{z^2}{2!} + \frac{z^3}{3!} + \ldots}$$

Dies definiert die **komplexe Exponentialfunktion** $\exp : \mathbb{C} \to \mathbb{C}$.

### Eulersche Formel

Für $z = x + iy$ mit reellen $x, y$ gilt:

$$\boxed{\exp(x + iy) = \exp(x) \cdot \exp(iy) = \exp(x)(\cos(y) + i\sin(y))}$$

Insbesondere für $x = 0$:

$$\boxed{e^{i\phi} = \cos(\phi) + i\sin(\phi)}$$

(Herleitung siehe [[VL.25 Anwendung Taylor-Approximation]])

### Periodizität

Die komplexe Exponentialfunktion ist **periodisch** mit Periode $2\pi i$:

$$e^{z + 2\pi i} = e^z \cdot e^{2\pi i} = e^z$$

**Folgerung:** $\exp : \mathbb{C} \to \mathbb{C}$ ist **nicht injektiv** und damit nicht eindeutig umkehrbar.

Dies führt zu Problemen bei der Definition eines komplexen Logarithmus.

### Komplexer Logarithmus (Ausblick)

Für $z = |z|e^{i\phi} \neq 0$ definiert man:

$$\log(z) := \ln(|z|) + i\phi, \quad \phi = \arg(z) \in [0, 2\pi[$$

⚠️ Der komplexe Logarithmus ist **mehrdeutig** (da der Winkel $\phi$ nur modulo $2\pi$ definiert ist).

Mehr dazu in "Analysis III für Ingenieurwissenschaften".

---

## 📌 Zusammenfassung

### Fundamentale Funktionen

| **Funktion** | **Definition** | **Ableitung** | **Wichtige Eigenschaft** |
|-------------|----------------|---------------|--------------------------|
| $\exp(x)$ | $\sum_{k=0}^{\infty} \frac{x^k}{k!}$ | $\exp'(x) = \exp(x)$ | $\exp(x+y) = \exp(x)\exp(y)$ |
| $\ln(x)$ | Umkehrfunktion von exp | $\ln'(x) = \frac{1}{x}$ | $\ln(xy) = \ln(x) + \ln(y)$ |
| $a^x$ | $\exp(x \ln(a))$ | $(a^x)' = \ln(a) \cdot a^x$ | $a^{x+y} = a^x \cdot a^y$ |
| $x^b$ | $\exp(b \ln(x))$ | $(x^b)' = b \cdot x^{b-1}$ | $(x^a)^b = x^{ab}$ |
| $\log_a(x)$ | $\frac{\ln(x)}{\ln(a)}$ | $\log_a'(x) = \frac{1}{x \ln(a)}$ | $\log_a(xy) = \log_a(x) + \log_a(y)$ |

### Wichtige Spezialfälle

- **Eulersche Zahl:** $e = \exp(1) \approx 2.71828...$
- **Natürliche Basis:** $e^x = \exp(x)$
- **Natürlicher Logarithmus:** $\ln(x) = \log_e(x)$
- **Euler-Formel:** $e^{i\phi} = \cos(\phi) + i\sin(\phi)$

### Wachstumsverhalten

**Hierarchie der Wachstumsraten** (für $x \to \infty$):
$$\ln(x) \ll x^\alpha \ll e^x$$

für jedes $\alpha > 0$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.06 Elementare Funktionen 1]]: Erste Einführung von exp und ln (ohne Beweis)
- [[VL.07 Komplexe Zahlen 2]]: Eulersche Formel und komplexe Zahlen
- [[VL.21 Differenzierbarkeit]]: Beispiele zur Differenzierbarkeit
- [[VL.22 Anwendung Differenzierbarkeit]]: Ableitung von ln
- [[VL.24 Taylor-Approximation]]: Taylor-Polynome und Restgliedabschätzung
- [[VL.25 Anwendung Taylor-Approximation]]: Konvergenz der Exponential-, Sinus- und Kosinusreihe; Herleitung der Eulerschen Formel

