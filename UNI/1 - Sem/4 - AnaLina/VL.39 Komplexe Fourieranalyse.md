**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #KomplexeFourieranalysis #Eulerformel #KomplexeFourierkoeffizienten #Umrechnungsformeln

---

## 🎯 Lernziele der Vorlesung

Sinus- und Cosinusfunktionen lassen sich bequemer mittels komplexer Exponentialfunktionen darstellen.

- **Euler-Formel** und komplexe Darstellung von Sinus/Cosinus
- **Komplexe trigonometrische Polynome**
- **Komplexe Fourierkoeffizienten** und Fourierpolynome
- **Umrechnungsformeln** zwischen reellen und komplexen Koeffizienten
- Vereinfachungen durch komplexe Schreibweise

---

## 1. Euler-Formel und trigonometrische Funktionen

### Euler-Formel

$$\boxed{e^{i\varphi} = \cos(\varphi) + i\sin(\varphi)}$$

### Darstellung von Sinus und Cosinus

Aus der Euler-Formel folgt:

$$\boxed{\cos(\varphi) = \text{Re}(e^{i\varphi}) = \frac{e^{i\varphi} + e^{-i\varphi}}{2}}$$

$$\boxed{\sin(\varphi) = \text{Im}(e^{i\varphi}) = \frac{e^{i\varphi} - e^{-i\varphi}}{2i}}$$

**Beweis:** 
- $e^{i\varphi} + e^{-i\varphi} = (\cos\varphi + i\sin\varphi) + (\cos\varphi - i\sin\varphi) = 2\cos\varphi$
- $e^{i\varphi} - e^{-i\varphi} = (\cos\varphi + i\sin\varphi) - (\cos\varphi - i\sin\varphi) = 2i\sin\varphi$

---

## 2. Von reellen zu komplexen trigonometrischen Polynomen

### Reelles trigonometrisches Polynom

$$\varphi(t) = \frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))$$

### Umformung in komplexe Schreibweise

Mit den Formeln für $\cos$ und $\sin$:

$$\varphi(t) = \frac{a_0}{2} + \sum_{k=1}^n \left(a_k \cdot \frac{e^{ik\omega t} + e^{-ik\omega t}}{2} + b_k \cdot \frac{e^{ik\omega t} - e^{-ik\omega t}}{2i}\right)$$

$$= \frac{a_0}{2} + \sum_{k=1}^n \left(\frac{a_k}{2}e^{ik\omega t} + \frac{a_k}{2}e^{-ik\omega t} + \frac{b_k}{2i}e^{ik\omega t} - \frac{b_k}{2i}e^{-ik\omega t}\right)$$

$$= \underbrace{\frac{a_0}{2}}_{=: c_0} + \sum_{k=1}^n \underbrace{\left(\frac{a_k}{2} - i\frac{b_k}{2}\right)}_{=: c_k} e^{ik\omega t} + \sum_{k=1}^n \underbrace{\left(\frac{a_k}{2} + i\frac{b_k}{2}\right)}_{=: c_{-k}} e^{-ik\omega t}$$

$$= \boxed{\sum_{k=-n}^n c_k e^{ik\omega t}}$$

**Wichtig:** Die Summe läuft jetzt von $-n$ bis $n$ (statt von 0 bis $n$)!

---

## 3. Orthonormalität der komplexen Basisfunktionen

### Komplexes Skalarprodukt

$$\boxed{\langle f, g \rangle = \frac{1}{T}\int_0^T f(t)\overline{g(t)}\,dt}$$

### Orthonormalität von $e^{ik\omega t}$

Für alle $k, \ell \in \mathbb{Z}$ gilt:

$$\boxed{\langle e^{ik\omega t}, e^{i\ell\omega t} \rangle = \frac{1}{T}\int_0^T e^{ik\omega t}e^{-i\ell\omega t}\,dt = \begin{cases} 1, & k = \ell \\ 0, & k \neq \ell \end{cases}}$$

**Beweis:** Wurde bereits in [[VL.30 Integrationsregeln 2]] (Beispiel 30.8) nachgerechnet.

**Für $k = \ell$:**

$$\int_0^T e^{ik\omega t}e^{-ik\omega t}\,dt = \int_0^T 1\,dt = T$$

**Für $k \neq \ell$:**

$$\int_0^T e^{i(k-\ell)\omega t}\,dt = \frac{1}{i(k-\ell)\omega}e^{i(k-\ell)\omega t}\bigg|_0^T = \frac{1}{i(k-\ell)\omega}(e^{i(k-\ell)2\pi} - 1) = 0$$

---

## 4. Komplexe trigonometrische Polynome

### Definition (Komplexe trigonometrische Polynome)

Sei $T > 0$ und $\omega = \frac{2\pi}{T}$. Die komplexwertigen Funktionen der Form

$$\boxed{\sum_{k=-n}^n c_k e^{ik\omega t}, \quad c_k \in \mathbb{C}}$$

heißen **komplexe trigonometrische Polynome vom Grad** (oder von der Ordnung) $n$.

Diese sind **$T$-periodisch**.

---

## 5. Komplexe Fourierkoeffizienten

### Herleitung

Sind $a_k, b_k$ die reellen Fourierkoeffizienten einer Funktion mit Periode $T = \frac{2\pi}{\omega}$, so für $k \geq 0$:

$$c_k = \frac{a_k}{2} - i\frac{b_k}{2} = \frac{1}{T}\int_0^T f(t)\cos(k\omega t)\,dt - i\frac{1}{T}\int_0^T f(t)\sin(k\omega t)\,dt$$

$$= \frac{1}{T}\int_0^T f(t)(\cos(k\omega t) - i\sin(k\omega t))\,dt = \frac{1}{T}\int_0^T f(t)e^{-ik\omega t}\,dt$$

Man kann nachrechnen, dass die Formel auch für $k < 0$ gilt.

### Definition (Komplexe Fourierkoeffizienten)

Sei $f : \mathbb{R} \to \mathbb{R}$ (oder $f : \mathbb{R} \to \mathbb{C}$) eine stückweise monotone Funktion der Periode $T > 0$ und $\omega = \frac{2\pi}{T}$.

Die **komplexen Fourierkoeffizienten** von $f$ sind:

$$\boxed{c_k = \langle f, e^{ik\omega t} \rangle = \frac{1}{T}\int_0^T f(t)e^{-ik\omega t}\,dt, \quad k \in \mathbb{Z}}$$

### Definition (Komplexes Fourierpolynom)

Das **$n$-te komplexe Fourierpolynom** von $f$ ist:

$$\boxed{\varphi_n(t) = \sum_{k=-n}^n c_k e^{ik\omega t}}$$

---

## 6. Vorteile der komplexen Schreibweise

### Bemerkungen

**1. Einfachere Formeln:**
- Faktor vor dem Integral: $\frac{1}{T}$ statt $\frac{2}{T}$
- Keine Sonderrolle von $a_0$ mehr (kein Faktor $\frac{1}{2}$)
- Nur eine Formel statt zwei ($a_k$ und $b_k$)

**2. Bestapproximation:**

Analog zu [[VL.38 Approximation im quadratischen mittel]] ist das komplexe Fourierpolynom vom Grad $n$ dasjenige komplexe trigonometrische Polynom vom Grad $n$, das $f$ **am besten im quadratischen Mittel** approximiert (mit dem komplexen Skalarprodukt), also in der Norm:

$$\|f\|_{L^2} = \sqrt{\langle f, f \rangle} = \sqrt{\frac{1}{T}\int_0^T |f(t)|^2\,dt}$$

**3. Symmetrie für reellwertige Funktionen:**

Ist $f$ **reellwertig**, so sind die Fourierkoeffizienten $a_k, b_k$ **reell** und es gilt:

$$\boxed{c_{-k} = \overline{c_k}}$$

**Beweis:**

$$c_{-k} = \frac{1}{T}\int_0^T f(t)e^{ik\omega t}\,dt = \overline{\frac{1}{T}\int_0^T f(t)e^{-ik\omega t}\,dt} = \overline{c_k}$$

(da $f(t)$ reell ist)

Dies kann die Berechnung vereinfachen: Man muss nur die Koeffizienten für $k \geq 0$ berechnen!

---

## 7. Beispiel: Sägezahnkurve (komplex)

### Funktion

Die 2-periodische Funktion $f : \mathbb{R} \to \mathbb{R}$ aus [[VL.37 Fourieranalysis]]:

$$f(t) = \begin{cases} 1 - t, & 0 < t < 2 \\ 0, & t = 0 \end{cases}$$

Es ist $T = 2$, also $\omega = \frac{2\pi}{T} = \pi$.

### Berechnung der komplexen Fourierkoeffizienten

**Für $k = 0$:**

$$c_0 = \frac{1}{2}\int_0^2 (1-t)e^{i0\pi t}\,dt = \frac{1}{2}\int_0^2 (1-t)\,dt = \frac{1}{2}\left(t - \frac{t^2}{2}\right)\bigg|_0^2 = 0$$

**Für $k \neq 0$:**

$$c_k = \frac{1}{2}\int_0^2 (1-t)e^{-ik\pi t}\,dt = \frac{1}{2}\int_0^2 e^{-ik\pi t}\,dt + \frac{1}{2}\int_0^2 te^{ik\pi t}\,dt$$

**Erstes Integral:** (orthogonal zu $e^{i0\pi t}$)

$$\int_0^2 e^{-ik\pi t}\,dt = \frac{1}{-ik\pi}e^{-ik\pi t}\bigg|_0^2 = \frac{1}{-ik\pi}(e^{-i2k\pi} - 1) = 0$$

**Zweites Integral:** (partielle Integration mit $u' = e^{ik\pi t}$, $v = t$)

$$\int_0^2 te^{ik\pi t}\,dt = \frac{t}{ik\pi}e^{ik\pi t}\bigg|_0^2 - \int_0^2 \frac{1}{ik\pi}e^{ik\pi t}\,dt$$

$$= \frac{2}{ik\pi}e^{i2k\pi} - \frac{1}{ik\pi} \cdot \frac{1}{ik\pi}e^{ik\pi t}\bigg|_0^2 = \frac{2}{ik\pi} - 0 = \frac{2}{ik\pi}$$

Also:

$$\boxed{c_k = \frac{1}{ik\pi} \quad \text{für } k \neq 0}$$

### Komplexes Fourierpolynom

$$\varphi_n(t) = \sum_{k=-n}^n c_k e^{ik\omega t} = \frac{1}{\pi}\sum_{\substack{k=-n \\ k \neq 0}}^n \frac{1}{ik}e^{ik\pi t}$$

### Umformung ins Reelle

Zusammenfassen der Terme mit negativem und positivem Index:

$$\varphi_n(t) = \frac{1}{\pi}\sum_{k=1}^n \left(\frac{1}{ik}e^{ik\pi t} + \frac{1}{-ik}e^{-ik\pi t}\right)$$

$$= \frac{1}{\pi}\sum_{k=1}^n \frac{1}{ik}(e^{ik\pi t} - e^{-ik\pi t}) = \frac{1}{\pi}\sum_{k=1}^n \frac{1}{ik} \cdot 2i\sin(k\pi t)$$

$$= \boxed{\frac{2}{\pi}\sum_{k=1}^n \frac{\sin(k\pi t)}{k}}$$

Dies ist das reelle Fourierpolynom aus Beispiel 37.7! ✓

---

## 8. Umrechnungsformeln

### Von reell zu komplex

Sei $f : \mathbb{R} \to \mathbb{R}$ (oder $f : \mathbb{R} \to \mathbb{C}$) eine $T$-periodische Funktion und $\omega = \frac{2\pi}{T}$.

Sind die **reellen Fourierkoeffizienten** $a_k, b_k$ gegeben, so sind:

$$\boxed{c_k = \frac{1}{2}(a_k - ib_k), \quad k \geq 1}$$

$$\boxed{c_0 = \frac{a_0}{2}}$$

$$\boxed{c_{-k} = \frac{1}{2}(a_k + ib_k), \quad k \geq 1}$$

**Merke:** $c_k$ und $c_{-k}$ sind konjugiert komplex, falls $a_k, b_k$ reell (d.h. $f$ reellwertig).

### Von komplex zu reell

Sind die **komplexen Fourierkoeffizienten** $c_k$, $k \in \mathbb{Z}$, gegeben, so gilt:

$$\boxed{a_0 = 2c_0}$$

$$\boxed{a_k = c_k + c_{-k}, \quad k \geq 1}$$

$$\boxed{b_k = i(c_k - c_{-k}), \quad k \geq 1}$$

**Probe:** Einsetzen der ersten Formeln in die zweiten ergibt die Identität.

---

## 📌 Zusammenfassung

### Euler-Formel und Darstellung

$$e^{i\varphi} = \cos(\varphi) + i\sin(\varphi)$$

$$\cos(\varphi) = \frac{e^{i\varphi} + e^{-i\varphi}}{2}, \quad \sin(\varphi) = \frac{e^{i\varphi} - e^{-i\varphi}}{2i}$$

### Komplexes vs. Reelles Fourierpolynom

| Eigenschaft | Reell | Komplex |
|-------------|-------|---------|
| **Form** | $\frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))$ | $\sum_{k=-n}^n c_k e^{ik\omega t}$ |
| **Koeffizienten** | $a_k = \frac{2}{T}\int_0^T f(t)\cos(k\omega t)\,dt$ <br> $b_k = \frac{2}{T}\int_0^T f(t)\sin(k\omega t)\,dt$ | $c_k = \frac{1}{T}\int_0^T f(t)e^{-ik\omega t}\,dt$ |
| **Faktor** | $\frac{2}{T}$ | $\frac{1}{T}$ |
| **Sonderfall $k=0$** | $\frac{a_0}{2}$ | $c_0$ (keine Sonderrolle!) |
| **Index** | $k \geq 0$ | $k \in \mathbb{Z}$ |

### Vorteile der komplexen Schreibweise

✅ **Einfachere Formeln** (ein Faktor, eine Formel, keine Sonderrolle von $a_0$)

✅ **Einheitliche Behandlung** aller Frequenzen

✅ **Symmetrie:** $c_{-k} = \overline{c_k}$ für reellwertige $f$

✅ **Orthonormale Basis:** $\{e^{ik\omega t}\}_{k \in \mathbb{Z}}$

### Umrechnungsformeln (Kurzfassung)

**Reell → Komplex:**

$$c_k = \frac{1}{2}(a_k - ib_k), \quad c_0 = \frac{a_0}{2}, \quad c_{-k} = \frac{1}{2}(a_k + ib_k)$$

**Komplex → Reell:**

$$a_0 = 2c_0, \quad a_k = c_k + c_{-k}, \quad b_k = i(c_k - c_{-k})$$

### Komplexes Skalarprodukt und Norm

$$\langle f, g \rangle = \frac{1}{T}\int_0^T f(t)\overline{g(t)}\,dt$$

$$\|f\|_{L^2} = \sqrt{\frac{1}{T}\int_0^T |f(t)|^2\,dt}$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.26 Elementare Funktionen 2]]: Euler-Formel, komplexe Exponentialfunktion
- [[VL.30 Integrationsregeln 2]]: Komplexe Orthogonalitätsrelationen
- [[VL.37 Reele Fourieranalyse]]: Reelle Fourierkoeffizienten
- [[VL.38 Approximation im quadratischen mittel]]: Bestapproximation