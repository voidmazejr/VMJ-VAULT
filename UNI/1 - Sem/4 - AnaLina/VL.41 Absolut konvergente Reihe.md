**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #AbsoluteKonvergenz #Majorantenkriterium #Quotientenkriterium #CauchyProdukt

---

## 🎯 Lernziele der Vorlesung

Ein stärkerer Konvergenzbegriff: absolute Konvergenz. Mit absolut konvergenten Reihen kann man wie mit endlichen Summen rechnen.

- **Absolute Konvergenz** und ihre Vorteile
- **Cauchy-Produkt** von Reihen
- **Konvergenzkriterien**: Majoranten-, Minoranten-, Quotientenkriterium
- **Komplexe Reihen**

---

## 1. Absolute Konvergenz

### Definition (Absolute Konvergenz)

Die Reihe $\sum_{k=0}^\infty a_k$ heißt **absolut konvergent**, falls die Reihe

$$\boxed{\sum_{k=0}^\infty |a_k|}$$

konvergent ist.

### Wichtiger Satz

Konvergiert eine Reihe **absolut**, so konvergiert sie auch im **gewöhnlichen** Sinne:

$$\boxed{\sum_{k=0}^\infty |a_k| \text{ konvergent} \implies \sum_{k=0}^\infty a_k \text{ konvergent}}$$

**Absolute Konvergenz ist stärker als gewöhnliche Konvergenz!**

⚠️ **Achtung:** Die **Umkehrung ist falsch**! Es gibt konvergente Reihen, die **nicht** absolut konvergieren.

### Beispiel: Alternierende harmonische Reihe

Die **alternierende harmonische Reihe** $\sum_{k=1}^\infty \frac{(-1)^k}{k}$ ist:

- ✅ **Konvergent** (nach Leibnizkriterium, siehe [[VL.40 Reihen]])
- ❌ **Nicht absolut konvergent**, denn:

$$\sum_{k=1}^\infty \left|\frac{(-1)^k}{k}\right| = \sum_{k=1}^\infty \frac{1}{k}$$

ist die **harmonische Reihe**, die divergiert!

### Vorteil absoluter Konvergenz

Mit absolut konvergenten Reihen kann man **wie mit endlichen Summen** rechnen:

- Umordnen der Summanden ändert den Wert nicht
- Multiplikation von Reihen (Cauchy-Produkt) funktioniert
- Robustere Konvergenz

---

## 2. Cauchy-Produkt

### Satz (Cauchy-Produkt)

Sind die Reihen $\sum_{k=0}^\infty a_k$ und $\sum_{k=0}^\infty b_k$ **beide absolut konvergent**, so ist auch ihr Produkt (das **Cauchy-Produkt**) absolut konvergent:

$$\boxed{\left(\sum_{k=0}^\infty a_k\right) \cdot \left(\sum_{k=0}^\infty b_k\right) = \sum_{k=0}^\infty c_k}$$

wobei

$$\boxed{c_k = a_0 b_k + a_1 b_{k-1} + a_2 b_{k-2} + \ldots + a_k b_0 = \sum_{j=0}^k a_j b_{k-j}}$$

**Merkhilfe:** Multipliziere $\sum_{k=0}^\infty a_k x^k$ und $\sum_{k=0}^\infty b_k x^k$ und sortiere nach Potenzen von $x$, dann für $x = 1$.

⚠️ **Wichtig:** Falls $\sum a_k$ und $\sum b_k$ konvergieren, aber **nicht absolut**, muss $\sum c_k$ nicht notwendigerweise konvergieren!

---

## 3. Majorantenkriterium

### Satz (Majorantenkriterium)

Die Reihe $\sum_{k=0}^\infty b_k$ sei **konvergent**, und es gelte:

$$\boxed{|a_k| \leq b_k \quad \text{für alle } k \in \mathbb{N}}$$

(Es genügt auch, wenn $|a_k| \leq b_k$ für alle $k \geq k_0$ ab einem Startwert $k_0 \in \mathbb{N}$ gilt.)

Dann ist die Reihe $\sum_{k=0}^\infty a_k$ **absolut konvergent**.

### Beweis

Wegen $b_k \geq |a_k| \geq 0$ sind alle $b_k \geq 0$ und die Folge der Partialsummen $\sum_{k=0}^n b_k$ ist monoton wachsend. Insbesondere gilt:

$$\sum_{k=0}^n |a_k| \leq \sum_{k=0}^n b_k \leq \sum_{k=0}^\infty b_k =: M$$

Daher ist die Folge der Partialsummen $\sum_{k=0}^n |a_k|$ durch $M$ beschränkt und monoton wachsend (da $|a_k| \geq 0$), also konvergent.

Damit konvergiert $\sum_{k=0}^\infty |a_k|$, d.h. $\sum_{k=0}^\infty a_k$ ist absolut konvergent. ✓

### Beispiel

Vergleiche die Reihen $\sum_{k=1}^\infty \frac{1}{k^2}$ und $\sum_{k=2}^\infty \left(\frac{1}{k-1} - \frac{1}{k}\right)$.

Für $k \geq 2$ ist:

$$\left|\frac{1}{k^2}\right| = \frac{1}{k^2} < \frac{1}{k(k-1)} = \frac{1}{k-1} - \frac{1}{k}$$

Die zweite Reihe konvergiert (Teleskopsumme):

$$\sum_{k=2}^n \left(\frac{1}{k-1} - \frac{1}{k}\right) = \left(1 - \frac{1}{2}\right) + \left(\frac{1}{2} - \frac{1}{3}\right) + \ldots + \left(\frac{1}{n-1} - \frac{1}{n}\right)$$

$$= 1 - \frac{1}{n} \to 1$$

Also konvergiert $\sum_{k=1}^\infty \frac{1}{k^2}$ nach dem Majorantenkriterium. ✓

(Den Wert $\sum_{k=1}^\infty \frac{1}{k^2} = \frac{\pi^2}{6}$ haben wir mit Fourier-Analysis in [[VL.38 Approximation im quadratischen mittel]] berechnet.)

---

## 4. Minorantenkriterium

### Satz (Minorantenkriterium)

Gilt $0 \leq b_k \leq a_k$ und ist die Reihe $\sum_{k=0}^\infty b_k$ **bestimmt divergent**, so ist auch die Reihe $\sum_{k=0}^\infty a_k$ **bestimmt divergent**.

### Beweis

Aus $0 \leq b_k \leq a_k$ folgt:

$$\sum_{k=0}^n b_k \leq \sum_{k=0}^n a_k$$

Da die erste Summe über alle Schranken wächst, tut das auch die zweite. ✓

**Interpretation:** Wenn eine "kleinere" Reihe divergiert, divergiert auch die "größere" Reihe.

---

## 5. Quotientenkriterium

### Satz (Quotientenkriterium)

Gegeben sei die Reihe $\sum_{k=0}^\infty a_k$. Falls der Grenzwert

$$\boxed{r = \lim_{k \to \infty} \left|\frac{a_{k+1}}{a_k}\right|}$$

existiert, so gilt:

- **Ist $r < 1$:** Die Reihe konvergiert **absolut**
- **Ist $r > 1$:** Die Reihe **divergiert**
- **Ist $r = 1$:** Das Kriterium trifft **keine Aussage** (alles ist möglich)

### Beweis-Idee

**Fall $r < 1$:** Wähle $q$ mit $r < q < 1$. Dann ist $\left|\frac{a_{k+1}}{a_k}\right| < q$ für alle $k \geq k_0$.

Daraus folgt:

$$|a_k| < q|a_{k-1}| < q^2|a_{k-2}| < \ldots < q^{k-k_0}|a_{k_0}| = q^k \frac{|a_{k_0}|}{q^{k_0}}$$

Mit der geometrischen Reihe:

$$\sum_{k=0}^\infty q^k \frac{|a_{k_0}|}{q^{k_0}} = \frac{|a_{k_0}|}{q^{k_0}} \cdot \frac{1}{1-q} < \infty$$

Das Majorantenkriterium zeigt die absolute Konvergenz. ✓

**Fall $r > 1$:** Für große $k$ ist $|a_{k+1}| > |a_k|$, also ist $(a_k)$ keine Nullfolge → Reihe divergiert (notwendiges Kriterium). ✓

### Verbesserte Aussage

Im Beweis haben wir nicht wirklich den Grenzwert verwendet. Es reicht:

**Gibt es ein $q < 1$ und ein $k_0$, so dass $\left|\frac{a_{k+1}}{a_k}\right| \leq q$ für alle $k \geq k_0$, so ist die Reihe absolut konvergent.**

### Beispiele

**Beispiel 1:** $\sum_{k=0}^\infty \frac{k}{2^k}$

$$\left|\frac{a_{k+1}}{a_k}\right| = \frac{\frac{k+1}{2^{k+1}}}{\frac{k}{2^k}} = \frac{k+1}{2^{k+1}} \cdot \frac{2^k}{k} = \frac{1}{2} \cdot \frac{k+1}{k} = \frac{1}{2}\left(1 + \frac{1}{k}\right) \to \frac{1}{2} < 1$$

Die Reihe konvergiert **absolut**. ✓

**Beispiel 2:** Harmonische Reihe $\sum_{k=1}^\infty \frac{1}{k}$

$$\lim_{k \to \infty} \left|\frac{\frac{1}{k+1}}{\frac{1}{k}}\right| = \lim_{k \to \infty} \frac{k}{k+1} = 1$$

**Keine Aussage!** (Wir wissen: divergiert)

**Beispiel 3:** $\sum_{k=1}^\infty \frac{1}{k^2}$

$$\lim_{k \to \infty} \left|\frac{\frac{1}{(k+1)^2}}{\frac{1}{k^2}}\right| = \lim_{k \to \infty} \left(\frac{k}{k+1}\right)^2 = 1$$

**Keine Aussage!** (Wir wissen: konvergiert)

**Folgerung:** Ist der Grenzwert im Quotientenkriterium $= 1$, so kann **alles** passieren (Konvergenz oder Divergenz).

### Strategie zur Konvergenzuntersuchung

**1. Wahl:** **Quotientenkriterium** (benötigt nur die zu untersuchende Reihe)

**Falls $r = 1$:** Versuche andere Kriterien:
- Integralvergleichskriterium
- Majoranten-/Minorantenkriterium
- Leibnizkriterium (für alternierende Reihen)

---

## 6. Komplexe Reihen

### Definition

Für Reihen mit **komplexen Gliedern** $a_k \in \mathbb{C}$ definiert man Konvergenz und absolute Konvergenz **genauso** wie für reelle Reihen.

### Gültige Kriterien für komplexe Reihen

Für komplexe Reihen gelten:

✅ Aus absoluter Konvergenz folgt Konvergenz

✅ Notwendiges Kriterium: $\lim_{k \to \infty} a_k = 0$

✅ Majorantenkriterium

✅ Minorantenkriterium

✅ Quotientenkriterium

❌ **Nicht gültig:**
- Leibnizkriterium (nur für reelle Reihen mit alternierenden Vorzeichen)
- Integralvergleichskriterium (nur für reellwertige Funktionen)

### Wichtigstes Beispiel: Geometrische Reihe

Für alle $z \in \mathbb{C}$ mit $|z| < 1$ gilt:

$$\boxed{\sum_{k=0}^\infty z^k = \frac{1}{1-z}}$$

---

## 📌 Zusammenfassung

### Absolute Konvergenz

$$\sum_{k=0}^\infty |a_k| \text{ konvergent} \implies \sum_{k=0}^\infty a_k \text{ konvergent}$$

**Aber:** Umkehrung ist falsch! (Gegenbeispiel: alternierende harmonische Reihe)

**Vorteil:** Mit absolut konvergenten Reihen kann man wie mit endlichen Summen rechnen.

### Cauchy-Produkt

$$\left(\sum a_k\right) \cdot \left(\sum b_k\right) = \sum c_k \quad \text{mit} \quad c_k = \sum_{j=0}^k a_j b_{k-j}$$

**Gilt nur**, wenn beide Reihen **absolut konvergent** sind!

### Konvergenzkriterien (Übersicht)

| Kriterium | Bedingung | Aussage |
|-----------|-----------|---------|
| **Majoranten** | $\|a_k\| \leq b_k$, $\sum b_k$ konv. | $\sum a_k$ **absolut konv.** |
| **Minoranten** | $0 \leq b_k \leq a_k$, $\sum b_k$ div. | $\sum a_k$ **divergent** |
| **Quotienten** | $r = \lim \left\|\frac{a_{k+1}}{a_k}\right\|$ | $r < 1$: abs. konv.<br>$r > 1$: divergent<br>$r = 1$: keine Aussage |

### Strategie zur Konvergenzuntersuchung

**1. Schritt:** **Quotientenkriterium** (einfachste Anwendung)

**2. Schritt:** Falls $r = 1$, versuche:
- Integralvergleich (bei $\sum f(k)$)
- Majoranten-/Minoranten (bei Abschätzungen)
- Leibniz (bei alternierenden Reihen)

### Beispiele wichtiger Reihen

| Reihe | Konvergenz | Absolute Konv. |
|-------|------------|----------------|
| $\sum \frac{1}{k}$ | ❌ Divergent | ❌ Divergent |
| $\sum \frac{(-1)^k}{k}$ | ✅ Konvergent | ❌ Divergent |
| $\sum \frac{1}{k^2}$ | ✅ Konvergent | ✅ Absolut konv. |
| $\sum \frac{k}{2^k}$ | ✅ Konvergent | ✅ Absolut konv. |

### Komplexe Reihen

- Definition wie für reelle Reihen
- Geometrische Reihe: $\sum z^k = \frac{1}{1-z}$ für $|z| < 1$
- Quotientenkriterium, Majoranten-, Minorantenkriterium gültig
- Leibniz- und Integralvergleichskriterium **nicht** gültig

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.40 Reihen]]: Konvergenz, notwendiges Kriterium, Leibnizkriterium
- [[VL.18 Berechnung von Grenzwerten]]: Geometrische Reihe
- [[VL.38 Approximation im quadratischen mittel]]: Wert von $\sum \frac{1}{k^2} = \frac{\pi^2}{6}$