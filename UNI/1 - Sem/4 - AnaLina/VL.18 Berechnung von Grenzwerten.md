**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Grenzwerte #Grenzwertsätze #SandwichTheorem #Monotoniekriterium #GeometrischeFolge

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung stellt wichtige Hilfsmittel zur Berechnung von Grenzwerten von Folgen bereit.

- **Grenzwertsätze** zur Berechnung komplexer Grenzwerte
- Zusammenhang zwischen **Grenzwerten und Ungleichungen**
- **Sandwich-Theorem** für Abschätzungen
- **Monotoniekriterium** als Konvergenzkriterium
- Wichtige **Standard-Grenzwerte** (geometrische Folge, Exponentialfunktion, etc.)

---

## 1. Grenzwertsätze

### Satz (Grenzwertsätze)

Seien $(a_n)_{n \in \mathbb{N}}$ und $(b_n)_{n \in \mathbb{N}}$ konvergente Folgen mit
$$\lim_{n \to \infty} a_n = a \quad \text{und} \quad \lim_{n \to \infty} b_n = b$$

Dann gilt:

1. **Summe:** $\lim_{n \to \infty} (a_n + b_n) = a + b$

2. **Differenz:** $\lim_{n \to \infty} (a_n - b_n) = a - b$

3. **Produkt:** $\lim_{n \to \infty} (a_n \cdot b_n) = a \cdot b$

4. **Skalarmultiplikation:** $\lim_{n \to \infty} (c \cdot a_n) = c \cdot a$ für alle $c \in \mathbb{R}$

5. **Quotient:** Falls $b \neq 0$, gibt es ein $n_0 \in \mathbb{N}$ mit $b_n \neq 0$ für alle $n \geq n_0$, und dann ist
   $$\lim_{n \to \infty} \frac{a_n}{b_n} = \frac{a}{b}$$

### Wichtige Bemerkung

⚠️ Die Grenzwertsätze gelten **nur für konvergente Folgen**!

**Gegenbeispiel:**
$$1 = \lim_{n \to \infty} 1 = \lim_{n \to \infty} \left(n \cdot \frac{1}{n}\right) \neq \left(\lim_{n \to \infty} n\right) \cdot \left(\lim_{n \to \infty} \frac{1}{n}\right) = \infty \cdot 0$$

Der Fehler: $\lim_{n \to \infty} n$ ist nicht konvergent!

### Beispiele

**1. Rationale Funktionen:** Für $(a_n) = \frac{2n+1}{1+n}$ gilt:
$$\lim_{n \to \infty} \frac{2n+1}{1+n} = \lim_{n \to \infty} \frac{2 + \frac{1}{n}}{\frac{1}{n} + 1} = \frac{2 + 0}{0 + 1} = 2$$

**2. Allgemeine Regel:** Für Polynome mit $p_k, q_\ell \neq 0$ ist:
$$\lim_{n \to \infty} \frac{p_k n^k + p_{k-1} n^{k-1} + \ldots + p_0}{q_\ell n^\ell + q_{\ell-1} n^{\ell-1} + \ldots + q_0} = \begin{cases} 
0, & k < \ell \\
\frac{p_k}{q_\ell}, & k = \ell \\
\pm\infty, & k > \ell
\end{cases}$$

*Trick:* Kürze die höchste Potenz!

---

## 2. Grenzwerte und Ungleichungen

### Satz (Erhaltung von Ungleichungen)

Seien $(a_n)_n$ und $(b_n)_n$ konvergente Folgen mit
$$a_n \leq b_n \quad \text{für alle } n \in \mathbb{N}$$

Dann gilt:
$$\lim_{n \to \infty} a_n \leq \lim_{n \to \infty} b_n$$

### Wichtiger Hinweis

⚠️ Aus $a_n < b_n$ folgt ebenfalls nur $a \leq b$!

Die **strikte Ungleichung geht im Grenzwert verloren**.

**Gegenbeispiel:**
- $a_n = 1 - \frac{1}{n} < 1 + \frac{1}{n} = b_n$ für alle $n \in \mathbb{N}$
- Aber: $\lim_{n \to \infty} a_n = 1 = \lim_{n \to \infty} b_n$

---

## 3. Sandwich-Theorem

### Satz (Sandwich-Theorem / Drei-Folgen-Satz)

Seien $(a_n)_n$, $(b_n)_n$, $(c_n)_n$ drei reelle Folgen mit
$$a_n \leq b_n \leq c_n \quad \text{für alle } n \in \mathbb{N}$$

und
$$\lim_{n \to \infty} a_n = \lim_{n \to \infty} c_n = a$$

Dann konvergiert auch $(b_n)_n$ gegen $a$:
$$\lim_{n \to \infty} b_n = a$$

### Folgerung

**Nullfolge mal beschränkte Folge ist wieder eine Nullfolge:**

Ist $(a_n)_n$ eine Nullfolge und $(b_n)_n$ beschränkt, so ist $(a_n \cdot b_n)_n$ eine Nullfolge.

### Beispiele

**1. Alternierende Folge:**
$$-\frac{1}{n} \leq \frac{(-1)^n}{n} \leq \frac{1}{n}$$

Da $\pm\frac{1}{n} \to 0$, folgt $\lim_{n \to \infty} \frac{(-1)^n}{n} = 0$.

**2. Sinus-Folge:**
$$0 \leq \left|\frac{\sin(n)}{n}\right| \leq \frac{1}{n} \to 0$$

Also: $\lim_{n \to \infty} \frac{\sin(n)}{n} = 0$.

**3. Fakultät dominiert Potenz:** Für $x \in \mathbb{R}$ gilt:
$$\lim_{n \to \infty} \frac{x^n}{n!} = 0$$

*Beweis-Idee:* Wähle $k > 2|x|$. Für $n \geq k$:
$$\left|\frac{x^n}{n!}\right| = \frac{|x|^k}{k!} \cdot \frac{|x|^{n-k}}{(k+1) \cdots n} \leq \frac{|x|^k}{k!} \cdot \left(\frac{1}{2}\right)^{n-k} \to 0$$

---

## 4. Monotoniekriterium

### Satz (Monotoniekriterium)

Jede **beschränkte und monotone** Folge reeller Zahlen ist **konvergent**.

### Wichtige Bemerkungen

1. Das Kriterium ist nur **hinreichend**, aber **nicht notwendig**
   - Konvergente Folgen sind beschränkt, aber nicht notwendig monoton
   - Beispiel: $\left(\frac{(-1)^n}{n}\right)_{n \geq 1}$ konvergiert, ist aber nicht monoton

2. Monotone Folgen, die **nicht beschränkt** sind, sind **bestimmt divergent**

### Beispiel: Wurzelfolge

Gegeben sei die rekursiv definierte Folge:
$$a_0 > 0 \quad \text{und} \quad a_{n+1} = \frac{1}{2}\left(a_n + \frac{2}{a_n}\right), \quad n \geq 0$$

**Behauptung:** Die Folge konvergiert gegen $\sqrt{2}$.

**Beweis:**

**(1) Nach unten beschränkt:** Für $n \geq 0$ gilt (arithmetisches ≥ geometrisches Mittel):
$$a_{n+1} = \frac{a_n + \frac{2}{a_n}}{2} \geq \sqrt{a_n \cdot \frac{2}{a_n}} = \sqrt{2}$$

**(2) Monoton fallend** (ab $n \geq 1$): Für $n \geq 1$ ist $a_n \geq \sqrt{2}$, also $a_n^2 \geq 2$:
$$\frac{a_{n+1}}{a_n} = \frac{1}{2}\left(1 + \frac{2}{a_n^2}\right) \leq \frac{1}{2}\left(1 + \frac{2}{2}\right) = 1$$

Also $a_{n+1} \leq a_n$.

**(3) Grenzwert bestimmen:** Da $a_n \to a$ und $a_{n+1} \to a$, gilt:
$$a = \lim_{n \to \infty} a_{n+1} = \lim_{n \to \infty} \frac{1}{2}\left(a_n + \frac{2}{a_n}\right) = \frac{1}{2}\left(a + \frac{2}{a}\right)$$

Daraus folgt: $a = \frac{a}{2} + \frac{1}{a}$, also $\frac{a}{2} = \frac{1}{a}$, also $a^2 = 2$.

Da $a \geq \sqrt{2}$ ist der Grenzwert $a = \sqrt{2}$.

**Numerisches Beispiel** (Startwert $a_0 = 1$):
- $a_0 = 1.000000000000000$
- $a_1 = 1.500000000000000$
- $a_2 = 1.416666666666667$
- $a_3 = 1.414215686274510$
- $a_4 = 1.414213562374690$
- $a_5 = 1.414213562373095$ ✓

Bereits nach 5 Schritten 15 korrekte Nachkommastellen!

### Beispiel: Eulerfolge

$$a_n = \left(1 + \frac{1}{n}\right)^n, \quad n \geq 1$$

Die Folge ist beschränkt und monoton wachsend, also konvergent. Der Grenzwert ist die **Eulersche Zahl**:
$$e = \lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n = 2.718281828459045...$$

---

## 5. Wichtige Grenzwerte

### Geometrische Folge

Für $q \in \mathbb{R}$ ist:
$$\lim_{n \to \infty} q^n = \begin{cases}
0, & -1 < q < 1 \\
1, & q = 1 \\
+\infty, & q > 1 \\
\text{divergent}, & q \leq -1
\end{cases}$$

### Geometrische Summe und Reihe

**Geometrische Summe:**
$$s_n := \sum_{k=0}^{n} q^k = \begin{cases}
\frac{1 - q^{n+1}}{1 - q}, & q \neq 1 \\
n + 1, & q = 1
\end{cases}$$

**Geometrische Reihe:**
$$\sum_{k=0}^{\infty} q^k = \lim_{n \to \infty} \sum_{k=0}^{n} q^k = \begin{cases}
\frac{1}{1-q}, & |q| < 1 \\
+\infty, & q \geq 1 \\
\text{divergent}, & q \leq -1
\end{cases}$$

### Standard-Grenzwerte (ohne Beweis)

|                          Grenzwert                          |                            Wert                             |                          Bemerkung                          |
| :---------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| ........................................................... | ........................................................... | ........................................................... |
|            $\lim_{n \to \infty} \frac{x^n}{n!}$             |                             $0$                             |                 für alle $x \in \mathbb{R}$                 |
|              $\lim_{n \to \infty} \sqrt[n]{x}$              |                             $1$                             |                         für $x > 0$                         |
|              $\lim_{n \to \infty} \sqrt[n]{n}$              |                             $1$                             |                              —                              |
|    $\lim_{n \to \infty} \left(1 + \frac{x}{n}\right)^n$     |                            $e^x$                            |                 für alle $x \in \mathbb{R}$                 |
|        $\lim_{n \to \infty} \frac{\ln(n)}{n^\alpha}$        |                             $0$                             |                      für $\alpha > 0$                       |
|     $\lim_{n \to \infty} \frac{n^\alpha}{e^{\beta n}}$      |                             $0$                             |           für $\alpha \in \mathbb{R}, \beta > 0$            |
|          $\lim_{n \to \infty} n^\alpha \cdot q^n$           |                             $0$                             |              für $\alpha \in \mathbb{R},q< 1$               |
|             $\lim_{n \to \infty} \sqrt[n]{n!}$              |                             $e$                             |                              —                              |

**Interpretation:**
- Fakultät $n!$ wächst schneller als jede Potenz $x^n$
- Exponentialfunktion $e^{\beta n}$ wächst schneller als jede Potenz $n^\alpha$
- Potenz $n^\alpha$ wächst schneller als Logarithmus $\ln(n)$

---

## 📌 Zusammenfassung

### Rechentechniken für Grenzwerte

1. **Grenzwertsätze:** Zerlege komplexe Ausdrücke in bekannte Teile
2. **Kürzen:** Bei rationalen Funktionen höchste Potenz kürzen
3. **Sandwich-Theorem:** Bei Abschätzungen $0 \leq |a_n| \leq b_n$ mit $b_n \to 0$
4. **Monotoniekriterium:** Bei rekursiven Folgen Monotonie und Beschränktheit zeigen

### Warnung: Vorsicht bei Grenzwerten

❌ **Falsch bei divergenten Folgen:**
- Grenzwertsätze gelten nur für konvergente Folgen
- $\infty \cdot 0$, $\frac{\infty}{\infty}$, $\infty - \infty$ sind **nicht definiert**

❌ **Grenzwert vor Konvergenzbeweis:**
- Erst Konvergenz zeigen, dann Grenzwert berechnen!
- Gegenbeispiel: $a_0 = 1, a_{n+1} = 3 - a_n$ ist divergent $(1, 2, 1, 2, \ldots)$

✓ **Richtig:**
- Strikte Ungleichungen $a_n < b_n$ werden zu $a \leq b$
- Sandwich-Theorem für Abschätzungen nutzen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.17 Konvergenz]]: Definition und Grundlagen der Konvergenz
- [[VL.19 Stetigkeit]]: Grenzwerte von Funktionen
- [[VL.20 Sätze über stetige Funktionen]]: Bisektionsverfahren vs. Wurzelfolge
- [[VL.26 Elementare Funktionen 2]]: Exponentialfunktion und Eulersche Zahl

---