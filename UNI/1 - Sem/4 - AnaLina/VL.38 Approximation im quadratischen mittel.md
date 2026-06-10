**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Fourierreihen #QuadratischesMittel #Konvergenz #ParsevalscheGleichung #Gibbsphänomen

---

## 🎯 Lernziele der Vorlesung

Wie gut approximieren Fourierpolynome eine periodische Funktion? Konvergenz im quadratischen Mittel und punktweise.

- **Fourierkoeffizienten** für gerade und ungerade Funktionen
- **Bestapproximation** im quadratischen Mittel
- **Fourierreihen** und deren Konvergenz
- **Parsevalsche Gleichung** und Besselsche Ungleichung
- Integration und Differentiation von Fourierreihen

---

## 1. Fourierkoeffizienten für gerade und ungerade Funktionen

### Erinnerung: Gerade und ungerade Funktionen

Die Funktion $f : \mathbb{R} \to \mathbb{R}$ heißt:

- **gerade**, falls $f(-x) = f(x)$ für alle $x \in \mathbb{R}$ (spiegelsymmetrisch zur $y$-Achse)
- **ungerade**, falls $f(-x) = -f(x)$ für alle $x \in \mathbb{R}$ (punktsymmetrisch zum Ursprung)

### Elementare Beobachtungen

**1. Sinus und Cosinus:**

Für alle $\omega \in \mathbb{R}$ und alle $k \in \mathbb{N}$:
- $\cos(k\omega t)$ ist **gerade**: $\cos(k\omega(-t)) = \cos(k\omega t)$
- $\sin(k\omega t)$ ist **ungerade**: $\sin(k\omega(-t)) = -\sin(k\omega t)$

**2. Produkte gerader/ungerader Funktionen:**

Sei $g$ gerade und $u$ ungerade. Dann:
- Ist $f$ gerade: $f \cdot g$ gerade, $f \cdot u$ ungerade
- Ist $f$ ungerade: $f \cdot g$ ungerade, $f \cdot u$ gerade

**3. Integration gerader/ungerader Funktionen:**

$$\boxed{\int_{-a}^a u(t)\,dt = 0} \quad \text{(ungerade)}$$

$$\boxed{\int_{-a}^a g(t)\,dt = 2\int_0^a g(t)\,dt} \quad \text{(gerade)}$$

**Beweis für ungerade Funktion:** Mit Substitution $s = -t$:

$$\int_{-a}^0 u(t)\,dt = -\int_a^0 u(-s)\,ds = \int_0^a u(-s)\,ds = -\int_0^a u(s)\,ds$$

Also: $\int_{-a}^a u(t)\,dt = \int_{-a}^0 u(t)\,dt + \int_0^a u(t)\,dt = 0$

**4. Periodische Funktionen - beliebiges Integrationsintervall:**

Ist $f$ $T$-periodisch, so gilt für jedes $a \in \mathbb{R}$:

$$\int_0^T f(t)\,dt = \int_a^{a+T} f(t)\,dt$$

Speziell für $a = -\frac{T}{2}$:

$$\int_0^T f(t)\,dt = \int_{-T/2}^{T/2} f(t)\,dt$$

### Satz (Fourierkoeffizienten für gerade/ungerade Funktionen)

Sei $f : \mathbb{R} \to \mathbb{R}$ eine $T$-periodische Funktion und $\omega = \frac{2\pi}{T} > 0$.

**1. Ist $f$ ungerade:** Für alle $k \in \mathbb{N}$

$$\boxed{a_k = 0, \quad b_k = \frac{4}{T}\int_0^{T/2} f(t)\sin(k\omega t)\,dt}$$

**2. Ist $f$ gerade:** Für alle $k \in \mathbb{N}$

$$\boxed{a_k = \frac{4}{T}\int_0^{T/2} f(t)\cos(k\omega t)\,dt, \quad b_k = 0}$$

**Beweis-Idee:** Mit Beobachtung 4 schreiben wir:

$$a_k = \frac{2}{T}\int_{-T/2}^{T/2} f(t)\cos(k\omega t)\,dt, \quad b_k = \frac{2}{T}\int_{-T/2}^{T/2} f(t)\sin(k\omega t)\,dt$$

Da $\cos(k\omega t)$ gerade und $\sin(k\omega t)$ ungerade ist:

- Für **ungerades** $f$: $f(t)\cos(k\omega t)$ ungerade → $a_k = 0$, $f(t)\sin(k\omega t)$ gerade → $b_k = \frac{4}{T}\int_0^{T/2} f(t)\sin(k\omega t)\,dt$
- Für **gerades** $f$: $f(t)\sin(k\omega t)$ ungerade → $b_k = 0$, $f(t)\cos(k\omega t)$ gerade → $a_k = \frac{4}{T}\int_0^{T/2} f(t)\cos(k\omega t)\,dt$

---

## 2. Beispiel: Rechteckspannung

### Funktion

Sei $f : \mathbb{R} \to \mathbb{R}$ **$2\pi$-periodisch** ($T = 2\pi$, $\omega = 1$):

$$f(t) = \begin{cases} -1, & -\pi < t < 0 \\ 0, & t = 0, \pi \\ 1, & 0 < t < \pi \end{cases}$$

Mit $f(0) = f(\pi) = 0$ wird $f$ **ungerade** → vereinfacht Berechnung!

### Berechnung der Fourierkoeffizienten

Da $f$ ungerade: $a_k = 0$ für alle $k \in \mathbb{N}$.

Für $b_k$ ($k \geq 1$):

$$b_k = \frac{4}{2\pi}\int_0^\pi f(t)\sin(kt)\,dt = \frac{2}{\pi}\int_0^\pi \sin(kt)\,dt$$

$$= \frac{2}{\pi} \cdot \left(-\frac{1}{k}\cos(kt)\right)\bigg|_0^\pi = -\frac{2}{k\pi}((-1)^k - 1)$$

$$= \begin{cases} 0, & k \text{ gerade} \\ \frac{4}{k\pi}, & k \text{ ungerade} \end{cases}$$

### Fourierpolynom

Das $(2n+1)$-te Fourierpolynom ist:

$$\varphi_{2n+1}(t) = \frac{4}{\pi}\sum_{m=0}^n \frac{1}{2m+1}\sin((2m+1)t)$$

$$= \frac{4}{\pi}\left(\sin(t) + \frac{1}{3}\sin(3t) + \frac{1}{5}\sin(5t) + \ldots + \frac{1}{2n+1}\sin((2n+1)t)\right)$$

### Gibbssches Phänomen

Der "Überschuss" (Überschwingungen) an den Sprungstellen ist ein nach **Gibbs** benanntes typisches Phänomen bei der Approximation von Sprungfunktionen durch Fourierpolynome.

**Er beträgt knapp 9% des Sprungs** und verschwindet **nicht** für $n \to \infty$!

---

## 3. Approximation im quadratischen Mittel

### $L^2$-Skalarprodukt und Norm

Das $L^2$-Skalarprodukt ist:

$$\langle f, g \rangle = \frac{2}{T}\int_0^T f(t)g(t)\,dt$$

mit induzierter Norm (quadratisches Mittel):

$$\boxed{\|f\|_{L^2} = \sqrt{\frac{2}{T}\int_0^T f(t)^2\,dt}}$$

### Satz (Approximation im quadratischen Mittel)

Sei $f$ eine stückweise monotone Funktion mit Periode $T = \frac{2\pi}{\omega} > 0$ und Fourierkoeffizienten $a_k, b_k$.

**1. Bestapproximation:** Unter allen trigonometrischen Polynomen der Ordnung $n$ liefert das $n$-te Fourierpolynom von $f$

$$\varphi_n(t) = \frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))$$

die **beste Approximation im quadratischen Mittel**.

**2. Quadratischer Fehler:**

$$\boxed{\|f - \varphi_n\|_{L^2}^2 = \|f\|_{L^2}^2 - \|\varphi_n\|_{L^2}^2}$$

Explizit:

$$\boxed{\frac{2}{T}\int_0^T (f(t) - \varphi_n(t))^2\,dt = \frac{2}{T}\int_0^T f(t)^2\,dt - \left(\frac{a_0^2}{2} + \sum_{k=1}^n (a_k^2 + b_k^2)\right)}$$

**3. Konvergenz:** Dieser Fehler **konvergiert für $n \to \infty$ gegen 0**, d.h. $f(t)$ kann im quadratischen Mittel beliebig gut durch Fourierpolynome approximiert werden.

### Beweis-Idee (für ungerade Funktion)

Suche unter allen ungeraden trigonometrischen Polynomen $\varphi(t) = \sum_{k=1}^n \beta_k \sin(k\omega t)$ dasjenige, das $\|f - \varphi\|_{L^2}^2$ minimiert.

Mit Orthogonalitätsrelationen:

$$\|\varphi\|_{L^2}^2 = \frac{2}{T}\int_0^T \varphi(t)^2\,dt = \sum_{k=1}^n \beta_k^2$$

$$\langle f, \varphi \rangle = \sum_{k=1}^n \beta_k b_k$$

Also:

$$\|f - \varphi\|_{L^2}^2 = \|f\|_{L^2}^2 - 2\sum_{k=1}^n \beta_k b_k + \sum_{k=1}^n \beta_k^2$$

$$= \|f\|_{L^2}^2 - \sum_{k=1}^n b_k^2 + \sum_{k=1}^n (b_k - \beta_k)^2$$

Wird **minimal** für $\beta_k = b_k$ (Fourierkoeffizienten)! ✓

---

## 4. Fourierreihen

### Definition (Fourierreihe)

Sei $f : \mathbb{R} \to \mathbb{R}$ eine $T$-periodische Funktion mit Fourierkoeffizienten $a_k, b_k$ und $\omega = \frac{2\pi}{T}$. Dann heißt:

$$\boxed{\frac{a_0}{2} + \sum_{k=1}^\infty (a_k \cos(k\omega t) + b_k \sin(k\omega t)) := \lim_{n \to \infty} \left(\frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))\right)}$$

die **Fourierreihe** von $f$.

### Interpretation

**1.** Die Fourierreihe entspricht der **ONB-Entwicklung** (siehe [[VL.35 Vektorräume mit Skalarprodukt 1]]), nur mit **unendlich vielen Termen**.

**2.** Die Fourierpolynome entsprechen der **Bestapproximation** durch trigonometrische Polynome (orthogonale Projektion, siehe [[VL.36 Vektorräume mit Skalarprodukt 2]]).

**3.** Der Approximationsfehler $\|f - \varphi_n\|_{L^2}$ konvergiert gegen 0 für $n \to \infty$ (Konvergenz im quadratischen Mittel).

---

## 5. Punktweise Konvergenz von Fourierreihen

### Satz (Konvergenz von Fourierreihen)

Die Funktion $f : \mathbb{R} \to \mathbb{R}$ sei $T$-periodisch und stückweise monoton, und es sei $\omega = \frac{2\pi}{T}$. Dann gilt:

**1. An Stetigkeitsstellen:** An allen Stetigkeitsstellen $t$ von $f$ konvergiert die Fourierreihe gegen $f(t)$.

**2. An Unstetigkeitsstellen:** Existieren die links- und rechtsseitigen Grenzwerte

$$f(t^-) = \lim_{\tau \nearrow t} f(\tau), \quad f(t^+) = \lim_{\tau \searrow t} f(\tau)$$

und die Fourierreihe konvergiert gegen den **Mittelwert**:

$$\boxed{\frac{f(t^-) + f(t^+)}{2}}$$

**Zusammengefasst:** Für alle $t$ gilt:

$$\boxed{\frac{f(t^-) + f(t^+)}{2} = \frac{a_0}{2} + \sum_{k=1}^\infty (a_k \cos(k\omega t) + b_k \sin(k\omega t))}$$

### Beispiele

**Beispiel 1: Sägezahnkurve**

Die 2-periodische Funktion $f(t) = \begin{cases} 1-t, & 0 < t < 2 \\ 0, & t = 0 \end{cases}$ aus [[VL.37 Reele Fourieranalyse]].

An der Unstetigkeitsstelle 0: $f(0^-) = -1$, $f(0^+) = 1$

Also: $\frac{f(0^-) + f(0^+)}{2} = 0 = f(0)$ ✓

Daher wird $f$ **überall** durch ihre Fourierreihe dargestellt:

$$\boxed{f(t) = \sum_{k=1}^\infty \frac{2}{\pi k}\sin(k\pi t) \quad \text{für alle } t \in \mathbb{R}}$$

**Beispiel 2: Rechteckspannung**

Die $2\pi$-periodische Funktion $g$ von oben. Für alle $t \in \mathbb{R}$:

$$\boxed{g(t) = \frac{4}{\pi}\sum_{k=0}^\infty \frac{1}{2k+1}\sin((2k+1)t)}$$

---

## 6. Parsevalsche Gleichung und Besselsche Ungleichung

### Satz (Parsevalsche Gleichung)

Die Funktion $f : \mathbb{R} \to \mathbb{R}$ sei $T = \frac{2\pi}{\omega}$-periodisch und stückweise monoton mit Fourierkoeffizienten $a_k, b_k$. Dann gilt:

$$\boxed{\frac{2}{T}\int_0^T f(t)^2\,dt = \frac{a_0^2}{2} + \sum_{k=1}^\infty (a_k^2 + b_k^2) := \lim_{n \to \infty} \left(\frac{a_0^2}{2} + \sum_{k=1}^n (a_k^2 + b_k^2)\right)}$$

**Interpretation:** Das "Energie"-Integral von $f$ entspricht der Summe der quadrierten Fourierkoeffizienten.

### Besselsche Ungleichung

Durch Abschneiden der Summe erhält man:

$$\boxed{\|f\|_{L^2}^2 = \frac{2}{T}\int_0^T f(t)^2\,dt \geq \frac{a_0^2}{2} + \sum_{k=1}^n (a_k^2 + b_k^2) = \|\varphi_n\|_{L^2}^2}$$

**Interpretation:** Das Fourierpolynom hat immer kleinere oder gleiche Norm als $f$.

### Anwendung: Berechnung von Reihen

Mit der Parsevalschen Gleichung lassen sich Grenzwerte von Reihen berechnen!

**Beispiel 1: Sägezahn** $f(t) = 1-t$, $0 < t < 2$

$$\sum_{k=1}^\infty \frac{4}{\pi^2 k^2} = \frac{2}{2}\int_0^2 (1-t)^2\,dt = -\frac{1}{3}(1-t)^3\bigg|_0^2 = \frac{2}{3}$$

Also:

$$\boxed{\sum_{k=1}^\infty \frac{1}{k^2} = \frac{\pi^2}{6}}$$

**Beispiel 2: Rechteckspannung** $g$

$$\frac{16}{\pi^2}\sum_{k=0}^\infty \frac{1}{(2k+1)^2} = \frac{2}{2\pi}\int_0^{2\pi} g(t)^2\,dt = 2$$

Also:

$$\boxed{\sum_{k=0}^\infty \frac{1}{(2k+1)^2} = \frac{\pi^2}{8}}$$

---

## 7. Integration und Differentiation von Fourierreihen

### Integration - ✅ Erlaubt

Konvergente Fourierreihen darf man **gliedweise integrieren**:

$$\boxed{\int_a^b \left(\frac{a_0}{2} + \sum_{k=1}^\infty (a_k \cos(k\omega t) + b_k \sin(k\omega t))\right)\,dt}$$

$$= \int_a^b \frac{a_0}{2}\,dt + \sum_{k=1}^\infty \int_a^b (a_k \cos(k\omega t) + b_k \sin(k\omega t))\,dt$$

Man kann jeden Summand einzeln integrieren!

### Differentiation - ❌ Im Allgemeinen nicht erlaubt

Man darf Fourierreihen **im Allgemeinen nicht gliedweise differenzieren**.

**Gegenbeispiel:** Sägezahn $1 - t = 2\sum_{k=1}^\infty \frac{1}{k\pi}\sin(k\pi t)$ für $0 < t < 2$.

Gliedweise Ableiten würde ergeben: $2\sum_{k=1}^\infty \cos(k\pi t)$

An der Stelle $t = 1$ (wo $f$ keinen Sprung hat!):

$$2\sum_{k=1}^\infty \cos(k\pi) = 2\sum_{k=1}^\infty (-1)^k$$

Diese Reihe **divergiert**! ❌

**Wichtig:** Probleme entstehen nicht nur an Sprungstellen!

---

## 📌 Zusammenfassung

### Fourierkoeffizienten für spezielle Funktionen

| Funktion | $a_k$ | $b_k$ |
|----------|-------|-------|
| **Ungerade** | $0$ | $\frac{4}{T}\int_0^{T/2} f(t)\sin(k\omega t)\,dt$ |
| **Gerade** | $\frac{4}{T}\int_0^{T/2} f(t)\cos(k\omega t)\,dt$ | $0$ |

**Vorteil:** Nur halbes Integrationsintervall, nur eine Art Koeffizient!

### Approximation im quadratischen Mittel

**Bestapproximation:** $\varphi_n$ ist unter allen trigonometrischen Polynomen Ordnung $n$ am nächsten an $f$ (in $L^2$-Norm)

**Quadratischer Fehler:** $\|f - \varphi_n\|_{L^2}^2 = \|f\|_{L^2}^2 - \|\varphi_n\|_{L^2}^2$

**Konvergenz:** $\|f - \varphi_n\|_{L^2} \to 0$ für $n \to \infty$

### Fourierreihen

$$\frac{a_0}{2} + \sum_{k=1}^\infty (a_k \cos(k\omega t) + b_k \sin(k\omega t))$$

**Punktweise Konvergenz:**
- An Stetigkeitsstellen: gegen $f(t)$
- An Unstetigkeitsstellen: gegen $\frac{f(t^-) + f(t^+)}{2}$

### Parsevalsche Gleichung

$$\frac{2}{T}\int_0^T f(t)^2\,dt = \frac{a_0^2}{2} + \sum_{k=1}^\infty (a_k^2 + b_k^2)$$

**Anwendung:** Berechnung von Reihen wie $\sum \frac{1}{k^2} = \frac{\pi^2}{6}$

### Integration vs. Differentiation

✅ **Gliedweise Integration** ist erlaubt

❌ **Gliedweise Differentiation** ist im Allgemeinen NICHT erlaubt

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.35 Vektorräume mit Skalarprodukt 1]]: ONB-Entwicklung, $L^2$-Skalarprodukt
- [[VL.36 Vektorräume mit Skalarprodukt 2]]: Bestapproximation, orthogonale Projektion
- [[VL.37 Reele Fourieranalyse]]: Fourierkoeffizienten, Fourierpolynome