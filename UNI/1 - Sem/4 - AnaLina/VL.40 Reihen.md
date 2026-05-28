**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Reihen #Konvergenz #GeometrischeReihe #HarmonischeReihe #Konvergenzkriterien

---

## 🎯 Lernziele der Vorlesung

Unendliche Reihen sind Grenzwerte von Summen für $n \to \infty$. Wir untersuchen, wann Reihen konvergieren.

- **Definition** von Reihen und Konvergenz
- **Geometrische Reihe** als wichtigste Reihe
- **Rechenregeln** für konvergente Reihen
- **Konvergenzkriterien**: Notwendiges Kriterium, Integralvergleich, Leibniz

---

## 1. Definition von Reihen

### Definition (Reihe)

**1. Partialsummen:**

Aus einer gegebenen Folge $(a_n)_{n \in \mathbb{N}}$ bilden wir eine neue Folge von **Summen** $(s_n)_{n \in \mathbb{N}}$:

$$\boxed{s_n = \sum_{k=0}^n a_k = a_0 + a_1 + \ldots + a_n}$$

Die Folge $(s_n)_{n \in \mathbb{N}}$ nennen wir eine **unendliche Reihe** und schreiben auch $\sum_{k=0}^\infty a_k$.

- Die $a_k$ heißen **Glieder der Reihe**
- Die Summe $s_n$ heißt die **$n$-te Partialsumme** der Reihe

**2. Konvergenz:**

Die Reihe **konvergiert** (bzw. **divergiert**), falls die Folge $(s_n)_{n \in \mathbb{N}}$ konvergiert (bzw. divergiert).

**3. Wert der Reihe:**

Existiert der Grenzwert $s = \lim_{n \to \infty} s_n$, so heißt $s$ der **Wert** (oder die **Summe**) der Reihe und wir schreiben:

$$\boxed{s = \sum_{k=0}^\infty a_k}$$

### Wichtige Bemerkung: Doppelbedeutung der Notation

Die Bezeichnung $\sum_{k=0}^\infty a_k$ hat **zwei Bedeutungen**:

1. **Alleinstehend:** $\sum_{k=0}^\infty a_k$ bezeichnet die **Folge** $(s_n)_{n \in \mathbb{N}}$ der Partialsummen
2. **In Gleichung:** $\sum_{k=0}^\infty a_k = s$ bezeichnet den **Grenzwert** $s = \lim_{n \to \infty} s_n$

### Beobachtung: Endlich viele Summanden spielen keine Rolle

Wenn $\sum_{k=0}^\infty a_k$ konvergiert, dann konvergiert auch $\sum_{k=m}^\infty a_k$ für jedes $m \in \mathbb{N}$, und es gilt:

$$\sum_{k=0}^\infty a_k = a_0 + a_1 + \ldots + a_{m-1} + \sum_{k=m}^\infty a_k$$

**Folgerung:** Die ersten Summanden spielen **keine Rolle für die Konvergenz**, wohl aber für den **Wert der Reihe**!

---

## 2. Die geometrische Reihe

### Definition

Sei $q \in \mathbb{R}$ und $a_k = q^k$. Die zugehörige Reihe

$$\boxed{\sum_{k=0}^\infty q^k = 1 + q + q^2 + q^3 + \ldots}$$

heißt die **geometrische Reihe**. Sie ist die **wichtigste Reihe überhaupt**!

### Satz (Konvergenz der geometrischen Reihe)

$$\boxed{\sum_{k=0}^\infty q^k = \begin{cases} \frac{1}{1-q}, & |q| < 1 \\ \text{divergent}, & |q| \geq 1 \end{cases}}$$

**Beweis:** Wurde bereits in [[VL.18 Folgen und Grenzwerte]] (Beispiel 18.12) gezeigt.

Für $|q| < 1$ ist die Partialsumme:

$$s_n = \sum_{k=0}^n q^k = \frac{1-q^{n+1}}{1-q}$$

und $\lim_{n \to \infty} q^{n+1} = 0$, also $\lim_{n \to \infty} s_n = \frac{1}{1-q}$.

### Beispiele

**Beispiel 1: Achilles und die Schildkröte**

Achilles ist 100 m von der Schildkröte entfernt und ist 10 mal so schnell. Wann hat er sie eingeholt?

Während Achilles 100 m zurücklegt, läuft die Schildkröte 10 m. Dann muss Achilles weitere 10 m laufen, wobei die Schildkröte 1 m läuft, usw.

Achilles holt die Schildkröte ein nach:

$$100 + 10 + 1 + \frac{1}{10} + \frac{1}{100} + \ldots = 110 + \sum_{k=0}^\infty \left(\frac{1}{10}\right)^k$$

$$= 110 + \frac{1}{1 - \frac{1}{10}} = 110 + \frac{10}{9} = 111{,}1\text{ m}$$

**Beispiel 2: $0{,}\overline{9} = 1$**

Mit der geometrischen Reihe:

$$0{,}\overline{9} = 0{,}999\ldots = \sum_{k=1}^\infty 9 \cdot \left(\frac{1}{10}\right)^k = \frac{9}{10}\sum_{k=0}^\infty \left(\frac{1}{10}\right)^k$$

$$= \frac{9}{10} \cdot \frac{1}{1 - \frac{1}{10}} = \frac{9}{10} \cdot \frac{10}{9} = 1$$

---

## 3. Rechenregeln für konvergente Reihen

### Satz (Rechenregeln)

Sind $\sum_{k=0}^\infty a_k$ und $\sum_{k=0}^\infty b_k$ konvergente Reihen und $c \in \mathbb{R}$, so konvergieren auch $\sum_{k=0}^\infty (a_k + b_k)$ und $\sum_{k=0}^\infty ca_k$, und es gilt:

$$\boxed{\sum_{k=0}^\infty (a_k + b_k) = \sum_{k=0}^\infty a_k + \sum_{k=0}^\infty b_k}$$

$$\boxed{\sum_{k=0}^\infty ca_k = c\sum_{k=0}^\infty a_k}$$

**Beweis:** Folgt unmittelbar aus den Grenzwertsätzen für Folgen (siehe [[VL.18 Folgen und Grenzwerte]]).

### Cauchy-Produkt (ohne Beweis)

Mit Produkten ist es komplizierter. Das **Cauchy-Produkt** lautet:

$$\left(\sum_{k=0}^\infty a_k\right) \cdot \left(\sum_{k=0}^\infty b_k\right) = \sum_{k=0}^\infty c_k$$

wobei $c_k = a_0 b_k + a_1 b_{k-1} + a_2 b_{k-2} + \ldots + a_k b_0$.

**Merkhilfe:** Multipliziere $\sum_{k=0}^\infty a_k x^k$ und $\sum_{k=0}^\infty b_k x^k$ und sortiere nach Potenzen von $x$, dann für $x = 1$.

**Achtung:** Die Formel gilt nur, wenn **alle drei Reihen** konvergieren. Es kann sein, dass $\sum a_k$ und $\sum b_k$ konvergieren, aber $\sum c_k$ **nicht** konvergiert!

---

## 4. Konvergenzkriterien

### Satz (Notwendiges Kriterium)

Wenn die Reihe $\sum_{k=0}^\infty a_k$ konvergiert, dann gilt:

$$\boxed{\lim_{k \to \infty} a_k = 0}$$

**Beweis:** Wenn die Reihe konvergiert, so gilt $s = \lim_{n \to \infty} s_n = \lim_{n \to \infty} s_{n-1}$. Daher:

$$0 = s - s = \lim_{n \to \infty} s_n - \lim_{n \to \infty} s_{n-1} = \lim_{n \to \infty} (s_n - s_{n-1}) = \lim_{n \to \infty} a_n$$

**Kontraposition (Divergenztest):**

$$\boxed{\text{Wenn } \lim_{k \to \infty} a_k \neq 0 \text{ (oder nicht existiert)}, \text{ dann divergiert } \sum_{k=0}^\infty a_k}$$

⚠️ **Achtung:** Die **Umkehrung ist falsch**! Aus $\lim_{k \to \infty} a_k = 0$ folgt **nicht** die Konvergenz der Reihe!

**Gegenbeispiel:** Die harmonische Reihe (siehe unten).

### Satz (Integralvergleichskriterium)

Sei $f : [m, \infty[ \to \mathbb{R}$, $m \in \mathbb{N}$, eine **monoton fallende** Funktion mit $f(x) \geq 0$ für alle $x \in [m, \infty[$. Dann gilt:

$$\boxed{\sum_{k=m}^\infty f(k) \text{ konvergiert} \iff \int_m^\infty f(x)\,dx \text{ existiert}}$$

**Abschätzungen:**

$$\boxed{\sum_{k=m+1}^\infty f(k) \leq \int_m^\infty f(x)\,dx \leq \sum_{k=m}^\infty f(k)}$$

**Beweis-Idee (Grafik):**

Da $f$ monoton fallend ist:

$$f(k+1) \leq f(x) \leq f(k) \quad \text{für alle } x \in [k, k+1]$$

Integration von $k$ bis $k+1$:

$$f(k+1) \leq \int_k^{k+1} f(x)\,dx \leq f(k)$$

Summiere über $k = m, \ldots, n$:

$$\sum_{k=m+1}^{n+1} f(k) \leq \int_m^{n+1} f(x)\,dx \leq \sum_{k=m}^n f(k)$$

Aus der Konvergenz der Reihe folgt Beschränktheit und damit Konvergenz des Integrals (und umgekehrt).

### Beispiele zum Integralvergleichskriterium

**Beispiel 1: Harmonische Reihe**

Die **harmonische Reihe** $\sum_{k=1}^\infty \frac{1}{k}$ ist **divergent**.

**Beweis:** Die Funktion $f(x) = \frac{1}{x}$ ist monoton fallend mit $f(x) \geq 0$ auf $[1, \infty[$, und:

$$\int_1^\infty \frac{1}{x}\,dx = \lim_{b \to \infty} \ln(x)\bigg|_1^b = \lim_{b \to \infty} \ln(b) = \infty$$

ist divergent (siehe [[VL.31 Uneigentliche Integrale]]).

**Wichtig:** Obwohl $\lim_{k \to \infty} \frac{1}{k} = 0$ (notwendiges Kriterium erfüllt!), divergiert die Reihe!

**Beispiel 2: $\sum \frac{1}{k^2}$**

Die Reihe $\sum_{k=1}^\infty \frac{1}{k^2}$ ist **konvergent**, da:

$$\int_1^\infty \frac{1}{x^2}\,dx = \lim_{b \to \infty} \left(-\frac{1}{x}\right)\bigg|_1^b = \lim_{b \to \infty} \left(-\frac{1}{b} + 1\right) = 1$$

konvergiert (siehe [[VL.31 Uneigentliche Integrale]]).

**Beispiel 3: Allgemeine $p$-Reihe**

Die Reihe $\sum_{k=1}^\infty \frac{1}{k^\alpha}$ ist:

$$\boxed{\sum_{k=1}^\infty \frac{1}{k^\alpha} \begin{cases} \text{konvergent}, & \alpha > 1 \\ \text{divergent}, & 0 < \alpha \leq 1 \end{cases}}$$

da die entsprechende Aussage für die uneigentlichen Integrale $\int_1^\infty \frac{1}{x^\alpha}\,dx$ gilt.

**Wichtig:** Bei Integralen können wir den Wert oft ausrechnen, bei Reihen ist das meist **nicht** möglich!

### Satz (Leibnizkriterium)

Ist die Folge $(a_k)_k$ **streng monoton fallend** und **gegen Null konvergent**, $\lim_{k \to \infty} a_k = 0$, so konvergiert:

$$\boxed{\sum_{k=0}^\infty (-1)^k a_k}$$

**Idee:** Die Partialsummen **oszillieren** mit **abnehmender Amplitude**, da:
- Aufeinander folgende Glieder haben verschiedene Vorzeichen
- $|a_{k+1}| < |a_k|$ (streng monoton fallend)

**Beispiel: Alternierende harmonische Reihe**

Die **alternierende harmonische Reihe** $\sum_{k=1}^\infty \frac{(-1)^k}{k}$ ist **konvergent**.

**Beweis:** $a_k = \frac{1}{k}$ ist streng monoton fallend mit $\lim_{k \to \infty} \frac{1}{k} = 0$.

Nach dem Leibnizkriterium konvergiert die Reihe. ✓

**Bemerkenswert:** Die harmonische Reihe $\sum \frac{1}{k}$ divergiert, aber die alternierende Version $\sum \frac{(-1)^k}{k}$ konvergiert!

---

## 📌 Zusammenfassung

### Definitionen

**Reihe:** $\sum_{k=0}^\infty a_k$ mit Partialsummen $s_n = \sum_{k=0}^n a_k$

**Konvergenz:** Wenn $(s_n)$ konvergiert

**Wert:** $s = \lim_{n \to \infty} s_n$ (falls existent)

### Geometrische Reihe (wichtigste Reihe!)

$$\sum_{k=0}^\infty q^k = \begin{cases} \frac{1}{1-q}, & |q| < 1 \\ \text{divergent}, & |q| \geq 1 \end{cases}$$

### Wichtige Reihen

| Reihe | Konvergenz | Bemerkung |
|-------|------------|-----------|
| $\sum_{k=1}^\infty \frac{1}{k}$ | ❌ Divergent | Harmonische Reihe |
| $\sum_{k=1}^\infty \frac{(-1)^k}{k}$ | ✅ Konvergent | Alt. harmonische Reihe |
| $\sum_{k=1}^\infty \frac{1}{k^2}$ | ✅ Konvergent | Wert: $\frac{\pi^2}{6}$ |
| $\sum_{k=1}^\infty \frac{1}{k^\alpha}$ | ✅ falls $\alpha > 1$ | $p$-Reihe |

### Konvergenzkriterien

| Kriterium | Aussage | Anwendung |
|-----------|---------|-----------|
| **Notwendig** | Konvergenz ⇒ $\lim a_k = 0$ | **Divergenztest** |
| **Integralvergleich** | $\sum f(k)$ konv. ⇔ $\int f(x)\,dx$ exist. | $f$ monoton fallend, $f \geq 0$ |
| **Leibniz** | $(a_k)$ mon. fallend, $\lim a_k = 0$ ⇒ $\sum (-1)^k a_k$ konv. | Alternierende Reihen |

### Rechenregeln

✅ $\sum (a_k + b_k) = \sum a_k + \sum b_k$ (falls beide konvergieren)

✅ $\sum ca_k = c\sum a_k$ (falls konvergiert)

⚠️ Cauchy-Produkt gilt nur wenn alle drei Reihen konvergieren

### Wichtige Erkenntnisse

✅ Endlich viele Summanden: keine Rolle für **Konvergenz**, aber für **Wert**

⚠️ $\lim a_k = 0$ ist **notwendig**, aber **nicht hinreichend** für Konvergenz

✅ Integralvergleich: verbindet Reihen mit uneigentlichen Integralen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.18 Berechnung von Grenzwerten]]: Konvergenz von Folgen, geometrische Reihe
- [[VL.24 Taylor-Approximation]]: Taylorreihen als spezielle Reihen
- [[VL.31 Uneigentliche Integrale]]: Integralvergleichskriterium
- [[VL.37 Reele Fourieranalyse]]: Fourierreihen
- [[VL.38 Approximation im quadratischen mittel]]: Parsevalsche Gleichung mit Reihen