**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Fourieranalysis #TrigonometrischePolynome #Fourierkoeffizienten #Frequenzanalyse

---

## 🎯 Lernziele der Vorlesung

Periodische Funktionen werden global durch Sinus- und Cosinusfunktionen approximiert - die Fourierapproximation.

- **Periodische Funktionen** und trigonometrische Polynome
- **Orthogonalitätsrelationen** für Sinus und Cosinus
- **Fourierkoeffizienten** und **Fourierpolynome**
- **Frequenzanalyse** von periodischen Schwingungen
- Anwendungen der Fourieranalysis

---

## 1. Motivation: Taylor vs. Fourier

### Taylor-Approximation (lokal)

Differenzierbare Funktionen lassen sich **lokal** gut durch Polynome approximieren:

$$f(x) = \sum_{k=0}^n a_k(x-x_0)^k \quad \text{mit} \quad a_k = \frac{f^{(k)}(x_0)}{k!}$$

**Problem bei periodischen Funktionen:** Polynome sind **nicht periodisch**!

### Fourier-Approximation (global)

Periodische Funktionen werden **global** durch **Sinus- und Cosinusfunktionen** approximiert.

**Vorteil:** Diese Bausteine sind selbst schon periodisch!

**Anwendung:** Frequenzanalyse von periodischen Schwingungen (Mechanik, Elektrotechnik, Akustik)

---

## 2. Periodische Funktionen

### Definition (Periodische Funktion)

Die Funktion $f : \mathbb{R} \to \mathbb{R}$ heißt **periodisch mit der Periode $T > 0$** (oder kurz **$T$-periodisch**), wenn:

$$\boxed{f(t + T) = f(t) \quad \text{für alle } t \in \mathbb{R}}$$

**Wichtige Bemerkung:** Eine Periode muss **nicht** die kleinste Zahl mit dieser Eigenschaft sein!

Ist $T$ eine Periode von $f$, so sind auch $2T, 3T, 4T, \ldots$ Perioden:

$$f(t + 2T) = f((t+T) + T) = f(t+T) = f(t)$$

### Beispiel: Sinus und Cosinus

Sei $T > 0$ und $\omega = \frac{2\pi}{T}$ die zugehörige **Kreisfrequenz**. Die Funktionen

$$\cos(k\omega t), \quad \sin(k\omega t)$$

sind für jedes $k \in \mathbb{N}$ periodisch mit der Periode $T$:

$$\cos(k\omega(t+T)) = \cos(k\omega t + k\omega T) = \cos(k\omega t + k \cdot 2\pi) = \cos(k\omega t)$$

Genauso für $\sin(k\omega t)$.

**Wichtig:** 
- $\sin(2\omega t)$ hat kleinste Periode $T/2$, ist aber auch $T$-periodisch
- $\sin(0\omega t) = 0$ und $\cos(0\omega t) = 1$

---

## 3. Trigonometrische Polynome

### Definition (Trigonometrisches Polynom)

Funktionen der Form

$$\boxed{\frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))}$$

heißen **trigonometrische Polynome vom Grad** (oder von der Ordnung) $n$.

**Konvention:** Der konstante Term wird als $\frac{a_0}{2}$ geschrieben (Grund siehe später).

### Physikalische Interpretation

Ein trigonometrisches Polynom besteht aus der **Überlagerung** von:

- **Grundschwingung** der Frequenz $\omega = \frac{2\pi}{T}$
- **Oberschwingungen** der Frequenzen $k\omega$ ($k = 2, 3, 4, \ldots$)

Die **Koeffizienten** $a_k, b_k$ geben an, mit welcher **Amplitude** die Oberschwingungen vertreten sind.

### Umrechnung der Periode

Ist $f : \mathbb{R} \to \mathbb{R}$ $T$-periodisch, dann ist

$$\tilde{f}(t) := f\left(\frac{T}{S}t\right)$$

**$S$-periodisch**:

$$\tilde{f}(t+S) = f\left(\frac{T}{S}(t+S)\right) = f\left(\frac{T}{S}t + T\right) = f\left(\frac{T}{S}t\right) = \tilde{f}(t)$$

---

## 4. Orthogonalitätsrelationen

### Satz (Orthogonalitätsrelationen)

Sei $T > 0$ und $\omega = \frac{2\pi}{T}$. Dann gilt für alle $k, \ell \in \mathbb{N}$:

**1. Cosinus-Cosinus:**

$$\boxed{\frac{2}{T}\int_0^T \cos(k\omega t)\cos(\ell\omega t)\,dt = \begin{cases} 2, & k = \ell = 0 \\ 1, & k = \ell > 0 \\ 0, & k \neq \ell \end{cases}}$$

**2. Sinus-Sinus:**

$$\boxed{\frac{2}{T}\int_0^T \sin(k\omega t)\sin(\ell\omega t)\,dt = \begin{cases} 1, & k = \ell > 0 \\ 0, & \text{sonst} \end{cases}}$$

**3. Sinus-Cosinus:**

$$\boxed{\frac{2}{T}\int_0^T \sin(k\omega t)\cos(\ell\omega t)\,dt = 0}$$

**Beweis-Skizze:** Wurde bereits in [[VL.30 Integrationsregeln 2]] nachgerechnet. Alternativ mit komplexer Exponentialfunktion (siehe Skript).

### $L^2$-Skalarprodukt

Die Orthogonalitätsrelationen besagen, dass die Funktionen $\cos(k\omega t)$ und $\sin(\ell\omega t)$ **orthogonal** bezüglich des $L^2$-Skalarprodukts

$$\boxed{\langle f, g \rangle = \frac{2}{T}\int_0^T f(t)g(t)\,dt}$$

sind.

Für $k \geq 1$ sind $\cos(k\omega t)$ und $\sin(k\omega t)$ sogar **orthonormal**:

$$\langle \cos(k\omega t), \cos(k\omega t) \rangle = 1, \quad \langle \sin(k\omega t), \sin(k\omega t) \rangle = 1$$

**Sonderfall** $k = 0$: $\cos(0\omega t) = 1$ mit

$$\langle \cos(0\omega t), \cos(0\omega t) \rangle = \frac{2}{T}\int_0^T 1\,dt = 2$$

Daher der Faktor $\frac{1}{2}$ beim konstanten Term $\frac{a_0}{2}$!

---

## 5. Fourierkoeffizienten und Fourierpolynome

### Generalvoraussetzung

Alle betrachteten Funktionen seien auf dem Periodenintervall $[0, T]$ **stückweise monoton** (siehe [[VL.28 Das Integral]]). Dies impliziert Integrierbarkeit.

**Beispiele:** Sinus, Cosinus, Sägezahn, Rechteck

### Definition (Fourierkoeffizienten)

Sei $f : \mathbb{R} \to \mathbb{R}$ (oder $f : \mathbb{R} \to \mathbb{C}$) eine stückweise monotone Funktion der Periode $T > 0$ und $\omega = \frac{2\pi}{T}$.

Dann heißen:

$$\boxed{a_k = \langle f, \cos(k\omega t) \rangle = \frac{2}{T}\int_0^T f(t)\cos(k\omega t)\,dt}$$

$$\boxed{b_k = \langle f, \sin(k\omega t) \rangle = \frac{2}{T}\int_0^T f(t)\sin(k\omega t)\,dt}$$

die **reellen Fourierkoeffizienten** von $f$ (für $k \in \mathbb{N}_0$).

### Definition (Fourierpolynom)

Das **$n$-te Fourierpolynom** (oder Fourierpolynom der Ordnung $n$) von $f$ ist:

$$\boxed{\varphi_n(t) = \frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))}$$

### Wichtige Bemerkungen

**1.** Die Fourierkoeffizienten sind wie Koordinaten bezüglich einer ONB definiert (vgl. [[VL.35 Vektorräume mit Skalarprodukt 1]]).

**2.** Der konstante Term ist $\frac{a_0}{2}$ statt $a_0$, da $\langle \cos(0\omega t), \cos(0\omega t) \rangle = 2 \neq 1$.

**3.** Es ist immer $b_0 = 0$, da $\sin(0\omega t) = 0$.

**4.** Für die Fourierkoeffizienten von $\varphi_n$ gilt (mit Orthogonalitätsrelationen):

$$\frac{2}{T}\int_0^T \varphi_n(t)\cos(k\omega t)\,dt = a_k = \frac{2}{T}\int_0^T f(t)\cos(k\omega t)\,dt$$

$$\frac{2}{T}\int_0^T \varphi_n(t)\sin(k\omega t)\,dt = b_k = \frac{2}{T}\int_0^T f(t)\sin(k\omega t)\,dt$$

**Interpretation:** Das Fourierpolynom hat dieselben Fourierkoeffizienten wie $f$ (bis zur Ordnung $n$).

---

## 6. Beispiel: Sägezahnkurve

### Funktion

Die Funktion $f : \mathbb{R} \to \mathbb{R}$ ist **2-periodisch** (d.h. $T = 2$) mit:

$$f(t) = \begin{cases} 1 - t, & 0 < t < 2 \\ 0, & t = 0 \end{cases}$$

Also $\omega = \frac{2\pi}{T} = \pi$.

### Berechnung der Fourierkoeffizienten

**Für $k \geq 1$:**

$$b_k = \frac{2}{2}\int_0^2 (1-t)\sin(k\pi t)\,dt = \int_0^2 \sin(k\pi t)\,dt - \int_0^2 t\sin(k\pi t)\,dt$$

**Erstes Integral:**

$$\int_0^2 \sin(k\pi t)\,dt = -\frac{1}{k\pi}\cos(k\pi t)\bigg|_0^2 = -\frac{1}{k\pi}(1-1) = 0$$

**Zweites Integral** (partielle Integration mit $u' = \sin(k\pi t)$, $v = t$):

$$\int_0^2 t\sin(k\pi t)\,dt = -\frac{t}{k\pi}\cos(k\pi t)\bigg|_0^2 + \int_0^2 \frac{1}{k\pi}\cos(k\pi t)\,dt$$

$$= -\frac{2}{k\pi}\cos(2k\pi) + \frac{1}{k\pi}\sin(k\pi t)\bigg|_0^2 = -\frac{2}{k\pi} + 0 = -\frac{2}{k\pi}$$

Also:

$$\boxed{b_k = 0 - \left(-\frac{2}{k\pi}\right) = \frac{2}{k\pi}}$$

**Für $a_0$:**

$$a_0 = \int_0^2 (1-t) \cdot 1\,dt = \left(t - \frac{t^2}{2}\right)\bigg|_0^2 = 0$$

**Für $a_k$ ($k \geq 1$):**

$$a_k = \int_0^2 (1-t)\cos(k\pi t)\,dt = \underbrace{\int_0^2 \cos(k\pi t)\,dt}_{=0} - \int_0^2 t\cos(k\pi t)\,dt$$

Partielle Integration:

$$\int_0^2 t\cos(k\pi t)\,dt = \frac{t}{k\pi}\sin(k\pi t)\bigg|_0^2 - \int_0^2 \frac{1}{k\pi}\sin(k\pi t)\,dt = 0 - 0 = 0$$

Also $\boxed{a_k = 0}$ für alle $k \geq 0$.

### Fourierpolynom der Sägezahnkurve

$$\boxed{\varphi_n(t) = \sum_{k=1}^n \frac{2}{k\pi}\sin(k\pi t)}$$

### Visualisierung der Approximation

Für wachsendes $n$ approximieren die Fourierpolynome die Funktion immer besser:

- **$n = 1$:** Grobe Approximation mit nur der Grundschwingung
- **$n = 5$:** Deutlich bessere Approximation
- **$n = 10$:** Sehr gute Approximation
- **$n = 50$:** Fast perfekte Approximation

### Frequenzspektrum

Die **Koeffizienten** $b_k = \frac{2}{k\pi}$ zeigen:

- Alle $a_k = 0$ (nur Sinus-Terme)
- $b_k$ nimmt mit $k$ ab: Oberschwingungen werden schwächer
- Hauptbeitrag von niedrigen Frequenzen

---

## 7. Anwendungen der Fourieranalysis

### Fourieranalyse vs. Fouriersynthese

- **Fourieranalyse:** Berechnung der Koeffizienten $a_k, b_k$ aus $f(t)$
- **Fouriersynthese:** Zusammenfügen der Koeffizienten zu einem trigonometrischen Polynom

### Praktische Anwendungen

**1. Menschliches Ohr**

Die Haarzellen des Cortischen Organs sind für bestimmte Frequenzen empfindlich. Das Ohr übermittelt dem Gehirn die **Fourierkoeffizienten** der akustischen Signale!

**2. Audiokompression (MP3)**

Rauschunterdrückungs- oder Kompressionsverfahren:
- Zerlegen Signale in ihr Frequenzspektrum (Fourieranalyse)
- Filtern unerwünschte/überflüssige Frequenzen heraus
- Setzen Signal wieder zusammen (Fouriersynthese)

**3. Regelungstechnik**

Die Wirkung linearer Systeme lässt sich an harmonischen Schwingungen testen und mit Fourieranalyse für beliebigen periodischen Input vorhersagen.

**4. Signalsynthese**

Generatoren liefern natürlicherweise harmonische Spannungen. Für technische Anwendungen (z.B. Sägezahnspannungen für Zeilensteuerung) synthetisiert man durch Überlagerung harmonischer Schwingungen.

**5. Partielle Differentialgleichungen**

Die Fourieranalyse dient bei Rand-Anfangswertproblemen als wichtiges Hilfsmittel (Verfahrens-, Energie-, Elektrotechnik).

---

## 📌 Zusammenfassung

### Periodische Funktionen

$$f(t+T) = f(t) \quad \text{für alle } t \in \mathbb{R}$$

**Trigonometrisches Polynom:** $\frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))$ mit $\omega = \frac{2\pi}{T}$

### Orthogonalitätsrelationen

Bezüglich $\langle f, g \rangle = \frac{2}{T}\int_0^T f(t)g(t)\,dt$:

- $\cos(k\omega t), \sin(\ell\omega t)$ sind orthogonal für $k \neq \ell$
- $\cos(k\omega t), \sin(k\omega t)$ sind orthonormal für $k \geq 1$
- $\cos(0\omega t) = 1$ hat Norm $\sqrt{2}$ (daher Faktor $\frac{1}{2}$)

### Fourierkoeffizienten

$$a_k = \frac{2}{T}\int_0^T f(t)\cos(k\omega t)\,dt$$

$$b_k = \frac{2}{T}\int_0^T f(t)\sin(k\omega t)\,dt$$

### Fourierpolynom

$$\varphi_n(t) = \frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))$$

**Interpretation:** Approximation von $f$ durch Überlagerung harmonischer Schwingungen

### Berechnungsschema

1. **Periode** $T$ und $\omega = \frac{2\pi}{T}$ bestimmen
2. **Fourierkoeffizienten** $a_k, b_k$ berechnen (Integration)
3. **Fourierpolynom** aufstellen: $\varphi_n(t) = \frac{a_0}{2} + \sum_{k=1}^n (a_k \cos(k\omega t) + b_k \sin(k\omega t))$
4. **Frequenzspektrum** analysieren: Welche Frequenzen dominieren?

### Wichtige Eigenschaften

✅ $\varphi_n$ hat dieselben Fourierkoeffizienten wie $f$ (bis Ordnung $n$)

✅ Für wachsendes $n$ wird Approximation besser (unter gewissen Bedingungen)

✅ Frequenzspektrum zeigt Zusammensetzung aus Grund- und Oberschwingungen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.28 Das Integral]]: Stückweise monotone Funktionen
- [[VL.30 Integrationsregeln 2]]: Orthogonalitätsrelationen bewiesen
- [[VL.35 Vektorräume mit Skalarprodukt 1]]: $L^2$-Skalarprodukt, ONB
- [[VL.36 Vektorräume mit Skalarprodukt 2]]: ONB-Entwicklung, beste Approximation