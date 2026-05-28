**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Potenzreihen #Konvergenzradius #Differentiation #Taylorreihen #Konvergenzkreis

---

## 🎯 Lernziele der Vorlesung

Potenzreihen sind Verallgemeinerungen von Polynomen und erlauben die Darstellung wichtiger Funktionen als unendliche Reihen.

- **Definition von Potenzreihen** und Entwicklungspunkt
- **Konvergenzradius** und Konvergenzkreis
- **Differentiation und Integration** von Potenzreihen
- Zusammenhang zwischen **Potenzreihen und Taylorreihen**
- Berechnung von Konvergenzradien

---

## 1. Definition von Potenzreihen

### Definition (Potenzreihe)

Seien $z, z_0, a_k \in \mathbb{C}$, $k \in \mathbb{N}$. Eine **Potenzreihe** ist eine unendliche Reihe der Form

$$\boxed{\sum_{k=0}^{\infty} a_k(z - z_0)^k}$$

Dabei heißt:
- $a_k$ die **Koeffizienten** der Potenzreihe
- $z_0$ der **Entwicklungspunkt** der Potenzreihe

### Funktionsdefinition

Auf der Menge $D \subseteq \mathbb{C}$ aller $z$, für die die Reihe konvergiert, definiert

$$f(z) := \sum_{k=0}^{\infty} a_k(z - z_0)^k$$

eine Funktion $f: D \to \mathbb{C}$.

### Bemerkung

Potenzreihen können als **Grenzwerte von Polynomen** $\sum_{k=0}^{n} a_k(z - z_0)^k$ für $n \to \infty$ angesehen werden.

---

## 2. Konvergenz von Potenzreihen

### Satz (Konvergenz von Potenzreihen)

Seien $z_0, a_k \in \mathbb{C}$, $k \in \mathbb{N}$. Dann gibt es ein $R \in [0, \infty] \cup \{\infty\}$ mit:

**1. Absolute Konvergenz:** Die Potenzreihe $\sum_{k=0}^{\infty} a_k(z - z_0)^k$ konvergiert **absolut** für alle $z \in \mathbb{C}$ mit 

$$\boxed{|z - z_0| < R}$$

**2. Divergenz:** Die Potenzreihe $\sum_{k=0}^{\infty} a_k(z - z_0)^k$ **divergiert** für alle $z \in \mathbb{C}$ mit

$$\boxed{|z - z_0| > R}$$

**3. Rand:** Das Konvergenzverhalten auf dem **Rand des Kreises** (für alle $z$ mit $|z - z_0| = R$) muss bei jeder speziellen Reihe in jedem Punkt **einzeln untersucht** werden.

### Definition (Konvergenzradius)

$R$ heißt **Konvergenzradius** der Potenzreihe. Existiert der Grenzwert

$$A := \lim_{k \to \infty} \left|\frac{a_{k+1}}{a_k}\right|,$$

so gilt:

$$\boxed{R = \begin{cases} 
\frac{1}{A} & \text{falls } A \neq 0 \\
\infty & \text{falls } A = 0
\end{cases}}$$

**Alternative Formel:**

$$\boxed{R = \lim_{k \to \infty} \left|\frac{a_k}{a_{k+1}}\right|}$$

(falls der Grenzwert existiert)

### Geometrische Interpretation

**Im Reellen:**

```
x₀ - R        x₀        x₀ + R
   |-----------|-----------|
divergent  ?  konvergent  ?  divergent
```

Das Konvergenzintervall ist $]x_0 - R, x_0 + R[$.

**Im Komplexen:**

```
        z₀ (Mittelpunkt)
         •
        ╱ ╲
       ╱   ╲  Konvergenzkreis
      │  •  │  (absolut konvergent)
       ╲   ╱
        ╲ ╱
         R (Radius)
    
    außerhalb: divergent
    Rand (?): einzeln untersuchen
```

Die Potenzreihe konvergiert im offenen **Konvergenzkreis** vom Radius $R$ um $z_0$.

### Wichtige Bemerkung

❌ Sage **nicht**: "Die Reihe konvergiert innerhalb des Konvergenzradius"  
✅ Sage: "Die Reihe konvergiert innerhalb des **Konvergenzkreises**"

(Der Konvergenzradius ist eine Zahl, z.B. 7, kein geometrisches Objekt!)

---

## 3. Beispiele zur Konvergenz

### Beispiel 1: Geometrische Reihe

Die **geometrische Reihe** $\sum_{k=0}^{\infty} z^k$ ist eine Potenzreihe mit $a_k = 1$ für alle $k$.

**Konvergenzradius:**

$$R = \lim_{k \to \infty} \left|\frac{a_k}{a_{k+1}}\right| = \lim_{k \to \infty} \left|\frac{1}{1}\right| = 1$$

**Konvergenz:**

- Für $|z| < 1$: $$f(z) = \sum_{k=0}^{\infty} z^k = \frac{1}{1-z}$$

- Für $|z| > 1$: divergent

- Für $|z| = 1$: Da $|z^k| = 1$ keine Nullfolge ist, ist die Reihe **divergent** (nach dem notwendigen Konvergenzkriterium)

### Beispiel 2: Logarithmus-Reihe

Die Potenzreihe $\sum_{k=0}^{\infty} \frac{1}{k+1}x^{k+1}$ hat Konvergenzradius $R = 1$.

**Randpunkte:**
- Für $x = 1$: $\sum_{k=0}^{\infty} \frac{1}{k+1}$ = harmonische Reihe → **divergent**
- Für $x = -1$: $\sum_{k=0}^{\infty} \frac{(-1)^k}{k+1}$ = alternierende harmonische Reihe → **konvergent**

**Funktionsdarstellung:** Für $x \in [-1, 1[$ gilt:

$$\boxed{\sum_{k=0}^{\infty} \frac{1}{k+1}x^{k+1} = -\ln(1-x)}$$

**Beweis-Idee:** 
1. Ableitung beider Seiten: $\sum_{k=0}^{\infty} x^k = \frac{1}{1-x}$ (geometrische Reihe)
2. Nach dem Konstanzkriterium: $\sum_{k=0}^{\infty} \frac{1}{k+1}x^{k+1} = -\ln(1-x) + c$
3. Einsetzen von $x = 0$: $c = 0$

**Spezialfall:** Für $x = -1$ (Multiplikation mit $-1$):

$$\boxed{\sum_{k=0}^{\infty} \frac{(-1)^k}{k+1} = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} \pm \ldots = \ln(2)}$$

### Beispiel 3: Reihe mit ungeraden Potenzen

Betrachte die Potenzreihe

$$\sum_{k=0}^{\infty} \frac{5^k}{k+1}z^{2k+1}$$

Diese enthält nur **ungerade Potenzen** von $z$, also $a_k = 0$ für alle geraden $k$.

**Problem:** Der Grenzwert $\lim_{k \to \infty} \left|\frac{a_k}{a_{k+1}}\right|$ existiert nicht (wegen $a_{2k} = 0$).

**Lösung 1 - Quotientenkriterium direkt:**

$$\lim_{k \to \infty} \left|\frac{\frac{5^{k+1}}{k+2}z^{2k+3}}{\frac{5^k}{k+1}z^{2k+1}}\right| = \lim_{k \to \infty} \left|\frac{k+1}{k+2} \cdot 5z^2\right| = 5|z|^2$$

Absolute Konvergenz für $5|z|^2 < 1$, also $|z| < \frac{1}{\sqrt{5}}$.

**Konvergenzradius:** $R = \frac{1}{\sqrt{5}}$

**Lösung 2 - Substitution:**

$$\sum_{k=0}^{\infty} \frac{5^k}{k+1}z^{2k+1} = z \sum_{k=0}^{\infty} \frac{5^k}{k+1}(z^2)^k$$

Setze $w = z^2$. Die Reihe $\sum_{k=0}^{\infty} \frac{5^k}{k+1}w^k$ hat Konvergenzradius

$$R_w = \lim_{k \to \infty} \left|\frac{\frac{5^k}{k+1}}{\frac{5^{k+1}}{k+2}}\right| = \lim_{k \to \infty} \frac{k+2}{5(k+1)} = \frac{1}{5}$$

Die Originalreihe konvergiert für $|z^2| < \frac{1}{5}$, also $|z| < \frac{1}{\sqrt{5}}$.

---

## 4. Differentiation von Potenzreihen

### Satz (Differentiation von Potenzreihen)

Die reelle Potenzreihe

$$\sum_{k=0}^{\infty} a_k(x - x_0)^k$$

habe den Konvergenzradius $R > 0$. Sie konvergiert also auf dem Intervall $]x_0 - R, x_0 + R[$ und definiert dort eine Funktion $f(x)$.

**Dann gilt:**

1. Die Funktion $f$ ist **differenzierbar** auf $]x_0 - R, x_0 + R[$

2. **Gliedweise Differentiation:**

$$\boxed{f'(x) = \sum_{k=1}^{\infty} ka_k(x - x_0)^{k-1}}$$

3. Der Konvergenzradius der **abgeleiteten Reihe** ist wieder $R$

### Bemerkung

✅ **Fazit:** Potenzreihen darf man **gliedweise differenzieren**

✅ Der **Konvergenzradius bleibt gleich**

✅ Ebenso darf man Potenzreihen **gliedweise integrieren**

### Wichtige Anmerkung

Bei **endlichen Summen** (Polynomen) ist gliedweise Differentiation trivial. Bei **Reihen** (unendlichen Summen) ist das Vertauschen von Grenzwerten und Ableitungen nicht selbstverständlich!

---

## 5. Taylor- und Potenzreihen

### Taylorreihe einer Funktion

Ist $f$ auf einem Intervall um $x_0$ **unendlich oft differenzierbar**, so kann man die **Taylorreihe** bilden:

$$\sum_{k=0}^{\infty} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k$$

Die Funktion stimmt genau dann mit ihrer Taylorreihe überein, wenn das **Restglied gegen 0 konvergiert**.

### Satz (Zusammenhang zwischen Potenz- und Taylorreihen)

Ist $f$ durch eine Potenzreihe mit Entwicklungspunkt $x_0$ gegeben, also

$$f(x) = \sum_{k=0}^{\infty} a_k(x - x_0)^k,$$

so ist die **Taylorreihe von $f$ in $x_0$ genau wieder die Potenzreihe von $f$**, d.h.

$$\boxed{f(x) = \sum_{k=0}^{\infty} \frac{f^{(k)}(x_0)}{k!}(x - x_0)^k}$$

### Beweis-Idee

Aus der Potenzreihe $f(x) = \sum_{k=0}^{\infty} a_k(x - x_0)^k$ folgt durch gliedweise Differentiation:

$$f(x_0) = a_0$$

$$f'(x) = \sum_{k=1}^{\infty} ka_k(x - x_0)^{k-1} \quad \Rightarrow \quad f'(x_0) = 1 \cdot a_1$$

$$f''(x) = \sum_{k=2}^{\infty} k(k-1)a_k(x - x_0)^{k-2} \quad \Rightarrow \quad f''(x_0) = 2! \cdot a_2$$

Per Induktion: $$\boxed{f^{(k)}(x_0) = k! \cdot a_k \quad \text{für alle } k = 0, 1, 2, \ldots}$$

Daher: $$a_k = \frac{f^{(k)}(x_0)}{k!}$$

---

## 📌 Zusammenfassung

### Definitionen

| Begriff | Definition | Bemerkung |
|---------|------------|-----------|
| **Potenzreihe** | $\sum_{k=0}^{\infty} a_k(z - z_0)^k$ | Entwicklungspunkt $z_0$ |
| **Konvergenzradius** | $R = \lim_{k \to \infty} \left\|\frac{a_k}{a_{k+1}}\right\|$ | Falls Grenzwert existiert |
| **Konvergenzkreis** | $\{z \in \mathbb{C} : \|z - z_0\| < R\}$ | Offener Kreis |

### Konvergenzverhalten

**Für Potenzreihe $\sum_{k=0}^{\infty} a_k(z - z_0)^k$ mit Konvergenzradius $R$:**

✅ $|z - z_0| < R$ → **absolut konvergent**

❌ $|z - z_0| > R$ → **divergent**

❓ $|z - z_0| = R$ → **einzeln untersuchen** (Rand)

### Rechenregeln

**Differentiation:**

$$f(x) = \sum_{k=0}^{\infty} a_k(x - x_0)^k \quad \Rightarrow \quad f'(x) = \sum_{k=1}^{\infty} ka_k(x - x_0)^{k-1}$$

Der Konvergenzradius bleibt gleich!

**Taylor = Potenzreihe:**

Wenn $f(x) = \sum_{k=0}^{\infty} a_k(x - x_0)^k$, dann $a_k = \frac{f^{(k)}(x_0)}{k!}$

### Wichtige Potenzreihen

| Funktion | Potenzreihe | Konvergenzradius |
|----------|-------------|------------------|
| $\frac{1}{1-z}$ | $\sum_{k=0}^{\infty} z^k$ | $R = 1$ |
| $-\ln(1-x)$ | $\sum_{k=0}^{\infty} \frac{1}{k+1}x^{k+1}$ | $R = 1$ |
| $e^x$ | $\sum_{k=0}^{\infty} \frac{x^k}{k!}$ | $R = \infty$ |
| $\sin(x)$ | $\sum_{k=0}^{\infty} \frac{(-1)^k}{(2k+1)!}x^{2k+1}$ | $R = \infty$ |
| $\cos(x)$ | $\sum_{k=0}^{\infty} \frac{(-1)^k}{(2k)!}x^{2k}$ | $R = \infty$ |

### Spezialwert

$$\boxed{\ln(2) = \sum_{k=0}^{\infty} \frac{(-1)^k}{k+1} = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} \pm \ldots}$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.23 Mittelwertsatz]]: Beweis der Logarithmus-Reihe
- [[VL.25 Anwendung Taylor-Approximation]]: Taylorreihen als spezielle Potenzreihen
- [[VL.26 Elementare Funktionen 2]]: $e^x$ als Potenzreihe
- [[VL.27 Elementare Funktionen 3]]: $\sin(x)$, $\cos(x)$ als Potenzreihen
- [[VL.40 Reihen]]: Konvergenzkriterien für Reihen

