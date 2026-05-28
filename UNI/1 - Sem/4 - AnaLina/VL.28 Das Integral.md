**Class:** [[AnaLina]]  
**Date:** 19-12-2025  
**Topics:** #Integral #RiemannscheSumme #Integralrechnung #Flächenberechnung #Mittelwertsatz

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt das bestimmte Integral ein und behandelt seine grundlegenden Eigenschaften und Anwendungen.

- **Definition des Integrals** über Riemannsche Summen
- **Flächenberechnung** unter Funktionsgraphen
- Erweiterung auf **stückweise stetige/monotone Funktionen**
- **Rechenregeln** für Integrale (Linearität, Monotonie, Dreiecksungleichung)
- Das Integral als **Mittelwert** der Funktion
- **Mittelwertsatz der Integralrechnung**
- **Anwendungen**: Flächenbilanz, Streckenberechnung, Massenberechnung

---

## 1. Integraldefinition und Flächenberechnung

### Problemstellung

**Frage:** Wie groß ist der Flächeninhalt zwischen dem Graphen einer Funktion $f : [a, b] \to \mathbb{R}$ und der $x$-Achse?![[Screenshot 2026-01-10 at 10.50.18.png]]

**Annahme:** Zunächst sei $f$ stetig und positiv ($f(x) \geq 0$ für $x \in [a, b]$).

### Idee: Approximation durch Rechtecke

**Zerlegung des Intervalls:**

Unterteile $[a, b]$ in $n$ gleichlange Teilintervalle:
$$a = x_0 < x_1 < x_2 < \dots < x_n = b$$

mit Länge $\Delta x = \frac{b-a}{n}$ und $x_j = a + j\Delta x = a + j\frac{b-a}{n}$

Die Punkte $x_0, x_1, \dots, x_n$ sind **äquidistant** (gleicher Abstand).
```
  |---|---|---|--...--|---|
  x₀  x₁  x₂  x₃  ... xₙ₋₁ xₙ
  a   Δx  Δx  Δx       Δx  b
```

**Approximation:** Approximiere $f$ auf $[x_{j-1}, x_j]$ durch die Konstante $f(x_{j-1})$.

### Riemannsche Summe

**Definition:** Die Summe

$$F_n = \sum_{j=1}^{n} f(x_{j-1})(x_j - x_{j-1}) = \sum_{j=1}^{n} f(x_{j-1})\Delta x = \sum_{j=1}^{n} f(x_{j-1}) \frac{b-a}{n}$$

heißt **Riemannsche Summe** der Funktion $f : [a, b] \to \mathbb{R}$.

Diese Summe ist die Fläche aller Rechtecke, mit der wir die Fläche unter dem Funktionsgraphen approximieren.
![[Screenshot 2026-01-10 at 10.51.38.png]]

**Erwartung:** Je größer $n$ ist, desto besser approximiert $F_n$ den exakten Wert $F$ des Flächeninhalts.

### Das bestimmte Integral

**Satz 28.1:** Ist $f : [a, b] \to \mathbb{R}$ stetig oder monoton, so existiert der Grenzwert

$$\lim_{n \to \infty} F_n =: \int_a^b f(x) \, dx$$

Wir nennen ihn das **bestimmte Integral** von $f$ über $[a, b]$.

**Notation und Terminologie:**

In $\int_a^b f(x) \, dx$ heißt:
- $f$ der **Integrand**
- $x$ die **Integrationsvariable**
- $a$ die **untere Integrationsgrenze**
- $b$ die **obere Integrationsgrenze**
- $\int$ das **Integralzeichen** (stilisiertes "S" für Summe)

**Wichtige Bemerkungen:**

1. Die Integrationsvariable ist **beliebig benennbar**:
   $$\int_a^b f(x) \, dx = \int_a^b f(t) \, dt = \int_a^b f(s) \, ds = \int_a^b f(u) \, du$$

2. Das bestimmte Integral $\int_a^b f(x) \, dx$ ist eine **reelle Zahl**.

3. In der Schreibweise $\int_a^b f(x) \, dx = \lim_{n \to \infty} \sum_{j=1}^{n} f(x_{j-1}) \cdot \Delta x$ erinnert:
   - $\int$ (langes S) an $\sum$ (Summe)
   - $dx$ an $\Delta x$
   
   Vergleiche auch: $\frac{df(x)}{dx} = \lim_{\Delta x \to 0} \frac{\Delta f(x)}{\Delta x} = \lim_{\Delta x \to 0} \frac{f(x+\Delta x) - f(x)}{\Delta x}$

---

## 2. Beispiel und Anwendungen

### Beispiel: Konstante Funktion

**Beispiel 28.3:** Ist $f : [a, b] \to \mathbb{R}$ konstant, also $f(x) = c$ für alle $x \in [a, b]$, so ist

$$\int_a^b f(x) \, dx = c(b-a)$$

- Für $c > 0$: Das ist genau der Flächeninhalt zwischen dem Graphen von $f$ und der $x$-Achse.
- Für $c < 0$: Das Integral ist das **Negative** des Flächeninhalts.![[Screenshot 2026-01-10 at 10.53.01.png]]
### Anwendung 1: Flächenbilanz und Flächenberechnung

Falls $f : [a, b] \to \mathbb{R}$ stetig ist, aber **nicht** $f(x) \geq 0$ für alle $x$ gilt, ergibt das Integral die **Flächenbilanz**:
- Fläche **über** der $x$-Achse zählt **positiv**
- Fläche **unter** der $x$-Achse zählt **negativ**
 ![[Screenshot 2026-01-10 at 10.53.19.png]]

**Berechnung:**
- **Flächenbilanz:** $\int_a^b f(x) \, dx = F_1 - F_2$
- **Gesamtfläche:** $F = F_1 + F_2$, wobei
  $$F_1 = \int_a^{x_1} f(x) \, dx, \quad F_2 = \left|\int_{x_1}^b f(x) \, dx\right|$$

Um die Gesamtfläche zu bestimmen, zerlege $[a, b]$ in Teilintervalle, auf denen $f$ das Vorzeichen nicht wechselt.

### Anwendung 2: Streckenberechnung (Freier Fall)

**Problem:** Ein Massenpunkt im freien Fall wird zur Zeit $t = 0$ losgelassen.

**Geschwindigkeit:** $v(t) = gt$ mit $g = 9.81 \, \text{m/s}^2$ (Erdbeschleunigung)

**Frage:** Wie groß ist die zurückgelegte Fallstrecke zum Zeitpunkt $T > 0$?

**Lösung über Riemannsche Summen:**

Zerlege $[0, T]$ in Teilintervalle $[t_{j-1}, t_j]$ mit $\Delta t = \frac{T}{n}$ und $t_j = j\Delta t = j\frac{T}{n}$.

Approximiere $v(t)$ auf $[t_{j-1}, t_j]$ durch $v(t_{j-1})$:

$$S \approx \sum_{j=1}^{n} v(t_{j-1})\Delta t$$

**Exakte Strecke:**

$$S = \lim_{n \to \infty} \sum_{j=1}^{n} v(t_{j-1})\Delta t = \int_0^T v(t) \, dt$$

**Berechnung:**

$$\int_0^T v(t) \, dt = \lim_{n \to \infty} \sum_{j=1}^{n} g(j-1)\frac{T}{n} \cdot \frac{T}{n} = \lim_{n \to \infty} \frac{gT^2}{n^2} \sum_{j=1}^{n} (j-1)$$

$$= \lim_{n \to \infty} \frac{gT^2}{n^2} \sum_{k=0}^{n-1} k = \lim_{n \to \infty} \frac{gT^2}{n^2} \cdot \frac{(n-1)n}{2} = \lim_{n \to \infty} \frac{gT^2}{2}\left(1 - \frac{1}{n}\right) = \frac{1}{2}gT^2$$

**Ergebnis:** Die Fallstrecke ist $S = \frac{1}{2}gT^2$ (bekannte Formel aus der Physik).

### Anwendung 3: Massenberechnung

**Problem:** Masse eines Drahtes der Länge $\ell$ mit Massendichte $\rho = \rho(x)$.

(Wir vernachlässigen die Ausdehnung in $y$- und $z$-Richtung.)

- **Falls $\rho$ konstant ist:** Gesamtmasse ist $m = \rho \ell$
- **Falls $\rho$ variabel ist:** 

Zerlege $[0, \ell]$ in $n$ Teilintervalle $[x_{j-1}, x_j]$ und approximiere $\rho(x)$ durch $\rho(x_{j-1})$ auf $[x_{j-1}, x_j]$.

**Gesamtmasse:**

$$m = \lim_{n \to \infty} \sum_{j=1}^{n} \rho(x_{j-1})\Delta x = \int_0^\ell \rho(x) \, dx$$

---

## 3. Erweiterung: Integrierbare Funktionen

### Motivation

In den Ingenieurwissenschaften müssen oft Funktionen integriert werden, die **weder monoton noch stetig** sind, z.B. die Steuerspannung des Kathodenstrahls einer Fernsehröhre:
![[Screenshot 2026-01-10 at 10.54.01.png]]

**Lösung:** Wir erweitern die Integraldefinition auf **stückweise stetige/monotone Funktionen**.

### Definition integrierbare Funktionen

**Definition 28.4:**

1. Wir nennen $f : [a, b] \to \mathbb{R}$ **stückweise stetig** (bzw. **stückweise monoton**), falls es endlich viele Stellen $x_0, x_1, \dots, x_N$ gibt mit
   $$a = x_0 < x_1 < \dots < x_N = b$$
   so dass $f : ]x_{j-1}, x_j[ \to \mathbb{R}$ für jedes $j$ die Einschränkung einer stetigen (bzw. monotonen) Funktion $f_j : [x_{j-1}, x_j] \to \mathbb{R}$ ist.

2. Ist $f$ wie in 1), so definieren wir
   $$\int_a^b f(x) \, dx := \int_{x_0}^{x_1} f_1(x) \, dx + \int_{x_1}^{x_2} f_2(x) \, dx + \dots + \int_{x_{N-1}}^{x_N} f_N(x) \, dx$$

3. Funktionen wie in 1) heißen **integrierbar**.

**Bemerkung 28.5:**
- Integrierbare Funktionen sind **beschränkt** und auf einem **kompakten Intervall** $[a, b]$ definiert.
- Diese Definition deckt sich nicht ganz mit der mathematischen Standardterminologie (dort ist die Klasse etwas größer).

### Beispiele

**Beispiel 28.6.1:** Die Funktion $f : [0, 1] \to \mathbb{R}$ mit

$$f(x) = \begin{cases} 0 & \text{für } x = 0 \\ \frac{1}{x} & \text{für } 0 < x \leq 1 \end{cases}$$

ist **nicht** stückweise stetig, denn $f : ]0, 1[ \to \mathbb{R}$ lässt sich nicht stetig auf $[0, 1]$ fortsetzen (Polstelle bei $x = 0$).

**Beispiel 28.6.2:** Die Funktion $f : [0, 2] \to \mathbb{R}$ mit

$$f(x) = \begin{cases} 1 & \text{für } x \in [0, 1[ \\ 2 & \text{für } x = 1 \\ 3 & \text{für } x \in ]1, 2] \end{cases}$$

ist stückweise stetig, denn:
- $f : ]0, 1[ \to \mathbb{R}$ ist die Einschränkung der stetigen Funktion $f_1 : [0, 1] \to \mathbb{R}$, $f_1(x) = 1$
- $f : ]1, 2[ \to \mathbb{R}$ ist die Einschränkung der stetigen Funktion $f_2 : [1, 2] \to \mathbb{R}$, $f_2(x) = 3$
- ![[Screenshot 2026-01-10 at 10.54.21.png]]

**Berechnung:**

$$\int_0^2 f(x) \, dx = \int_0^1 f_1(x) \, dx + \int_1^2 f_2(x) \, dx = 1(1-0) + 3(2-1) = 4$$

**Wichtig (Bemerkung 28.7):** Der Funktionswert in $x = 1$ (hier $f(1) = 2$) geht **nicht** in das Integral ein. Endlich viele Punktänderungen beeinflussen das Integral nicht.

---

## 4. Rechenregeln für Integrale

### Konventionen

Wir vereinbaren:
- $\int_a^a f(x) \, dx := 0$ (kein Flächeninhalt)
- Für $a < b$: $\int_a^b f(x) \, dx := -\int_b^a f(x) \, dx$ (Orientierung!)

### Satz 28.8: Rechenregeln

Seien $f, g : [a, b] \to \mathbb{R}$ integrierbar und $\lambda \in \mathbb{R}$. Dann gilt:

1. **Linearität:**
   $$\int_a^b (f(x) + g(x)) \, dx = \int_a^b f(x) \, dx + \int_a^b g(x) \, dx$$
   $$\int_a^b \lambda f(x) \, dx = \lambda \int_a^b f(x) \, dx$$

2. **Monotonie:** Falls $f(x) \leq g(x)$ für alle $x \in [a, b]$, so ist
   $$\int_a^b f(x) \, dx \leq \int_a^b g(x) \, dx$$

3. **Dreiecksungleichung:**
   $$\left|\int_a^b f(x) \, dx\right| \leq \int_a^b |f(x)| \, dx$$

4. **Intervalladitivität:** Für $a < c < b$ ist
   $$\int_a^b f(x) \, dx = \int_a^c f(x) \, dx + \int_c^b f(x) \, dx$$
   
   (Diese Regel gilt sogar für **alle** $a, b, c \in \mathbb{R}$ im Definitionsbereich von $f$.)

**Beweis:** Die Aussagen lassen sich leicht für Riemannsche Summen nachprüfen und bleiben im Grenzwert erhalten.

---

## 5. Das Integral als Mittelwert

### Abschätzung des Integrals

**Satz 28.9:** Sei $f : [a, b] \to \mathbb{R}$ integrierbar und $m \leq f(x) \leq M$ für alle $x \in [a, b]$. Dann gilt

$$m(b-a) \leq \int_a^b f(x) \, dx \leq M(b-a)$$

**Beweis:** Für die konstante Funktion $g(x) = m$ ist $g(x) \leq f(x)$ für alle $x$, also nach Monotonie:

$$m(b-a) = \int_a^b g(x) \, dx \leq \int_a^b f(x) \, dx$$

Die zweite Ungleichung folgt analog mit $g(x) = M$.

**Grafische Darstellung:**
![[Screenshot 2026-01-10 at 10.54.49.png]]

### Interpretation als Mittelwert

**Bemerkung 28.10:** Es ist

$$\frac{1}{b-a} \int_a^b f(x) \, dx = \lim_{n \to \infty} \frac{1}{b-a} \sum_{j=1}^{n} f(x_{j-1}) \frac{b-a}{n} = \lim_{n \to \infty} \frac{1}{n} \sum_{j=1}^{n} f(x_{j-1})$$

Die Summe $\frac{1}{n}\sum_{j=1}^{n} f(x_{j-1})$ ist genau der **Mittelwert** der Funktionswerte $f(x_0), f(x_1), \dots, f(x_{n-1})$.

**Interpretation:** Das Integral $\frac{1}{b-a}\int_a^b f(x) \, dx$ kann als **Mittelwert der Funktion** $f$ angesehen werden.

Satz 28.9 besagt also, dass das **Integralmittel** zwischen dem kleinsten und größten Funktionswert liegt.

### Mittelwertsatz der Integralrechnung

**Satz 28.11 (Mittelwertsatz der Integralrechnung):** Sei $f : [a, b] \to \mathbb{R}$ stetig. Dann existiert ein $\xi \in [a, b]$ mit

$$f(\xi) = \frac{1}{b-a} \int_a^b f(x) \, dx$$

**Interpretation:** Der Mittelwert der Funktion wird tatsächlich an (mindestens) einer Stelle **angenommen**.

**Beweis:**

1. Als stetige Funktion nimmt $f$ ihr Minimum $m$ und Maximum $M$ in $[a, b]$ an (Satz 20.12).

2. Mit der Integralabschätzung (Satz 28.9) ist
   $$m \leq \frac{1}{b-a} \int_a^b f(x) \, dx \leq M$$

3. Nach dem Zwischenwertsatz (Satz 20.11) nimmt $f$ jeden Wert zwischen Minimum und Maximum an, d.h. es existiert ein $\xi \in [a, b]$ mit
   $$f(\xi) = \frac{1}{b-a} \int_a^b f(x) \, dx$$

---

## 📌 Zusammenfassung

| **Begriff** | **Definition/Formel** | **Bedeutung** |
|------------|----------------------|---------------|
| Riemannsche Summe | $F_n = \sum_{j=1}^{n} f(x_{j-1})\Delta x$ | Approximation der Fläche durch Rechtecke |
| Bestimmtes Integral | $\int_a^b f(x) \, dx = \lim_{n \to \infty} F_n$ | Exakte Fläche (oder Flächenbilanz) |
| Linearität | $\int_a^b (f+g) = \int_a^b f + \int_a^b g$ | Integral ist linear |
| Monotonie | $f \leq g \implies \int_a^b f \leq \int_a^b g$ | Ordnungserhaltend |
| Intervalladitivität | $\int_a^b f = \int_a^c f + \int_c^b f$ | Zerlegung möglich |
| Mittelwert | $\bar{f} = \frac{1}{b-a}\int_a^b f(x) \, dx$ | Durchschnittlicher Funktionswert |
| Mittelwertsatz | $\exists \xi: f(\xi) = \frac{1}{b-a}\int_a^b f$ | Mittelwert wird angenommen |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.20 Sätze über stetige Funktionen]]: Stetigkeit, Minimum/Maximum, Zwischenwertsatz (für Mittelwertsatz)
- [[VL.29 Integrationsregeln 1]]: Hauptsatz der Differential- und Integralrechnung (nächste VL)
- [[VL.30 Integrationsregeln 2]]: Integrationstechniken (Substitution, partielle Integration)
