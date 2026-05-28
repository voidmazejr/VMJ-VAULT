**Class:** [[AnaLina]]  
**Date:** 27-12-2025  
**Topics:** #KomplexeZahlen #Polardarstellung #EulerFormel #KomplexeWurzeln #Arctan

---
## 🎯 Lernziele der Vorlesung

- Polardarstellung komplexer Zahlen verstehen
- Euler-Formel kennen und anwenden
- Umrechnung zwischen kartesischer und Polardarstellung
- Multiplikation in Polardarstellung
- n-te Wurzeln komplexer Zahlen berechnen
- Quadratische Gleichungen mit komplexen Koeffizienten lösen

---

## 1. Polardarstellung

### Wiederholung: Kartesische Darstellung

In [[VL.03 Komplexe Zahlen 1]] haben wir komplexe Zahlen kennengelernt: $$z = x + iy \quad \text{mit } x, y \in \mathbb{R}$$

wobei $x$ und $y$ die kartesischen Koordinaten in der Gaußschen Zahlenebene sind.

### Herleitung der Polardarstellung

Betrachten wir ein rechtwinkliges Dreieck in der Gaußschen Zahlenebene:

![[Screenshot 2025-12-26 at 21.21.52.png]]

Aus der Trigonometrie am Einheitskreis folgt: $$x = r \cos(\varphi), \quad y = r \sin(\varphi)$$

Damit erhalten wir: $$z = x + iy = r\cos(\varphi) + ir\sin(\varphi) = r(\cos(\varphi) + i\sin(\varphi))$$

Das ist die **Polardarstellung** von $z$.

### Definition: Betrag und Argument

Für $z = r(\cos(\varphi) + i\sin(\varphi))$ heißen:

1. **Betrag:** $r = |z| = \sqrt{x^2 + y^2}$ (Abstand zum Ursprung)
    
2. **Argument:** $\varphi = \arg(z)$ (Winkel zur positiven reellen Achse, im Bogenmaß)
    

⚠️ **Wichtig:** Das Argument ist **nicht eindeutig**! Mit $\varphi$ ist auch $\varphi + 2\pi k$ für $k \in \mathbb{Z}$ ein Argument von $z$.

**Konvention:** Man wählt meist einen Bereich für $\varphi$:

- $[0, 2\pi[$
- $]-\pi, \pi]$
- $\left[-\frac{\pi}{2}, \frac{3\pi}{2}\right[$

**Spezialfall:** Für $z = 0$ ist $r = 0$ und $\varphi$ beliebig (nicht bestimmt).

---

## 2. Umrechnung zwischen Darstellungen

### Von Polar zu Kartesisch

**Gegeben:** $r, \varphi$ in Polardarstellung  
**Gesucht:** $x, y$ in kartesischer Darstellung

**Formeln:** $$x = r\cos(\varphi), \quad y = r\sin(\varphi)$$

### Von Kartesisch zu Polar

**Gegeben:** $z = x + iy \neq 0$ in kartesischer Darstellung  
**Gesucht:** $r, \varphi$ in Polardarstellung

**Betrag:** $$r = |z| = \sqrt{x^2 + y^2}$$

**Argument:** Division der Gleichungen ergibt: $$\frac{y}{x} = \frac{r\sin(\varphi)}{r\cos(\varphi)} = \tan(\varphi) \quad \text{(falls } x \neq 0\text{)}$$

### Arcus Tangens

Der **Tangens** ist $\pi$-periodisch: $\tan(\varphi + k\pi) = \tan(\varphi)$ für $k \in \mathbb{Z}$

![[Screenshot 2025-12-26 at 14.38.49.png]]

Eingeschränkt auf $\left]-\frac{\pi}{2}, \frac{\pi}{2}\right[$ ist $\tan$ **injektiv** und besitzt die Umkehrfunktion: $$\arctan = \tan^{-1} : \mathbb{R} \to \left]-\frac{\pi}{2}, \frac{\pi}{2}\right[$$

### Berechnung des Arguments

Für $z = x + iy \neq 0$ mit $\varphi \in \left[-\frac{\pi}{2}, \frac{3\pi}{2}\right[$:

$$\varphi = \begin{cases} 
\arctan\left(\frac{y}{x}\right) & \text{falls } x > 0 \text{ (1. und 4. Quadrant)} \\[0.5em] 
\arctan\left(\frac{y}{x}\right) + \pi & \text{falls } x < 0 \text{ (2. und 3. Quadrant)} \\[0.5em] 
+\frac{\pi}{2} & \text{falls } x = 0, y > 0 \text{ (positive y-Achse)} \\[0.5em] 
-\frac{\pi}{2} & \text{falls } x = 0, y < 0 \text{ (negative y-Achse)} 
\end{cases}$$

**Merkhilfe:**

- Rechte Halbebene ($x > 0$): $\arctan$ direkt
- Linke Halbebene ($x < 0$): $\arctan$ plus $\pi$
- y-Achse: $\pm\frac{\pi}{2}$

### Beispiele

**Beispiel 1:** $z_1 = 2 + 2i$

- $r = \sqrt{2^2 + 2^2} = \sqrt{8} = 2\sqrt{2}$
- $\tan(\varphi) = \frac{2}{2} = 1$ $\Rightarrow$ $\arctan(1) = \frac{\pi}{4}$
- $x = 2 > 0$ $\Rightarrow$ $\varphi = \frac{\pi}{4}$
- $z_1 = 2\sqrt{2}\left(\cos\left(\frac{\pi}{4}\right) + i\sin\left(\frac{\pi}{4}\right)\right)$

**Beispiel 2:** $z_2 = -1 - i$

- $r = \sqrt{(-1)^2 + (-1)^2} = \sqrt{2}$
- $\tan(\varphi) = \frac{-1}{-1} = 1$ $\Rightarrow$ $\arctan(1) = \frac{\pi}{4}$
- $x = -1 < 0$ $\Rightarrow$ $\varphi = \frac{\pi}{4} + \pi = \frac{5\pi}{4}$
- $z_2 = \sqrt{2}\left(\cos\left(\frac{5\pi}{4}\right) + i\sin\left(\frac{5\pi}{4}\right)\right)$

**Beispiel 3:** $z_3 = 3i$

- $r = \sqrt{0^2 + 3^2} = 3$
- $x = 0, y = 3 > 0$ $\Rightarrow$ $\varphi = \frac{\pi}{2}$
- $z_3 = 3\left(\cos\left(\frac{\pi}{2}\right) + i\sin\left(\frac{\pi}{2}\right)\right)$

![[Screenshot 2025-12-26 at 21.23.36.png]]

---

## 3. Euler-Formel

### Definition

Zur Abkürzung der Schreibweise wird die **Euler-Formel** verwendet: $$e^{i\varphi} = \cos(\varphi) + i\sin(\varphi)$$

Diese stellt eine fundamentale Verbindung zwischen der komplexen Exponentialfunktion und den trigonometrischen Funktionen her.

⚠️ **Bemerkung:** Den vollständigen Nachweis liefern wir später in [[VL.25 Anwendung Taylor-Approximation]].

### Eulerdarstellung

Mit der Euler-Formel können wir eine komplexe Zahl schreiben als: $$z = x + iy = r(\cos(\varphi) + i\sin(\varphi)) = re^{i\varphi}$$

Die Schreibweise $re^{i\varphi}$ heißt **Eulerdarstellung** von $z$.

**Beispiele:**

- $z_1 = 2 + 2i = 2\sqrt{2}e^{i\frac{\pi}{4}}$
- $z_2 = -1 - i = \sqrt{2}e^{i\frac{5\pi}{4}}$
- $z_3 = 3i = 3e^{i\frac{\pi}{2}}$

### Potenzgesetze

Es gelten die üblichen Potenzgesetze: $$(e^{i\varphi})^n = e^{in\varphi}$$

---

## 4. Multiplikation in Polardarstellung

### Satz: Multiplikation

Seien $z_1 = r_1(\cos(\varphi_1) + i\sin(\varphi_1))$ und $z_2 = r_2(\cos(\varphi_2) + i\sin(\varphi_2))$ in Polardarstellung. Dann: $$z_1 z_2 = r_1 r_2 (\cos(\varphi_1 + \varphi_2) + i\sin(\varphi_1 + \varphi_2))$$

**Beweis:** Ausmultiplizieren und Additionstheoreme: $$z_1 z_2 = r_1 r_2 (\cos(\varphi_1)\cos(\varphi_2) - \sin(\varphi_1)\sin(\varphi_2)$$ $$+ i(\cos(\varphi_1)\sin(\varphi_2) + \sin(\varphi_1)\cos(\varphi_2)))$$ $$= r_1 r_2 (\cos(\varphi_1 + \varphi_2) + i\sin(\varphi_1 + \varphi_2))$$

**Mit Eulerdarstellung** noch einfacher: $$z_1 z_2 = r_1 e^{i\varphi_1} \cdot r_2 e^{i\varphi_2} = r_1 r_2 e^{i(\varphi_1 + \varphi_2)}$$

### Regel für Multiplikation

Bei der Multiplikation komplexer Zahlen:

1. **Beträge multiplizieren sich:** $|z_1 z_2| = |z_1| \cdot |z_2|$
2. **Argumente addieren sich:** $\arg(z_1 z_2) = \arg(z_1) + \arg(z_2)$ (modulo $2\pi$)

**Geometrische Interpretation:**

![[Screenshot 2025-12-26 at 21.24.51.png]]
### Potenzen

Potenzen komplexer Zahlen sind in Eulerdarstellung **extrem einfach**: $$z^{42} = (re^{i\varphi})^{42} = r^{42} e^{i \cdot 42\varphi}$$

**Vergleich:** In kartesischer Darstellung: $$z^{42} = (x + iy)^{42} = \text{???}$$ Selbst mit dem binomischen Lehrsatz sehr kompliziert!

---

## 5. Komplexe Wurzeln

### Aufgabe

**Gegeben:** $a \in \mathbb{C}$ und $n \in \mathbb{N}$, $n \geq 1$  
**Gesucht:** Alle Lösungen von $z^n = a$

### Lösung in Polardarstellung

Schreibe $z = re^{i\varphi}$ und $a = se^{i\alpha}$ mit $s = |a| \geq 0$ und $\alpha \in \mathbb{R}$.

Dann gilt: $$z^n = r^n e^{in\varphi} = se^{i\alpha}$$

**Vergleich:**

1. **Beträge:** $r^n = s$ $\Rightarrow$ $r = \sqrt[n]{s}$
    
2. **Argumente:** $n\varphi = \alpha + 2\pi k$ mit $k \in \mathbb{Z}$ $\Rightarrow$ $\varphi = \frac{\alpha}{n} + \frac{2\pi k}{n}$
    

**Lösungen:** $$z_k = \sqrt[n]{s} \cdot e^{i\left(\frac{\alpha}{n} + \frac{2\pi k}{n}\right)}, \quad k = 0, 1, 2, ..., n-1$$

Da $\varphi + 2\pi$ und $\varphi$ denselben Winkel beschreiben, gibt es genau **n verschiedene Lösungen**.

### Geometrische Interpretation

Die $n$ Lösungen bilden ein **regelmäßiges n-Eck** mit Mittelpunkt im Ursprung!

**Abstand zwischen benachbarten Lösungen:** $\frac{2\pi}{n}$ (Winkel)

### Beispiel 1: Einheitswurzeln ($z^n = 1$)

**Aufgabe:** Löse $z^n = 1$

**Lösung:** Schreibe $1 = 1 \cdot e^{i \cdot 0}$, also $s = 1$ und $\alpha = 0$.

Dann: $r = \sqrt[n]{1} = 1$ und $\varphi = \frac{0}{n} + \frac{2\pi k}{n} = \frac{2\pi k}{n}$

**Die n Einheitswurzeln:** $$z_k = e^{i\frac{2\pi k}{n}}, \quad k = 0, 1, 2, ..., n-1$$

**Für n = 4:**

- $z_0 = e^{i \cdot 0} = 1$
- $z_1 = e^{i\frac{\pi}{2}} = i$
- $z_2 = e^{i\pi} = -1$
- $z_3 = e^{i\frac{3\pi}{2}} = -i$
![[Screenshot 2025-12-26 at 21.25.48.png]]

**Für n = 5:** $$z_k = e^{i\frac{2\pi k}{5}}, \quad k = 0, 1, 2, 3, 4$$
![[Screenshot 2025-12-26 at 21.26.07.png]]

**Für n = 6:** $$z_k = e^{i\frac{\pi k}{3}}, \quad k = 0, 1, 2, 3, 4, 5$$

Winkel: $0, \frac{\pi}{3}, \frac{2\pi}{3}, \pi, \frac{4\pi}{3}, \frac{5\pi}{3}$

![[Screenshot 2025-12-26 at 21.26.23.png]]
### Beispiel 2: $z^2 = 4i$

**Aufgabe:** Löse $z^2 = 4i$

**Lösung:** Schreibe $4i = 4e^{i\frac{\pi}{2}}$, also $s = 4$ und $\alpha = \frac{\pi}{2}$.

Dann:

- $r = \sqrt{4} = 2$
- $\varphi = \frac{\pi/2}{2} + \frac{2\pi k}{2} = \frac{\pi}{4} + \pi k$

**Die beiden Lösungen:**

**Für k = 0:** $$z_0 = 2e^{i\frac{\pi}{4}} = 2\left(\cos\left(\frac{\pi}{4}\right) + i\sin\left(\frac{\pi}{4}\right)\right)$$ $$= 2\left(\frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2}\right) = \sqrt{2} + i\sqrt{2}$$

**Für k = 1:** $$z_1 = 2e^{i\frac{5\pi}{4}} = 2e^{i(\frac{\pi}{4} + \pi)} = 2e^{i\frac{\pi}{4}} \cdot e^{i\pi} = -z_0 = -\sqrt{2} - i\sqrt{2}$$

**Probe für** $z_0$: $$z_0^2 = (\sqrt{2} + i\sqrt{2})^2 = 2 + 2i\sqrt{2} \cdot \sqrt{2} + (i\sqrt{2})^2$$ $$= 2 + 4i - 2 = 4i \quad \checkmark$$

---

## 6. Quadratische Gleichungen mit komplexen Koeffizienten

### Allgemeine Form

**Gegeben:** $az^2 + bz + c = 0$ mit $a, b, c \in \mathbb{C}$ und $a \neq 0$

### Lösungsformel

Die Gleichung hat immer die beiden Lösungen: $$z_{1,2} = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

### Interpretation des Wurzelzeichens

Sei $d = b^2 - 4ac$ die **Diskriminante**. Es gibt drei Fälle:

**Fall 1:** $d = 0$

- Doppelte Lösung: $z_1 = z_2 = -\frac{b}{2a}$

**Fall 2:** $d \in \mathbb{R}$ und $d \geq 0$

- $\sqrt{d}$ ist die gewöhnliche reelle Quadratwurzel
- Für $d < 0$: $\sqrt{d} = i\sqrt{-d}$ (wie in [[VL.03 Komplexe Zahlen 1]])

**Fall 3:** $d \in \mathbb{C} \setminus \mathbb{R}$ (d ist komplex)

- Die beiden Wurzeln "$\pm\sqrt{d}$" sind die beiden Lösungen von $z^2 = d$: $$\sqrt{|d|} \cdot e^{i\frac{\arg(d)}{2}} \quad \text{und} \quad \sqrt{|d|} \cdot e^{i\left(\frac{\arg(d)}{2} + \pi\right)} = -\sqrt{|d|} \cdot e^{i\frac{\arg(d)}{2}}$$
- Die beiden Lösungen unterscheiden sich nur im Vorzeichen!

**Bemerkung:** In [[VL.03 Komplexe Zahlen 1]] hatten wir uns auf reelle Koeffizienten beschränkt. Jetzt können wir auch komplexe Koeffizienten behandeln!

---

## 📌 Zusammenfassung

|**Darstellung**|**Form**|**Vorteil**|
|---|---|---|
|**Kartesisch**|$z = x + iy$|Addition einfach|
|**Polar**|$z = r(\cos(\varphi) + i\sin(\varphi))$|Multiplikation geometrisch|
|**Euler**|$z = re^{i\varphi}$|Multiplikation und Potenzen einfach|

**Wichtige Formeln:**

- Euler-Formel: $e^{i\varphi} = \cos(\varphi) + i\sin(\varphi)$
- Multiplikation: $r_1 e^{i\varphi_1} \cdot r_2 e^{i\varphi_2} = r_1 r_2 e^{i(\varphi_1 + \varphi_2)}$
- n-te Wurzeln von $a = se^{i\alpha}$: $z_k = \sqrt[n]{s} \cdot e^{i\left(\frac{\alpha}{n} + \frac{2\pi k}{n}\right)}$, $k = 0, ..., n-1$
- Einheitswurzeln: $z_k = e^{i\frac{2\pi k}{n}}$, $k = 0, ..., n-1$ (regelmäßiges n-Eck!)

**Umrechnung:**

- Polar → Kartesisch: $x = r\cos(\varphi)$, $y = r\sin(\varphi)$
- Kartesisch → Polar: $r = \sqrt{x^2 + y^2}$, $\varphi$ über $\arctan$ und Quadrantencheck

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.03 Komplexe Zahlen 1]] Kartesische Darstellung, Grundrechenarten
- [[VL.06 Elementare Funktionen 1]] Sinus, Cosinus, Tangens
- [[VL.08 Polynome]] Nullstellen von Polynomen
- [[VL.25 Anwendung Taylor-Approximation]] Beweis der Euler-Formel
- [[VL.26 Elementare Funktionen 2]] Komplexe Exponentialfunktion
