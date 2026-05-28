**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Stammfunktion #UnbestimmtesIntegral #Hauptsatz #PartielleIntegration #Grundintegrale

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt Stammfunktionen ein und zeigt, wie man Integrale durch den Hauptsatz berechnet.

- Definition der **Stammfunktion** und des **unbestimmten Integrals**
- **Hauptsatz der Differential- und Integralrechnung**
- **Grundintegrale** und bekannte Stammfunktionen
- **Partielle Integration** (Integration nach Teilen)
- Nicht-elementare Stammfunktionen (Fresnel, Gauß-Fehlerfunktion)

---

## 1. Stammfunktionen

### Definition (Stammfunktion)

Sei $f : D \to \mathbb{R}$ eine Funktion ($D \subseteq \mathbb{R}$). Eine differenzierbare Funktion $F : D \to \mathbb{R}$ heißt eine **Stammfunktion** von $f$, falls

$$\boxed{F'(x) = f(x) \quad \text{für alle } x \in D}$$

### Eindeutigkeit von Stammfunktionen

**Satz:** Auf **Intervallen** sind Stammfunktionen **bis auf eine Konstante eindeutig**.

**Beweis:** Seien $F$ und $G$ zwei Stammfunktionen von $f$ auf einem Intervall $I$. Dann ist:
$$(G - F)' = G' - F' = f - f = 0$$

Nach dem Konstanzkriterium (Satz 23.7) ist $G - F$ konstant, d.h. es existiert $c \in \mathbb{R}$ mit:
$$G(x) = F(x) + c \quad \text{für alle } x \in I$$

### Beispiele

**1.** $f(x) = x$ hat die Stammfunktion $F(x) = \frac{1}{2}x^2$
- Auch $G(x) = \frac{1}{2}x^2 + 3$ ist eine Stammfunktion
- Auch $H(x) = \frac{1}{2}x^2 - 12000$ ist eine Stammfunktion

**2.** $f(x) = e^x$ hat die Stammfunktion $F(x) = e^x$
- Wegen $(e^x)' = e^x$

**3.** $f(x) = \cos(x)$ hat die Stammfunktion $F(x) = \sin(x)$
- Auch $F(x) = \sin(x) + 42$ ist eine Stammfunktion

---

## 2. Unbestimmtes Integral

### Definition (Unbestimmtes Integral)

Die **Menge aller Stammfunktionen** von $f : [a, b] \to \mathbb{R}$ wird mit $\int f(x)\,dx$ bezeichnet und heißt das **unbestimmte Integral** von $f$.

Ist $F$ eine Stammfunktion von $f$, so ist:
$$\int f(x)\,dx = \{F + c \mid c \in \mathbb{R}\}$$

**Übliche Schreibweise** (ohne Mengenklammern):
$$\boxed{\int f(x)\,dx = F(x) + c, \quad c \in \mathbb{R} \text{ beliebig}}$$

### Interpretation

Das unbestimmte Integral ist die **Lösungsmenge** der linearen Gleichung:
$$\frac{d}{dx}F(x) = f(x)$$

Wie bei linearen Gleichungssystemen: **Partikuläre Lösung** $F$ plus **Lösung der homogenen Gleichung** (= Konstanten).

---

## 3. Hauptsatz der Differential- und Integralrechnung

### Satz (Hauptsatz)

**Teil 1: Existenz einer Stammfunktion**

Ist $f : [a, b] \to \mathbb{R}$ stetig, so ist die durch
$$F : [a, b] \to \mathbb{R}, \quad F(x) = \int_a^x f(t)\,dt$$

definierte **Integralfunktion** eine Stammfunktion von $f$.

**Teil 2: Berechnung des bestimmten Integrals**

Ist $F : [a, b] \to \mathbb{R}$ eine Stammfunktion der stetigen Funktion $f : [a, b] \to \mathbb{R}$, so gilt:

$$\boxed{\int_a^b f(x)\,dx = F\bigg|_a^b := F(b) - F(a)}$$

**Alternative Schreibweisen:** $[F]_a^b$ oder ähnlich

### Beweis-Skizze Teil 1

Zeige: $F'(x) = f(x)$

$$\frac{F(x+h) - F(x)}{h} = \frac{1}{h}\left(\int_a^{x+h} f(t)\,dt - \int_a^x f(t)\,dt\right) = \frac{1}{h}\int_x^{x+h} f(t)\,dt$$

Nach dem Mittelwertsatz der Integralrechnung:
$$\frac{1}{h}\int_x^{x+h} f(t)\,dt = f(\xi)$$

für ein $\xi$ zwischen $x$ und $x+h$. Für $h \to 0$ ist $\xi \to x$ und (wegen Stetigkeit):
$$F'(x) = \lim_{h \to 0} f(\xi) = f(x)$$

### Beweis-Skizze Teil 2

Da $F$ und $\int_a^x f(t)\,dt$ beide Stammfunktionen von $f$ auf $[a, b]$ sind, gibt es eine Konstante $c \in \mathbb{R}$ mit:
$$F(x) = \int_a^x f(t)\,dt + c$$

Für $x = a$: $F(a) = 0 + c$, also $c = F(a)$

Für $x = b$:
$$\int_a^b f(t)\,dt = F(b) - c = F(b) - F(a)$$

### Bedeutung

Der Hauptsatz ermöglicht es, das **bestimmte Integral** einer stetigen Funktion ganz einfach durch **Auswerten einer Stammfunktion** zu berechnen, falls man diese kennt!

---

## 4. Beispiele zum Hauptsatz

### Beispiel 1: $\int_a^b x\,dx$

**Stammfunktion:** $F(x) = \frac{1}{2}x^2$

$$\int_a^b x\,dx = \frac{1}{2}x^2\bigg|_a^b = \frac{1}{2}(b^2 - a^2)$$

**Spezialfall:** $\int_0^1 x\,dx = \frac{1}{2}$

Dies ist genau der Flächeninhalt des Dreiecks mit Ecken $(0, 0)$, $(1, 0)$, $(1, 1)$.

### Beispiel 2: $\int_0^\pi \sin(x)\,dx$

**Stammfunktion:** $F(x) = -\cos(x)$

$$\int_0^\pi \sin(x)\,dx = -\cos(x)\bigg|_0^\pi = -\cos(\pi) + \cos(0) = 1 + 1 = 2$$

**Vergleich:** Versuch mal, dies direkt mit der Definition zu berechnen:
$$\int_0^\pi \sin(x)\,dx = \lim_{n \to \infty} \sum_{j=1}^n \sin\left(\frac{(j-1)\pi}{n}\right) \cdot \frac{\pi}{n}$$

Der Hauptsatz ist **viel einfacher**!

### Beispiel 3: Exponentialfunktion

$$\int_a^b e^x\,dx = e^x\bigg|_a^b = e^b - e^a$$

### Beispiel 4: Arcus Tangens

$$\int_a^b \frac{1}{1+x^2}\,dx = \arctan(x)\bigg|_a^b = \arctan(b) - \arctan(a)$$

**Integraldarstellung:** Mit $a = 0$:
$$\arctan(x) = \int_0^x \frac{1}{1+t^2}\,dt$$

### Beispiel 5: Arcus Sinus

$$\int_a^b \frac{1}{\sqrt{1-x^2}}\,dx = \arcsin(x)\bigg|_a^b = \arcsin(b) - \arcsin(a)$$

### Beispiel 6: Heaviside-Funktion (Warnung!)

**Gegeben:** $H : \mathbb{R} \to \mathbb{R}, H(x) = \begin{cases} 0, & x < 0 \\ 1, & x \geq 0 \end{cases}$

Für $b > 0$ und $H : [-b, b] \to \mathbb{R}$:
$$F(x) := \int_{-b}^x H(t)\,dt = \begin{cases} 0, & x < 0 \\ x, & x \geq 0 \end{cases}$$

**Problem:** $F$ hat eine **Knickstelle** in $x = 0$, ist dort **nicht differenzierbar**!

$\Rightarrow$ $F$ ist **keine Stammfunktion** von $H$

**Folgerung:** Die **Stetigkeit** von $f$ im Hauptsatz ist **wesentlich**!

---

## 5. Grundintegrale

### Potenzfunktionen

**Für** $\alpha \in \mathbb{R} \setminus \{-1\}$:
$$\boxed{\int x^\alpha\,dx = \frac{1}{\alpha + 1}x^{\alpha+1} + c}$$

**Definitionsbereich:**
- $D = \mathbb{R}$, falls $\alpha \in \mathbb{N}$
- $D = \mathbb{R} \setminus \{0\}$, falls $\alpha \in \mathbb{Z} \setminus \mathbb{N}$ (z.B. $x^{-2} = \frac{1}{x^2}$)
- $D = \,]0, \infty[$, falls $\alpha \in \mathbb{R} \setminus \mathbb{Z}$ (allgemeine Potenz)

**Spezialfälle:**
- $\int x^n\,dx = \frac{1}{n+1}x^{n+1} + c$ für $n \in \mathbb{N}$
- $\int x^{-2}\,dx = -x^{-1} + c = -\frac{1}{x} + c$

### Reziproke Funktion

**Für** $f(x) = \frac{1}{x}$ auf $D = \mathbb{R} \setminus \{0\}$:

$$\boxed{\int \frac{1}{x}\,dx = \ln|x| + c}$$

**Beweis:**
- Für $x > 0$: $\frac{d}{dx}\ln(x) = \frac{1}{x}$
- Für $x < 0$: $\frac{d}{dx}\ln(-x) = \frac{1}{-x} \cdot (-1) = \frac{1}{x}$ (Kettenregel)

**Wichtig:** $\ln(x)$ ist nur auf $\,]0, \infty[$ definiert, daher brauchen wir $\ln|x|$ für ganz $\mathbb{R} \setminus \{0\}$!

**Verallgemeinerung:**
$$\int \frac{1}{x-a}\,dx = \ln|x-a| + c$$

### Exponentialfunktion

$$\int e^{ax}\,dx = \frac{1}{a}e^{ax} + c$$

### Trigonometrische Funktionen

$$\begin{align}
\int \sin(x)\,dx &= -\cos(x) + c \\
\int \cos(x)\,dx &= \sin(x) + c \\
\int \frac{1}{\cos^2(x)}\,dx &= \tan(x) + c \quad (x \neq \frac{\pi}{2} + k\pi) \\
\int \frac{-1}{\sin^2(x)}\,dx &= \cot(x) + c \quad (x \neq k\pi)
\end{align}$$

---

## 6. Nicht-elementare Stammfunktionen

### Motivation

Manche Stammfunktionen lassen sich **nicht elementar ausdrücken** (d.h. durch Polynome, $e^x$, sin, cos, etc. und deren Addition, Multiplikation, Verkettung).

In diesem Fall geben die **Integralfunktionen** "neue" Funktionen!

### Beispiel 1: Fresnel-Integral

**Funktion:** $f(x) = \sin(x^2)$ ist stetig, besitzt also eine Stammfunktion.

**Fresnel-Integral:**
$$\text{FresnelS}(x) = \int_0^x \sin\left(\frac{\pi}{2}t^2\right)\,dt$$

**Anwendung:** Geometrische Optik

### Beispiel 2: Gauß-Fehlerfunktion

**Funktion:** $f(x) = e^{-x^2}$

Die Stammfunktion kann **nicht durch elementare Funktionen** angegeben werden!

**Gauß-Fehlerfunktion (Error Function):**
$$\boxed{\text{erf}(x) = \frac{2}{\sqrt{\pi}}\int_0^x e^{-t^2}\,dt}$$

**Anwendungen:**
- Diffusionsprozesse
- Statistik (Normalverteilung)

### Beispiel 3: Integralsinus

**Funktion:** $f(x) = \frac{\sin(x)}{x}$

**Integralsinus:**
$$\text{Si}(x) = \int_0^x \frac{\sin(t)}{t}\,dt$$

Diese Funktion ist ebenfalls **nicht durch elementare Funktionen darstellbar**.

---

## 7. Partielle Integration

### Motivation

Die **partielle Integration** (= **Integration nach Teilen**) entspricht der **Produktregel** beim Ableiten.

### Herleitung

Aus der Produktregel:
$$(uv)' = u'v + uv'$$

folgt durch Integration:
$$uv = \int u'v\,dx + \int uv'\,dx$$

Umstellen ergibt:
$$\int u'v\,dx = uv - \int uv'\,dx$$

### Satz (Partielle Integration)

Sind $u, v : [a, b] \to \mathbb{R}$ differenzierbar mit stetigen Ableitungen, so gelten:

**Für unbestimmte Integrale:**
$$\boxed{\int u'(x)v(x)\,dx = u(x)v(x) - \int u(x)v'(x)\,dx}$$

**Für bestimmte Integrale:**
$$\boxed{\int_a^b u'(x)v(x)\,dx = (uv)\bigg|_a^b - \int_a^b u(x)v'(x)\,dx}$$

### Merkregel

Man wählt:
- $u'$ so, dass es **leicht integrierbar** ist
- $v$ so, dass $v'$ **einfacher** als $v$ ist (oft: Polynom ableiten!)

---

## 8. Beispiele zur partiellen Integration

### Beispiel 1: $\int_a^b xe^x\,dx$

**Falsche Wahl:** $u'(x) = x$, $v(x) = e^x$
- Dann $u(x) = \frac{1}{2}x^2$, $v'(x) = e^x$
- Integral wird komplizierter: $\int \frac{1}{2}x^2 e^x\,dx$ ✗

**Richtige Wahl:** $u'(x) = e^x$, $v(x) = x$
- Dann $u(x) = e^x$, $v'(x) = 1$

$$\int_a^b xe^x\,dx = xe^x\bigg|_a^b - \int_a^b e^x\,dx = xe^x\bigg|_a^b - e^x\bigg|_a^b = (x-1)e^x\bigg|_a^b$$

**Merke:** Polynom **ableiten** ist oft hilfreich!

### Beispiel 2: $\int x^2\cos(x)\,dx$

**Idee:** Mit partieller Integration das $x^2$ "wegdifferenzieren"

**Erste partielle Integration:** $u'(x) = \cos(x)$, $v(x) = x^2$
$$\int x^2\cos(x)\,dx = x^2\sin(x) - \int 2x\sin(x)\,dx$$

**Zweite partielle Integration:** $u'(x) = -\sin(x)$, $v(x) = 2x$
$$\int x^2\cos(x)\,dx = x^2\sin(x) + 2x\cos(x) - \int 2\cos(x)\,dx$$
$$= x^2\sin(x) + 2x\cos(x) - 2\sin(x) + c$$
$$= (x^2 - 2)\sin(x) + 2x\cos(x) + c$$

### Beispiel 3: $\int \cos^2(x)\,dx$

**Trick:** $u'(x) = \cos(x)$, $v(x) = \cos(x)$
- Dann $u(x) = \sin(x)$, $v'(x) = -\sin(x)$

$$\int \cos^2(x)\,dx = \sin(x)\cos(x) + \int \sin^2(x)\,dx$$

Mit $\sin^2(x) = 1 - \cos^2(x)$:
$$\int \cos^2(x)\,dx = \sin(x)\cos(x) + \int (1 - \cos^2(x))\,dx$$
$$= \sin(x)\cos(x) + x - \int \cos^2(x)\,dx$$

Auflösen nach $\int \cos^2(x)\,dx$:
$$2\int \cos^2(x)\,dx = \sin(x)\cos(x) + x$$
$$\boxed{\int \cos^2(x)\,dx = \frac{1}{2}(\sin(x)\cos(x) + x) + c}$$

**Anwendung:** $\int_0^{2\pi} \cos^2(x)\,dx = \frac{1}{2}(\sin(x)\cos(x) + x)\bigg|_0^{2\pi} = \pi$

### Beispiel 4: $\int \ln(x)\,dx$ (Trick!)

**Trick:** $u'(x) = 1$, $v(x) = \ln(x)$
- Dann $u(x) = x$, $v'(x) = \frac{1}{x}$

$$\int \ln(x)\,dx = x\ln(x) - \int x \cdot \frac{1}{x}\,dx = x\ln(x) - \int 1\,dx$$
$$\boxed{\int \ln(x)\,dx = x\ln(x) - x + c}$$

---

## 📌 Zusammenfassung

### Wichtige Stammfunktionen (Auswahl)

| $f(x)$ | $F(x)$ | Bemerkungen |
|--------|--------|-------------|
| $x^n$ | $\frac{1}{n+1}x^{n+1}$ | $n \in \mathbb{N}$ |
| $x^\alpha$ | $\frac{1}{\alpha+1}x^{\alpha+1}$ | $\alpha \neq -1$ |
| $\frac{1}{x}$ | $\ln\|x\|$ | $x \neq 0$ |
| $e^{ax}$ | $\frac{1}{a}e^{ax}$ | $a \neq 0$ |
| $\sin(x)$ | $-\cos(x)$ | — |
| $\cos(x)$ | $\sin(x)$ | — |
| $\frac{1}{\cos^2(x)}$ | $\tan(x)$ | $x \neq \frac{\pi}{2} + k\pi$ |
| $\frac{1}{1+x^2}$ | $\arctan(x)$ | — |
| $\frac{1}{\sqrt{1-x^2}}$ | $\arcsin(x)$ | $\|x\| < 1$ |

### Hauptsatz der Differential- und Integralrechnung

**Teil 1:** Jede stetige Funktion hat eine Stammfunktion:
$$F(x) = \int_a^x f(t)\,dt$$

**Teil 2:** Berechnung über Stammfunktion:
$$\int_a^b f(x)\,dx = F(b) - F(a)$$

### Partielle Integration

$$\int u'v\,dx = uv - \int uv'\,dx$$

**Merkregel:** Polynom ableiten, Rest integrieren!

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.21 Differenzierbarkeit]]: Produktregel als Basis für partielle Integration
- [[VL.23 Mittelwertsatz]]: Konstanzkriterium
- [[VL.28 Das Integral]]: Definition des bestimmten Integrals
- [[VL.30 Integrationsregeln 2]]: Substitutionsregel

