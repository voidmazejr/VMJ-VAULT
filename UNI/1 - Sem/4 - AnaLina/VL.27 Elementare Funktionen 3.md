**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #TrigonometrischeFunktionen #ArcusFunktionen #HyperbolischeFunktionen #Additionstheoreme

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt trigonometrische und hyperbolische Funktionen, ihre Eigenschaften und Umkehrfunktionen.

- Beweis der **Additionstheoreme** für Sinus und Cosinus mittels komplexer Exponentialfunktion
- Definition und Eigenschaften von **Tangens und Cotangens**
- **Arcus-Funktionen** als Umkehrfunktionen der Winkelfunktionen
- **Hyperbolische Funktionen** (sinh, cosh, tanh, coth) und ihre Eigenschaften
- **Area-Funktionen** als Umkehrfunktionen der Hyperbelfunktionen
- Übersicht über **Ableitungen aller elementaren Funktionen**

---

## 1. Trigonometrische Funktionen

### Additionstheoreme von Sinus und Cosinus
**Zusatz:** 
$$cos(x) = sin(\frac {\pi}{2} - x)$$

**Satz 27.1 (Additionstheoreme):** Für alle $x, y \in \mathbb{R}$ gilt:

$$\cos(x + y) = \cos(x)\cos(y) - \sin(x)\sin(y)$$
$$\sin(x + y) = \sin(x)\cos(y) + \cos(x)\sin(y)$$

**Beweis mit komplexer Exponentialfunktion:**

Aus der Eulerschen Formel (vgl. [[VL.26 Elementare Funktionen 2]]) wissen wir:
$$e^{ix} = \cos(x) + i\sin(x), \quad e^{iy} = \cos(y) + i\sin(y)$$


Daher:
$$\cos(x+y) + i\sin(x+y) = e^{i(x+y)} = e^{ix} \cdot e^{iy}$$

$$= (\cos(x) + i\sin(x))(\cos(y) + i\sin(y))$$

$$= \underbrace{(\cos(x)\cos(y) - \sin(x)\sin(y))}_{\text{Realteil}} + i\underbrace{(\sin(x)\cos(y) + \cos(x)\sin(y))}_{\text{Imaginärteil}}$$


Vergleich von Real- und Imaginärteil liefert beide Additionstheoreme. ✓

**Wichtige Spezialfälle:**

- **Periodizität mit Periode** $2\pi$:
  $$\cos(x + 2\pi) = \cos(x), \quad \sin(x + 2\pi) = \sin(x)$$

- **Verschiebung um** $\pi$:
  $$\cos(x + \pi) = -\cos(x), \quad \sin(x + \pi) = -\sin(x)$$

### Tangens und Cotangens

**Definition:**

$$\tan(x) = \frac{\sin(x)}{\cos(x)}, \quad x \neq \frac{\pi}{2} + k\pi, \, k \in \mathbb{Z}$$

$$\cot(x) = \frac{\cos(x)}{\sin(x)}, \quad x \neq k\pi, \, k \in \mathbb{Z}$$

**Definitionsbereiche:**
- Tangens: $D_1 = \mathbb{R} \setminus \left\{\frac{\pi}{2} + k\pi \mid k \in \mathbb{Z}\right\}$
- Cotangens: $D_2 = \mathbb{R} \setminus \{k\pi \mid k \in \mathbb{Z}\}$

**Periodizität:** Beide Funktionen sind $\pi$-periodisch:
$$\tan(x + \pi) = \tan(x), \quad \cot(x + \pi) = \cot(x)$$

*Begründung:* Da $\sin(x+\pi) = -\sin(x)$ und $\cos(x+\pi) = -\cos(x)$, kürzen sich die Minuszeichen im Bruch.

**Grafische Darstellung:![[Screenshot 2025-12-16 at 14.02.31.png]]
Blau: $tan(x)$
Pink: $cot(x)$

**Ableitungen:**

Mit der Quotientenregel und dem trigonometrischen Pythagoras $\cos^2(x) + \sin^2(x) = 1$:

$$\tan'(x) = \frac{\sin'(x)\cos(x) - \sin(x)\cos'(x)}{\cos^2(x)} = \frac{\cos^2(x) + \sin^2(x)}{\cos^2(x)} = \frac{1}{\cos^2(x)} = 1 + \tan^2(x)$$

$$\cot'(x) = -\frac{1}{\sin^2(x)} = -1 - \cot^2(x)$$

**Additionstheorem für Tangens:**
$$\tan(x + y) = \frac{\tan(x) + \tan(y)}{1 - \tan(x)\tan(y)}$$
---

## 2. Arcus-Funktionen (Umkehrfunktionen)

Keine der Funktionen cos, sin, tan, cot ist auf ganz $\mathbb{R}$ injektiv (alle sind periodisch). Durch **Einschränkung auf geeignete Intervalle** erhält man injektive Funktionen, die umkehrbar sind.

### Arcussinus

**Einschränkung:** $\sin : \left[-\frac{\pi}{2}, \frac{\pi}{2}\right] \to [-1, 1]$ ist streng monoton wachsend, also bijektiv.

**Umkehrfunktion:**
$$\arcsin : [-1, 1] \to \left[-\frac{\pi}{2}, \frac{\pi}{2}\right]$$

Der Winkel $y \in \left[-\frac{\pi}{2}, \frac{\pi}{2}\right]$ heißt **Hauptwert** des Arcussinus.

**Grafische Darstellung:**
![[Screenshot 2025-12-16 at 11.19.02.png|600]]

**Ableitung (Satz 27.2):**
$$\arcsin'(x) = \frac{1}{\sqrt{1-x^2}}, \quad -1 < x < 1$$
*Beweis mit Umkehrregel:*
$$\arcsin'(x) = \frac{1}{\sin'(\arcsin(x))} = \frac{1}{\cos(\arcsin(x))}$$
Für $y \in \left[-\frac{\pi}{2}, \frac{\pi}{2}\right]$ ist $\cos(y) = +\sqrt{1 - \sin^2(y)}$ (positiv in diesem Intervall), also:
$$\arcsin'(x) = \frac{1}{\sqrt{1 - \sin^2(\arcsin(x))}} = \frac{1}{\sqrt{1-x^2}}$$
### Arcuscosinus

**Einschränkung:** $\cos : [0, \pi] \to [-1, 1]$ ist streng monoton fallend, also bijektiv.

**Umkehrfunktion:**
$$\arccos : [-1, 1] \to [0, \pi]$$
**Grafische Darstellung:**
![[Screenshot 2025-12-16 at 11.17.45.png|700]]

**Ableitung:**
$$\arccos'(x) = -\frac{1}{\sqrt{1-x^2}}, \quad -1 < x < 1$$
### Arcustangens

**Einschränkung:** $\tan : \left]-\frac{\pi}{2}, \frac{\pi}{2}\right[ \to \mathbb{R}$ ist streng monoton wachsend (da $\tan'(x) = 1 + \tan^2(x) \geq 1 > 0$), also bijektiv.

**Umkehrfunktion:**
$$\arctan : \mathbb{R} \to \left]-\frac{\pi}{2}, \frac{\pi}{2}\right[$$

**Grafische Darstellung:**![[Screenshot 2025-12-16 at 11.14.28.png|700]]

**Ableitung:**

$$\arctan'(x) = \frac{1}{1+x^2}, \quad x \in \mathbb{R}$$

*Beweis:*
$$\arctan'(x) = \frac{1}{\tan'(\arctan(x))} = \frac{1}{1 + \tan^2(\arctan(x))} = \frac{1}{1+x^2}$$

**Anwendung:** Der Arcustangens wurde bereits in [[VL.07 Komplexe Zahlen 2]] zur Bestimmung des Arguments komplexer Zahlen verwendet. Da $\arctan$ nur Werte in $\left]-\frac{\pi}{2}, \frac{\pi}{2}\right[$ annimmt, erhält man nur Argumente von Zahlen in der rechten Halbebene ($\text{Re}(z) > 0$).

### Arcuscotangens

**Einschränkung:** $\cot : ]0, \pi[ \to \mathbb{R}$ ist streng monoton fallend, also bijektiv.

**Umkehrfunktion:**
$$\text{arccot} : \mathbb{R} \to ]0, \pi[$$

**Ableitung:**

$$\text{arccot}'(x) = -\frac{1}{1+x^2}, \quad x \in \mathbb{R}$$

**Grafische Darstellung:
![[Screenshot 2025-12-16 at 14.12.30.png]]

---

## 3. Hyperbolische Funktionen

Mit Hilfe der Exponentialfunktion definieren wir zwei für die Ingenieurmathematik wichtige Funktionen (z.B. in Mechanik II).

### Definition

**Definition 27.3 (Hyperbelfunktionen):**

$$\cosh(x) = \frac{e^x + e^{-x}}{2} \quad \text{(Cosinus hyperbolicus)}$$

$$\sinh(x) = \frac{e^x - e^{-x}}{2} \quad \text{(Sinus hyperbolicus)}$$

**Grafische Darstellung:
![[Screenshot 2025-12-16 at 11.11.42.png|700]]  

**Blau:** $cosh(x)$
**Pink:** $sinh(x)$
### Eigenschaften hyperbolischer Funktionen

**Satz 27.4:** Für die hyperbolischen Funktionen gilt:

1. **Hyperbolischer Pythagoras:**
   $$\cosh^2(x) - \sinh^2(x) = 1 \quad \text{für alle } x \in \mathbb{R}$$
   
   *Beweis:*
   $$\cosh^2(x) - \sinh^2(x) = \left(\frac{e^x + e^{-x}}{2}\right)^2 - \left(\frac{e^x - e^{-x}}{2}\right)^2$$
   $$= \frac{e^{2x} + 2 + e^{-2x}}{4} - \frac{e^{2x} - 2 + e^{-2x}}{4} = \frac{4}{4} = 1$$

2. **Ableitungen:**
   $$\cosh'(x) = \sinh(x), \quad \sinh'(x) = \cosh(x)$$

3. **Symmetrie:** cosh ist **gerade**, sinh ist **ungerade**:
   $$\cosh(-x) = \cosh(x), \quad \sinh(-x) = -\sinh(x)$$

4. **Bijektivität von sinh:** $\sinh : \mathbb{R} \to \mathbb{R}$ ist bijektiv.
   
   *Begründung:* $\sinh'(x) = \cosh(x) = \frac{e^x + e^{-x}}{2} \geq 1 > 0$ für alle $x$ ⟹ streng monoton wachsend ⟹ injektiv. Außerdem $\lim_{x \to \pm\infty} \sinh(x) = \pm\infty$ ⟹ surjektiv.

5. **Bijektivität von cosh:** $\cosh : [0, \infty[ \to [1, \infty[$ ist bijektiv.

### Taylorreihen

Aus der Exponentialreihe $e^x = \sum_{k=0}^{\infty} \frac{x^k}{k!}$ folgen:

$$\cosh(x) = \sum_{k=0}^{\infty} \frac{x^{2k}}{(2k)!} = 1 + \frac{x^2}{2!} + \frac{x^4}{4!} + \frac{x^6}{6!} + \dots$$

$$\sinh(x) = \sum_{k=0}^{\infty} \frac{x^{2k+1}}{(2k+1)!} = x + \frac{x^3}{3!} + \frac{x^5}{5!} + \frac{x^7}{7!} + \dots$$

*Vergleich:* Die Struktur ist ähnlich zu cos und sin, aber **ohne alternierende Vorzeichen**.

### Geometrische Interpretation an der Einheitshyperbel

Die **Einheitshyperbel** ist definiert als:
$$H = \{(x, y) \in \mathbb{R}^2 \mid x^2 - y^2 = 1\}$$

Wegen $\cosh^2(t) - \sinh^2(t) = 1$ liegt jeder Punkt $(\cosh(t), \sinh(t))$ auf der Einheitshyperbel.

**Interpretation:** Zu jedem Punkt $(x, y) \in H$ mit $x > 0$ gibt es ein $t \in \mathbb{R}$ mit $x = \cosh(t)$ und $y = \sinh(t)$. Dabei ist $|t|$ der **Flächeninhalt** des Hyperbelausschnitts.

### Tangens und Cotangens hyperbolicus

**Definitionen:**

$$\tanh(x) = \frac{\sinh(x)}{\cosh(x)} = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

$$\coth(x) = \frac{\cosh(x)}{\sinh(x)} = \frac{e^x + e^{-x}}{e^x - e^{-x}}, \quad x \neq 0$$

**Eigenschaften:**
- $\tanh : \mathbb{R} \to ]-1, 1[$ ist bijektiv
- $\coth : \mathbb{R} \setminus \{0\} \to \mathbb{R} \setminus [-1, 1]$ ist bijektiv

**Ableitungen:**

$$\tanh'(x) = 1 - \tanh^2(x) = \frac{1}{\cosh^2(x)}$$

$$\coth'(x) = 1 - \coth^2(x) = -\frac{1}{\sinh^2(x)}$$

**Grafische Darstellung:**
![[Screenshot 2025-12-16 at 11.30.52.png|700]]
**Blau:** $tanh(x)$
**Pink:** $coth(x)$

---

## 4. Area-Funktionen (Umkehrfunktionen)

### Areasinus hyperbolicus

Da $\sinh : \mathbb{R} \to \mathbb{R}$ bijektiv ist, existiert die Umkehrfunktion:

$$\text{arsinh} : \mathbb{R} \to \mathbb{R}$$

**Explizite Formel:**

$$\text{arsinh}(x) = \ln\left(x + \sqrt{x^2 + 1}\right)$$

**Ableitung:**

$$\text{arsinh}'(x) = \frac{1}{\sqrt{1+x^2}}$$

### Areacosinus hyperbolicus

Da $\cosh : [0, \infty[ \to [1, \infty[$ bijektiv ist, existiert die Umkehrfunktion:

$$\text{arcosh} : [1, \infty[ \to [0, \infty[$$

**Explizite Formel:**

$$\text{arcosh}(x) = \ln\left(x + \sqrt{x^2 - 1}\right), \quad x \geq 1$$

**Ableitung:**

$$\text{arcosh}'(x) = \frac{1}{\sqrt{x^2-1}}, \quad x \in ]1, \infty[$$

### Areatangens hyperbolicus

Die Umkehrfunktion von $\tanh : \mathbb{R} \to ]-1, 1[$:

$$\text{artanh} : ]-1, 1[ \to \mathbb{R}$$

**Explizite Formel:**

$$\text{artanh}(x) = \frac{1}{2}\ln\left(\frac{1+x}{1-x}\right), \quad |x| < 1$$

**Ableitung:**

$$\text{artanh}'(x) = \frac{1}{1-x^2}, \quad |x| < 1$$

### Areacotangens hyperbolicus

Die Umkehrfunktion von $\coth : \mathbb{R} \setminus \{0\} \to \mathbb{R} \setminus [-1, 1]$:

$$\text{arcoth} : \mathbb{R} \setminus [-1, 1] \to \mathbb{R} \setminus \{0\}$$

**Explizite Formel:**

$$\text{arcoth}(x) = \frac{1}{2}\ln\left(\frac{x+1}{x-1}\right), \quad |x| > 1$$

**Ableitung:**

$$\text{arcoth}'(x) = \frac{1}{1-x^2}, \quad |x| > 1$$

---

## 📌 Ableitungen aller elementaren Funktionen

### Potenz- und Exponentialfunktionen

| **Funktion** | **Ableitung** | **Bemerkungen** |
|-------------|---------------|-----------------|
| $x^n$ | $nx^{n-1}$ | $n \in \mathbb{N}$ |
| $\exp(x)$ | $\exp(x)$ | |
| $a^x$ | $a^x \ln(a)$ | $a > 0, x \in \mathbb{R}$ |
| $\ln(\|x\|)$ | $\frac{1}{x}$ | $x \neq 0$ |
| $\log_a(\|x\|)$ | $\frac{1}{x \ln(a)}$ | $a, x > 0$ |
| $x^a$ | $ax^{a-1}$ | $x > 0, a \in \mathbb{R}$ |

### Trigonometrische Funktionen

| **Funktion** | **Ableitung** | **Bemerkungen** |
|-------------|---------------|-----------------|
| $\sin(x)$ | $\cos(x)$ | |
| $\cos(x)$ | $-\sin(x)$ | |
| $\tan(x)$ | $\frac{1}{\cos^2(x)} = 1 + \tan^2(x)$ | $x \neq \frac{\pi}{2} + k\pi$ |
| $\cot(x)$ | $-\frac{1}{\sin^2(x)} = -1 - \cot^2(x)$ | $x \neq k\pi$ |

### Arcus-Funktionen

| **Funktion** | **Ableitung** | **Bemerkungen** |
|-------------|---------------|-----------------|
| $\arcsin(x)$ | $\frac{1}{\sqrt{1-x^2}}$ | $\|x\| < 1$ |
| $\arccos(x)$ | $-\frac{1}{\sqrt{1-x^2}}$ | $\|x\| < 1$ |
| $\arctan(x)$ | $\frac{1}{1+x^2}$ | $x \in \mathbb{R}$ |
| $\text{arccot}(x)$ | $-\frac{1}{1+x^2}$ | $x \in \mathbb{R}$ |

### Hyperbolische Funktionen

| **Funktion** | **Ableitung** | **Bemerkungen** |
|-------------|---------------|-----------------|
| $\cosh(x)$ | $\sinh(x)$ | |
| $\sinh(x)$ | $\cosh(x)$ | |
| $\tanh(x)$ | $\frac{1}{\cosh^2(x)} = 1 - \tanh^2(x)$ | |
| $\coth(x)$ | $-\frac{1}{\sinh^2(x)} = 1 - \coth^2(x)$ | $x \neq 0$ |

### Area-Funktionen

| **Funktion**       | **Ableitung**            | **Bemerkungen**     |
| ------------------ | ------------------------ | ------------------- |
| $\text{arsinh}(x)$ | $\frac{1}{\sqrt{1+x^2}}$ | $x \in \mathbb{R}$  |
| $\text{arcosh}(x)$ | $\frac{1}{\sqrt{x^2-1}}$ | $x \in ]1, \infty[$ |
| $\text{artanh}(x)$ | $\frac{1}{1-x^2}$        | $\|x\| < 1$         |
| $\text{arcoth}(x)$ | $\frac{1}{1-x^2}$        | $\|x\| > 1$         |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.06 Elementare Funktionen 1]]: Erste Einführung von sin, cos, tan (geometrisch am Einheitskreis)
- [[VL.07 Komplexe Zahlen 2]]: Eulersche Formel, arctan zur Bestimmung des Arguments komplexer Zahlen
- [[VL.19 Stetigkeit]]: Geometrische Interpretation von tan und cot am Einheitskreis
- [[VL.22 Anwendung Differenzierbarkeit]]: Ableitung der Umkehrfunktion (für Arcus-Funktionen)
- [[VL.23 Mittelwertsatz]]: Quotientenregel (für tan' und cot')
- [[VL.25 Anwendung Taylor-Approximation]]: Taylorreihen von sin und cos
- [[VL.26 Elementare Funktionen 2]]: Komplexe Exponentialfunktion, Exponentialreihe
