**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Substitutionsregel #KomplexeIntegration #Orthogonalität #Fourier

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt die Substitutionsregel ein und erweitert die Integration auf komplexwertige Funktionen.

- **Substitutionsregel** (zwei Versionen) für bestimmte und unbestimmte Integrale
- Anwendungsbeispiele der Substitution
- **Integration komplexwertiger Funktionen**
- **Orthogonalitätsrelationen** für trigonometrische Funktionen

---

## 1. Substitutionsregel - Version 1

### Motivation

Die **Substitutionsregel** (= **Ersetzungsregel**) entspricht der **Kettenregel** beim Ableiten.

Aus der Kettenregel: $$\frac{d}{dx}F(g(x)) = F'(g(x)) \cdot g'(x) = f(g(x)) \cdot g'(x)$$

folgt durch Integration: $$\int f(g(x))g'(x),dx = F(g(x)) + c$$

### Satz (Substitutionsregel - Version 1, unbestimmt)

**Berechnung von** $\int f(g(x))g'(x),dx$:

**Schritt 1: Substitution** $$t = g(x), \quad dt = g'(x),dx$$

(Formal: $\frac{dt}{dx} = g'(x)$, mit $dx$ multiplizieren)

$$\int f(g(x))g'(x),dx = \int f(t),dt$$

**Schritt 2: Stammfunktion berechnen** $$\int f(t),dt = F(t) + c, \quad c \in \mathbb{R}$$

**Schritt 3: Rücksubstitution** $t = g(x)$ $$\boxed{\int f(g(x))g'(x),dx = F(g(x)) + c, \quad c \in \mathbb{R}}$$

### Satz (Substitutionsregel - Version 1, bestimmt)

**Berechnung von** $\int_a^b f(g(x))g'(x),dx$:

**Schritt 1: Substitution mit Grenzentransformation** $$t = g(x), \quad dt = g'(x),dx$$

$$\int_{x=a}^{x=b} f(g(x))g'(x),dx = \int_{t=g(a)}^{t=g(b)} f(t),dt$$

**Schritt 2: Stammfunktion auswerten** $$\boxed{\int_a^b f(g(x))g'(x),dx = F\bigg|_{g(a)}^{g(b)} = F(g(b)) - F(g(a))}$$

**Vorteil:** Keine Rücksubstitution nötig, wenn man die Grenzen direkt transformiert!

---

## 2. Beispiele zur Substitutionsregel - Version 1

### Beispiel 1: $\int \cos(x^2) \cdot 2x,dx$

**Substitution:** $t = x^2$, dann $dt = 2x,dx$

$$\int \cos(x^2) \cdot 2x,dx = \int \cos(t),dt = \sin(t) + c = \sin(x^2) + c$$

### Beispiel 2: $\int_0^2 \cos(x^2) \cdot 2x,dx$

**Substitution:** $t = x^2$, dann $dt = 2x,dx$

**Grenzen transformieren:**

- $x = 0 \Rightarrow t = 0$
- $x = 2 \Rightarrow t = 4$

$$\int_{x=0}^{x=2} \cos(x^2) \cdot 2x,dx = \int_{t=0}^{t=4} \cos(t),dt = \sin(t)\bigg|_0^4 = \sin(4)$$

### Beispiel 3: $\int_0^3 \frac{x}{(1+x^2)^2},dx$

**Substitution:** $t = 1 + x^2$, dann $dt = 2x,dx$

**Grenzen:**

- $x = 0 \Rightarrow t = 1$
- $x = 3 \Rightarrow t = 10$

$$\int_{x=0}^{x=3} \frac{x}{(1+x^2)^2},dx = \int_{t=1}^{t=10} \frac{1}{t^2} \cdot \frac{1}{2},dt = -\frac{1}{2} \cdot \frac{1}{t}\bigg|_1^{10} = -\frac{1}{2}\left(\frac{1}{10} - 1\right) = \frac{9}{20}$$

### Beispiel 4: Wichtige Formel

**Mit Substitution** $t = g(x)$, also $dt = g'(x),dx$:

$$\boxed{\int \frac{g'(x)}{g(x)},dx = \int \frac{1}{t},dt = \ln|t| + c = \ln|g(x)| + c}$$

**Merke:** Ableitung geteilt durch Funktion = ln der Funktion!

### Beispiel 5: Mehrfache Substitution

**Berechne** $\int \frac{4x \arcsin(x^2)}{\sqrt{1-x^4}},dx$

**Erste Substitution:** $\phi = x^2$, dann $d\phi = 2x,dx$

$$\int \frac{4x \arcsin(x^2)}{\sqrt{1-x^4}},dx = \int \frac{2\arcsin(\phi)}{\sqrt{1-\phi^2}},d\phi$$

**Zweite Substitution:** $t = \arcsin(\phi)$, dann $dt = \frac{1}{\sqrt{1-\phi^2}},d\phi$

$$= \int 2t,dt = t^2 + c$$

**Rücksubstitution:** $$= \arcsin(x^2)^2 + c$$

---

## 3. Substitutionsregel - Version 2

### Satz (Substitutionsregel - Version 2, unbestimmt)

**Berechnung von** $\int f(x),dx$:

**Schritt 1: Substitution** $$x = g(t), \quad dx = g'(t),dt$$

(mit umkehrbarem $g$)

$$\int f(x),dx = \int f(g(t))g'(t),dt$$

**Schritt 2: Stammfunktion berechnen** $$\int f(g(t))g'(t),dt = H(t) + c, \quad c \in \mathbb{R}$$

**Schritt 3: Rücksubstitution** $t = g^{-1}(x)$ $$\boxed{\int f(x),dx = H(g^{-1}(x)) + c, \quad c \in \mathbb{R}}$$

### Satz (Substitutionsregel - Version 2, bestimmt)

**Berechnung von** $\int_a^b f(x),dx$:

**Schritt 1: Substitution mit Grenzentransformation** $$x = g(t), \quad dx = g'(t),dt$$

$$\int_{x=a}^{x=b} f(x),dx = \int_{t=g^{-1}(a)}^{t=g^{-1}(b)} f(g(t))g'(t),dt$$

**Schritt 2: Stammfunktion auswerten** $$\boxed{\int_a^b f(x),dx = H(g^{-1}(b)) - H(g^{-1}(a))}$$

---

## 4. Beispiele zur Substitutionsregel - Version 2

### Beispiel 1: Fläche eines Kreises

**Berechne die Fläche** des Kreises mit Radius $r > 0$:

Auf dem Kreisrand: $x^2 + y^2 = r^2$, also $y = \pm\sqrt{r^2 - x^2}$

**Fläche:** $$A = 2\int_{-r}^r \sqrt{r^2 - x^2},dx$$

**Substitution:** $x = r\sin(t)$, dann $dx = r\cos(t),dt$

**Grenzen:**

- $x = -r \Rightarrow t = -\frac{\pi}{2}$
- $x = r \Rightarrow t = \frac{\pi}{2}$

$$A = 2\int_{-\pi/2}^{\pi/2} \sqrt{r^2 - r^2\sin^2(t)} \cdot r\cos(t),dt = 2r^2 \int_{-\pi/2}^{\pi/2} \sqrt{\cos^2(t)} \cdot \cos(t),dt$$

Da $\cos(t) \geq 0$ für $t \in [-\frac{\pi}{2}, \frac{\pi}{2}]$: $$= 2r^2 \int_{-\pi/2}^{\pi/2} \cos^2(t),dt$$

Mit der Stammfunktion aus [[VL.29 Integrationsregeln 1]] ($\int \cos^2(t),dt = \frac{1}{2}(\sin(t)\cos(t) + t)$):

$$A = 2r^2 \cdot \frac{1}{2}(\sin(t)\cos(t) + t)\bigg|_{-\pi/2}^{\pi/2} = r^2 \cdot \pi = \boxed{\pi r^2}$$

### Beispiel 2: $\int \arcsin(x),dx$

**Substitution:** $x = \sin(t)$, dann $t = \arcsin(x)$ und $dx = \cos(t),dt$

$$\int \arcsin(x),dx = \int t\cos(t),dt$$

**Partielle Integration:** $u'(t) = \cos(t)$, $v(t) = t$ $$= t\sin(t) - \int \sin(t),dt = t\sin(t) + \cos(t) + c$$

Mit $\cos(t) = \sqrt{1 - \sin^2(t)}$ (da $t = \arcsin(x) \in [-\frac{\pi}{2}, \frac{\pi}{2}]$):

**Rücksubstitution:** $$\boxed{\int \arcsin(x),dx = x\arcsin(x) + \sqrt{1-x^2} + c}$$

---

## 5. Orthogonalitätsrelationen

### Motivation

Die folgenden Integrale sind wichtig für die **Fourieranalyse** (siehe Vorlesung 37).

### Satz (Orthogonalitätsrelationen)

Sei $T > 0$ (Periode) und $\omega = \frac{2\pi}{T}$ (Kreisfrequenz). Dann gilt für $k, \ell \in \mathbb{N}$:

**1. Kosinus-Kosinus:** $$\boxed{\frac{2}{T}\int_0^T \cos(k\omega x)\cos(\ell\omega x),dx = \begin{cases} 2, & k = \ell = 0 \\ 1, & k = \ell > 0 \\ 0, & k \neq \ell \end{cases}}$$

**2. Sinus-Sinus:** $$\boxed{\frac{2}{T}\int_0^T \sin(k\omega x)\sin(\ell\omega x),dx = \begin{cases} 1, & k = \ell > 0 \\ 0, & \text{sonst} \end{cases}}$$

**3. Sinus-Kosinus:** $$\boxed{\frac{2}{T}\int_0^T \sin(k\omega x)\cos(\ell\omega x),dx = 0}$$

### Beweis-Skizze

**Additionstheoreme:** $$\begin{align} \cos(\alpha)\cos(\beta) &= \frac{1}{2}(\cos(\alpha + \beta) + \cos(\alpha - \beta)) \ \sin(\alpha)\sin(\beta) &= \frac{1}{2}(\cos(\alpha - \beta) - \cos(\alpha + \beta)) \ \sin(\alpha)\cos(\beta) &= \frac{1}{2}(\sin(\alpha + \beta) + \sin(\alpha - \beta)) \end{align}$$

**Für** $k \neq \ell$: Die Integrale von $\cos(m\omega x)$ und $\sin(m\omega x)$ über eine volle Periode sind $0$ (für $m \neq 0$).

**Für** $k = \ell$: Direktes Ausrechnen mit Substitution.

---

## 6. Integration komplexer Funktionen

### Definition (Integral komplexwertiger Funktionen)

Sei $f : [a, b] \to \mathbb{C}$ und seien $u, v : [a, b] \to \mathbb{R}$ mit:

- $u(x) = \text{Re}(f(x))$
- $v(x) = \text{Im}(f(x))$

also $f = u + iv$.

Sind $u, v$ integrierbar, so ist: $$\boxed{\int_a^b f(x),dx := \int_a^b u(x),dx + i\int_a^b v(x),dx}$$

**Interpretation:** Integriere **Real- und Imaginärteil getrennt**.

### Was bleibt gültig?

**Bleiben gültig für komplexwertige Funktionen:**

1. ✅ **Hauptsatz:** $\int_a^b f(x),dx = F(b) - F(a)$ (falls $F' = f$)
2. ✅ **Partielle Integration**
3. ✅ **Substitutionsregel**
4. ✅ **Linearität**
5. ✅ **Dreiecksungleichung**
6. ✅ **Aufteilen an Zwischenpunkt**

**Nicht mehr gültig:**

1. ❌ **Monotonie** (macht für komplexe Zahlen keinen Sinn)
2. ❌ **Integralabschätzung**
3. ❌ **Mittelwertsatz der Integralrechnung**

### Beispiele

**Beispiel 1:** $f(x) = (x + i)^2$

**Methode 1 (direktes Ausrechnen):** $$\int (x+i)^2,dx = \int (x^2 + 2ix - 1),dx = \int (x^2 - 1),dx + i\int 2x,dx$$ $$= \frac{1}{3}x^3 - x + ix^2 + c$$

**Methode 2 (mit Stammfunktion):** $$F(x) = \frac{1}{3}(x+i)^3$$

Probe: $F'(x) = (x+i)^2$ ✓

Ausmultiplizieren: $$F(x) = \frac{1}{3}(x^3 + 3ix^2 - 3x - i) = \frac{1}{3}x^3 - x + ix^2 - \frac{i}{3}$$

Dies ist die Stammfunktion mit $c = -\frac{i}{3}$.

**Beispiel 2:** $f(x) = \frac{1}{x-i}$

**Naiver Ansatz:** $F(x) = \ln|x-i|$ funktioniert **nicht**!

Probe: $F(x) = \frac{1}{2}\ln(x^2 + 1)$, also $F'(x) = \frac{x}{x^2+1} \neq f(x)$ ✗

(Klar: $F$ ist reellwertig, kann also keine komplexwertige Funktion als Ableitung haben!)

**Richtig:** $$\int \frac{1}{x-i},dx = \int \frac{x+i}{x^2+1},dx = \int \frac{x}{x^2+1},dx + i\int \frac{1}{x^2+1},dx$$ $$\boxed{= \frac{1}{2}\ln(x^2+1) + i\arctan(x) + c}$$

---

## 7. Wichtige Formel für komplexe Exponentialfunktion

### Satz

Für alle $z \in \mathbb{C}$, $z \neq 0$: $$\boxed{\int e^{zx},dx = \frac{1}{z}e^{zx} + c, \quad c \in \mathbb{C}}$$

### Beweis

Für $z = a + ib$ mit reellen $a, b$: $$e^{zx} = e^{ax+ibx} = e^{ax}(\cos(bx) + i\sin(bx))$$

Ableitung: $$\frac{d}{dx}e^{zx} = ae^{ax}(\cos(bx) + i\sin(bx)) + e^{ax}(-b\sin(bx) + ib\cos(bx))$$ $$= (a + ib)e^{ax}(\cos(bx) + i\sin(bx)) = ze^{zx}$$

Also ist $\frac{1}{z}e^{zx}$ eine Stammfunktion von $e^{zx}$.

### Anwendung: Komplexe Orthogonalitätsrelationen

**Seien** $k, \ell \in \mathbb{Z}$ und $T > 0$, $\omega = \frac{2\pi}{T}$:

**Für** $k = \ell$: $$\int_0^T e^{ik\omega t}e^{-i\ell\omega t},dt = \int_0^T 1,dt = T$$

**Für** $k \neq \ell$: $$\int_0^T e^{i(k-\ell)\omega t},dt = \frac{1}{i(k-\ell)\omega}e^{i(k-\ell)\omega t}\bigg|_0^T = \frac{1}{i(k-\ell)\omega}(e^{i(k-\ell)2\pi} - 1) = 0$$

**Kompakt:** $$\boxed{\frac{1}{T}\int_0^T e^{ik\omega t}e^{-i\ell\omega t},dt = \begin{cases} 1, & k = \ell \\ 0, & k \neq \ell \end{cases}}$$

**Bemerkung:** Durch Vergleich von Real- und Imaginärteil erhält man die Orthogonalitätsrelationen aus Abschnitt 5!

Die Rechnung im **Komplexen** ist **viel einfacher** als im Reellen!

---

## 📌 Zusammenfassung

### Substitutionsregel - Zwei Versionen

|**Version**|**Substitution**|**Anwendung**|
|---|---|---|
|**Version 1**|$t = g(x)$|$\int f(g(x))g'(x),dx$ gegeben|
|**Version 2**|$x = g(t)$|$\int f(x),dx$ mit geschicktem $g$|

### Wichtige Formeln

$$\int \frac{g'(x)}{g(x)},dx = \ln|g(x)| + c$$

$$\int e^{zx},dx = \frac{1}{z}e^{zx} + c \quad (z \in \mathbb{C}, z \neq 0)$$

### Orthogonalitätsrelationen

**Reell (Sinus/Kosinus):** $$\frac{2}{T}\int_0^T \cos(k\omega x)\cos(\ell\omega x),dx = \delta_{k\ell}$$ (für $k, \ell > 0$, wobei $\delta_{k\ell}$ das Kronecker-Delta ist)

**Komplex:** $$\frac{1}{T}\int_0^T e^{ik\omega t}e^{-i\ell\omega t},dt = \delta_{k\ell}$$

### Komplexe Integration

- Integriere Real- und Imaginärteil getrennt
- Hauptsatz, partielle Integration, Substitution bleiben gültig
- Monotonie, Mittelwertsatz gelten nicht mehr

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.21 Differenzierbarkeit]]: Kettenregel als Basis für Substitution
- [[VL.26 Elementare Funktionen 2]]: Komplexe Exponentialfunktion
- [[VL.29 Integrationsregeln 1]]: Partielle Integration, Grundintegrale
- [[VL.37 Reele Fourieranalyse]]: Orthogonalitätsrelationen (wird dort verwendet)
