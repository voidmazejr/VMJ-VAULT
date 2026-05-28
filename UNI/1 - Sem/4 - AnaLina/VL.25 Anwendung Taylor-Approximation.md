  **Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #TaylorReihe #Fehlerabschätzung #Diskretisierung #EulerFormel #Funktionswertberechnung

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung zeigt praktische Anwendungen der Taylor-Approximation und führt Taylorreihen ein.

- **Näherungsweise Berechnung von Funktionswerten** mit Taylorpolynomen
- **Fehlerabschätzung** bei Messungen mit Taylor-Approximation
- **Diskretisierung von Ableitungen** für numerische Verfahren
- **Taylorreihen** als Grenzwert der Taylorpolynome
- Herleitung der **Euler-Formel** aus Taylorreihen

---

## 1. Näherungsweise Berechnung von Funktionswerten

### Anwendung in Computern

Eine wichtige Anwendung der Taylorformel steckt heute in jedem Computer: Die **Berechnung von Funktionswerten**.

Das Taylorpolynom gibt die Möglichkeit, eine mehrfach differenzierbare Funktion in der Umgebung eines Entwicklungspunktes durch ein **Polynom zu approximieren** und den Approximationsfehler abzuschätzen.

### Beispiel 1: Berechnung von $\sqrt{4.4}$

**Ziel:** Berechne näherungsweise $\sqrt{4.4}$

**Vorgehen:** Verwende das 2-te Taylorpolynom von $f(x) = \sqrt{x}$ im Entwicklungspunkt $x_0 = 4$ (dort kennen wir $\sqrt{4} = 2$)

**Ableitungen:**
$$\begin{align}
f(x) &= x^{1/2} &\Rightarrow f(4) &= 2 \\
f'(x) &= \frac{1}{2}x^{-1/2} = \frac{1}{2\sqrt{x}} &\Rightarrow f'(4) &= \frac{1}{4} \\
f''(x) &= -\frac{1}{4}x^{-3/2} = -\frac{1}{4\sqrt{x^3}} &\Rightarrow f''(4) &= -\frac{1}{32} \\
f'''(x) &= \frac{3}{8}x^{-5/2} = \frac{3}{8\sqrt{x^5}}
\end{align}$$

**2-tes Taylorpolynom:**
$$T_2(x) = f(4) + f'(4)(x-4) + \frac{f''(4)}{2}(x-4)^2 = 2 + \frac{1}{4}(x-4) - \frac{1}{64}(x-4)^2$$

**Approximation:**
$$\sqrt{4.4} \approx T_2(4.4) = 2 + \frac{1}{4} \cdot 0.4 - \frac{1}{64} \cdot (0.4)^2$$
$$= 2 + 0.1 - \frac{0.16}{64} = 2.1 - 0.0025 = 2.0975$$

**Fehlerabschätzung mit Lagrange-Restglied:**
$$R_2(x) = \frac{f'''(\xi)}{3!}(x-4)^3 = \frac{1}{16} \cdot \frac{(x-4)^3}{\sqrt{\xi^5}}$$

Für $x = 4.4$ liegt $\xi$ zwischen $4$ und $4.4$, also $\xi \geq 4$:
$$|R_2(4.4)| = \frac{(0.4)^3}{16\sqrt{\xi^5}} \leq \frac{0.064}{16\sqrt{4^5}} = \frac{0.064}{16 \cdot 32} = \frac{0.064}{512} = 0.000125$$

**Ergebnis:**
$$\sqrt{4.4} \approx 2.0975 \pm 0.000125$$

Also:
$$2.097375 \leq \sqrt{4.4} \leq 2.097625$$

**Vergleich:** Taschenrechner gibt $\sqrt{4.4} = 2.0976177...$ 

Die Approximation mit $T_2$ liefert bereits **drei korrekte Nachkommastellen**!

### Beispiel 2: Nachweis $e < 3$

**Ziel:** Zeige $e = e^1 < 3$

**Strategie:** Zeige $e^{-1} > \frac{1}{3}$ mit Taylor-Approximation

**Taylor-Entwicklung von** $e^x$ **um** $x_0 = 0$:
$$e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{e^\xi}{4!}x^4$$

Für $x = -1$ (wobei $\xi$ zwischen $0$ und $-1$ liegt):
$$e^{-1} = 1 - 1 + \frac{1}{2} - \frac{1}{6} + \frac{e^\xi}{24} = \frac{1}{3} + \frac{e^\xi}{24}$$

Da $e^\xi > 0$ für jedes $\xi \in \mathbb{R}$:
$$e^{-1} > \frac{1}{3}$$

Also: $e < 3$ ✓

### Beispiel 3: Exponentialfunktion auf $[-1, 1]$

**Ziel:** Berechne $e^x$ auf $[-1, 1]$ mit Genauigkeit $< 10^{-5}$

**Restglied:**
$$R_n(x) = \frac{e^\xi}{(n+1)!}x^{n+1}$$

Für $x \in [-1, 1]$ und $\xi$ zwischen $0$ und $x$:
- $|x| \leq 1$
- $|\xi| \leq 1 \Rightarrow e^\xi \leq e^1 \leq 3$

Also:
$$|R_n(x)| \leq \frac{3}{(n+1)!}$$

**Für** $n = 8$:
$$|R_8(x)| \leq \frac{3}{9!} = \frac{3}{362880} \approx 0.0000083 < 10^{-5}$$

Mit $T_8(x)$ haben wir also bereits **5 korrekte Nachkommastellen**!

---

## 2. Fehlerabschätzung

### Motivation

Wie wirken sich **Messfehler** bei Experimenten aus?

### Linearer Fall

**Beispiel:** $f(x) = 3x$ mit Messfehler $\Delta x$

Beobachteter Wert: $f(x + \Delta x)$

**Fehler:**
$$\Delta f := f(x + \Delta x) - f(x) = 3(x + \Delta x) - 3x = 3\Delta x$$

Der Fehler **verdreifacht** sich!

### Allgemeiner Fall

Für **nichtlineare Funktionen** hilft die **Taylor-Approximation 1. Ordnung**:

$$f(x + \Delta x) = f(x) + f'(x)\Delta x + \frac{1}{2}f''(\xi)(\Delta x)^2$$

**Fehler:**
$$\Delta f := f(x + \Delta x) - f(x) = f'(x)\Delta x + \frac{1}{2}f''(\xi)(\Delta x)^2$$

Für **kleine** $\Delta x$ ist $(\Delta x)^2 \ll \Delta x$, also:

$$\boxed{|\Delta f| \approx |f'(x)| \cdot |\Delta x|}$$ 

**(Qualitative Fehlerabschätzung)**

**Verlässliche Schranke:**
$$\boxed{|\Delta f| \leq |f'(x)| \cdot |\Delta x| + \frac{1}{2}\max_\xi |f''(\xi)| \cdot (\Delta x)^2}$$

wobei $\xi$ alle Werte zwischen $x$ und $x + \Delta x$ durchläuft.

### Beispiel: Turmhöhe aus Winkel

**Situation:**
- Position
- Entfernung zum Turm: $\ell$ (bekannt)
- Erhebungswinkel: $\alpha$ (gemessen mit Fehler $\Delta \alpha$)
- Gesuchte Turmhöhe: $h$

**Zusammenhang:**
$$\tan(\alpha) = \frac{h}{\ell} \quad \Rightarrow \quad h = \ell \tan(\alpha)$$

**Ableitung:**
$$h'(\alpha) = \ell \tan'(\alpha) = \frac{\ell}{\cos^2(\alpha)}$$

**Fehlerabschätzung:**
$$|\Delta h| \approx |h'(\alpha)| \cdot |\Delta \alpha| = \frac{\ell}{\cos^2(\alpha)} \cdot |\Delta \alpha|$$

**Numerisches Beispiel:**
- $\ell = 70$ m
- $\alpha = \frac{\pi}{4}$ (45°)
- $\Delta \alpha = \pm 1° = \frac{\pi}{180}$

**Höhe:**
$$h = 70 \tan\left(\frac{\pi}{4}\right) = 70 \text{ m}$$

**Fehler (qualitativ):**
$$|\Delta h| \approx \frac{70}{\cos^2(\pi/4)} \cdot \frac{\pi}{180} = \frac{70}{(1/\sqrt{2})^2} \cdot \frac{\pi}{180} = 140 \cdot \frac{\pi}{180} \approx 2.44 \text{ m}$$

**Präzise Schranke mit zweiter Ableitung:**
$$h''(\alpha) = \frac{2\ell \tan(\alpha)}{\cos^2(\alpha)}$$

$$|\Delta h| \leq 140 \cdot \frac{\pi}{180} + 70 \cdot \frac{\tan(\pi/4 + \pi/180)}{\cos^2(\pi/4 + \pi/180)} \cdot \left(\frac{\pi}{180}\right)^2 \approx 2.49 \text{ m}$$

Die qualitative Fehlerabschätzung war also schon sehr gut!

### Beispiel: Wheatstone-Brücke

**Widerstandsmessung:**
$$\frac{R}{R_0} = \frac{x}{\ell - x} \quad \Rightarrow \quad R = R(x) = \frac{R_0 x}{\ell - x}$$

**Ableitung:**
$$R'(x) = \frac{R_0 \ell}{(\ell - x)^2}$$

**Fehler:**
$$\Delta R \approx R'(x) \Delta x = \frac{R_0 \ell}{(\ell - x)^2} \Delta x$$

**Numerisches Beispiel:**
- $\ell = 10$ cm
- $R_0 = 300$ Ω
- $x = 2$ cm mit Fehler $\Delta x = \pm 0.1$ cm

**Gesuchter Widerstand:**
$$R = \frac{300 \cdot 2}{8} = 75 \text{ Ω}$$

**Fehler:**
$$\Delta R \approx \frac{300 \cdot 10}{8^2} \cdot 0.1 = \frac{3000}{64} \cdot 0.1 \approx 4.7 \text{ Ω}$$

---

## 3. Diskretisierung von Ableitungen

### Motivation

Viele **physikalische Gesetze** sind durch **Differentialgleichungen** gegeben:
- $y' = ay$
- $y'' = -y$
- etc.

Viele dieser Gleichungen lassen sich **nicht explizit lösen** → **numerische Lösungsverfahren** nötig!

### Finite-Differenzen-Methode

**Idee:** Die gesuchte Funktion $y(x)$ wird durch eine **diskrete Zahlenfolge** $y_k$ ersetzt:
$$y_k \approx y(x_k) \quad \text{mit} \quad x_k = x_0 + kh$$

wobei $h$ die **Diskretisierungskonstante** ist.

### Diskretisierung der Ableitungen

Aus der Taylorformel für kleines $h$:
$$\begin{align}
f(x + h) &\approx f(x) + f'(x)h + \frac{1}{2}f''(x)h^2 \\
f(x - h) &\approx f(x) - f'(x)h + \frac{1}{2}f''(x)h^2
\end{align}$$

**Addition:**
$$f(x+h) + f(x-h) \approx 2f(x) + f''(x)h^2$$

**Zweite Ableitung:**
$$\boxed{f''(x) \approx \frac{f(x+h) - 2f(x) + f(x-h)}{h^2}}$$

**Erste Ableitung (direkt aus Definition):**
$$\boxed{f'(x) \approx \frac{f(x+h) - f(x)}{h}}$$

### Beispiel: Differentialgleichung 2. Ordnung

**Gegeben:**
$$y'' + 6y' + 9y = 0, \quad y(0) = 0, \quad y'(0) = 0.5$$

**Diskretisierung:**
$$\frac{y_{k+1} - 2y_k + y_{k-1}}{h^2} + 6 \cdot \frac{y_{k+1} - y_k}{h} + 9y_k = 0$$

mit $y_0 = 0$ und $y_1 = 0.5h$

**Rekursion:**
$$y_{k+1} = \frac{(2 + 6h - 9h^2)y_k - y_{k-1}}{1 + 6h}$$

**Exakte Lösung:** $y(x) = \frac{1}{2}xe^{-3x}$

**Vergleich:** Für $h = 0.001$ ist die numerische Lösung praktisch identisch mit der exakten Lösung!

---

## 4. Taylorreihen

### Definition (Taylorreihe)

Sei $f : D \to \mathbb{R}$ **beliebig oft differenzierbar**. Die **Taylorreihe** von $f$ im Entwicklungspunkt $x_0 \in D$ ist der **Grenzwert der Taylorpolynome**:

$$\boxed{\sum_{k=0}^{\infty} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k := \lim_{n \to \infty} \sum_{k=0}^{n} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k}$$

### Konvergenzbedingung

Der Grenzwert existiert und ist gleich $f(x)$ **genau dann, wenn**:
$$\lim_{n \to \infty} R_n(x) = 0$$

d.h. das **Restglied** muss gegen $0$ konvergieren.

### Hinreichendes Konvergenzkriterium

Ein **hinreichendes Kriterium** für die Konvergenz im Intervall $\,]a, b[$ ist:
$$|f^{(n)}(x)| \leq A \cdot B^n \quad \text{für alle } x \in \,]a, b[$$

mit Konstanten $A, B$ **unabhängig von** $n$.

**Beweis:**
$$|R_n(x)| = \frac{|f^{(n+1)}(\xi)|}{(n+1)!}|x - x_0|^{n+1} \leq \frac{AB^{n+1}}{(n+1)!}|x - x_0|^{n+1} = A \cdot \frac{(B|x - x_0|)^{n+1}}{(n+1)!} \to 0$$

(nach [[VL.18 Berechnung von Grenzwerten]], Beispiel: $\frac{x^n}{n!} \to 0$)

### Warnung

⚠️ **Vorsicht:**

1. Es kann passieren, dass die Taylorreihe für **kein** $x \neq x_0$ konvergiert

2. Es kann passieren, dass die Taylorreihe **konvergiert**, aber **nicht gegen** $f(x)$

**Beispiel:** $f(x) = e^{-1/x^2}$ für $x \neq 0$ und $f(0) = 0$
- Man kann zeigen: $f^{(k)}(0) = 0$ für alle $k \in \mathbb{N}$
- Die Taylorreihe ist die **Nullfunktion**
- Aber $f(x) \neq 0$ für $x \neq 0$!

Dies sind aber **eher Ausnahmen**.

---

## 5. Wichtige Taylorreihen

### Exponentialfunktion

$$\boxed{e^x = \sum_{k=0}^{\infty} \frac{x^k}{k!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{x^4}{4!} + \ldots}$$

**Konvergenz:** Für **alle** $x \in \mathbb{R}$

**Beweis:** $|f^{(n)}(x)| = e^x \leq e^{|x|}$, also gilt das hinreichende Kriterium mit $A = 1, B = e^{|x|}$ auf jedem beschränkten Intervall.

### Sinusfunktion

$$\boxed{\sin(x) = \sum_{k=0}^{\infty} \frac{(-1)^k}{(2k+1)!}x^{2k+1} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \ldots}$$

**Konvergenz:** Für **alle** $x \in \mathbb{R}$

**Beweis:** $|\sin^{(n)}(x)| \leq 1 = 1 \cdot 1^n$ für alle $x \in \mathbb{R}$

**Beobachtung:** Nur **ungerade Potenzen**!

### Kosinusfunktion

$$\boxed{\cos(x) = \sum_{k=0}^{\infty} \frac{(-1)^k}{(2k)!}x^{2k} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \ldots}$$

**Konvergenz:** Für **alle** $x \in \mathbb{R}$

**Beweis:** $|\cos^{(n)}(x)| \leq 1 = 1 \cdot 1^n$ für alle $x \in \mathbb{R}$

**Beobachtung:** Nur **gerade Potenzen**!

### Bemerkung

Die Reihen von Sinus und Cosinus können **alternativ als Definition** für Sinus und Cosinus genommen werden!

---

## 6. Herleitung der Euler-Formel

### Euler-Formel

$$\boxed{e^{ix} = \cos(x) + i\sin(x)}$$

### Beweis mit Taylorreihen

**Ausgangspunkt:** Taylorreihe von $e^x$:
$$e^{ix} = \sum_{k=0}^{\infty} \frac{(ix)^k}{k!} = \sum_{k=0}^{\infty} \frac{i^k x^k}{k!}$$

**Aufteilung** in gerade ($k = 2\ell$) und ungerade ($k = 2\ell + 1$) Summanden:
$$e^{ix} = \sum_{\ell=0}^{\infty} \frac{i^{2\ell} x^{2\ell}}{(2\ell)!} + \sum_{\ell=0}^{\infty} \frac{i^{2\ell+1} x^{2\ell+1}}{(2\ell+1)!}$$

**Vereinfachung mit** $i^2 = -1$:
$$\begin{align}
e^{ix} &= \sum_{\ell=0}^{\infty} \frac{(i^2)^\ell x^{2\ell}}{(2\ell)!} + \sum_{\ell=0}^{\infty} \frac{i \cdot (i^2)^\ell x^{2\ell+1}}{(2\ell+1)!} \\
&= \sum_{\ell=0}^{\infty} \frac{(-1)^\ell x^{2\ell}}{(2\ell)!} + i \sum_{\ell=0}^{\infty} \frac{(-1)^\ell x^{2\ell+1}}{(2\ell+1)!} \\
&= \cos(x) + i\sin(x)
\end{align}$$

✓ **Euler-Formel bewiesen!**

### Spezialfälle der Euler-Formel

**Für** $x = \pi$:
$$e^{i\pi} = \cos(\pi) + i\sin(\pi) = -1 + i \cdot 0 = -1$$

$$\boxed{e^{i\pi} + 1 = 0}$$

**(Euler'sche Identität - "die schönste Formel der Mathematik")**

**Für** $x = \frac{\pi}{2}$:
$$e^{i\pi/2} = \cos(\pi/2) + i\sin(\pi/2) = 0 + i \cdot 1 = i$$

---

## 📌 Zusammenfassung

### Wichtige Taylorreihen (um $x_0 = 0$)

| **Funktion** | **Taylorreihe** | **Konvergenz** |
|-------------|-----------------|----------------|
| $e^x$ | $\sum_{k=0}^{\infty} \frac{x^k}{k!}$ | alle $x \in \mathbb{R}$ |
| $\sin(x)$ | $\sum_{k=0}^{\infty} \frac{(-1)^k}{(2k+1)!}x^{2k+1}$ | alle $x \in \mathbb{R}$ |
| $\cos(x)$ | $\sum_{k=0}^{\infty} \frac{(-1)^k}{(2k)!}x^{2k}$ | alle $x \in \mathbb{R}$ |

### Praktische Anwendungen

| **Anwendung** | **Methode** |
|--------------|-------------|
| Funktionswerte berechnen | Taylorpolynom + Fehlerabschätzung |
| Messfehler bestimmen | $\|\Delta f\| \approx \|f'(x)\| \cdot \|\Delta x\|$ |
| Ableitungen diskretisieren | $f''(x) \approx \frac{f(x+h) - 2f(x) + f(x-h)}{h^2}$ |
| Differentialgleichungen lösen | Finite-Differenzen-Methode |

### Konvergenzkriterium

**Hinreichend für Konvergenz:**
$$|f^{(n)}(x)| \leq A \cdot B^n \quad \Rightarrow \quad \lim_{n \to \infty} R_n(x) = 0$$

### Euler-Formel

$$e^{ix} = \cos(x) + i\sin(x)$$

**Herleitung:** Taylorreihe von $e^{ix}$ aufteilen in gerade und ungerade Potenzen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.07 Komplexe Zahlen 2]]: Euler-Formel (dort postuliert, hier bewiesen!)
- [[VL.18 Berechnung von Grenzwerten]]: $\frac{x^n}{n!} \to 0$ für Konvergenzbeweis
- [[VL.24 Taylor-Approximation]]: Taylorpolynom und Restglied
- [[VL.26 Elementare Funktionen 2]]: Reihendarstellung als Definition
