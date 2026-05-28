**Class:** [[AnaLina]]  
**Date:** 10-01-2026 
**Topics:** #Mittelwertsatz #Extremwerte #Monotoniekriterium #KritischePunkte #Extremwerttest

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt den Mittelwertsatz und seine Anwendungen zur Bestimmung von Extremwerten differenzierbarer Funktionen.

- Definition **lokaler und globaler Extrema**
- **Notwendiges Extremwertkriterium** ($f'(x_0) = 0$)
- **Mittelwertsatz** und seine Bedeutung
- **Monotoniekriterium** und **Konstanzkriterium**
- **Extremwert-Test** zur Charakterisierung von Extremstellen

---

## 1. Lokale und globale Extrema

### Definition (Lokale und globale Extrema)

Sei $f : D \to \mathbb{R}$ mit $D \subseteq \mathbb{R}$. Man nennt $x_0 \in D$

**1. Stelle eines globalen Maximums**, falls
$$f(x_0) \geq f(x) \quad \text{für alle } x \in D$$

Der Wert $f(x_0)$ heißt das **globale Maximum**.

**2. Stelle eines globalen Minimums**, falls
$$f(x_0) \leq f(x) \quad \text{für alle } x \in D$$

Der Wert $f(x_0)$ heißt das **globale Minimum**.

**3. Stelle eines lokalen Maximums**, falls es $\varepsilon > 0$ gibt, so dass für alle $x \in D$ mit $|x - x_0| < \varepsilon$ gilt:
$$f(x_0) \geq f(x)$$

Der Wert $f(x_0)$ heißt ein **lokales Maximum**.

**4. Stelle eines lokalen Minimums**, falls es $\varepsilon > 0$ gibt, so dass für alle $x \in D$ mit $|x - x_0| < \varepsilon$ gilt:
$$f(x_0) \leq f(x)$$

Der Wert $f(x_0)$ heißt ein **lokales Minimum**.

### Strikte Extrema

Gilt sogar $>$ statt $\geq$ bzw. $<$ statt $\leq$ (und ist $x \in D \setminus \{x_0\}$), so spricht man von **strengen** oder **strikten** lokalen oder globalen Extrema.

### Unterschied zwischen lokal und global

**Globales Maximum:**
- Größter Wert, den die Funktion annimmt
- Ist **eindeutig bestimmt** (der Wert, nicht die Stelle!)
- Kann an **mehreren Stellen** angenommen werden
- Ist auch ein lokales Maximum

**Lokales Maximum:**
- Es reicht aus, dass die Funktion in einer **kleinen Umgebung** kleiner oder gleich diesem Wert ist
- Es kann **mehrere** lokale Maxima geben
- Nicht jedes lokale Maximum ist ein globales Maximum

Analoges gilt für globale und lokale Minima.

---

## 2. Notwendiges Extremwertkriterium

### Anschauliche Herleitung

Nimmt $f : [a, b] \to \mathbb{R}$ in einem inneren Punkt $x_0 \in \,]a, b[$ ein Maximum an, dann haben:
- Die Sekanten **links** von $x_0$ eine Steigung $\geq 0$
- Die Sekanten **rechts** von $x_0$ eine Steigung $\leq 0$

Ist $f$ in $x_0$ differenzierbar, so ist $f'(x_0)$ der Grenzwert der Steigungen der Sekanten, also:
$$f'(x_0) \geq 0 \quad \text{und} \quad f'(x_0) \leq 0$$

Daraus folgt: $f'(x_0) = 0$

### Satz (Notwendiges Extremwertkriterium)

Sei $f : D \to \mathbb{R}$ im **inneren Punkt** $x_0$ differenzierbar. 

Wenn $x_0$ eine lokale Extremstelle ist, so ist die Ableitung dort Null:
$$\boxed{f'(x_0) = 0}$$

### Wichtige Bemerkungen

1. **Gilt nur für innere Punkte!** In Randpunkten muss $f'(x_0) = 0$ **nicht** gelten.

2. **Nur notwendige Bedingung!** Das bedeutet:
   - In einem lokalen Extremum ist $f'(x_0) = 0$ ✓
   - Aber $f'(x_0) = 0$ kann gelten, **ohne** dass in $x_0$ ein lokales Extremum vorliegt ✗

### Gegenbeispiel

$f : [-1, 1] \to \mathbb{R}, f(x) = x^3$

- $f'(x) = 3x^2$ hat eine Nullstelle in $x = 0$
- Aber $f$ hat in $x = 0$ **kein lokales Extremum** (Wendepunkt/Sattelpunkt)

### Nicht-differenzierbare Punkte

⚠️ Ist $f$ im Punkt $x_0$ **nicht differenzierbar**, so kann dort ebenfalls ein lokales Extremum vorliegen!

**Beispiel:** $f(x) = |x|$ hat in $x_0 = 0$ ein lokales (und globales) Minimum, obwohl $f$ dort nicht differenzierbar ist.

---

## 3. Kandidaten für Extremstellen

### Satz (Kandidaten für lokale Extremstellen)

Ist $f : [a, b] \to \mathbb{R}$ differenzierbar, so sind die **einzigen Kandidaten** für lokale Extremstellen:

1. **Die Randpunkte** $a$ und $b$

2. **Die Nullstellen von** $f'$ in $\,]a, b[$

Die Nullstellen von $f'$ heißen auch **kritische Punkte** oder **stationäre Punkte** von $f$.

### Praktisches Vorgehen

Typischerweise gibt es nur **endlich viele** Kandidaten. Man kann dann:
1. Alle kritischen Punkte und Randpunkte bestimmen
2. Die Funktionswerte an diesen Stellen berechnen
3. Die größten und kleinsten Werte identifizieren

Dies sind dann wirklich das globale Maximum und Minimum (da $f$ stetig auf $[a, b]$ ist).

---

## 4. Mittelwertsatz

### Satz (Mittelwertsatz)

Sei $f : I \to \mathbb{R}$ differenzierbar auf dem Intervall $I \subseteq \mathbb{R}$. 

Sind $a, b \in I$ beliebig mit $a < b$, so gibt es **mindestens eine Stelle** $\xi \in \,]a, b[$ mit

$$\boxed{\frac{f(b) - f(a)}{b - a} = f'(\xi)}$$

### Anschauliche Interpretation

Es gibt irgendwo eine **Tangente**, die die gleiche Steigung wie die **Sekante** durch $(a, f(a))$ und $(b, f(b))$ besitzt.

### Beweis-Idee

Betrachte die Differenz zwischen $f$ und der Sekante:
$$g(x) = f(x) - \left[f(a) + \frac{f(b) - f(a)}{b - a}(x - a)\right]$$

Dann ist $g(a) = 0 = g(b)$. 

Da $g$ stetig auf $[a, b]$ ist, hat $g$ mindestens einen Extremwert $\xi$ in $\,]a, b[$. 

Da $g$ in $\,]a, b[$ differenzierbar ist, folgt $g'(\xi) = 0$.

Aus $g'(x) = f'(x) - \frac{f(b) - f(a)}{b - a}$ folgt die Behauptung.

### Physikalische Interpretation

Bezeichnet $s(t)$ den zum Zeitpunkt $t$ zurückgelegten Weg, so besagt der Mittelwertsatz:

**Es gibt einen Zeitpunkt** $\tau$, **zu dem die Momentangeschwindigkeit gleich der Durchschnittsgeschwindigkeit ist:**

$$v(\tau) = s'(\tau) = \frac{s(b) - s(a)}{b - a}$$

### Bedeutung

Der Mittelwertsatz ist die **Brücke von Ableitungsinformationen zu Informationen über die Funktion selbst**.

### Visualisierung
![[Screenshot 2026-01-10 at 15.59.32.png]]

---

## 5. Anwendungen des Mittelwertsatzes

### Satz (Schrankensatz)

Sei $f : [a, b] \to \mathbb{R}$ stetig und auf $\,]a, b[$ differenzierbar. 

Ist $|f'(x)| \leq M$ für alle $x \in \,]a, b[$ und für ein $M > 0$, so ist

$$|f(x_2) - f(x_1)| \leq M(x_2 - x_1) \quad \text{für alle } x_1, x_2 \in [a, b] \text{ mit } x_1 < x_2$$

**Interpretation:** Die Ableitung beschränkt die Änderungsrate der Funktion.

---

## 6. Monotoniekriterium

### Satz (Monotoniekriterium)

Sei $f : [a, b] \to \mathbb{R}$ stetig und auf $\,]a, b[$ differenzierbar. Dann gilt:

**1. Streng monoton wachsend:**
$$f'(x) > 0 \text{ für alle } x \in \,]a, b[ \quad \Rightarrow \quad f \text{ ist streng monoton wachsend}$$

Das heißt: $x_1 < x_2 \Rightarrow f(x_1) < f(x_2)$

**2. Streng monoton fallend:**
$$f'(x) < 0 \text{ für alle } x \in \,]a, b[ \quad \Rightarrow \quad f \text{ ist streng monoton fallend}$$

Das heißt: $x_1 < x_2 \Rightarrow f(x_2) < f(x_1)$

**3. Monoton wachsend:**
$$f'(x) \geq 0 \text{ für alle } x \in \,]a, b[ \quad \Leftrightarrow \quad f \text{ ist monoton wachsend}$$

**4. Monoton fallend:**
$$f'(x) \leq 0 \text{ für alle } x \in \,]a, b[ \quad \Leftrightarrow \quad f \text{ ist monoton fallend}$$

### Beweis-Skizze (für 1)

Seien $x_1, x_2 \in [a, b]$ mit $x_1 < x_2$. Nach dem Mittelwertsatz existiert $\xi \in \,]x_1, x_2[$ mit
$$f(x_2) - f(x_1) = f'(\xi) \underbrace{(x_2 - x_1)}_{> 0} > 0$$

Also $f(x_2) > f(x_1)$, d.h. $f$ ist streng monoton wachsend.

### Wichtige Bemerkungen

1. **Randpunkte:** Ist $f$ in einem Randpunkt nicht definiert, gilt das Kriterium immer noch für das entsprechend angepasste Intervall (z.B. $\,]a, b]$ statt $[a, b]$).

2. **Richtung "⇐" gilt nicht immer!** In (1) und (2) gilt nur die Richtung "$\Rightarrow$".

   **Gegenbeispiel:** $f(x) = x^3$ ist streng monoton wachsend, aber $f'(0) = 0$.

### Beispiel: Monotonie des Tangens

Zeige: $\tan : \,]-\frac{\pi}{2}, \frac{\pi}{2}[ \to \mathbb{R}$ ist streng monoton wachsend.

**Ableitung:**
$$\tan'(x) = \frac{\sin'(x)\cos(x) - \sin(x)\cos'(x)}{\cos^2(x)} = \frac{\cos^2(x) + \sin^2(x)}{\cos^2(x)} = \frac{1}{\cos^2(x)} > 0$$

Nach dem Monotoniekriterium ist $\tan$ streng monoton wachsend.

---

## 7. Konstanzkriterium

### Satz (Konstanzkriterium)

Sei $f : [a, b] \to \mathbb{R}$ stetig und auf $\,]a, b[$ differenzierbar. Dann gilt:

$$\boxed{f'(x) = 0 \text{ für alle } x \in \,]a, b[ \quad \Leftrightarrow \quad f \text{ ist konstant auf } [a, b]}$$

### Beweis

**"$\Leftarrow$":** Klar, konstante Funktionen haben Ableitung 0.

**"$\Rightarrow$":** Wenn $f'(x) = 0$ für alle $x \in \,]a, b[$, dann ist gleichzeitig $f'(x) \geq 0$ und $f'(x) \leq 0$. 

Nach dem Monotoniekriterium ist $f$ zugleich monoton wachsend und monoton fallend, also konstant.

---

## 8. Extremwert-Test

### Satz (Extremwert-Test mit erster Ableitung)

Sei $f$ differenzierbar im offenen Intervall $\,]a, b[$ und sei $x_0$ ein **kritischer Punkt**, also $f'(x_0) = 0$. Dann gilt:

**1. Lokales Maximum:** $f$ hat in $x_0$ ein lokales Maximum, falls ein $\varepsilon > 0$ existiert mit:
$$f'(x) > 0 \text{ für alle } x \in \,]x_0 - \varepsilon, x_0[ \quad \text{und} \quad f'(x) < 0 \text{ für alle } x \in \,]x_0, x_0 + \varepsilon[$$

**Merkhilfe:** $f'$ wechselt von **+ nach –** (Funktion steigt, dann fällt)

**2. Lokales Minimum:** $f$ hat in $x_0$ ein lokales Minimum, falls ein $\varepsilon > 0$ existiert mit:
$$f'(x) < 0 \text{ für alle } x \in \,]x_0 - \varepsilon, x_0[ \quad \text{und} \quad f'(x) > 0 \text{ für alle } x \in \,]x_0, x_0 + \varepsilon[$$

**Merkhilfe:** $f'$ wechselt von **– nach +** (Funktion fällt, dann steigt)

### Visualisierung

![[Screenshot 2026-01-10 at 15.59.52.png]]

### Wichtige Bemerkungen

1. **Kein Vorzeichenwechsel:** Ist $f'(x) > 0$ (oder $f'(x) < 0$) für alle $x$ links und rechts von $x_0$, so ist $f$ streng monoton und hat **kein Extremum** in $x_0$.

2. **Randpunkte:** Der Test gibt nur für **innere Punkte** Auskunft. Randpunkte müssen immer getrennt betrachtet werden.

3. **Extrema an Randpunkten:** Ist $f$ in $a$ noch stetig, so gilt:
   - $f'(x) > 0$ in $\,]a, a + \varepsilon[$ → $f$ hat in $a$ ein **lokales Minimum**
   - $f'(x) < 0$ in $\,]a, a + \varepsilon[$ → $f$ hat in $a$ ein **lokales Maximum**
   
   Analog für Randpunkt $b$:
   - $f'(x) > 0$ in $\,]b - \varepsilon, b[$ → $f$ hat in $b$ ein **lokales Maximum**
   - $f'(x) < 0$ in $\,]b - \varepsilon, b[$ → $f$ hat in $b$ ein **lokales Minimum**

---

## 9. Beispiel: Vollständige Extremwertbestimmung

**Gegeben:** $f : [-1, 2] \to \mathbb{R}, f(x) = 2x^3 - 3x^2 + 1$

### Schritt 1: Kritische Punkte finden

$$f'(x) = 6x^2 - 6x = 6x(x - 1)$$

Nullstellen: $x = 0$ und $x = 1$

### Schritt 2: Vorzeichentabelle erstellen

| $x$     | $-1$     | $0$     | $1$     | $2$     |
| ------- | -------- | ------- | ------- | ------- |
| $f'(x)$ | $+$      | $0$     | $-$     | $0$     |
| $f(x)$  | steigend | **max** | fallend | **min** |

### Schritt 3: Kandidaten bewerten

**Kritische Punkte:**
- $x = 0$: $f'$ wechselt von $+$ nach $-$ → **lokales Maximum** mit $f(0) = 1$
- $x = 1$: $f'$ wechselt von $-$ nach $+$ → **lokales Minimum** mit $f(1) = 0$

**Randpunkte:**
- $x = -1$: $f'(x) > 0$ rechts von $-1$ → **lokales Minimum** mit $f(-1) = -4$
- $x = 2$: $f'(x) > 0$ links von $2$ → **lokales Maximum** mit $f(2) = 5$

### Schritt 4: Globale Extrema

- **Globales Maximum:** $f(2) = 5$ (größter Wert)
- **Globales Minimum:** $f(-1) = -4$ (kleinster Wert)

---

## 📌 Zusammenfassung

### Wichtige Begriffe

| **Begriff** | **Bedeutung** |
|------------|---------------|
| **Globales Maximum** | Größter Wert auf ganz $D$ |
| **Lokales Maximum** | Größter Wert in einer Umgebung |
| **Kritischer Punkt** | Punkt mit $f'(x_0) = 0$ |
| **Stationärer Punkt** | Synonym für kritischer Punkt |

### Zentrale Sätze

| **Satz** | **Aussage** |
|----------|-------------|
| **Notwendiges Kriterium** | Lokales Extremum in innerem Punkt → $f'(x_0) = 0$ |
| **Mittelwertsatz** | $\exists \xi \in \,]a, b[: \frac{f(b) - f(a)}{b - a} = f'(\xi)$ |
| **Monotoniekriterium** | $f' > 0 \Rightarrow f \nearrow$, $f' < 0 \Rightarrow f \searrow$ |
| **Konstanzkriterium** | $f' = 0 \Leftrightarrow f$ konstant |
| **Extremwert-Test** | Vorzeichenwechsel von $f'$ → Extremum |

### Praktische Vorgehensweise zur Extremwertbestimmung

1. **Kritische Punkte** finden: Löse $f'(x) = 0$
2. **Randpunkte** hinzufügen (falls vorhanden)
3. **Vorzeichentabelle** von $f'$ erstellen
4. **Extremwert-Test** anwenden
5. **Funktionswerte** an allen Kandidaten berechnen
6. **Globale Extrema** durch Vergleich bestimmen

### Häufige Fehler

❌ **Falsch:** "Jeder kritische Punkt ist ein Extremum"
✅ **Richtig:** Kritische Punkte sind nur Kandidaten (z.B. $x^3$ in $x = 0$)

❌ **Falsch:** "Streng monoton → $f' \neq 0$ überall"
✅ **Richtig:** Gegenbeispiel $x^3$ mit $f'(0) = 0$

❌ **Falsch:** "Extremum → $f'(x_0) = 0$"
✅ **Richtig:** Gilt nur für innere Punkte; Randpunkte und nicht-differenzierbare Punkte ausgenommen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.20 Sätze über stetige Funktionen]]: Existenz von Extremwerten
- [[VL.21 Differenzierbarkeit]]: Grundlagen der Ableitung
- [[VL.22 Anwendung Differenzierbarkeit]]: Höhere Ableitungen
- [[VL.24 Taylor-Approximation]]: Extremwert-Test mit zweiter Ableitung

