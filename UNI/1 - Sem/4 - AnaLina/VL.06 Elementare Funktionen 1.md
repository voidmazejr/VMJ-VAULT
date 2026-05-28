**Class:** [[AnaLina]]  
**Date:** 27-12-2025 
**Topics:** #Exponentialfunktion #Logarithmus #Sinus #Cosinus #Tangens #Trigonometrie

---
## 🎯 Lernziele der Vorlesung

- Exponentialfunktion und ihre Eigenschaften kennen
- Logarithmus als Umkehrfunktion verstehen
- Sinus und Cosinus aus dem Einheitskreis verstehen
- Additionstheoreme anwenden können
- Sinusschwingungen mit Amplitude, Frequenz und Phasenverschiebung
- Tangens definieren und anwenden

---

## 1. Exponentialfunktion

### Definition und Graph

Die **Exponentialfunktion** ist definiert als: $$\exp : \mathbb{R} \to \mathbb{R}, \quad \exp(x) = e^x$$

wobei $e \approx 2.71828...$ die **Eulersche Zahl** ist.

### Eigenschaften der Exponentialfunktion

**Satz:** Für die Exponentialfunktion gilt:

1. $e^0 = 1$
    
2. **Funktionalgleichung:** $e^{x+y} = e^x \cdot e^y$ für alle $x, y \in \mathbb{R}$
    
3. $e^x \neq 0$ und $e^{-x} = \frac{1}{e^x}$ für alle $x \in \mathbb{R}$
    
4. $e^x > 0$ für alle $x \in \mathbb{R}$ (Exponentialfunktion ist immer positiv!)
    
5. $\exp$ ist **streng monoton wachsend**
    
6. $\exp : \mathbb{R} \to ]0, \infty[$ ist **bijektiv**
    

⚠️ **Bemerkung:** Den vollständigen Beweis dieser Eigenschaften liefern wir später in [[VL.26 Elementare Funktionen 2]], wenn wir die Exponentialfunktion über ihre Reihendarstellung definieren.

### Grafische Darstellung:
![[Screenshot 2025-12-26 at 11.57.32.png]]


---

## 2. Logarithmus

### Definition

Da $\exp : \mathbb{R} \to ]0, \infty[$ bijektiv ist, existiert eine Umkehrfunktion.

Die **Umkehrfunktion der Exponentialfunktion** heißt **natürlicher Logarithmus** (oder einfach Logarithmus): $$\ln : ]0, \infty[ \to \mathbb{R}$$

Alternative Notation: $\log$ (ohne Basis bedeutet meist $\ln$)

### Umkehreigenschaften

Für die Umkehrfunktion gelten: $$\ln(e^x) = x \quad \text{für alle } x \in \mathbb{R}$$ $$e^{\ln(x)} = x \quad \text{für alle } x \in ]0, \infty[$$

### Grafische Darstellung

Der Graph von $\ln$ entsteht durch **Spiegelung** des Graphen von $\exp$ an der Winkelhalbierenden $y = x$:

![[Screenshot 2025-12-26 at 11.57.56.png]]
### Eigenschaften des Logarithmus

**Satz:** Für den Logarithmus gilt:

1. $\ln(1) = 0$
    
2. **Funktionalgleichung:** $\ln(xy) = \ln(x) + \ln(y)$ für alle $x, y > 0$
    
3. $\ln\left(\frac{1}{x}\right) = -\ln(x)$ für alle $x > 0$
    
4. $\ln\left(\frac{x}{y}\right) = \ln(x) - \ln(y)$ für alle $x, y > 0$
    
5. $\ln(x^n) = n \cdot \ln(x)$ für alle $x > 0$ und $n \in \mathbb{Z}$
    
6. $\ln$ ist **streng monoton wachsend**
    
7. $\ln : ]0, \infty[ \to \mathbb{R}$ ist **bijektiv**
    

### Beweis ausgewählter Eigenschaften

**Beweis von (1):** $$\ln(1) = \ln(e^0) = 0$$

**Beweis von (2):** Für $x, y > 0$ gilt $x = e^{\ln(x)}$ und $y = e^{\ln(y)}$. Damit: $$\ln(xy) = \ln(e^{\ln(x)} \cdot e^{\ln(y)}) = \ln(e^{\ln(x) + \ln(y)}) = \ln(x) + \ln(y)$$

wobei wir die Funktionalgleichung von $\exp$ verwendet haben.

**Beweis von (3):** Für $x > 0$ ist: $$0 = \ln(1) = \ln\left(\frac{x}{x}\right) = \ln(x) + \ln\left(\frac{1}{x}\right)$$ $$\Rightarrow \ln\left(\frac{1}{x}\right) = -\ln(x)$$

---

## 3. Sinus und Cosinus

### Definition am Einheitskreis

**Einheitskreis:** Die Menge aller Punkte $(x, y)$ mit $x^2 + y^2 = 1$

Ein Punkt auf dem Einheitskreis ist durch einen **Winkel** $\varphi$ zur positiven x-Achse festgelegt.

![[Screenshot 2025-12-26 at 11.58.40.png]]

**Bogenmaß:** Winkel werden im **Bogenmaß** gemessen (nicht in Grad!) $$\pi ,\text{(Bogenmaß)} = 180° \quad \text{und} \quad 2\pi = 360°$$

**Umrechnung:** $$\varphi ,\text{(Bogenmaß)} = \frac{\pi}{180} \cdot \alpha ,\text{(Grad)}$$ $$\alpha ,\text{(Grad)} = \frac{180}{\pi} \cdot \varphi ,\text{(Bogenmaß)}$$

### Definition von Sinus und Cosinus

Für einen Winkel $\varphi$ haben wir ein rechtwinkliges Dreieck mit Hypothenuse der Länge 1:
![[Screenshot 2025-12-26 at 12.12.59.png]]
**Definition:** $$\cos(\varphi) = \frac{x}{1} = x \quad \text{(x-Koordinate auf Einheitskreis)}$$ $$\sin(\varphi) = \frac{y}{1} = y \quad \text{(y-Koordinate auf Einheitskreis)}$$

Damit sind $\cos$ und $\sin$ für jedes $\varphi \in \mathbb{R}$ definiert.

### Graph von Sinus und Cosinus

![[Screenshot 2025-12-26 at 12.13.29.png]]

### Eigenschaften von Sinus und Cosinus

**Satz:** Es gelten für alle $x \in \mathbb{R}$:

1. **Beschränktheit:** $-1 \leq \cos(x) \leq 1$ und $-1 \leq \sin(x) \leq 1$
    
2. **Cosinus ist gerade:** $\cos(-x) = \cos(x)$
    
3. **Sinus ist ungerade:** $\sin(-x) = -\sin(x)$
    
4. **Trigonometrischer Pythagoras:** $\cos^2(x) + \sin^2(x) = 1$
    
5. **Periodizität:** $\cos(x + 2\pi k) = \cos(x)$ und $\sin(x + 2\pi k) = \sin(x)$ für $k \in \mathbb{Z}$
    
    - Sinus und Cosinus sind $2\pi$-periodisch
6. **Nullstellen von Cosinus:** $\cos(x) = 0$ $\Leftrightarrow$ $x = \pm\frac{\pi}{2}, \pm\frac{3\pi}{2}, \pm\frac{5\pi}{2}, ...$
    
7. **Nullstellen von Sinus:** $\sin(x) = 0$ $\Leftrightarrow$ $x = 0, \pm\pi, \pm 2\pi, ...$
    

**Schreibweise:** Wir vereinbaren: $$\cos^2(x) := (\cos(x))^2 = \cos(x)^2$$ $$\sin^2(x) := (\sin(x))^2 = \sin(x)^2$$

Also: $\cos^2(x) + \sin^2(x) = 1$ (trigonometrischer Pythagoras)

### Additionstheoreme

**Satz:** Für alle $x, y \in \mathbb{R}$ gilt: $$\cos(x + y) = \cos(x)\cos(y) - \sin(x)\sin(y)$$ $$\sin(x + y) = \sin(x)\cos(y) + \cos(x)\sin(y)$$

⚠️ **Bemerkung:** Der vollständige Beweis wird in [[VL.27 Elementare Funktionen 3|VL.27 Elementare Funktionen 3]] gezeigt.

### Spezielle Werte

**Wichtige Winkel und ihre Werte:**

|    $x$    |    $0$    |   $\frac{\pi}{6}$    |   $\frac{\pi}{4}$    |   $\frac{\pi}{3}$    | $\frac{\pi}{2}$ |   $\frac{2\pi}{3}$   |   $\frac{3\pi}{4}$    |   $\frac{5\pi}{6}$    |    $\pi$    |
| :-------: | :-------: | :------------------: | :------------------: | :------------------: | :-------------: | :------------------: | :-------------------: | :-------------------: | :---------: |
|  $Grad$   | $0^\circ$ |      $30^\circ$      |      $45^\circ$      |      $60^\circ$      |   $90^\circ$    |     $120^\circ$      |      $135^\circ$      |      $150^\circ$      | $180^\circ$ |
| $\cos(x)$ |    $1$    | $\frac{\sqrt{3}}{2}$ | $\frac{\sqrt{2}}{2}$ |    $\frac{1}{2}$     |       $0$       |    $-\frac{1}{2}$    | $-\frac{\sqrt{2}}{2}$ | $-\frac{\sqrt{3}}{2}$ |    $-1$     |
| $\sin(x)$ |    $0$    |    $\frac{1}{2}$     | $\frac{\sqrt{2}}{2}$ | $\frac{\sqrt{3}}{2}$ |       $1$       | $\frac{\sqrt{3}}{2}$ | $\frac{\sqrt{2}}{2}$  |     $\frac{1}{2}$     |     $0$     |
**Merkhilfe am Einheitskreis:**
![[Screenshot 2025-12-26 at 12.14.03.png]]

**Trick:** Die Werte folgen dem Muster $\frac{\sqrt{0}}{2}, \frac{\sqrt{1}}{2}, \frac{\sqrt{2}}{2}, \frac{\sqrt{3}}{2}, \frac{\sqrt{4}}{2}$

### Anwendungen der Additionstheoreme

**Beispiel 1:** Setze $y = \frac{\pi}{2}$ in die Additionstheoreme ein: $$\cos\left(x + \frac{\pi}{2}\right) = \cos(x)\cos\left(\frac{\pi}{2}\right) - \sin(x)\sin\left(\frac{\pi}{2}\right) = -\sin(x)$$ $$\sin\left(x + \frac{\pi}{2}\right) = \sin(x)\cos\left(\frac{\pi}{2}\right) + \cos(x)\sin\left(\frac{\pi}{2}\right) = \cos(x)$$

**Beispiel 2:** Setze $y = x$: $$\cos(2x) = \cos^2(x) - \sin^2(x)$$ $$\sin(2x) = 2\sin(x)\cos(x)$$

---

## 4. Sinusschwingungen

### Allgemeine Form

Eine **Sinusschwingung** hat die Form: $$f : \mathbb{R} \to \mathbb{R}, \quad x \mapsto A \sin(\omega x - \varphi)$$

wobei:

- $A$ = **Amplitude** (Höhe der Schwingung)
- $\omega$ = **Frequenz** (Anzahl der Schwingungen)
- $\varphi$ = **Phasenverschiebung** (Verschiebung nach links/rechts)

### Amplitude A

Die Funktion $A \sin(x)$ ist eine **Streckung** oder **Stauchung** von $\sin(x)$ in **y-Richtung**.

**Beispiele:**

- $2\sin(x)$: gestreckt um Faktor 2 (schwingt zwischen -2 und 2)
- $\frac{1}{2}\sin(x)$: gestaucht um Faktor 2 (schwingt zwischen -0.5 und 0.5)

![[Screenshot 2025-12-26 at 12.15.06.png]]

### Frequenz ω

Die Funktion $\sin(\omega x)$ ist eine **Streckung** oder **Stauchung** in **x-Richtung**.

- $\sin(2x)$: schwingt **doppelt so schnell**, Periode $T = \frac{2\pi}{2} = \pi$
- $\sin(3x)$: schwingt **dreimal so schnell**, Periode $T = \frac{2\pi}{3}$
- $\sin\left(\frac{1}{2}x\right)$: schwingt **halb so schnell**, Periode $T = 4\pi$

**Allgemein:** $\sin(\omega x)$ und $\cos(\omega x)$ haben:

- Frequenz: $\omega > 0$
- Periode: $T = \frac{2\pi}{\omega}$

![[Screenshot 2025-12-26 at 12.15.38.png]]
### Phasenverschiebung φ

Die Funktion $\sin(x - \varphi)$ ist eine **Verschiebung** entlang der **x-Achse**.

- $\varphi > 0$: Verschiebung nach **rechts**
- $\varphi < 0$: Verschiebung nach **links**

**Beispiele:**

- $\sin\left(x - \frac{\pi}{4}\right)$: um $\frac{\pi}{4}$ nach rechts verschoben
- $\sin\left(x + \frac{\pi}{2}\right) = \cos(x)$: um $\frac{\pi}{2}$ nach links verschoben

![[Screenshot 2025-12-26 at 14.36.17.png]]
### Harmonische Schwingung

**Problem:** Wie kann man $f(x) = a\cos(\omega x) + b\sin(\omega x)$ vereinfachen?

**Lösung:** Für $a^2 + b^2 > 0$ kann man schreiben: $$f(x) = \sqrt{a^2 + b^2} \cdot \cos(\omega x - \varphi)$$

wobei $\varphi$ so gewählt wird, dass: $$\cos(\varphi) = \frac{a}{\sqrt{a^2 + b^2}}, \quad \sin(\varphi) = \frac{b}{\sqrt{a^2 + b^2}}$$

**Beweis:** Mit dem Additionstheorem: $$\sqrt{a^2 + b^2} \cdot (\cos(\varphi)\cos(\omega x) + \sin(\varphi)\sin(\omega x))$$ $$= \sqrt{a^2 + b^2} \cdot \cos(\omega x - \varphi)$$

**Interpretation:** Jede Überlagerung von $\cos$ und $\sin$ mit gleicher Frequenz lässt sich als eine einzige Cosinus- (oder Sinus-) Schwingung mit Phasenverschiebung schreiben!

---

## 5. Tangens

### Definition

Der **Tangens** ist definiert als: $$\tan(x) := \frac{\sin(x)}{\cos(x)}$$

für alle $x \in \mathbb{R} \setminus \left\{ \frac{\pi}{2} + k\pi \mid k \in \mathbb{Z} \right\}$

(überall dort, wo $\cos(x) \neq 0$)

### Graph des Tangens

![[Screenshot 2025-12-26 at 14.38.49.png]]

Der Tangens hat **vertikale Asymptoten** bei $x = \frac{\pi}{2} + k\pi$, $k \in \mathbb{Z}$.

### Eigenschaften des Tangens

Aus den Eigenschaften von Sinus und Cosinus folgen:

1. $\tan$ ist eine **ungerade Funktion:** $\tan(-x) = -\tan(x)$
    
2. $\tan$ ist **$\pi$-periodisch:** $\tan(x + \pi) = \tan(x)$
    
3. **Additionstheorem:** $$\tan(x + y) = \frac{\tan(x) + \tan(y)}{1 - \tan(x)\tan(y)}$$
    

(für alle $x, y$ wo beide Seiten definiert sind)

**Übung:** Rechnen Sie das Additionstheorem nach!

---

## 📌 Zusammenfassung

|**Funktion**|**Definitionsbereich**|**Wertebereich**|**Wichtige Eigenschaft**|
|---|---|---|---|
|$e^x$|$\mathbb{R}$|$]0, \infty[$|$e^{x+y} = e^x \cdot e^y$|
|$\ln(x)$|$]0, \infty[$|$\mathbb{R}$|$\ln(xy) = \ln(x) + \ln(y)$|
|$\sin(x)$|$\mathbb{R}$|$[-1, 1]$|ungerade, $2\pi$-periodisch|
|$\cos(x)$|$\mathbb{R}$|$[-1, 1]$|gerade, $2\pi$-periodisch|
|$\tan(x)$|$\mathbb{R} \setminus {\frac{\pi}{2} + k\pi}$|$\mathbb{R}$|ungerade, $\pi$-periodisch|

**Wichtige Formeln:**

- $\cos^2(x) + \sin^2(x) = 1$ (Pythagoras)
- $\cos(x+y) = \cos(x)\cos(y) - \sin(x)\sin(y)$
- $\sin(x+y) = \sin(x)\cos(y) + \cos(x)\sin(y)$
- Sinusschwingung: $A\sin(\omega x - \varphi)$ mit Amplitude $A$, Frequenz $\omega$, Phase $\varphi$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Abbildungen]] Bijektivität von exp und ln
- [[VL.07 Komplexe Zahlen 2]] Eulersche Formel: $e^{i\varphi} = \cos(\varphi) + i\sin(\varphi)$
- [[VL.26 Elementare Funktionen 2]] Rigorose Definition von exp über Reihendarstellung
- [[VL.27 Elementare Funktionen 3]] Beweis der Additionstheoreme, Arcusfunktionen